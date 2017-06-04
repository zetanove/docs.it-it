---
title: "Programmazione di rete in .NET Framework | Microsoft Docs"
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
  - "Internet"
  - "Internet, servizi Internet di .NET Framework"
  - "Risorse di rete"
ms.assetid: 8d455610-67a0-4fa8-a62f-7747064a9256
caps.latest.revision: 24
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 24
---
# Programmazione di rete in .NET Framework
Con Microsoft .NET Framework viene fornita un'implementazione a più livelli, estendibile e gestita, di servizi Internet che possono essere integrati nelle applicazioni in modo rapido e semplice. Le applicazioni di rete possono essere compilate su protocolli modulari per usufruire automaticamente di nuovi protocolli Internet oppure possono utilizzare un'implementazione gestita dell'interfaccia Windows Sockets per utilizzare la rete a livello di socket.  
  
## In questa sezione  
 [Introduzione ai protocolli di collegamento](../../../docs/framework/network-programming/introducing-pluggable-protocols.md)  
 Viene descritto come accedere a una risorsa Internet indipendentemente dal protocollo di accesso richiesto.  
  
 [Richiesta di dati](../../../docs/framework/network-programming/requesting-data.md)  
 Viene illustrato come utilizzare i protocolli modulari per caricare e scaricare i dati dalle risorse Internet.  
  
 [Programmazione di protocolli di collegamento](../../../docs/framework/network-programming/programming-pluggable-protocols.md)  
 Viene illustrato come derivare classi specifiche del protocollo per implementare protocolli modulari.  
  
 [Uso di protocolli applicativi](../../../docs/framework/network-programming/using-application-protocols.md)  
 Viene descritta la programmazione di applicazioni che utilizzano protocolli di rete come TCP, UDP e HTTP.  
  
 [Protocollo IPv6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 Vengono illustrati i vantaggi della versione 6 \(IPv6\) del protocollo Internet rispetto alla versione corrente della famiglia di prodotti del protocollo Internet \(IPv4\), vengono descritti l'indirizzamento, il routing e la configurazione automatica del protocollo IPv6 e come abilitare e disabilitare il protocollo IPv6.  
  
 [configurazione di applicazioni Internet](../../../docs/framework/network-programming/configuring-internet-applications.md)  
 Viene spiegato come utilizzare i file di configurazione di .NET Framework per configurare le applicazioni Internet.  
  
 [Tracciatura di rete in .NET Framework](../../../docs/framework/network-programming/network-tracing.md)  
 Viene spiegato come utilizzare la traccia di rete per ottenere informazioni sulle chiamate ai metodi e sul traffico di rete generato da un'applicazione gestita.  
  
 [Gestione della cache per le applicazioni di rete](../../../docs/framework/network-programming/cache-management-for-network-applications.md)  
 Viene descritto come utilizzare la memorizzazione nella cache per le applicazioni che utilizzano le classi <xref:System.Net.WebClient?displayProperty=fullName>, <xref:System.Net.WebRequest?displayProperty=fullName> e <xref:System.Net.HttpWebRequest?displayProperty=fullName>.  
  
 [Sicurezza in programmazione di rete](../../../docs/framework/network-programming/security-in-network-programming.md)  
 Viene descritto come utilizzare le tecniche standard di sicurezza e di autenticazione Internet.  
  
 [Procedure consigliate per le classi System.Net](../../../docs/framework/network-programming/best-practices-for-system-net-classes.md)  
 Vengono forniti consigli e suggerimenti per usufruire al meglio delle applicazioni Internet.  
  
 [Accesso a Internet con un proxy](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)  
 Viene descritto come configurare i proxy.  
  
 [NetworkInformation](../../../docs/framework/network-programming/networkinformation.md)  
 Viene descritto come raccogliere informazioni sugli eventi, le modifiche, le statistiche e le proprietà di rete e viene inoltre illustrato come determinare se un host remoto è raggiungibile tramite la classe <xref:System.Net.NetworkInformation.Ping?displayProperty=fullName>.  
  
 [Modifiche apportate allo spazio dei nomi System.Uri nella versione 2.0](../../../docs/framework/network-programming/changes-to-the-system-uri-namespace-in-version-2-0.md)  
 Vengono illustrate varie modifiche apportate alla classe <xref:System.Uri?displayProperty=fullName> nella versione 2.0 per correggere un comportamento non corretto, migliorare l'usabilità e aumentare la sicurezza.  
  
 [Supporto per IRI \(International Resource Identifier\) in System.Uri](../../../docs/framework/network-programming/international-resource-identifier-support-in-system-uri.md)  
 Vengono descritti i miglioramenti alla classe <xref:System.Uri?displayProperty=fullName> nelle versioni 3.5, 3.0 SP1 e 2.0 SP1 per il supporto dell'IRI \(International Resource Identifier\) e l'IDN \(Internationalized Domain Name\).  
  
 [Miglioramenti apportati alle prestazioni socket nella versione 3.5](../../../docs/framework/network-programming/socket-performance-enhancements-in-version-3-5.md)  
 Viene descritta una serie di miglioramenti apportati alla classe <xref:System.Net.Sockets.Socket?displayProperty=fullName> nelle versioni 3.5, 3.0 SP1 e 2.0 SP1 che forniscono un modello asincrono alternativo che può essere utilizzato da applicazioni socket ad alte prestazioni specializzate.  
  
 [Protocollo PNRP \(Peer Name Resolution Protocol\)](../../../docs/framework/network-programming/peer-name-resolution-protocol.md)  
 Viene descritto il supporto aggiunto nella versione 3.5 per supportare il protocollo PNRP \(Peer Name Resolution Protocol\), un protocollo di risoluzione dei nomi e di registrazione dei nomi dinamica senza server. Queste nuove funzionalità sono supportate dallo spazio dei nomi <xref:System.Net.PeerToPeer?displayProperty=fullName>.  
  
 [Collaborazione peer\-to\-peer](../../../docs/framework/network-programming/peer-to-peer-collaboration.md)  
 Viene descritto il supporto aggiunto nella versione 3.5 per supportare la collaborazione peer\-to\-peer che sfrutta il protocollo PNRP. Queste nuove funzionalità sono supportate dallo spazio dei nomi <xref:System.Net.PeerToPeer.Collaboration?displayProperty=fullName>.  
  
 [Modifiche apportate all'autenticazione NTLM per HttpWebRequest nella versione 3.5 SP1](../../../docs/framework/network-programming/changes-to-ntlm-authentication-for-httpwebrequest-in-version-3-5-sp1.md)  
 Vengono descritte le modifiche di sicurezza apportate nella versione 3.5 SP1 che influiscono sul modo in cui l'autenticazione Windows integrata viene gestita da <xref:System.Net.HttpWebRequest?displayProperty=fullName>, <xref:System.Net.HttpListener?displayProperty=fullName>, <xref:System.Net.Security.NegotiateStream?displayProperty=fullName> e le classi correlate nello spazio dei nomi System.Net.  
  
 [Autenticazione di Windows integrata con Protezione estesa](../../../docs/framework/network-programming/integrated-windows-authentication-with-extended-protection.md)  
 Vengono descritti i miglioramenti alla protezione estesa che influiscono sul modo in cui l'autenticazione Windows integrata viene gestita da <xref:System.Net.HttpWebRequest?displayProperty=fullName>, <xref:System.Net.HttpListener?displayProperty=fullName>, <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>, <xref:System.Net.Security.SslStream?displayProperty=fullName>, <xref:System.Net.Security.NegotiateStream?displayProperty=fullName> e le classi correlate nello spazio dei nomi <xref:System.Net?displayProperty=fullName> e in quelli correlati.  
  
 [Attraversamento NAT con IPv6 e Teredo](../../../docs/framework/network-programming/nat-traversal-using-ipv6-and-teredo.md)  
 Vengono descritti i miglioramenti aggiunti agli spazi dei nomi <xref:System.Net?displayProperty=fullName>, <xref:System.Net.NetworkInformation?displayProperty=fullName> e <xref:System.Net.Sockets?displayProperty=fullName> per il supporto dell'attraversamento NAT tramite IPv6 e Teredo.  
  
 [Isolamento rete per app di Windows Store](../../../docs/framework/network-programming/network-isolation-for-windows-store-apps.md)  
 Viene descritto l'impatto dell'isolamento di rete quando le classi negli spazi dei nomi <xref:System.Net>, <xref:System.Net.Http> e <xref:System.Net.Http.Headers> sono utilizzate nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)  
 Collegamenti a esempi scaricabili di programmazione di rete che utilizzano le classi negli spazi dei nomi <xref:System.Net>, <xref:System.Net.Cache>, <xref:System.Net.Configuration>, <xref:System.Net.Mail>, <xref:System.Net.Mime>, <xref:System.Net.NetworkInformation>, <xref:System.Net.PeerToPeer>, <xref:System.Net.Security>, <xref:System.Net.Sockets>.  
  
## Riferimenti  
 <xref:System.Net?displayProperty=fullName>  
 Fornisce una semplice interfaccia di programmazione per molti dei protocolli attualmente usati per le reti. Le classi <xref:System.Net.WebRequest?displayProperty=fullName> e <xref:System.Net.WebResponse?displayProperty=fullName> in questo spazio dei nomi sono la base dei protocolli modulari.  
  
 <xref:System.Net.Cache?displayProperty=fullName>  
 Definisce i tipi e le enumerazioni utilizzati per specificare i criteri di cache per le risorse ottenute mediante le classi <xref:System.Net.WebRequest?displayProperty=fullName> e <xref:System.Net.HttpWebRequest?displayProperty=fullName>.  
  
 <xref:System.Net.Configuration?displayProperty=fullName>  
 Classi utilizzate dalle applicazioni per accedere a livello di codice alle impostazioni di configurazione dello spazio dei nomi System.Net e per aggiornarle.  
  
 <xref:System.Net.Http?displayProperty=fullName>  
 Classi che forniscono un'interfaccia di programmazione per le moderne applicazioni HTTP.  
  
 <xref:System.Net.Http.Headers?displayProperty=fullName>  
 Fornisce il supporto per le raccolte di intestazioni HTTP utilizzate dallo spazio dei nomi <xref:System.Net.Http?displayProperty=fullName>.  
  
 <xref:System.Net.Mail?displayProperty=fullName>  
 Classi per creare e inviare messaggi di posta elettronica utilizzando il protocollo SMTP.  
  
 <xref:System.Net.Mime?displayProperty=fullName>  
 Definisce i tipi che sono utilizzati per rappresentare le intestazioni MIME \(Multipurpose Internet Mail Exchange\) utilizzate dalle classi nello spazio dei nomi <xref:System.Net.Mail?displayProperty=fullName>.  
  
 <xref:System.Net.NetworkInformation?displayProperty=fullName>  
 Classi per raccogliere a livello di codice informazioni sugli eventi, le modifiche, le statistiche e le proprietà della rete.  
  
 <xref:System.Net.PeerToPeer?displayProperty=fullName>  
 Fornisce un'implementazione gestita del protocollo PNRP \(Peer Name Resolution Protocol\) per gli sviluppatori.  
  
 <xref:System.Net.PeerToPeer.Collaboration?displayProperty=fullName>  
 Fornisce un'implementazione gestita dell'interfaccia di collaborazione peer\-to\-peer per gli sviluppatori.  
  
 <xref:System.Net.Security?displayProperty=fullName>  
 Classi per fornire i flussi di rete per comunicazioni sicure tra host.  
  
 <xref:System.Net.Sockets?displayProperty=fullName>  
 Fornisce un'implementazione gestita dell'interfaccia Windows Sockets \(Winsock\) per sviluppatori che hanno la necessità di mantenere sotto controllo l'accesso alla rete.  
  
 <xref:System.Net.WebSockets?displayProperty=fullName>  
 Fornisce un'implementazione gestita dell'interfaccia WebSocket per gli sviluppatori.  
  
 <xref:System.Uri?displayProperty=fullName>  
 Fornisce una rappresentazione in forma di oggetto di un identificatore URI \(uniform resource identifier\) e un pratico accesso alle parti dell'URI.  
  
 <xref:System.Security.Authentication.ExtendedProtection?displayProperty=fullName>  
 Fornisce il supporto per l'autenticazione utilizzando la protezione estesa per le applicazioni.  
  
 <xref:System.Security.Authentication.ExtendedProtection.Configuration?displayProperty=fullName>  
 Fornisce il supporto per la configurazione dell'autenticazione utilizzando la protezione estesa per le applicazioni.  
  
## Vedere anche  
 [Procedure per la programmazione di rete](../../../docs/framework/network-programming/network-programming-how-to-topics.md)   
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)   
 [Esempi di rete per .NET in MSDN Code Gallery](http://code.msdn.microsoft.com/Wiki/View.aspx?ProjectName=nclsamples)   
 [Esempio con HttpClient](http://go.microsoft.com/fwlink/?LinkId=242550)