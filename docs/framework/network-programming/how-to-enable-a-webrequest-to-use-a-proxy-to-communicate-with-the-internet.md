---
title: "Procedura: Consentire a un elemento WebRequest di usare un proxy per comunicare con Internet | Microsoft Docs"
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
ms.assetid: 63c0ef2c-44b5-4c54-9804-ba0b9b001ac7
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Procedura: Consentire a un elemento WebRequest di usare un proxy per comunicare con Internet
In questo esempio viene creata un'istanza globale del proxy che consente a qualsiasi <xref:System.Net.WebRequest> per utilizzare un proxy per comunicare con Internet.  L'esempio presuppone che il server sia denominato `webproxy` e che comunicano sulla porta 80, la porta standard HTTP.  
  
## Esempio  
  
```csharp  
WebProxy proxyObject = new WebProxy("http://webproxy:80/");  
GlobalProxySelection.Select = proxyObject;  
```  
  
```vb  
Dim proxyObject As WebProxy = New WebProxy("http://webproxy:80/")  
GlobalProxySelection.Select = proxyObject  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli spazi dei nomi **System.Net**.  
  
## Vedere anche  
 [Uso di protocolli applicativi](../../../docs/framework/network-programming/using-application-protocols.md)   
 [Accesso a Internet con un proxy](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)