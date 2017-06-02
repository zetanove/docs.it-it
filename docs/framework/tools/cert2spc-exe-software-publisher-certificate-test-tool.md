---
title: "Cert2spc.exe (Software Publisher Certificate Test Tool) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "SPC"
  - "Software Publisher Certificate Test tool"
  - "Software Publisher Certificate"
  - "Cert2spc.exe"
  - "certificates, Software Publisher's Certificate"
ms.assetid: be434d7d-9c0d-46e7-8392-58a9b542d11d
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Cert2spc.exe (Software Publisher Certificate Test Tool)
Lo strumento di verifica dei certificati dell'editore del software \(Cert2spc.exe\) crea un certificato SPC \(Software Publisher's Certificate\) da uno o più certificati X.509  ed è finalizzato unicamente ai test.  È possibile ottenere un certificato SPC valido da un'autorità di certificazione quale VeriSign o Thawte.  Per ulteriori informazioni sulla creazione di certificati X.509, vedere [Makecert.exe \(Certificate Creation Tool\)](../Topic/Makecert.exe%20\(Certificate%20Creation%20Tool\).md).  
  
 Viene installato automaticamente con Visual Studio.  Per eseguire lo strumento, utilizzare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per ulteriori informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
cert2spc cert1.cer | crl1.crl [... certN.cer | crlN.crl] outputSPCfile.spc  
```  
  
#### Parametri  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|`certN.cer`|Il nome di un certificato X.509 da includere nel file SPC.  È possibile specificare più nomi separati da spazi.|  
|`crlN.crl`|Il nome di un elenco di revoche di certificati da includere nel file SPC.  È possibile specificare più nomi separati da spazi.|  
|`outputSPCfile.spc`|Il nome dell'oggetto PKCS \#7 che conterrà i certificati X.509.|  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
## Esempi  
 Il comando che segue crea un certificato SPC da `myCertificate.cer` e lo inserisce in `mySPCFile.spc`.  
  
```  
cert2spc myCertificate.cer mySPCFile.spc  
```  
  
 Il comando che segue crea un certificato SPC da `oneCertificate.cer` e `twoCertificate.cer` e lo inserisce in `mySPCFile.spc`.  
  
```  
cert2spc oneCertificate.cer twoCertificate.cer mySPCFile.spc  
```  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Makecert.exe \(Certificate Creation Tool\)](../Topic/Makecert.exe%20\(Certificate%20Creation%20Tool\).md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)