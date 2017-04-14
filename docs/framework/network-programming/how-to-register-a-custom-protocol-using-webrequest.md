---
title: "Procedura: Registrare un protocollo personalizzato con WebRequest | Microsoft Docs"
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
ms.assetid: 98ddbdb9-66b1-4080-92ad-51f5c447fcf8
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Procedura: Registrare un protocollo personalizzato con WebRequest
In questo esempio viene mostrato come registrare un classthatspecifico di protocollo viene definita altrove.  In questo esempio, `CustomWebRequestCreator` è l'oggetto implementato dall'utente che implementa il metodo **Create** che restituisce l'oggetto `CustomWebRequest`.  L'esempio di codice seguente si presuppone che sia stato scritto il codice `CustomWebRequest` che implementa il protocollo personalizzato.  
  
## Esempio  
  
```csharp  
WebRequest.RegisterPrefix("custom", new CustomWebRequestCreator());  
WebRequest req = WebRequest.Create("custom://customHost.contoso.com/");  
```  
  
```vb  
WebRequest.RegisterPrefix("custom", New CustomWebRequestCreator())  
Dim req As WebRequest = WebRequest.Create("custom://customHost.contoso.com/")  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
 Riferimenti agli spazi dei nomi <xref:System.Net>.  
  
## Vedere anche  
 [Programmazione di protocolli di collegamento](../../../docs/framework/network-programming/programming-pluggable-protocols.md)