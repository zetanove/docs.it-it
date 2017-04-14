---
title: "Esecuzione di query | Microsoft Docs"
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
ms.assetid: c0e6cf23-63ac-47dd-bfe9-d5bdca826fac
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Esecuzione di query
Dopo essere stata creata da un utente, una query LINQ viene convertita in un albero dei comandi.  Un albero dei comandi è una rappresentazione di una query compatibile con Entity Framework.  L'albero dei comandi viene quindi eseguito sull'origine dati.  In fase di runtime della query, tutte le espressioni di query, ovvero tutti i componenti della query, vengono valutate, incluse le espressioni usate nella materializzazione del risultato.  
  
 Il momento di esecuzione delle espressioni di query può variare.  Le query LINQ vengono sempre eseguite quando la variabile di query viene scorsa e non quando viene creata.  Questo processo è noto come *esecuzione posticipata*.  È inoltre possibile forzare l'esecuzione immediata di una query. Questa operazione è utile per memorizzare nella cache i risultati della query  e verrà descritta di seguito in questo argomento.  
  
 Quando viene eseguita una query LINQ to Entities, è possibile che alcune espressioni nella query vengano eseguite nel server e che alcune parti vengano eseguite localmente nel client.  La valutazione sul lato client di un'espressione viene effettuata prima dell'esecuzione della query nel server.  Se un'espressione viene valutata nel client, il risultato della valutazione sostituisce l'espressione nella query e la query viene quindi eseguita nel server.  Poiché le query vengono eseguite sull'origine dati, la configurazione dell'origine dati prevale sul comportamento specificato nel client.  La gestione dei valori Null e la precisione numerica dipendono ad esempio dalle impostazioni del server.  Tutte le eccezioni generate durante l'esecuzione della query nel server vengono passate direttamente al client.  
  
## Esecuzione di query posticipata  
 In una query che restituisce una sequenza di valori, la variabile di query stessa non contiene mai i risultati della query ma viene usata solo per l'archiviazione dei comandi della query.  L'esecuzione della query viene posticipata finché non viene eseguita un'iterazione della variabile di query in un ciclo `foreach` o `For Each`.  In base a questo approccio, noto come *esecuzione posticipata*, la query viene eseguita qualche tempo dopo essere stata costruita.  È quindi possibile eseguire una query il numero di volte desiderato.  Tale caratteristica è utile, ad esempio, quando si dispone di un database che viene aggiornato da altre applicazioni.  Nell'applicazione è possibile creare una query per recuperare le informazioni più recenti ed eseguire ripetutamente la query che restituisce ogni volta le informazioni aggiornate.  
  
 L'esecuzione posticipata consente di combinare più query o di estendere una query.  Una query estesa viene modificata in modo da includere nuove operazioni. Le modifiche verranno quindi riflesse nell'eventuale esecuzione.  Nell'esempio seguente la prima query restituisce tutti i prodotti.  La seconda query estende la prima usando `Where` per restituire tutti i prodotti di taglia "L":  
  
 [!code-csharp[DP L2E Conceptual Examples#Composing1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#composing1)]
 [!code-vb[DP L2E Conceptual Examples#Composing1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#composing1)]  
  
 Dopo aver eseguito una query, per tutte le query successive vengono usati gli operatori LINQ in memoria.  Se si scorre una variabile di query usando un'istruzione `foreach` o `For Each` o chiamando uno degli operatori di conversione LINQ, la query viene eseguita immediatamente.  Gli operatori di conversione includono <xref:System.Linq.Enumerable.ToList%2A>, <xref:System.Linq.Enumerable.ToArray%2A>, <xref:System.Linq.Enumerable.ToLookup%2A> e <xref:System.Linq.Enumerable.ToDictionary%2A>.  
  
## Esecuzione di query immediata  
 A differenza dell'esecuzione posticipata delle query che restituiscono una sequenza di valori, le query che restituiscono un valore singleton vengono eseguite immediatamente.  Alcuni esempi di query singleton sono <xref:System.Linq.Enumerable.Average%2A>, <xref:System.Linq.Enumerable.Count%2A>, <xref:System.Linq.Enumerable.First%2A> e <xref:System.Linq.Enumerable.Max%2A>.  Tali query vengono eseguite immediatamente perché la query deve restituire una sequenza per calcolare il risultato singleton.  È anche possibile forzare l'esecuzione immediata.  Questa operazione è utile quando si desidera memorizzare nella cache i risultati di una query.  Per forzare l'esecuzione immediata di una query che non restituisce un valore singleton, è possibile chiamare il metodo <xref:System.Linq.Enumerable.ToList%2A>, <xref:System.Linq.Enumerable.ToDictionary%2A> o <xref:System.Linq.Enumerable.ToArray%2A> su una query o su una variabile di query.  Nell'esempio seguente viene usato il metodo <xref:System.Linq.Enumerable.ToArray%2A> per restituire immediatamente una matrice da una sequenza.  
  
 [!code-csharp[DP L2E Examples#ToArray](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#toarray)]
 [!code-vb[DP L2E Examples#ToArray](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#toarray)]  
  
 È anche possibile forzare l'esecuzione inserendo il ciclo `foreach` o `For Each` immediatamente dopo l'espressione di query, mentre chiamando <xref:System.Linq.Enumerable.ToList%2A> o <xref:System.Linq.Enumerable.ToArray%2A> si memorizzano nella cache tutti i dati in un singolo oggetto Collection.  
  
## Esecuzione nell'archivio  
 Poiché in genere le espressioni in LINQ to Entities vengono valutate nel server, non è previsto che il comportamento dell'espressione sia conforme alla semantica CLR \(Common Language Runtime\), ma piuttosto a quella dell'origine dati.  Vi sono tuttavia eccezioni, ad esempio quando l'espressione viene eseguita nel client.  Questo può provocare risultati imprevisti, ad esempio quando il server e il client si trovano in fusi orari diversi.  
  
 Alcune espressioni nella query possono venire eseguite nel client.  In generale, è previsto che la maggior parte dell'esecuzione della query avvenga nel server.  Oltre ai metodi eseguiti su elementi della query mappati all'origine dati, vi sono spesso espressioni nella query che possono essere eseguite localmente.  L'esecuzione locale di un'espressione di query produce un valore che può essere usato nell'esecuzione della query o nella costruzione del risultato.  
  
 Determinate operazioni vengono eseguite sempre nel client, ad esempio l'associazione di valori, le sottoespressioni, le sottoquery e la materializzazione di oggetti nei risultati della query.  Di conseguenza questi elementi, ad esempio i valori dei parametri, non possono essere aggiornati durante l'esecuzione.  I tipi anonimi possono essere costruiti inline nell'origine dati, ma questo comportamento non deve essere presupposto.  Anche i raggruppamenti inline possono essere costruiti nell'origine dati, ma questo comportamento non deve essere presupposto in ogni istanza.  In generale, è consigliabile non fare presupposizioni relativamente agli elementi che verranno costruiti nel server.  
  
 Contenuto della sezione vengono descritti scenari in cui il codice viene eseguito localmente nel client.  Per altre informazioni sui tipi di espressioni eseguiti localmente, vedere [Espressioni nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md).  
  
### Valori letterali e parametri  
 Le variabili locali, ad esempio la variabile `orderID` nell'esempio seguente, vengono valutate nel client.  
  
 [!code-csharp[DP L2E Conceptual Examples#LiteralParameter1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#literalparameter1)]
 [!code-vb[DP L2E Conceptual Examples#LiteralParameter1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#literalparameter1)]  
  
 Anche i parametri dei metodi vengono valutati nel client.  Un esempio è costituito dal parametro `orderID` passato al metodo `MethodParameterExample`, come illustrato di seguito.  
  
 [!code-csharp[DP L2E Conceptual Examples#MethodParameterExample](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#methodparameterexample)]
 [!code-vb[DP L2E Conceptual Examples#MethodParameterExample](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#methodparameterexample)]  
  
### Esecuzione del cast di valori letterali nel client  
 Il cast da un valore `null` a un tipo CLR viene eseguito nel client:  
  
 [!code-csharp[DP L2E Conceptual Examples#NullCastToString](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#nullcasttostring)]
 [!code-vb[DP L2E Conceptual Examples#NullCastToString](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#nullcasttostring)]  
  
 Il cast a un tipo, ad esempio un oggetto <xref:System.Decimal> che ammette i valori Null, viene eseguito nel client:  
  
 [!code-csharp[DP L2E Conceptual Examples#CastToNullable](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#casttonullable)]
 [!code-vb[DP L2E Conceptual Examples#CastToNullable](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#casttonullable)]  
  
### Costruttori per i valori letterali  
 I nuovi tipi CLR di cui è possibile eseguire il mapping al modello concettuale vengono eseguiti nel client:  
  
 [!code-csharp[DP L2E Conceptual Examples#ConstructorForLiteral](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#constructorforliteral)]
 [!code-vb[DP L2E Conceptual Examples#ConstructorForLiteral](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#constructorforliteral)]  
  
 Anche le nuove matrici vengono eseguite nel client.  
  
## Eccezioni nell'archivio  
 Qualsiasi errore che si verifica nell'archivio durante l'esecuzione della query viene passato al client e non viene mappato o gestito.  
  
## Configurazione dell'archivio  
 Quando la query viene eseguita nell'archivio, la configurazione dell'archivio sostituisce tutti i comportamenti client e la semantica dell'archivio viene espressa per tutte le operazioni e le espressioni.  Ciò può determinare una differenza nel comportamento tra l'esecuzione nell'archivio e quella conforme a CLR per quanto riguarda aspetti come il confronto di valori Null, l'ordinamento di GUID, la precisione e l'accuratezza di operazioni che includono tipi di dati non precisi, ad esempio tipi a virgola mobile o <xref:System.DateTime>, e le operazioni di stringa.  È importante tenere presente questo aspetto quando si esaminano i risultati della query.  
  
 Di seguito vengono illustrate alcune differenze di comportamento tra CLR e SQL Server:  
  
-   In SQL Server i GUID vengono ordinati in modo diverso rispetto a CLR.  
  
-   Possono esserci anche differenze nella precisione del risultato in caso di utilizzo del tipo Decimal in SQL Server.  Queste differenze sono dovute ai requisiti fissi di precisione del tipo Decimal in SQL Server.  La media dei valori <xref:System.Decimal> 0,0, 0,0 e 1,0 è ad esempio 0,3333333333333333333333333333 nella memoria del client, ma 0,333333 nell'archivio, in base alla precisione predefinita per il tipo Decimal di SQL Server.  
  
-   Anche alcune operazioni di confronto di stringhe vengono gestite in SQL Server in modo diverso rispetto a quanto avviene in CLR.  Il comportamento del confronto di stringhe dipende dalle impostazioni delle regole di confronto nel server.  
  
-   Le chiamate alle funzioni o ai metodi, quando incluse in una query LINQ to Entities, vengono mappate a funzioni canoniche in Entity Framework, che vengono convertite quindi in Transact\-SQL ed eseguite nel database di SQL Server.  In alcuni casi il comportamento delle funzioni mappate può differire dall'implementazione nelle librerie di classi di base.  La chiamata ai metodi <xref:System.String.Contains%2A>, <xref:System.String.StartsWith%2A> e <xref:System.String.EndsWith%2A> con una stringa vuota come parametro restituisce ad esempio `true` quando eseguita in CLR, mentre restituisce `false` in caso di esecuzione in SQL Server.  Anche il metodo <xref:System.String.EndsWith%2A> può restituire risultati diversi, in quanto due stringhe che differiscono solo per lo spazio vuoto finale vengono considerate uguali in SQL Server ma non in CLR.  Questo comportamento è illustrato nell'esempio seguente:  
  
 [!code-csharp[DP L2E Conceptual Examples#CanonicalFuncVsCLRBaseType](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#canonicalfuncvsclrbasetype)]
 [!code-vb[DP L2E Conceptual Examples#CanonicalFuncVsCLRBaseType](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#canonicalfuncvsclrbasetype)]