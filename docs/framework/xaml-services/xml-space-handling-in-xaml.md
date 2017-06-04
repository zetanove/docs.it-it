---
title: "xml:space Handling in XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XAML [XAML Services], xml:space attribute"
  - "XAML [XAML Services], whitespace processing"
  - "xml:space attribute [XAML Services]"
  - "whitespace processing [XAML Services]"
ms.assetid: 5e1814f0-5b30-43d5-8c88-dede335a89d7
caps.latest.revision: 15
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 15
---
# xml:space Handling in XAML
L'attributo `xml:space` è un attributo definito da XML che dichiara il comportamento di elaborazione degli spazi vuoti significativi all'interno di un elemento oggetto.  Tale comportamento è relativo a tutto il contenuto \(testo interno\) all'interno dell'elemento dove `xml:space` viene dichiarato, e anche agli ambiti degli elementi figlio.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object xml:space="preserve" />  
```  
  
 \- oppure \-  
  
```  
<object xml:space="default" />  
```  
  
## Note  
 La definizione dell'attributo `xml:space` in XAML inclusi i due valori possibili è derivata da `xml:space` definito come un "attributo speciale" dalle specifiche W3C per XML.  
  
 Il valore predefinito dell’attributo `xml:space` è il valore letterale `"default"`.  Per il valore `"default"`, oppure se `xml:space` non è indicato, il comportamento di analisi degli spazi vuoti significativi è la gestione predefinita, come definito nell’argomento [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md).  
  
 Per mantenere gli spazi vuoti all'interno del contenuto degli elementi oggetto, specificare `xml:space="preserve"` in quell’elemento oggetto.  
  
 Nella maggior parte delle interpretazioni, l'ambito degli effetti dell'attributo `xml:space` e del valore dell'attributo è costituito dagli elementi figlio.  
  
 Per una discussione completa sull'elaborazione di spazi vuoti in XAML, vedere [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md).  
  
## Vedere anche  
 [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)