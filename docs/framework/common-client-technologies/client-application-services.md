---
title: "Servizi applicazioni client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "impostazioni di applicazioni, servizi delle applicazioni client"
  - "servizi ASP.NET, servizi delle applicazioni client"
  - "autenticazione [ASP.NET], servizi delle applicazioni client"
  - "servizi delle applicazioni client"
  - "servizi delle applicazioni client, informazioni sui servizi delle applicazioni client"
  - "applicazioni client, servizi ASP.NET"
  - "credenziali [.NET Framework]"
  - "accessi [servizi delle applicazioni client]"
  - "profili [ASP.NET], servizi delle applicazioni client"
  - "sicurezza basata sui ruoli [.NET Framework], servizi delle applicazioni client"
  - "ruoli [.NET Framework], servizi delle applicazioni client"
  - "condivisione di informazioni e funzionalità [servizi delle applicazioni client]"
  - "impostazioni Web [servizi delle applicazioni client]"
  - "applicazioni basate su Windows, servizi delle applicazioni client"
ms.assetid: 1487d8df-089e-4f21-abfb-a791a652b58e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Servizi applicazioni client
I servizi delle applicazioni client semplificano la creazione di applicazioni basate su Windows che usano servizi dell'applicazione di accesso, ruoli e profilo di [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] inclusi in Microsoft ASP.NET 2.0 AJAX Extensions.  Questi servizi consentono a più applicazioni Web e applicazioni basate su Windows di condividere informazioni utente e funzionalità di gestione degli utenti da un singolo server.  Ad esempio, è possibile usare questi servizi per eseguire le seguenti attività:  
  
-   Autenticare un utente.  È possibile usare il servizio di autenticazione per verificare l'identità di un utente.  
  
-   Determinare uno o più ruoli di un utente autenticato.  È possibile usare il servizio ruoli per modificare l'interfaccia utente dell'applicazione in base al ruolo dell'utente.  Ad esempio, è possibile fornire funzionalità aggiuntive per gli utenti a cui è assegnato un ruolo di amministratore.  
  
-   Archiviare le impostazioni delle applicazioni per singolo utente presenti nel server e accedervi.  È possibile usare il servizio impostazioni Web \(noto anche come servizio profilo\) per condividere le impostazioni tra più applicazioni e percorsi.  
  
 I servizi delle applicazioni client sfruttano il modello di estendibilità dei servizi Web tramite provider di servizi client che è possibile specificare nei file di configurazione delle applicazioni.  Questi provider di servizi includono funzionalità offline che usano una cache locale per i dati relativi all'autenticazione, ai ruoli e alle impostazioni quando non è disponibile una connessione di rete.  
  
 Per altre informazioni sui servizi delle applicazioni [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], vedere l'argomento relativo ai [ASP.NET Application Services Overview](../Topic/ASP.NET%20Application%20Services%20Overview.md).  
  
## In questa sezione  
 [Cenni preliminari sui servizi delle applicazioni client](../../../docs/framework/common-client-technologies/client-application-services-overview.md)  
 Vengono descritte le funzionalità disponibili tramite il provider di servizi delle applicazioni client.  
  
 [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)  
 Viene descritto come usare Creazione progetti di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per abilitare e configurare i servizi delle applicazioni client.  Vengono inoltre illustrate le modifiche corrispondenti apportate al file App.config.  
  
 [Procedura: implementare l'accesso utente con i servizi dell'applicazione client](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)  
 Viene descritto come convalidare un utente quando l'applicazione è configurata per l'uso di un provider di servizi di autenticazione client.  
  
 [Procedura dettagliata: utilizzo di servizi delle applicazioni client](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)  
 Viene descritto come combinare tutte le funzionalità dei servizi delle applicazioni client in una singola applicazione.  Questa procedura dettagliata contiene indicazioni end\-to\-end,  ad esempio include istruzioni su come creare un'applicazione del servizio Web ASP.NET utilizzabile per testare i servizi delle applicazioni client.  
  
## Riferimenti  
 <xref:System.Web.ClientServices.ClientFormsIdentity>  
 <xref:System.Web.ClientServices.ClientRolePrincipal>  
 <xref:System.Web.ClientServices.ConnectivityStatus>  
 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials>  
 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>  
 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider>  
 <xref:System.Web.ClientServices.Providers.ClientWindowsAuthenticationMembershipProvider>  
 <xref:System.Web.ClientServices.Providers.ClientRoleProvider>  
 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider>  
 <xref:System.Web.ClientServices.Providers.SettingsSavedEventArgs>  
 <xref:System.Web.ClientServices.Providers.UserValidatedEventArgs>  
  
## Vedere anche  
 [ASP.NET Application Services Overview](../Topic/ASP.NET%20Application%20Services%20Overview.md)   
 [Using Forms Authentication with Microsoft Ajax](../Topic/Using%20Forms%20Authentication%20with%20Microsoft%20Ajax.md)   
 [Using Roles Information with Microsoft Ajax](../Topic/Using%20Roles%20Information%20with%20Microsoft%20Ajax.md)   
 [Using Profile Information with Microsoft Ajax](../Topic/Using%20Profile%20Information%20with%20Microsoft%20Ajax.md)   
 [ASP.NET Authentication](../Topic/ASP.NET%20Authentication.md)   
 [Managing Authorization Using Roles](../Topic/Managing%20Authorization%20Using%20Roles.md)   
 [OLD NIB: Managing Application Settings](http://msdn.microsoft.com/it-it/7de3c3bd-e0dc-4e75-a1aa-7b0ecfaac4fc)   
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../docs/framework/winforms/advanced/application-settings-overview.md)