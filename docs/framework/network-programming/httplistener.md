---
title: "HttpListener | Microsoft Docs"
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
  - "HTTP"
ms.assetid: 5b89d3fb-3c9a-49e2-af1f-c34c020c68ac
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# HttpListener
La classe <xref:System.Net.HttpListener> fornisce un listener del protocollo HTTP controllato a livello di codice.  Il listener è attivo per la durata dell'oggetto <xref:System.Net.HttpListener> e viene eseguito all'interno dell'applicazione.  
  
## HTTP.SYS  
 La classe <xref:System.Net.HttpListener> si basa su HTTP.sys, il listener in modalità kernel che gestisce tutto il traffico HTTP per Windows.  HTTP.sys fornisce la gestione della connessione, la limitazione della larghezza di banda e la registrazione del server Web.  Usare lo strumento `HttpCfg.exe` per aggiungere i certificati SSL.  Per altre informazioni, vedere la documentazione sullo strumento [HttpCfg.exe](http://go.microsoft.com/fwlink/?LinkID=178284) nella documentazione del [server](http://go.microsoft.com/fwlink/?LinkID=178285).  
  
## Vedere anche  
 <xref:System.Net.HttpListener>   
 <xref:System.Net.HttpWebRequest>   
 <xref:System.Net.HttpWebResponse>   
 [Server HTTP](http://go.microsoft.com/fwlink/?LinkID=178285)   
 [Miglioramenti della sicurezza nelle informazioni Internet](http://go.microsoft.com/fwlink/?LinkID=178286)   
 [Esempio di applicazione host ASPX HttpListener](http://go.microsoft.com/fwlink/?LinkID=179560)   
 [Esempio di tecnologia HttpListener](http://go.microsoft.com/fwlink/?LinkID=179558)   
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)