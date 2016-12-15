---
title: "Procedura: utilizzare un dizionario per archiviare istanze di evento (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "eventi [C#], memorizzazione di istanze in un oggetto Dictionary"
ms.assetid: 9512c64d-5aaf-40cd-b941-ca2a592f0064
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: utilizzare un dizionario per archiviare istanze di evento (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare `accessor-declarations` per esporre numerosi eventi senza allocare un campo per ciascuno di essi, bensì utilizzando un dizionario per archiviare le istanze degli venti.  Tuttavia, questa soluzione risulta utile solo se il numero di eventi è elevato e si prevede che la maggior parte non venga implementata.  
  
## Esempio  
 [!code-cs[csProgGuideEvents#9](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-use-a-dictionary-to-store-event-instances_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)