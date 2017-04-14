---
title: "Attenuazione: Protocolli TLS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33f97d13-3022-43da-8b18-cdb5c88df9c2
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Attenuazione: Protocolli TLS
A partire da .NET Framework 4.6, le classi <xref:System.Net.ServicePointManager?displayProperty=fullName> e <xref:System.Net.Security.SslStream?displayProperty=fullName> possono usare uno dei tre protocolli seguenti: Tls1.0, Tls1.1 o Tls 1.2.  Il protocollo SSL 3.0 e la crittografia RC4 non sono supportati.  
  
## Impatto  
 Questa modifica interessa:  
  
-   Qualsiasi app che usa SSL per comunicare con un server HTTPS o un server socket tramite uno qualsiasi dei tipi seguenti: <xref:System.Net.Http.HttpClient>, <xref:System.Net.HttpWebRequest>, <xref:System.Net.FtpWebRequest>, <xref:System.Net.Mail.SmtpClient> e <xref:System.Net.Security.SslStream>.  
  
-   Qualsiasi app sul lato server che non può essere aggiornata per supportare Tls1.0, Tls1.1 o Tls 1.2.  
  
## Attenuazione  
 L'attenuazione consigliata consiste nell'aggiornare l'app sul lato server a Tls1.0, Tls1.1 o Tls 1.2.  Se ciò non è fattibile o se le app client non funzionano, è possibile usare la classe <xref:System.AppContext> per rifiutare esplicitamente questa funzionalità in uno dei due modi seguenti:  
  
-   A livello di codice, usando un frammento di codice simile al seguente:  
  
     [!code-csharp[AppCompat.SSLProtocols#1](../../../samples/snippets/csharp/VS_Snippets_CLR/appcompat.sslprotocols/cs/program.cs#1)]
     [!code-vb[AppCompat.SSLProtocols#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/appcompat.sslprotocols/vb/module1.vb#1)]  
  
     Poiché l'oggetto <xref:System.Net.ServicePointManager> viene inizializzato una sola volta, la definizione di queste impostazioni di compatibilità deve essere la prima attività eseguita dall'applicazione.  
  
-   Aggiungendo la riga seguente alla sezione [\<runtime\>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file app.config.  
  
    ```xml  
    <AppContextSwitchOverrides value="Switch.System.Net.DontEnableSchUseStrongCrypto=true"/>  
    ```  
  
 Si noti, tuttavia, che il rifiuto esplicito del comportamento non è consigliabile, in quanto rende meno sicura l'applicazione.  
  
## Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)