---
title: "Esecuzione di query tra relazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 297878d0-685b-4c01-b2e0-9d731b7322bc
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Esecuzione di query tra relazioni
I riferimenti ad altri oggetti o raccolte di altri oggetti nelle definizioni della classe corrispondono direttamente alle relazioni di chiavi esterne nel database.  È possibile usare queste relazioni quando si esegue una query usando la notazione del punto per accedere alle proprietà della relazione e spostarsi tra gli oggetti.  Queste operazioni di accesso vengono convertite in join più complessi o sottoquery correlate nell'equivalente SQL.  
  
 Ad esempio, usando la query seguente è possibile spostarsi da ordini a clienti per limitare i risultati solo agli ordini per i clienti residenti nell'area londinese.  
  
 [!code-csharp[DLinqQueryConcepts#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#3)]
 [!code-vb[DLinqQueryConcepts#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#3)]  
  
 Se le proprietà della relazione non esistessero, sarebbe necessario scriverle manualmente come *join*, esattamente come in una query SQL, come nel codice seguente:  
  
 [!code-csharp[DLinqQueryConcepts#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#4)]
 [!code-vb[DLinqQueryConcepts#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#4)]  
  
 È possibile usare la proprietà della *relazione* per definire questa particolare relazione una sola volta,  quindi usare la più pratica sintassi del punto.  Le proprietà della relazione esistono tuttavia soprattutto perché i modelli a oggetti specifici del dominio sono in genere definiti come gerarchie o grafici.  Gli oggetti usati nella programmazione dispongono di riferimenti ad altri oggetti.  È solo una coincidenza che le relazioni da oggetto a oggetto corrispondano alle relazioni di tipo chiave esterna nei database.  L'accesso alle proprietà offre quindi un modo pratico per scrivere join.  
  
 A questo riguardo, le proprietà della relazione sono più importanti sul lato dei risultati di una query anziché nella query stessa.  Dopo il recupero dei dati su un cliente particolare tramite la query, la definizione della classe indica che sono presenti ordini.  In altre parole, si prevede che la proprietà `Orders` di un particolare cliente sia una raccolta popolata con tutti gli ordini di tale cliente.  Si tratta in effetti del contratto dichiarato definendo le classi in questo modo.  Si prevede che nei risultati siano inclusi gli ordini, anche se non sono stati espressamente richiesti nella query.  Si prevede che il modello a oggetti appaia come un'estensione in memoria del database con gli oggetti correlati immediatamente disponibili.  
  
 Dopo avere creato le relazioni, è possibile scrivere query facendo riferimento alle proprietà delle relazioni definite nelle classi.  Questi riferimenti alle relazioni corrispondono alle relazioni di chiave esterna nel database.  Le operazioni che usano queste relazioni vengono convertite in join più complessi nell'equivalente SQL.  A condizione che sia stata definita una relazione usando l'attributo <xref:System.Data.Linq.Mapping.AssociationAttribute>, non sarà necessario codificare un join esplicito in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 Per mantenere questa apparenza, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene implementata una tecnica detta *caricamento posticipato*.  Per altre informazioni, vedere [Caricamento rinviato e immediato](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md).  
  
 Si consideri la query SQL seguente per la proiezione di un elenco di coppie `CustomerID`\- `OrderID`:  
  
```  
SELECT t0.CustomerID, t1.OrderID  
FROM   Customers AS t0 INNER JOIN  
          Orders AS t1 ON t0.CustomerID = t1.CustomerID  
WHERE  (t0.City = @p0)  
```  
  
 Per ottenere gli stessi risultati tramite [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], usare il riferimento alla proprietà `Orders` esistente nella classe `Customer`.  Il riferimento a `Orders` fornisce le informazioni necessarie per eseguire la query e creare una proiezione delle coppie `CustomerID`\-`OrderID`, come nel codice seguente:  
  
 [!code-csharp[DLinqQueryConcepts#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#5)]
 [!code-vb[DLinqQueryConcepts#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#5)]  
  
 È inoltre possibile procedere in senso inverso,  ovvero eseguire una query su `Orders` e usare il relativo riferimento alla relazione di `Customer` per accedere alle informazioni sull'oggetto `Customer` associato.  Nel codice seguente vengono proiettate le stesse coppie `CustomerID`\-`OrderID` come nell'esempio precedente, ma in questo caso eseguendo una query su `Orders` anziché su `Customers`.  
  
 [!code-csharp[DLinqQueryConcepts#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#6)]
 [!code-vb[DLinqQueryConcepts#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#6)]  
  
## Vedere anche  
 [Concetti relativi alle query](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)