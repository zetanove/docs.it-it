---
title: "HTTP | Microsoft Docs"
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
  - "protocolli, HTTP"
  - "invio di dati, HTTP"
  - "HttpWebResponse (classe), invio e ricezione di dati"
  - "HTTP"
  - "ricezione di dati, HTTP"
  - "protocolli applicativi, HTTP"
  - "Internet, HTTP"
  - "risorse di rete, HTTP"
  - "HTTP, informazioni"
  - "HttpWebRequest (classe), invio e ricezione di dati"
ms.assetid: 985fe5d8-eb71-4024-b361-41fbdc1618d8
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# HTTP
.NET Framework fornisce supporto completo del protocollo HTTP, che costituisce la maggior parte del traffico Internet, con le classi <xref:System.Net.HttpWebResponse> e di<xref:System.Net.HttpWebRequest>.  Queste classi derivate da, <xref:System.Net.WebRequest> e da <xref:System.Net.WebResponse>, vengono restituite per impostazione predefinita ogni volta che il metodo statico <xref:System.Net.WebRequest.Create%2A?displayProperty=fullName> rileva un URI a partire da “HTTP„ o “da„ HTTPS.  Nella maggior parte dei casi, le classi **WebResponse** e **WebRequest** forniscono tutto ciò che è necessario eseguire la richiesta, ma se è necessario accedere a funzionalità specifiche HTTP\- esposte come proprietà, è possibile eseguire su di essi un cast queste classi a **HttpWebRequest** o a **HttpWebResponse**.  
  
 **HttpWebRequest** e **HttpWebResponse** incapsulano una transazione di richiesta\-e\- risposta HTTP standard e forniscono l'accesso alle intestazioni HTTP comuni.  Queste classi supportano anche la maggior parte delle funzionalità HTTP 1.1, inclusi pipelining, inviando e ricevente i dati in blocchi, l'autenticazione, preauthentication, crittografia, supporto del proxy, convalida del certificato server e gestione della connessione.  Le intestazioni personalizzate e intestazioni non fornite tramite le proprietà possono essere archiviate in e accedervi mediante la proprietà **Headers**.  
  
 **HttpWebRequest** è la classe predefinita utilizzata da **WebRequest** e non deve essere registrato prima che sia possibile passare un URI al metodo **WebRequest.Create**.  
  
 È possibile rendere l'applicazione seguire HTTP reindirizzato automaticamente impostando la proprietà <xref:System.Net.HttpWebRequest.AllowAutoRedirect%2A> a **true** \(impostazione predefinita\).  L'applicazione verrà reindirizzata le richieste e la proprietà [ResponseURI](frlrfsystemnethttpwebresponseclassresponseuritopic)**HttpWebResponse** conterrà l'effettiva risorsa Web che ha risposto alla richiesta.  Se **AllowAutoRedirect** impostato su **false**, l'applicazione deve essere reindirizzati come gestire errori del protocollo HTTP.  
  
 Le applicazioni ricevono gli errori del protocollo HTTP intercettando <xref:System.Net.WebException> con <xref:System.Net.WebException.Status%2A> impostato su [WebExceptionStatus.ProtocolError](frlrfsystemnetwebexceptionstatusclasstopic).  La proprietà <xref:System.Net.WebException.Response%2A> contiene **WebResponse** inviato al server e indica all'errore HTTP rilevato.  
  
## Vedere anche  
 [Accesso a Internet con un proxy](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)   
 [Uso di protocolli applicativi](../../../docs/framework/network-programming/using-application-protocols.md)   
 [Procedura: Accedere a proprietà specifiche di HTTP](../../../docs/framework/network-programming/how-to-access-http-specific-properties.md)