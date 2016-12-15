---
title: "&#39;&lt;attribute&gt;&#39; cannot be applied because the format of the GUID &#39;&lt;number&gt;&#39; is not correct | Microsoft Docs"
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
  - "vbc32500"
  - "bc32500"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32500"
ms.assetid: 6fa34c55-368e-4d7d-b488-07a3fffe045f
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;&lt;attribute&gt;&#39; cannot be applied because the format of the GUID &#39;&lt;number&gt;&#39; is not correct
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un blocco di attributi `COMClassAttribute` specifica un identificatore univoco globale \(GUID\) non conforme al formato appropriato per un GUID.  `COMClassAttribute` utilizza i GUID per identificare in modo univoco la classe, l'interfaccia e l'evento di creazione.  
  
 Un GUID è composto da 16 byte \(otto byte numerici seguiti da otto byte binari\).  È generato da utilità Microsoft quali uuidgen.exe ed è univoco nello spazio e nel tempo.  
  
 **ID errore:** BC32500  
  
### Per correggere l'errore  
  
1.  Determinare il GUID o i GUID corretti necessari per identificare l'oggetto COM.  
  
2.  Assicurarsi che le stringhe GUID presentate al blocco di attributi `COMClassAttribute` siano copiate correttamente.  
  
## Vedere anche  
 <xref:System.Guid>   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)