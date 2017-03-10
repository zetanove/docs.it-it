---
title: "L&#39;uso dell&#39;istanza predefinita di una classe nel costruttore della classe potrebbe generare una chiamata ricorsiva infinita | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
ms.assetid: 9645b47f-7de5-46d0-bb45-d5fdaa8aaa2a
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# L&#39;uso dell&#39;istanza predefinita di una classe nel costruttore della classe potrebbe generare una chiamata ricorsiva infinita
Nel costruttore della classe è stata usata un'istanza predefinita di una classe. Questo può causare una chiamata ricorsiva infinita, detta anche ciclo infinito.  
  
### Per correggere l'errore  
  
-   Rimuovere l'istanza predefinita dal costruttore della classe.  
  
## Vedere anche  
 [NOT IN BUILD: Utilizzo di costruttori e distruttori](http://msdn.microsoft.com/it-it/548eebe1-86c4-4377-b2f5-447cb8be3d90)