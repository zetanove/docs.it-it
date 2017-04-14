---
title: "LIKE (Entity SQL) | Microsoft Docs"
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
ms.assetid: 8300e6d2-875b-481e-9ef4-e1e7c12d46fa
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# LIKE (Entity SQL)
Determina se un oggetto `String` di caratteri specifico corrisponde a un criterio specificato.  
  
## Sintassi  
  
```  
  
match [NOT] LIKE pattern [ESCAPE escape]  
```  
  
## Argomenti  
 `match`  
 Espressione [!INCLUDE[esql](../../../../../../includes/esql-md.md)] che restituisce un oggetto `String`.  
  
 `pattern`  
 Criterio da confrontare con l'oggetto `String` specificato.  
  
 `escape`  
 Carattere di escape.  
  
 NOT  
 Specifica la negazione del risultato di LIKE.  
  
## Valore restituito  
 `true` se `string` corrisponde al criterio; in caso contrario, `false`.  
  
## Note  
 Le espressioni [!INCLUDE[esql](../../../../../../includes/esql-md.md)] che usano l'operatore LIKE vengono valutate in modo analogo alle espressioni in cui viene usata l'uguaglianza come criterio di filtro. Le espressioni [!INCLUDE[esql](../../../../../../includes/esql-md.md)] che usano l'operatore LIKE possono tuttavia includere sia valori letterali che caratteri jolly.  
  
 Nella tabella seguente viene descritta la sintassi del modello `string`.  
  
|Carattere jolly|Descrizione|Esempio|  
|---------------------|-----------------|-------------|  
|%|Qualsiasi `string` di zero o più caratteri.|`title like '%computer%'` consente di trovare tutti i titoli in cui è presente la parola `"computer"` in qualsiasi posizione.|  
|\_ \(carattere di sottolineatura\)|Qualsiasi carattere singolo.|`firstname like '_ean'` consente di trovare tutti i nomi di quattro lettere che terminano con `"ean`", ad esempio Dean o Sean.|  
|\[ \]|Qualsiasi carattere singolo compreso nell'intervallo \(\[a\-f\]\) o nel set \(\[abcdef\]\) specificato.|`lastname like '[C-P]arsen'` consente di trovare i cognomi che terminano con "arsen" e che iniziano con qualsiasi carattere singolo compreso tra C e P, ad esempio Carsen o Larsen.|  
|\[^\]|Qualsiasi carattere singolo non compreso nell'intervallo \(\[^a\-f\]\) o nel set \(\[^abcdef\]\) specificato.|`lastname like 'de[^l]%'` consente di trovare tutti i cognomi che iniziano con "de" e che non includono "l" come lettera seguente.|  
  
> [!NOTE]
>  La clausola ESCAPE e l'operatore LIKE [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non possono essere applicati ai valori `System.DateTime` o `System.Guid`.  
  
 LIKE supporta i criteri di ricerca ASCII e Unicode. Quando tutti i parametri sono caratteri ASCII, viene eseguita una ricerca ASCII. Se uno o più argomenti sono di tipo Unicode, tutti gli argomenti vengono convertiti in Unicode e viene eseguita una ricerca Unicode. Quando si usa il formato Unicode con LIKE, gli spazi finali sono significativi, a differenza del formato non Unicode, in cui gli spazi finali non sono significativi. La sintassi della stringa criterio di [!INCLUDE[esql](../../../../../../includes/esql-md.md)] corrisponde a quella di [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)].  
  
 Un criterio può includere caratteri normali e caratteri jolly. Durante la ricerca i caratteri normali devono corrispondere esattamente ai caratteri specificati nell'oggetto `string` di caratteri. I caratteri jolly possono tuttavia corrispondere a frammenti arbitrari della stringa di caratteri. Quando viene usato con i caratteri jolly, l'operatore LIKE è più flessibile rispetto agli operatori di confronto tra stringhe \= e \!\=.  
  
> [!NOTE]
>  Se la destinazione è costituita da un provider specifico, è possibile usare estensioni specifiche del provider. Tali costrutti possono tuttavia essere trattati in modo diverso, ad esempio da altri provider. SqlServer supporta ad esempio i modelli \[first\-last\] e \[^first\-last\], dove il primo consente di trovare una corrispondenza esatta di un carattere compreso tra il primo e l'ultimo, mentre il secondo consente di trovare una corrispondenza esatta di un carattere non compreso tra il primo e l'ultimo.  
  
### Escape  
 Usando la clausola ESCAPE, è possibile cercare stringhe di caratteri che includono uno o più dei caratteri jolly speciali descritti nella tabella nella sezione precedente. Si presupponga, ad esempio, che diversi documenti includano il valore letterale "100%" nel titolo e che si desideri cercare tutti i documenti di questo tipo. Poiché il carattere di percentuale \(%\) è un carattere jolly, è necessario usare caratteri di escape per questo carattere usando la clausola ESCAPE [!INCLUDE[esql](../../../../../../includes/esql-md.md)] per eseguire correttamente la ricerca. Di seguito viene illustrato un esempio di questo filtro.  
  
```  
"title like '%100!%%' escape '!'"  
```  
  
 In questa espressione di ricerca il carattere jolly di percentuale \(%\) immediatamente successivo al carattere punto esclamativo \(\!\) viene trattato come valore letterale anziché come carattere jolly. È possibile usare come carattere di escape qualsiasi carattere, ad eccezione dei caratteri jolly [!INCLUDE[esql](../../../../../../includes/esql-md.md)] e delle parentesi quadre \(`[ ]`\). Nell'esempio precedente il carattere punto esclamativo \(\!\) è il carattere di escape.  
  
## Esempio  
 Nelle due query [!INCLUDE[esql](../../../../../../includes/esql-md.md)] seguenti vengono usati gli operatori LIKE e ESCAPE per determinare se una stringa di caratteri specifica corrisponde a un criterio specificato. La prima query consente di eseguire una ricerca per l'oggetto `Name` che inizia con i caratteri `Down_`. In questa query viene usata l'opzione ESCAPE perché la sottolineatura \(`_`\) è un carattere jolly. Senza l'opzione ESCAPE, tramite la query verrebbe eseguita una ricerca di qualsiasi valore `Name` che inizia con la parola `Down` seguita da qualsiasi carattere singolo diverso dal carattere di sottolineatura. Le query sono basate sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecutePrimitiveTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#LIKE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#like)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)