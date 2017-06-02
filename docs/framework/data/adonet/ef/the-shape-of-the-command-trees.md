---
title: "Forma degli alberi dei comandi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2215585e-ca47-45f8-98d4-8cb982f8c1d3
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Forma degli alberi dei comandi
Il modulo di generazione SQL è responsabile della generazione di una query SQL specifica di back\-end basata su una determinata espressione dell'albero dei comandi della query di input.  Questa sezione descrive le caratteristiche, le proprietà e la forma degli alberi dei comandi di query.  
  
## Panoramica degli alberi dei comandi di query  
 Un albero dei comandi di query è una rappresentazione del modello a oggetti di una query.  Tali alberi dei comandi di query hanno due funzioni:  
  
-   Esprimere una query di input specificata per [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
-   Esprimere una query di output specificata per un provider, che descrive una query sul back\-end.  
  
 Gli alberi dei comandi di query supportano una semantica più completa rispetto alle query conformi a SQL:1999, che include il supporto per l'uso di raccolte annidate e l'esecuzione di operazioni sui tipi, ad esempio quelle per verificare se un'entità è di un determinato tipo o filtrare i set in base a un tipo.  
  
 La proprietà DBQueryCommandTree.Query è la radice dell'albero delle espressioni che descrive la logica della query.  La proprietà DBQueryCommandTree.Parameters contiene un elenco di parametri usati nella query.  L'albero delle espressioni è costituito da oggetti DbExpression.  
  
 Un oggetto DbExpression rappresenta un'attività di calcolo.  In [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] sono disponibili diversi tipi di espressione per la creazione di espressioni di query, incluse costanti, variabili, funzioni, costruttori e operatori relazionali standard come gli operatori di filtro e join.  Ogni oggetto DbExpression include una proprietà ResultType che rappresenta il tipo di risultato prodotto dall'espressione.  Questo tipo viene espresso come TypeUsage.  
  
## Forme dell'albero dei comandi di query di output  
 Gli alberi dei comandi di query di output rappresentano in modo accurato query SQL relazionali e rispettano regole più rigorose rispetto a quelle applicate agli alberi dei comandi di query.  Contengono in genere costrutti che vengono convertiti facilmente in SQL.  
  
 Gli alberi dei comandi di input vengono espresse in base al modello concettuale, che supporta proprietà di navigazione, associazioni tra entità ed ereditarietà.  Gli alberi dei comandi di output vengono espresse in base al modello di archiviazione.  Diversamente da questi ultimi, gli alberi dei comandi di input consentono di proiettare raccolte annidate.  
  
 Gli alberi dei comandi di query di output vengono compilati usando un subset degli oggetti DbExpression disponibili, che contiene alcune espressioni con un utilizzo limitato.  
  
 Le operazioni sui tipi, ad esempio quelle per verificare se una determinata espressione è di un tipo specifico o filtrare i set in base a un tipo, non sono presenti negli alberi dei comandi di output.  
  
 Negli alberi dei comandi di output solo le espressioni che restituiscono valori booleani vengono usate per le proiezioni e solo per i predicati nelle espressioni che richiedono un predicato, ad esempio un'istruzione Case o per il filtro.  
  
 La radice degli alberi dei comandi di query di output è un oggetto DbProjectExpression.  
  
### Tipi di espressione non inclusi negli alberi dei comandi di query di output  
 I tipi di espressione seguenti non sono validi in un albero dei comandi di query di output e non devono essere gestiti dai provider:  
  
 DbDerefExpression  
  
 DbEntityRefExpression  
  
 DbRefKeyExpression  
  
 DbIsOfExpression  
  
 DbOfTypeExpression  
  
 DbRefExpression  
  
 DbRelationshipNavigationExpression  
  
 DbTreatExpression  
  
### Restrizioni e note relative alle espressioni  
 Molte espressioni possono essere usate solo in modo limitato negli alberi dei comandi di query di output:  
  
#### DbFunctionExpression  
 È possibile passare i tipi di funzione seguenti:  
  
-   Funzioni canoniche riconosciute dallo spazio dei nomi Edm.  
  
-   Funzioni di archivio predefinite riconosciute da BuiltInAttribute.  
  
-   Funzioni definite dall'utente.  
  
 Le funzioni canoniche \(vedere [Funzioni canoniche](../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md) per altre informazioni\) vengono specificate come parte di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] e i provider devono fornire implementazioni per le funzioni canoniche basate su tali specifiche.  Le funzioni di archivio si basano sulle specifiche contenute nel file manifesto del provider corrispondente.  Le funzioni definite dall'utente si basano sulle specifiche di SSDL.  
  
 Inoltre, le funzioni che includono l'attributo NiladicFunction non dispongono di argomenti e devono essere convertite senza la parentesi finale,  ovvero in *\<functionName\>* anziché in *\<functionName\>\(\)*.  
  
#### DbNewInstanceExpression  
 DbNewInstanceExpression può essere specificato solo nei due casi seguenti:  
  
-   Come proprietà Projection di DbProjectExpression.  In questo caso, vengono applicate le restrizioni seguenti:  
  
    -   Il risultato deve essere un tipo di riga.  
  
    -   I relativi argomenti devono essere espressioni che producono un risultato con un tipo primitivo.  In genere, ogni argomento è un'espressione scalare, ad esempio un oggetto PropertyExpression su un oggetto DbVariableReferenceExpression, una chiamata a una funzione o un calcolo aritmetico di DbPropertyExpression su un oggetto DbVariableReferenceExpression o una chiamata a una funzione.  È tuttavia possibile specificare un'espressione che rappresenta una subquery scalare anche nell'elenco di argomenti di un oggetto DbNewInstanceExpression.  Un'espressione che rappresenta una subquery scalare è un albero delle espressioni che rappresenta una subquery che restituisce esattamente una riga e una colonna di un tipo primitivo con una radice dell'oggetto DbElementExpression.  
  
-   Con un tipo restituito di raccolta, nel qual caso definisce una nuova raccolta delle espressioni specificate come argomenti.  
  
#### DbVariableReferenceExpression  
 Un oggetto DbVariableReferenceExpression deve essere un elemento figlio del nodo DbPropertyExpression.  
  
#### DbGroupByExpression  
 La proprietà Aggregates di un oggetto DbGroupByExpression può presentare solo elementi di tipo DbFunctionAggregate.  Non esistono altri tipi di aggregazione.  
  
#### DbLimitExpression  
 La proprietà Limit può essere solo un oggetto DbConstantExpression o DbParameterReferenceExpression.  Inoltre, la proprietà WithTies è sempre false in .NET Framework 3.5 e versioni precedenti.  
  
#### DbScanExpression  
 Quando viene usato negli alberi dei comandi di output, DbScanExpression rappresenta in modo efficiente un'analisi di una query di tabella, visualizzazione o archivio, rappresentata da EnitySetBase::Target.  
  
 Se la query di definizione della proprietà Target dei metadati è diversa da null, rappresenta una query il cui testo è specificato nella proprietà dei metadati con il linguaggio o il sottolinguaggio specifico del provider in base a quanto specificato nella definizione dello schema dell'archivio.  
  
 In caso contrario, la destinazione rappresenta una tabella o una visualizzazione.  Il prefisso dello schema si trova nella proprietà dei metadati "Schema", se non è null. In caso contrario, corrisponde al nome del contenitore di entità.  Il nome della tabella o della visualizzazione corrisponde alla proprietà dei metadati "Table", se non è null. In caso contrario, corrisponde alla proprietà Name della base dei set di entità.  
  
 Tutte queste proprietà hanno origine dalla definizione dell'EntitySet corrispondente nel file SSDL \(Store Schema Definition Language\).  
  
### Utilizzo dei tipi primitivi  
 Quando si fa riferimento ai tipi primitivi negli alberi dei comandi di output, in genere il riferimento è contenuto nei tipi primitivi del modello concettuale.  Per determinate espressioni, tuttavia, i, provider richiedono il tipo primitivo dell'archivio corrispondente.  Esempi di tali espressioni includono DbCastExpression e in alcuni casi DbNullExpression, se il provider deve eseguire il cast del valore null al tipo corrispondente.  In questi casi, i provider devono eseguire il mapping al tipo di provider in base al tipo primitivo e ai relativi facet.  
  
## Vedere anche  
 [Generazione SQL](../../../../../docs/framework/data/adonet/ef/sql-generation.md)