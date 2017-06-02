---
title: "Procedura: Richiedere una pagina Web e recuperare i risultati sotto forma di flusso | Microsoft Docs"
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
ms.assetid: d32b7f35-29d8-4fb7-ad71-d219edc5e359
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Procedura: Richiedere una pagina Web e recuperare i risultati sotto forma di flusso
In questo esempio viene illustrato come richiedere una pagina Web e recuperare i risultati in un flusso.  
  
## Esempio  
  
```csharp  
WebClient myClient = new WebClient();  
Stream response = myClient.OpenRead("http://www.contoso.com/index.htm");  
// The stream data is used here.  
response.Close();  
```  
  
```vb  
Dim myClient As WebClient = New WebClient()  
Dim response As Stream = myClient.OpenRead("http://www.contoso.com/index.htm")  
' The stream data is used here.  
response.Close()  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli spazi dei nomi <xref:System.IO> e <xref:System.Net>.  
  
## Vedere anche  
 [Richiesta di dati](../../../docs/framework/network-programming/requesting-data.md)