---
title: "A reference was created to embedded interop assembly &#39;&lt;assembly1&gt;&#39; because of an indirect reference to that assembly from assembly &#39;&lt;assembly2&gt;&#39; | Microsoft Docs"
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
  - "vbc40059"
  - "bc40059"
helpviewer_keywords: 
  - "VBC40059"
  - "BC40059"
ms.assetid: 520e39cb-8ab6-46f5-aa00-08afd51b4b7c
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# A reference was created to embedded interop assembly &#39;&lt;assembly1&gt;&#39; because of an indirect reference to that assembly from assembly &#39;&lt;assembly2&gt;&#39;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È stato creato un riferimento all'assembly di interoperabilità incorporato '\<assembly1\>' a causa di un riferimento indiretto a tale assembly dall'assembly '\<assembly2\>'.Modificare la proprietà "Incorpora tipi di interoperabilità" su un assembly.  
  
 È stato aggiunto un riferimento a un assembly \(assembly1\) che dispone della proprietà `Embed Interop Types` impostata su `True`.  Ciò indica al compilatore di incorporare informazioni sul tipo di interoperabilità da tale assembly.  Tuttavia, il compilatore non può incorporare informazioni sul tipo di interoperabilità da tale assembly perché anche un altro assembly a cui si è fatto riferimento \(assembly2\) fa riferimento a quell'assembly \(assembly1\) e dispone della proprietà `Embed Interop Types` impostata su `False`.  
  
> [!NOTE]
>  L'impostazione della proprietà `Embed Interop Types` per un riferimento all'assembly su `True` equivale a fare riferimento all'assembly utilizzando l'opzione `/link` per il compilatore della riga di comando.  
  
 **ID errore:** BC40059  
  
### Se viene visualizzato questo avvertimento  
  
-   Per incorporare informazioni sul tipo di interoperabilità per entrambi gli assembly, impostare la proprietà `Embed Interop Types` per tutti i riferimenti all'assembly1 su `True`.  
  
-   Per rimuovere l'avviso, è possibile impostare la proprietà `Embed Interop Types` dell'assembly1 su `False`.  In questo caso, le informazioni sul tipo di interoperabilità vengono fornite da un assembly di interoperabilità primario.  
  
## Vedere anche  
 [\/link](../../../visual-basic/reference/command-line-compiler/link.md)   
 [Programming with Primary Interop Assemblies](http://msdn.microsoft.com/it-it/306fa1d6-0703-4004-9e93-d0a57f1be81e)