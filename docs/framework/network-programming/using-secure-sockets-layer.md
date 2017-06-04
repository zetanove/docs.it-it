---
title: "Uso di Secure Sockets Layer | Microsoft Docs"
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
  - "Servizi di rete"
  - "SSL"
  - "Secure Sockets Layer"
  - "richiesta di dati da Internet, Secure Sockets Layer"
  - "invio di dati, Secure Sockets Layer"
  - "Risorse di rete"
  - "richieste di dati, Secure Sockets Layer"
  - "ricezione di dati, Secure Sockets Layer"
  - "Internet, Secure Sockets Layer"
ms.assetid: 6e4289e6-d1b7-4e82-ab0d-e83e3b6063ed
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Uso di Secure Sockets Layer
Le classi <xref:System.Net> utilizzano Secure Sockets Layer \(SSL\) per crittografare la connessione per diversi protocolli di rete.  
  
 Per le connessioni HTTP, le classi <xref:System.Net.WebResponse> e <xref:System.Net.WebRequest> utilizzare SSL per comunicare con gli host Web che supportano SSL.  La decisione di utilizzare SSL viene effettuata dalla classe <xref:System.Net.WebRequest>, in base all'URI disponibile.  Se l'uri inizia con “HTTPS: „, SSL viene utilizzato; se l'uri inizia con “HTTP: „, una connessione crittografata non viene utilizzata.  
  
 Per utilizzare SSL con protocollo FTP \(FTP\), impostare la proprietà <xref:System.Net.FtpWebRequest.EnableSsl> per allineare prima di chiamare <xref:System.Net.FtpWebRequest.GetResponse>.  Analogamente, utilizzare SSL con protocollo di trasporto \(SMTP\) di Simple Mail, impostare la proprietà <xref:System.Net.Mail.SmtpClient.EnableSsl> per allineare prima di inviare posta elettronica.  
  
 La classe <xref:System.Net.Security.SslStream> fornisce un'astrazione in base al flusso per SSL e fornisce molti modi per configurare il handshake SSL.  
  
## Esempio  
  
### Codice  
  
```vb  
Dim MyURI As String = "https://www.contoso.com/"  
Dim Wreq As WebRequest = WebRequest.Create(MyURI)  
  
Dim serverUri As String = "ftp://ftp.contoso.com/file.txt"  
Dim request As FtpWebRequest = CType(WebRequest.Create(serverUri), FtpWebRequest)  
request.Method = WebRequestMethods.Ftp.DeleteFile  
request.EnableSsl = True  
Dim response As FtpWebResponse = CType(request.GetResponse(), FtpWebResponse)  
```  
  
```csharp  
String MyURI = "https://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
  
String serverUri = "ftp://ftp.contoso.com/file.txt"  
FtpWebRequest request = (FtpWebRequest)WebRequest.Create(serverUri);  
request.EnableSsl = true;  
request.Method = WebRequestMethods.Ftp.DeleteFile;  
FtpWebResponse response = (FtpWebResponse)request.GetResponse();  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli spazi dei nomi **System.Net**.  
  
## Vedere anche  
 [Sicurezza in programmazione di rete](../../../docs/framework/network-programming/security-in-network-programming.md)   
 [Programmazione di rete in .NET Framework](../../../docs/framework/network-programming/index.md)   
 [Selezione e convalida dei certificati](../../../docs/framework/network-programming/certificate-selection-and-validation.md)