---
title: "Differenze tra Entity SQL e Transact-SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 9c9ee36d-f294-4c8b-a196-f0114c94f559
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Differenze tra Entity SQL e Transact-SQL
In questo argomento vengono descritte le differenze tra [!INCLUDE[esql](../../../../../../includes/esql-md.md)] e [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)].  
  
## Supporto di ereditarietà e relazioni  
 In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] vengono usati direttamente gli schemi di entità concettuali e sono supportate funzionalità del modello concettuale, quali l'ereditarietà e le relazioni.  
  
 Quando si usa l'ereditarietà, è spesso utile selezionare le istanze di un sottotipo da una raccolta di istanze di supertipi.  Questa capacità è fornita dall'operatore [oftype](../../../../../../docs/framework/data/adonet/ef/language-reference/oftype-entity-sql.md) in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] \(simile a `oftype` nelle sequenze in C\#\).  
  
## Supporto per le raccolte  
 In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] le raccolte vengono trattate come entità di prima classe.  Ad esempio:  
  
-   Le espressioni sulle raccolte sono valide in una clausola `from`.  
  
-   Le sottoquery `in` e `exists` sono state generalizzate per consentire qualsiasi raccolta.  
  
     Una sottoquery è un tipo di raccolta.  `e1 in e2` e `exists(e)` sono i construct [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usati per eseguire queste operazioni.  
  
-   Le operazioni Set, ad esempio `union`, `intersect` ed `except`, possono ora essere usate sulle raccolte.  
  
-   I join funzionano sulle raccolte.  
  
## Supporto per le espressioni  
 In [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] sono presenti sottoquery \(tabelle\) ed espressioni \(righe e colonne\).  
  
 Per supportare le raccolte e le raccolte annidate, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] trasforma tutti gli elementi in espressione.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] è più componibile rispetto a [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)]: ogni espressione può essere usata in qualunque posizione.  Le espressioni di query restituiscono sempre raccolte dei tipi previsti e possono essere usate in qualunque posizione in cui è consentita un'espressione sulle raccolte.  Per informazioni sulle espressioni [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] non supportate in [!INCLUDE[esql](../../../../../../includes/esql-md.md)], vedere [Espressioni non supportate](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md).  
  
 Le query seguenti sono tutte query [!INCLUDE[esql](../../../../../../includes/esql-md.md)] valide:  
  
```  
1+2 *3  
"abc"  
row(1 as a, 2 as b)  
{ 1, 3, 5}   
e1 union all e2  
set(e1)  
```  
  
## Modalità di gestione uniforme delle sottoquery  
 Vista l'enfasi posta sulle tabelle, in [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] viene eseguita l'interpretazione contestuale delle sottoquery.  Una sottoquery nella clausola `from` viene ad esempio considerata come un multiset \(tabella\).  La stessa sottoquery usata nella clausola `select` viene invece considerata come una sottoquery scalare.  Analogamente, una sottoquery usata sul lato sinistro di un operatore `in` viene considerata come una sottoquery scalare, mentre sul lato destro è prevista una sottoquery multiset.  
  
 In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] vengono eliminate queste differenze.  Un'espressione dispone di un'interpretazione uniforme che non dipende dal contesto in cui viene usata.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] considera tutte le sottoquery come sottoquery multiset.  Se dalla sottoquery si desidera ottenere un valore scalare, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce l'operatore `anyelement` che opera su una raccolta, in questo caso, la sottoquery, ed estrae un valore singleton dalla raccolta.  
  
### Eliminazione della presenza di coercizioni implicite per le sottoquery  
 Un effetto collaterale della modalità di gestione uniforme delle sottoquery è la conversione implicita delle sottoquery in valori scalari.  In particolare, in [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] un multiset di righe \(con un singolo campo\) viene convertito in modo implicito in un valore scalare il cui tipo di dati è quello del campo.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non supporta questa coercizione implicita.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce un operatore ANYELEMENT per estrarre un valore Singleton da una raccolta e una clausola `select value` per evitare di creare un wrapper di riga durante un'espressione di query.  
  
## SELECT VALUE: eliminazione della presenza del wrapper di riga implicito  
 Tramite la clausola SELECT in una sottoquery [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] viene creato in modo implicito un wrapper di riga intorno agli elementi della clausola.  Questo implica che non si possono creare raccolte di scalari o oggetti.  [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] consente una coercizione implicita tra un rowtype con un campo e un valore Singleton dello stesso tipo di dati.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce la clausola `select value` per ignorare la costruzione di riga implicita.  Nella clausola `select value` è possibile specificare un solo elemento.  Quando viene usata questa clausola, non viene costruito alcun wrapper di riga intorno agli elementi nella clausola `select` e può essere prodotta una raccolta della forma desiderata, ad esempio `select value a`.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce inoltre il costruttore ROW per la costruzione di righe arbitrarie.  `select` prende uno o più elementi nella proiezione e crea un record di dati con campi, come mostrato di seguito:  
  
 `select a, b, c`  
  
## Correlazione sinistra e utilizzo di alias  
 In [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] le espressioni in un determinato ambito \(una singola clausola come `select` o `from`\) non possono fare riferimento alle espressioni definite in precedenza nello stesso ambito.  Alcuni dialetti di SQL \(incluso [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)]\) supportano forme limitate di questi comportamenti nella clausola `from`.  
  
 In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] le correlazioni sinistre nella clausola `from` vengono generalizzate e trattate in modo uniforme.  Le espressioni nella clausola `from` possono fare riferimento a definizioni precedenti \(definizioni a sinistra\) nella stessa clausola senza che sia necessaria sintassi aggiuntiva.  
  
 In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] vengono inoltre imposte restrizioni aggiuntive sulle query che implicano l'uso di clausole `group by`.  Le espressioni nella clausola `select` e nella clausola `having` di tali query possono fare riferimento alle chiavi `group by` solo tramite i relativi alias.  Il costrutto seguente è valido in [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] ma non in [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
select t.x + t.y from T as t group by t.x + t.y  
```  
  
 Per eseguire questa operazione in [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
select k from T as t group by (t.x + t.y) as k  
```  
  
## Riferimento a colonne \(proprietà\) di tabelle \(raccolte\)  
 Tutti i riferimenti alle colonne in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] devono essere qualificati con l'alias di tabella.  Il costrutto seguente \(presupponendo che `a` sia una colonna valida della tabella `T`\) è valido in [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] ma non in [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
```  
select a from T  
```  
  
 Il formato in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] è:  
  
```  
select t.a as A from T as t  
```  
  
 Gli alias di tabella sono facoltativi nella clausola `from`.  Il nome della tabella viene usato come l'alias implicito.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] consente anche l'uso del formato seguente:  
  
```  
select Tab.a from Tab  
```  
  
## Navigazione negli oggetti  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] usa la notazione "." per fare riferimento a colonne di \(una riga di\) una tabella.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] estende questa notazione \(preso in prestito dai linguaggi di programmazione\) per supportare la navigazione tra le proprietà di un oggetto.  
  
 Se, ad esempio, `p` è un'espressione del tipo Person, di seguito è riportata la sintassi [!INCLUDE[esql](../../../../../../includes/esql-md.md)] che consente di fare riferimento alla città dell'indirizzo di tale persona.  
  
```  
p.Address.City   
```  
  
## Mancanza di supporto per \*  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] supporta la sintassi \* non qualificata come alias per l'intera riga e la sintassi \* qualificata \(t. \*\) come collegamento per i campi della tabella.  In [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] è inoltre consentita un'aggregazione count\(\*\) speciale che include i valori null.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non supporta il construct \*.  Le query [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] del form `select * from T` e `select T1.* from T1, T2...` possono essere espresse in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] rispettivamente  come `select value t from T as t` e `select value t1 from T1 as t1, T2 as t2...`.  Questi costrutti consentono inoltre di gestire l'ereditarietà \(sostituibilità del valore\), mentre le varianti `select *` sono limitate alle proprietà di primo livello del tipo dichiarato.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non supporta l'aggregato `count(*)`.  In alternativa, usare `count(0)`.  
  
## Modifiche a Group By  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] supporta l'uso di alias delle chiavi `group by`.  Le espressioni nella clausola `select` e nella clausola `having` devono fare riferimento alle chiavi `group by` attraverso questi alias. Ad esempio, la sintassi [!INCLUDE[esql](../../../../../../includes/esql-md.md)] seguente:  
  
```  
select k1, count(t.a), sum(t.a)  
from T as t  
group by t.b + t.c as k1  
```  
  
 ...è equivalente alla sintassi [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] seguente:  
  
```  
select b + c, count(*), sum(a)   
from T  
group by b + c  
```  
  
## Aggregazioni basate sulle raccolte  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] supporta due tipi di aggregazioni.  
  
 Le aggregazioni basate sulle raccolte operano sulle raccolte e producono il risultato aggregato.  Possono essere presenti in un punto qualsiasi nella query e non richiedono una clausola `group by`.  Ad esempio:  
  
```  
select t.a as a, count({1,2,3}) as b from T as t     
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] supporta inoltre le aggregazioni di tipo SQL.  Ad esempio:  
  
```  
select a, sum(t.b) from T as t group by t.a as a  
```  
  
## Utilizzo della clausola ORDER BY  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] consente di specificare le clausole ORDER BY solo nel blocco SELECT .. FROM ..  WHERE di livello superiore.  In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] è possibile usare un'espressione ORDER BY annidata e posizionarla in un punto qualsiasi nella query, ma l'ordinamento in una query annidata non viene mantenuto.  
  
```  
-- The following query will order the results by the last name  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## Identificatori  
 In [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] il confronto tra identificatori si basa sulle regole di confronto del database corrente.  Negli identificatori di [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non viene mai operata la distinzione tra maiuscole e minuscole, mentre viene operata la distinzione tra caratteri accentati e non accentati, ovvero in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 'e' non è uguale a 'è'. In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] le versioni delle lettere che appaiono uguali ma presentano una tabella codici diversa vengono considerati come caratteri differenti.  Per altre informazioni, vedere [Set di caratteri di input](../../../../../../docs/framework/data/adonet/ef/language-reference/input-character-set-entity-sql.md).  
  
## Funzionalità Transact\-SQL non disponibili in Entity SQL  
 Le funzionalità [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] seguenti non sono disponibili in [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
 DML  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non fornisce attualmente supporto per le istruzioni DML \(INSERT, UPDATE, DELETE\).  
  
 DDL  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non fornisce supporto per DDL nella versione corrente.  
  
 programmazione imperativa  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non fornisce supporto per la programmazione imperativa, a differenza di [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)].  Usare invece un linguaggio di programmazione.  
  
 Funzioni di raggruppamento  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non fornisce ancora supporto per le funzioni di raggruppamento \(ad esempio CUBE, ROLLUP e GROUPING\_SET\).  
  
 Funzioni analitiche  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non fornisce \(ancora\) supporto per le funzioni analitiche.  
  
 Funzioni e operatori predefiniti  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] supporta un subset di funzioni e operatori [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] predefiniti.  Questi operatori e funzioni saranno supportati probabilmente dai provider dell'archivio principali.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usa le funzioni specifiche dell'archivio dichiarate in un manifesto del provider.  Inoltre, [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] consente di dichiarare funzioni dell'archivio esistenti predefinite e definite dall'utente da usare in [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
 Hint  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non fornisce meccanismi per gli hint per le query.  
  
 Invio in batch dei risultati di query  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non supporta l'invio in batch dei risultati di query.  Ad esempio, l'operazione [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] seguente \(invio in batch\) è valida:  
  
```  
select * from products;  
select * from catagories;  
```  
  
 Tuttavia, l'espressione equivalente [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non è supportata:  
  
```  
Select value p from Products as p;  
Select value c from Categories as c;  
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] supporta solo un'istruzione di query che restituisce un risultato per comando.  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Espressioni non supportate](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md)