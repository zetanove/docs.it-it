---
title: "Autenticazione NTLM e Kerberos | Microsoft Docs"
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
  - "autenticazione [.NET Framework], NTLM"
  - "autenticazione [.NET Framework], Keberos"
  - "autenticazione utente, Kerberos"
  - "autenticazione utente, NTLM"
  - "autenticazione Kerberos"
  - "ricezione di dati, autenticazione"
  - "autenticazione NTLM"
  - "Internet, autenticazione"
  - "autenticazione client, Kerberos"
  - "invio di dati, autenticazione"
  - "risorse di rete, autenticazione"
  - "classi [.NET Framework], autenticazione"
  - "autenticazione client, NTLM"
ms.assetid: 9ef65560-f596-4469-bcce-f4d5407b55cd
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Autenticazione NTLM e Kerberos
L'autenticazione NTLM predefinita e Kerberos utilizzano le credenziali utente di Microsoft Windows NT associate all'applicazione chiamante eseguire l'autenticazione con il server.  Quando si utilizza l'autenticazione NTLM non predefinito, l'applicazione imposta il tipo di autenticazione a NTLM e utilizza un oggetto <xref:System.Net.NetworkCredential> per passare il nome utente, password e il dominio all'host, come illustrato nell'esempio seguente.  
  
```vb  
Dim MyURI As String = "http://www.contoso.com/"  
Dim WReq As WebRequest = WebRequest.Create(MyURI)  
WReq.Credentials = _  
    New NetworkCredential(UserName, SecurelyStoredPassword, Domain)  
```  
  
```csharp  
String MyURI = "http://www.contoso.com/";  
WebRequest WReq = WebRequest.Create (MyURI);  
WReq.Credentials =   
    new NetworkCredential(UserName, SecurelyStoredPassword, Domain);  
```  
  
 Le applicazioni che devono connettersi ai servizi Internet utilizzando le credenziali dell'applicazione possono eseguire questa operazione con credenziali predefinite dell'utente, come illustrato nell'esempio seguente.  
  
```vb  
Dim MyURI As String = "http://www.contoso.com/"  
Dim WReq As WebRequest = WebRequest.Create(MyURI)  
WReq.Credentials = CredentialCache.DefaultCredentials  
```  
  
```csharp  
String MyURI = "http://www.contoso.com/";  
WebRequest WReq = WebRequest.Create (MyURI);  
WReq.Credentials = CredentialCache.DefaultCredentials;  
```  
  
 Il modulo autenticazione di negoziazione spazio determina se il server remoto utilizza NTLM o l'autenticazione Kerberos e invia una risposta appropriata.  
  
> [!NOTE]
>  L'autenticazione NTLM non viene eseguita tramite un server proxy.  
  
## Vedere anche  
 [Autenticazione di base e del digest](../../../docs/framework/network-programming/basic-and-digest-authentication.md)   
 [Autenticazione Internet](../../../docs/framework/network-programming/internet-authentication.md)