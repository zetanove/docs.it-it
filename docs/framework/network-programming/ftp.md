---
title: "FTP | Microsoft Docs"
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
  - "FTP"
ms.assetid: 9b43f8b4-89d7-46a7-89fc-71aca916dd32
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# FTP
.NET Framework fornisce supporto completo del protocollo FTP con le classi <xref:System.Net.FtpWebResponse> e <xref:System.Net.FtpWebRequest>.  Queste classi che derivano da <xref:System.Net.WebRequest> e da <xref:System.Net.WebResponse>.  Nella maggior parte dei casi, <xref:System.Net.WebRequest> e le classi <xref:System.Net.WebResponse> forniscono tutto ciò che è necessario eseguire la richiesta, ma se è necessario accedere a funzionalità specifiche FTP\- esposte come proprietà, è possibile eseguire su di essi un cast queste classi in <xref:System.Net.FtpWebRequest> o a <xref:System.Net.FtpWebResponse>.  
  
## Esempi  
 Per ulteriori informazioni, vedere i seguenti argomenti: [Procedura: Scaricare file con FTP](../../../docs/framework/network-programming/how-to-download-files-with-ftp.md), [Procedura: Caricare file con FTP](../../../docs/framework/network-programming/how-to-upload-files-with-ftp.md)e [Procedura: Elencare il contenuto della directory con FTP](../../../docs/framework/network-programming/how-to-list-directory-contents-with-ftp.md).  
  
## FTP e proxy  
 Se un proxy \(specificato dalla proprietà <xref:System.Net.FtpWebRequest.Proxy%2A> \) è un proxy HTTP, è solo <xref:System.Net.WebRequestMethods.Ftp.DownloadFile>, <xref:System.Net.WebRequestMethods.Ftp.ListDirectory>e i comandi <xref:System.Net.WebRequestMethods.Ftp.ListDirectoryDetails> sono supportati.  
  
## Vedere anche  
 [Accesso a Internet con un proxy](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)   
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)   
 [Esempio client di tecnologia FTP](http://go.microsoft.com/fwlink/?LinkID=179557)   
 [Esempio di esplorazione di tecnologia FTP](http://go.microsoft.com/fwlink/?LinkID=179569)   
 [Uso di protocolli applicativi](../../../docs/framework/network-programming/using-application-protocols.md)