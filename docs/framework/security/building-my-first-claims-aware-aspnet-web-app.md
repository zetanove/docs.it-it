---
title: "Creazione della prima applicazione Web ASP.NET in grado di riconoscere attestazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3ee8ee7f-caba-4267-9343-e313fae2876d
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# Creazione della prima applicazione Web ASP.NET in grado di riconoscere attestazioni
## Si applica a  
  
-   Windows Identity Foundation \(WIF\)  
  
-   ASP.NET  
  
 In questo argomento viene illustrato lo scenario di compilazione di applicazioni Web ASP.NET in grado di riconoscere attestazioni mediante WIF.  Uno scenario di applicazione in grado di riconoscere attestazioni prevede in genere tre partecipanti: l'applicazione stessa, l'utente finale e il servizio token di sicurezza,  come illustrato nella figura seguente:  
  
 ![App Web di base WIF](../../../docs/framework/security/media/wifbasicwebapp.png "WIFBasicWebApp")  
  
1.  Tramite l'applicazione in grado di riconoscere attestazioni viene utilizzato WIF per identificare le richieste non autenticate e per reindirizzarle al servizio token di sicurezza.  
  
2.  L'utente finale fornisce le credenziali al servizio token di sicurezza e alla riuscita dell'autenticazione all'utente viene rilasciato un token dal servizio in questione.  
  
3.  L'utente viene reindirizzato dal servizio token di sicurezza all'applicazione in grado di riconoscere attestazioni con il token rilasciato da questo servizio nella richiesta.  
  
4.  L'applicazione in grado di riconoscere attestazioni viene configurata per considerare attendibili il servizio token di sicurezza e i token da quest'ultimo rilasciati.  Tramite l'applicazione in grado di riconoscere attestazioni viene utilizzato WIF per convalidare il token e analizzarlo.  Gli sviluppatori utilizzano tipi e API WIF appropriati, ad esempio, **ClaimsPrincipal**, per esigenze dell'applicazione, quale l'implementazione della relativa autorizzazione.  
  
 A partire da .NET 4.5, WIF fa parte del pacchetto .NET Framework.  La disponibilità delle classi di WIF direttamente nel framework stesso consente una maggiore integrazione dell'identità basata sulle attestazioni nella piattaforma .NET, semplificando così l'utilizzo delle attestazioni.  Con WIF 4.5 non è necessario installare altri componenti fuori banda per avviare lo sviluppo di applicazioni Web in grado di riconoscere attestazioni.  Le classi di WIF vengono ora estese tra diversi assembly, i principali dei quali sono System.Security.Claims, System.IdentityModel e System.IdentityModel.Services.  
  
 Il servizio token di sicurezza è un servizio tramite cui vengono rilasciati dei token alla riuscita dell'autenticazione.  Microsoft offre due servizi token di sicurezza standard del settore:  
  
-   [Active Directory Federation Services \(AD FS\) 2.0](http://go.microsoft.com/fwlink/?LinkID=247516) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=247516\)  
  
-   [Servizio di controllo di accesso \(ACS\) di Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=247517) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=247517\).  
  
 AD FS 2.0 fa parte di Windows Server R2 e può essere utilizzato come servizio token di sicurezza in scenari locali.  ACS è un servizio cloud, fornito come parte della piattaforma Microsoft Azure.  Per fini di test e didattici, è inoltre possibile utilizzare altri servizi token di sicurezza per compilare applicazioni in grado di riconoscere attestazioni.  Ad esempio, è possibile utilizzare il servizio token di sicurezza di sviluppo locale che fa parte di [Identity and Access Tool for Visual Studio](http://go.microsoft.com/fwlink/?LinkID=245849) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=245849\) disponibile gratuitamente online.  
  
 Per compilare la prima applicazione ASP.NET in grado di riconoscere attestazioni mediante WIF, seguire le istruzioni in uno dei collegamenti seguenti:  
  
-   [Procedura: Compilare un'applicazione Web ASP.NET MVC in grado di riconoscere attestazioni con WIF](../../../docs/framework/security/how-to-build-claims-aware-aspnet-mvc-web-app-using-wif.md)  
  
-   [Procedura: Compilare un'applicazione Web Form ASP.NET in grado di riconoscere attestazioni con WIF](../../../docs/framework/security/how-to-build-claims-aware-aspnet-web-forms-app-using-wif.md)  
  
-   [Procedura: Compilare un'applicazione ASP.NET in grado di riconoscere attestazioni con l'autenticazione basata su moduli](../../../docs/framework/security/claims-aware-aspnet-app-forms-authentication.md)  
  
## Vedere anche  
 [Guida introduttiva a WIF](../../../docs/framework/security/getting-started-with-wif.md)