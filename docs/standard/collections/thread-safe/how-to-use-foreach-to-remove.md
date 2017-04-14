---
title: "Procedura: utilizzare ForEach per rimuovere elementi in un oggetto BlockingCollection | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "raccolte thread-safe, modalità di enumerazione di raccolte di blocco"
ms.assetid: 2096103c-22f7-420d-b631-f102bc33a6dd
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: utilizzare ForEach per rimuovere elementi in un oggetto BlockingCollection
Oltre a ottenere gli elementi da un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> tramite i metodi <xref:System.Collections.Concurrent.BlockingCollection%601.Take%2A> e <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A>, per rimuovere gli elementi è anche possibile utilizzare un ciclo [foreach](../Topic/foreach,%20in%20\(C%23%20Reference\).md) \([For Each](../Topic/For%20Each...Next%20Statement%20\(Visual%20Basic\).md) in Visual Basic\) finché l'aggiunta non è stata eseguita e la raccolta è vuota.  Si tratta di una *enumerazione di modifica* o *enumerazione di utilizzo* perché, diversamente da un ciclo `foreach` \(`For Each`\) tipico, questo enumeratore modifica la raccolta di origine rimuovendo gli elementi.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come rimuovere tutti gli elementi in un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> tramite un ciclo `foreach` \(`For Each`\).  
  
 [!code-csharp[CDS_BlockingCollection#03](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example03.cs#03)]
 [!code-vb[CDS_BlockingCollection#03](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/enumeratebc.vb#03)]  
  
 In questo esempio viene utilizzato un ciclo `foreach` con il metodo <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A?displayProperty=fullName> nel thread consumer, affinché ciascun elemento venga rimosso dalla raccolta secondo l'enumerazione.  L'oggetto <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> limita il numero massimo di elementi che la raccolta può contenere in qualsiasi momento.  L'enumerazione della raccolta eseguita in questo modo blocca il thread consumer se non è disponibile alcun elemento o se la raccolta è vuota.  In questo esempio il blocco non rappresenta un problema poiché la velocità con cui il thread producer aggiunge elementi è maggiore della velocità massima con cui vengono utilizzati.  
  
 Non esiste alcuna garanzia che gli elementi vengano enumerati nello stesso ordine in cui vengono aggiunti dai thread producer.  
  
 Per enumerare la raccolta senza modificarla, utilizzare semplicemente `foreach` \(`For Each`\) senza il metodo <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A>.  Tuttavia, è importante capire che questo tipo di enumerazione rappresenta uno snapshot della raccolta in un dato momento.  Se altri thread aggiungono o rimuovono elementi contemporaneamente mentre si esegue il ciclo, il ciclo potrebbe non rappresentare lo stato effettivo della raccolta.  
  
## Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Parallel Programming](../../../../docs/standard/parallel-programming/index.md)