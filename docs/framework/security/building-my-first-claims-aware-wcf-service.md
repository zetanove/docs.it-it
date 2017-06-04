---
title: "Compilazione del primo servizio WCF in grado di riconoscere attestazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e0e6d091-9a97-4888-8f2c-cbcee42d90ee
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# Compilazione del primo servizio WCF in grado di riconoscere attestazioni
## Si applica a  
  
-   Windows Identity Foundation \(WIF\)  
  
-   Windows Communication Foundation \(WCF\)  
  
## Panoramica  
 In questo argomento viene illustrato lo scenario di compilazione di servizi WCF in grado di riconoscere attestazioni mediante WIF.  Uno scenario di servizio Web in grado di riconoscere attestazioni è in genere caratterizzato da tre partecipanti: il servizio Web stesso, l'utente finale e il servizio token di sicurezza.  come illustrato nella figura seguente:  
  
 ![Servizio WCF basato su attestazioni di base WIF](../../../docs/framework/security/media/wifbasicclaimsawarewcfservice.png "WIFBasicClaimsAwareWCFService")  
  
1.  Tramite il client del servizio WCF \(talvolta definito agente\) viene utilizzato WIF per inviare le credenziali al servizio token di sicurezza e alla riuscita dell'autenticazione, tramite l'agente viene emesso un token dal servizio token di sicurezza.  
  
2.  L'agente invia questo token emesso dal servizio token di sicurezza al servizio WCF.  
  
3.  Il servizio WCF in grado di riconoscere attestazioni viene configurato per considerare attendibili il servizio token di sicurezza e i token da quest'ultimo emessi.  Tramite il servizio WCF in grado di riconoscere attestazioni viene utilizzato WIF per convalidare il token e analizzarlo.  Gli sviluppatori utilizzano tipi e API WIF appropriati, ad esempio, **ClaimsPrincipal**, per esigenze dell'applicazione, quale l'implementazione della relativa autorizzazione.  
  
 A partire da .NET 4.5, WIF fa parte del pacchetto .NET Framework.  La disponibilità delle classi di WIF direttamente nel framework stesso consente una maggiore integrazione dell'identità basata sulle attestazioni nella piattaforma .NET, semplificando così l'utilizzo delle attestazioni.  Con WIF 4.5 non è necessario installare altri componenti fuori banda per avviare lo sviluppo di applicazioni Web in grado di riconoscere attestazioni.  Le classi di WIF vengono ora estese tra diversi assembly, i principali dei quali sono System.Security.Claims, System.IdentityModel e System.IdentityModel.Services.  
  
 Il servizio token di sicurezza è un servizio tramite cui vengono rilasciati dei token alla riuscita dell'autenticazione.  Microsoft offre due servizi token di sicurezza standard del settore:  
  
-   [Active Directory Federation Services \(AD FS\) 2.0](http://go.microsoft.com/fwlink/?LinkID=247516) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=247516\)  
  
-   [Servizio di controllo di accesso \(ACS\) di Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=247517) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=247517\).  
  
 AD FS 2.0 fa parte di Windows Server R2 e può essere utilizzato come servizio token di sicurezza in scenari locali.  Azure Active Directory Access Control \(detto anche Servizio di controllo di accesso o ACS\) è un servizio cloud, fornito come parte di Microsoft Azure.  Per fini di test e didattici, è inoltre possibile utilizzare altri servizi token di sicurezza per compilare applicazioni in grado di riconoscere attestazioni.  Ad esempio, è possibile usare il servizio token di sicurezza di sviluppo locale che fa parte di [Identity and Access Tool for Visual Studio](http://go.microsoft.com/fwlink/?LinkID=245849) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=245849\) disponibile gratuitamente online.  
  
 Per compilare il primo servizio WCF in grado di riconoscere attestazioni usando WIF, vedere [How To: Build Claims\-Aware WCF Service Using WIF](http://msdn.microsoft.com/it-it/431e6415-62ed-4a9f-af03-f14d2b4dfe6d).  
  
## Vedere anche  
 [Guida introduttiva a WIF](../../../docs/framework/security/getting-started-with-wif.md)