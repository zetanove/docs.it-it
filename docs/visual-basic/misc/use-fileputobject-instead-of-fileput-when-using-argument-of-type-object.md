---
title: "Quando si usano argomenti di tipo &#39;Object&#39;, utilizzare &#39;FilePutObject&#39; anzich&#233; &#39;FilePut&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrUseFilePutObject"
ms.assetid: d207b9b7-5898-4c13-8b03-9feefac5f726
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Quando si usano argomenti di tipo &#39;Object&#39;, utilizzare &#39;FilePutObject&#39; anzich&#233; &#39;FilePut&#39;
Il metodo `FilePut` include un argomento di tipo`Object`. Per evitare ambiguità, è opportuno usare `FilePutObject` invece di `FilePut`.  
  
### Per correggere l'errore  
  
-   Sostituire `FilePut` con `FilePutObject`.  
  
-   Eseguire il cast dell'argomento `Object` su un tipo più specifico.  
  
-   Usare la funzionalità disponibile nell'oggetto `My.Computer.FileSystem`.  
  
## Vedere anche  
 [NOT IN BUILD: Funzione FilePutObject](http://msdn.microsoft.com/it-it/a0f52a1c-5ecc-4945-b18c-03147af61d6b)   
 [My.Computer.FileSystem Object](../../visual-basic/language-reference/objects/my-computer-filesystem-object.md)   
 [Metodo My.Computer.FileSystem.WriteAllBytes](http://msdn.microsoft.com/it-it/b1a24dc1-eac8-4e22-8ffa-cc3bacbaf826)