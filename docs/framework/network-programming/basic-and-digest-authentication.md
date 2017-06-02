---
title: "Autenticazione di base e del digest | Microsoft Docs"
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
helpviewer_keywords: 
  - "autenticazione [.NET Framework], classi"
  - "autenticazione di base"
  - "autenticazione [.NET Framework], di base"
  - "autenticazione client, di base"
  - "autenticazione utente, di base"
  - "autenticazione [.NET Framework], digest"
  - "ricezione di dati, autenticazione"
  - "autenticazione client, digest"
  - "Internet, autenticazione"
  - "autenticazione digest"
  - "invio di dati, autenticazione"
  - "risorse di rete, autenticazione"
  - "autenticazione utente, digest"
ms.assetid: 8cce2742-8d52-4643-9dd2-64ddf38aa878
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Autenticazione di base e del digest
L'implementazione <xref:System.Net> di base e di autenticazione del digest conforme a RFC2617 – autenticazione HTTP: Autenticazione di base e classificata \(disponibili sul sito Web del World Wide Web Consortium a www.w3.org\).  
  
 Per utilizzare la base e l'autenticazione del digest, un'applicazione deve fornire un nome utente e una password nella proprietà <xref:System.Net.WebRequest.Credentials%2A> dell'oggetto <xref:System.Net.WebRequest> che utilizzi i dati della richiesta da Internet, come illustrato nell'esempio seguente.  
  
```vb  
Dim MyURI As String = "http://www.contoso.com/"  
Dim WReq As WebRequest = WebRequest.Create(MyURI)  
WReq.Credentials = New NetworkCredential(UserName, SecurelyStoredPassword)  
```  
  
```csharp  
String MyURI = "http://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
WReq.Credentials = new NetworkCredential(UserName, SecurelyStoredPassword);  
```  
  
> [!CAUTION]
>  I dati inviati con autenticazione di base e classificata non sono crittografati, pertanto i dati possono essere visualizzate da un avversario.  Inoltre, le credenziali di autenticazione di base \(nome utente e password vengono inviate in chiaro e possono essere rilevate.  
  
## Vedere anche  
 [Autenticazione NTLM e Kerberos](../../../docs/framework/network-programming/ntlm-and-kerberos-authentication.md)   
 [Autenticazione Internet](../../../docs/framework/network-programming/internet-authentication.md)