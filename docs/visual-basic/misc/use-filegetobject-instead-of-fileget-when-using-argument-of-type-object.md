---
title: "Quando si usano argomenti di tipo &#39;Object&#39;, utilizzare &#39;FileGetObject&#39; anzich&#233; &#39;FileGet&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: 090b8088-895a-482a-9362-606596bac304
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Quando si usano argomenti di tipo &#39;Object&#39;, utilizzare &#39;FileGetObject&#39; anzich&#233; &#39;FileGet&#39;
Il metodo `FileGet` include un argomento di tipo `Object`. Per evitare ambiguità, è opportuno usare `FileGetObject` invece di `FileGet`.  
  
 Si noti che la funzionalità offerta da `My.Computer.Filesystem` garantisce una maggiore facilità d'uso e prestazioni superiori sia rispetto a `FileGet` che a `FileGetObject`.  
  
### Per correggere l'errore  
  
1.  Sostituire `FileGet` con `FileGetObject`.  
  
2.  Eseguire il cast dell'argomento `Object` su un tipo più specifico.  
  
## Vedere anche  
 [NOT IN BUILD: Funzione FileGetObject](http://msdn.microsoft.com/it-it/3eda786b-d1ee-4b44-9dd7-0ea6bff072c0)   
 [My.Computer.FileSystem Object](../../visual-basic/language-reference/objects/my-computer-filesystem-object.md)