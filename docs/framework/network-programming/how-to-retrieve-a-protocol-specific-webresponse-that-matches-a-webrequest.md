---
title: "Procedura: Recuperare un oggetto WebResponse specifico del protocollo corrispondente a un oggetto WebRequest | Microsoft Docs"
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
ms.assetid: d8c90785-f16b-42a5-8439-ed2f731b2ba8
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Procedura: Recuperare un oggetto WebResponse specifico del protocollo corrispondente a un oggetto WebRequest
In questo esempio viene illustrato come recuperare un WebResponse protocollo specifico che corrisponde a un WebRequest.  
  
## Esempio  
  
```csharp  
WebRequest req = WebRequest.Create("http://www.contoso.com/");  
WebResponse resp = req.GetResponse();  
```  
  
```vb  
Dim req As WebRequest = WebRequest.Create("http://www.contoso.com")  
Dim resp As WebResponse = req.GetResponse()  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli spazi dei nomi **System.Net**.  
  
## Vedere anche  
 [Richiesta di dati](../../../docs/framework/network-programming/requesting-data.md)