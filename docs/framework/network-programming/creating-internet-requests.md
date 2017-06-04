---
title: "Creazione di richieste Internet | Microsoft Docs"
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
  - "WebRequest (classe), invio e ricezione di dati"
  - "Servizi di rete"
  - "HttpWebResponse (classe), invio e ricezione di dati"
  - "richiesta di dati da Internet, creazione di richieste"
  - "Risorse di rete"
  - "Internet, richiesta di dati"
  - "richieste dati, creazione di richieste"
ms.assetid: faab683e-3f1e-4eee-b5e9-59f7245033d5
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Creazione di richieste Internet
Le applicazioni creano istanze <xref:System.Net.WebRequest> con il metodo <xref:System.Net.WebRequest.Create%2A?displayProperty=fullName>.  Questo è un metodo statico che crea una classe derivata da **WebRequest** in base allo schema URI passato.  
  
## Web, file e richieste FTP  
 .NET Framework fornisce la classe <xref:System.Net.HttpWebRequest>, derivata da **WebRequest**, per gestire richieste di HTTPS e HTTP.  Nella maggior parte dei casi, la classe **WebRequest** fornisce tutte le proprietà che è necessario effettuare una richiesta, per quanto se necessario, è possibile eseguire il cast degli oggetti **WebRequest** creati dal metodo **WebRequest.Create** al tipo **HttpWebRequest** per accedere alle proprietà HTTP\- specifiche della richiesta.  Analogamente, un handle dell'oggetto **HttpWebResponse** le risposte alle richieste di HTTPS e HTTP.  Per accedere ad accedere a proprietà specifiche HTTP **HttpWebResponse** oggetto, è necessario eseguire il cast degli oggetti **WebResponse** al tipo **HttpWebResponse** .  
  
 .NET Framework fornisce inoltre le classi <xref:System.Net.FileWebResponse> e <xref:System.Net.FileWebRequest> alle richieste di handle per le risorse che utilizzano “il file: „ Schema URI.  Inoltre, <xref:System.Net.FtpWebRequest> e le classi <xref:System.Net.FtpWebResponse> vengono forniti alle richieste di handle per le risorse che utilizzano “FTP: „.  Se la richiesta è per una risorsa che utilizza una di queste combinazioni, è possibile utilizzare il metodo **WebRequest.Create** per ottenere un oggetto con cui effettuare la richiesta.  
  
 Per gestire le richieste che utilizzano altri protocolli a livello di applicazione, è necessario implementare classi specifiche del protocollo derivate da **WebRequest** e da **WebResponse**.  Per ulteriori informazioni, vedere [Protocolli innestabili di programmazione](../../../docs/framework/network-programming/programming-pluggable-protocols.md).  
  
## Vedere anche  
 [Procedura: Richiedere dati con la classe WebRequest](../../../docs/framework/network-programming/how-to-request-data-using-the-webrequest-class.md)   
 [Richiesta di dati](../../../docs/framework/network-programming/requesting-data.md)