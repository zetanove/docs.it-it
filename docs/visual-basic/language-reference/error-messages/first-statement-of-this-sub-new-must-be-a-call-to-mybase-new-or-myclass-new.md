---
title: "First statement of this &#39;Sub New&#39; must be a call to &#39;MyBase.New&#39; or &#39;MyClass.New&#39; (No Accessible Constructor Without Parameters) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30148"
  - "vbc30148"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30148"
ms.assetid: 4426e8fc-cb39-4eb8-ba95-503cd32fcc89
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# First statement of this &#39;Sub New&#39; must be a call to &#39;MyBase.New&#39; or &#39;MyClass.New&#39; (No Accessible Constructor Without Parameters)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La prima istruzione di questo 'Sub New' deve essere una chiamata a 'MyBase.New' o a 'MyClass.New' perché la classe base '\<nomebase\>' di '\<nomederivato\>' non dispone di un 'Sub New' accessibile che possa essere chiamato senza argomenti.  
  
 In una classe derivata ciascun costruttore deve chiamare un costruttore di classe base \(`MyBase.New`\).  Se per la classe base è definito un costruttore senza parametri accessibile alle classi derivate, `MyBase.New` può essere chiamata automaticamente.  In caso contrario, è necessario chiamare un costruttore di classe base con parametri, ma questa operazione non può essere eseguita automaticamente.  In questo caso, la prima istruzione di ciascun costruttore di classe derivata deve chiamare un costruttore con parametri sulla classe base, oppure un altro costruttore nella classe derivata che effettua una chiamata al costruttore della classe base.  
  
 **ID errore:** BC30148  
  
### Per correggere l'errore  
  
-   Chiamare `MyBase.New` specificando i parametri richiesti, oppure chiamare un costruttore paritetico che esegua la chiamata.  
  
     Ad esempio, se la classe base dispone di un costruttore che viene dichiarato come `Public Sub New(ByVal index as Integer)`, la prima istruzione nel costruttore della classe derivata potrebbe essere `MyBase.New(100)`.  
  
## Vedere anche  
 [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)