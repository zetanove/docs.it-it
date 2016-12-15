---
title: "Attribute &#39;&lt;attributename&gt;&#39; cannot be applied multiple times | Microsoft Docs"
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
  - "bc30663"
  - "vbc30663"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30663"
ms.assetid: 3760e7ff-7238-40a1-8676-77d858a64fc0
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Attribute &#39;&lt;attributename&gt;&#39; cannot be applied multiple times
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile applicare l'attributo una sola volta.  Il numero di volte per cui è possibile utilizzare un attributo viene specificato tramite l'attributo `AttributeUsage`.  
  
 **ID errore:** BC30663  
  
### Per correggere l'errore  
  
1.  Assicurarsi che l'attributo sia applicato solo una volta.  
  
2.  Se si utilizzano attributi personalizzati, provare a modificare l'attributo `AttributeUsage` relativo all'attributo per cui si desidera consentire più utilizzi, come illustrato nel seguente esempio.  
  
    ```  
    <AttributeUsage(AllowMultiple := True)>  
    ```  
  
## Vedere anche  
 <xref:System.AttributeUsageAttribute>   
 [Creazione di attributi personalizzati](../Topic/Creating%20Custom%20Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [AttributeUsage](../Topic/AttributeUsage%20\(C%23%20and%20Visual%20Basic\).md)