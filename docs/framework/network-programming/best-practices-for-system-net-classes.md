---
title: "Procedure consigliate per le classi System.Net | Microsoft Docs"
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
  - "invio di dati, procedure consigliate"
  - "richiesta di dati da Internet, procedure consigliate"
  - "WebRequest (classe), procedure consigliate"
  - "richieste di dati, procedure consigliate"
  - "WebResponse (classe), procedure consigliate"
  - "procedure consigliate, richieste di dati"
  - "ricezione di dati, procedure consigliate"
ms.assetid: 716decc6-5952-47b7-9c5a-ba6fc5698684
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Procedure consigliate per le classi System.Net
I requisiti seguenti consentiranno a utilizzare le classi contenute in <xref:System.Net> al meglio i vantaggi:  
  
-   Utilizzare <xref:System.Net.WebRequest> e <xref:System.Net.WebResponse> laddove possibile invece di tipo che esegue il cast alle classi derivate.  Le applicazioni che utilizzano **WebRequest** e **WebResponse** possono beneficiare di nuovi protocolli Internet senza la necessità di modifiche estese al codice.  
  
-   Quando si scrivono applicazioni ASP.NET eseguite in un server utilizzando le classi **System.Net**, è spesso consigliabile, da un punto di vista delle prestazioni, utilizzare i metodi asincroni per <xref:System.Net.WebRequest.GetResponse%2A> e <xref:System.Net.WebResponse.GetResponseStream%2A>.  
  
-   Il numero di connessioni aperte in una risorsa Internet può avere un impatto notevole sulle prestazioni di rete e sulla velocità effettiva.  **System.Net** utilizza due connessioni per l'applicazione da host per impostazione predefinita.  Impostare la proprietà <xref:System.Net.ServicePoint.ConnectionLimit%2A> in <xref:System.Net.ServicePoint> per l'applicazione può aumentare questo valore per un host specifico.  Impostare la proprietà <xref:System.Net.ServicePointManager.DefaultPersistentConnectionLimit?displayProperty=fullName> può aumentare questa impostazione predefinita per tutti gli host.  
  
-   Quando si scrivono di protocolli, di prova livelli di socket per utilizzare [TCPClient](frlrfsystemnetsocketstcpclientclasstopic) o [UDPClient](frlrfsystemnetsocketsudpclientclasstopic) laddove possibile anziché scrivere direttamente a <xref:System.Net.Sockets.Socket>.  Queste due classi client incapsulano la creazione di socket di UDP e TCP senza la necessità di gestire i dettagli della connessione.  
  
-   Quando si accede ai siti che richiedono le credenziali, utilizzare la classe <xref:System.Net.CredentialCache> per creare una cache delle credenziali anziché è necessario immetterle a ogni richiesta.  La classe **CredentialCache** cerca nella cache per individuare le credenziali appropriate per presentare con una richiesta, sollevante della responsabilità di creare e presentazione delle credenziali in base all'URL.  
  
## Vedere anche  
 [Programmazione di rete in .NET Framework](../../../docs/framework/network-programming/index.md)