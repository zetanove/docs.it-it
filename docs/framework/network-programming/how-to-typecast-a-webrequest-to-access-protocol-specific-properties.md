---
title: "Procedura: Eseguire il cast di tipo di un oggetto WebRequest per accedere a propriet&#224; specifiche del protocollo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: d9a8eae2-7454-46f9-b43b-c98477c5bcde
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Procedura: Eseguire il cast di tipo di un oggetto WebRequest per accedere a propriet&#224; specifiche del protocollo
In questo esempio viene illustrato come eseguire un cast di tipo su una WebRequest in modo che sia possibile accedere a proprietà specifiche del protocollo.  
  
## Esempio  
  
```csharp  
HttpWebRequest httpreq =   
   (HttpWebRequest) WebRequest.Create("http://www.contoso.com/");  
```  
  
```vb  
Dim httpreq As HttpWebRequest = _  
   CType(WebRequest.Create("http://www.contoso.com/"), HttpWebRequest)  
```  
  
## Vedere anche  
 [Programmazione di protocolli di collegamento](../../../docs/framework/network-programming/programming-pluggable-protocols.md)