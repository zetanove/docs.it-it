---
title: "Concetti relativi alla sicurezza utilizzati in WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b9dfcf5-4bf1-4f35-9070-723171c823a1
caps.latest.revision: 15
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 15
---
# Concetti relativi alla sicurezza utilizzati in WCF
La sicurezza [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene generata su concetti già in uso e distribuita in varie infrastrutture di sicurezza.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta alcune di quelle infrastrutture, ad esempio Secure Sockets Layer \(SSL\) su HTTP \(HTTPS\).[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], tuttavia, va oltre, supportando infrastrutture di sicurezza esistenti tramite l'implementazione di standard di sicurezza interoperativi più recenti \(ad esempio WS\-Security\) su messaggi con codifica SOAP.Tanto per l'utilizzo di meccanismi esistenti che di standard interoperativi nuovi, i concetti di sicurezza alla base di entrambi sono gli stessi.La comprensione di concetti sottostanti le infrastrutture esistenti e gli standard più recenti è fondamentale per l'implementazione del modello di sicurezza migliore per un'applicazione.  
  
## Introduzione alla sicurezza per i servizi Web WCF  
 Il gruppo Microsoft Patterns and Practices ha scritto un white paper dettagliato sulla guida alla sicurezza di WCF disponibile per il download qui: [Guida alla sicurezza di WCF](http://go.microsoft.com/fwlink/?LinkId=210210).In questo white paper vengono descritti i concetti di sicurezza fondamentali relativi ai servizi Web, i principali concetti di sicurezza di WCF, gli scenari di applicazione nell'Intranet e gli scenari di applicazione in Internet.  
  
## Specifiche di sicurezza del settore  
  
### Infrastruttura a chiave pubblica  
 L'infrastruttura a chiave pubblica \(PKI\) è un sistema di certificati digitali, autorità di certificazione e altre autorità di registrazione che verificano e autenticano ogni parte coinvolta in una transazione elettronica tramite l'utilizzo di crittografia a chiave pubblica.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Servizi certificati di Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkId=210211).  
  
### Protocollo Kerberos  
 Il *protocollo Kerberos* è una specifica per la creazione di un meccanismo di sicurezza che autentica gli utenti in un dominio Windows.Consente a un utente di stabilire un contesto protetto con altre entità in un dominio.Windows 2000 e le piattaforme successive utilizzano il protocollo Kerberos per impostazione predefinita.La comprensione dei meccanismi del sistema è utile in caso di creazione di un servizio che dovrà interagire con i client Intranet.Poiché, inoltre, l'*associazione Kerberos di Web Services Security* è pubblicata in modo esteso, è possibile utilizzare il protocollo Kerberos per comunicare con i client Internet, ovvero, il protocollo Kerberos è interoperativo.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] come il protocollo Kerberos viene implementato in Windows, vedere la pagina relativa al [Kerberos Microsoft](http://go.microsoft.com/fwlink/?LinkId=210212).  
  
### Certificati X.509  
 I certificati X.509 costituiscono un form di credenziali primario utilizzato nelle applicazioni di sicurezza.Per ulteriori informazioni sui certificati X.509, vedere [Certificati di chiave pubblica X.509](http://go.microsoft.com/fwlink/?LinkId=210213).I certificati X.509 vengono archiviati all'interno di un archivio certificati.I computer che eseguono Windows dispongono di vari tipi di archivi certificati, ognuno dei quali con un scopo diverso.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] archivi differenti, vedere [Archivi certificati](http://go.microsoft.com/fwlink/?LinkID=87787).  
  
## Specifiche di sicurezza dei servizi Web  
 Le associazioni definite dal sistema supportano molte specifiche di sicurezza di servizi Web di uso comune.Per l'elenco completo delle associazioni fornite dal sistema e delle specifiche dei servizi Web supportate, vedere: [Protocolli di servizi Web supportati da associazioni di interoperabilità fornite dal sistema](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)  
  
## Meccanismi del controllo di accesso  
 WCF fornisce numerosi modi per controllare l'accesso a un servizio o un'operazione,tra i quali:  
  
1.  <xref:System.Security.Permissions.PrinciplePermissionAttribute>  
  
2.  Provider di appartenenze ASP.NET  
  
3.  Provider di ruoli ASP.NET  
  
4.  Gestione autorizzazioni  
  
5.  Modello di identità  
  
 Per ulteriori informazioni su questi argomenti, vedere [Meccanismi del controllo di accesso](../../../../docs/framework/wcf/feature-details/access-control-mechanisms.md).  
  
## Vedere anche  
 [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Modello di sicurezza per Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)