---
title: Servizi delle applicazioni client | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- role-based security [.NET Framework], client application services
- client application services
- credentials [.NET Framework]
- Windows-based applications, client application services
- application settings, client application services
- profiles [ASP.NET], client application services
- logins [client application services]
- sharing information and functionality [client application services]
- Web settings [client application services]
- authentication [ASP.NET], client application services
- ASP.NET services, client application services
- client applications, ASP.NET services
- roles [.NET Framework], client application services
- client application services, about client application services
ms.assetid: 1487d8df-089e-4f21-abfb-a791a652b58e
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3ec7d3a3cf4c43349f0a10cac95cff507b59cfc5
ms.openlocfilehash: 227c163bcdeb26d7bd4dd005e7e872300d58a2c3
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="client-application-services"></a>Servizi applicazioni client
I servizi delle applicazioni client semplificano la creazione di applicazioni basate su Windows che usano servizi dell'applicazione di accesso, ruoli e profilo di [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)] inclusi in Microsoft ASP.NET 2.0 AJAX Extensions. Questi servizi consentono a più applicazioni Web e applicazioni basate su Windows di condividere informazioni utente e funzionalità di gestione degli utenti da un singolo server. Ad esempio, è possibile usare questi servizi per eseguire le seguenti attività:  
  
-   Autenticare un utente. È possibile usare il servizio di autenticazione per verificare l'identità di un utente.  
  
-   Determinare uno o più ruoli di un utente autenticato. È possibile usare il servizio ruoli per modificare l'interfaccia utente dell'applicazione in base al ruolo dell'utente. Ad esempio, è possibile fornire funzionalità aggiuntive per gli utenti a cui è assegnato un ruolo di amministratore.  
  
-   Archiviare le impostazioni delle applicazioni per singolo utente presenti nel server e accedervi. È possibile usare il servizio impostazioni Web (noto anche come servizio profilo) per condividere le impostazioni tra più applicazioni e percorsi.  
  
 I servizi delle applicazioni client sfruttano il modello di estendibilità dei servizi Web tramite provider di servizi client che è possibile specificare nei file di configurazione delle applicazioni. Questi provider di servizi includono funzionalità offline che usano una cache locale per i dati relativi all'autenticazione, ai ruoli e alle impostazioni quando non è disponibile una connessione di rete.  
  
 Per altre informazioni sui servizi delle applicazioni di [!INCLUDE[ajax_current_short](../../../includes/ajax-current-short-md.md)], vedere [Cenni preliminari sui servizi delle applicazioni ASP.NET](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Cenni preliminari sui servizi delle applicazioni client](../../../docs/framework/common-client-technologies/client-application-services-overview.md)  
 Vengono descritte le funzionalità disponibili tramite il provider di servizi delle applicazioni client.  
  
 [Procedura: configurare i servizi delle applicazioni client](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)  
 Viene descritto come usare Creazione progetti di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per abilitare e configurare i servizi delle applicazioni client. Vengono inoltre illustrate le modifiche corrispondenti apportate al file App.config.  
  
 [Procedura: implementare l'accesso utente con i servizi dell'applicazione client](../../../docs/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services.md)  
 Viene descritto come convalidare un utente quando l'applicazione è configurata per l'uso di un provider di servizi di autenticazione client.  
  
 [Procedura dettagliata: uso di servizi delle applicazioni client](../../../docs/framework/common-client-technologies/walkthrough-using-client-application-services.md)  
 Viene descritto come combinare tutte le funzionalità dei servizi delle applicazioni client in una singola applicazione. Questa procedura dettagliata contiene indicazioni end-to-end, ad esempio include istruzioni su come creare un'applicazione del servizio Web ASP.NET utilizzabile per testare i servizi delle applicazioni client.  
  
## <a name="reference"></a>Riferimento  
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
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sui servizi delle applicazioni ASP.NET](http://msdn.microsoft.com/library/1162e529-0d70-44b2-b3ab-83e60c695013)   
 [Uso dell'autenticazione basata su moduli con Microsoft Ajax](http://msdn.microsoft.com/library/c50f7dc5-323c-4c63-b4f3-96edfc1e815e)   
 [Uso delle informazioni sui ruoli con Microsoft Ajax](http://msdn.microsoft.com/library/280f6ad9-ba1a-4fc9-b0cc-22e39e54a82d)   
 [Uso delle informazioni sul profilo con Microsoft Ajax](http://msdn.microsoft.com/library/91239ae6-d01c-4f4e-a433-eb9040dbed61)   
 [Autenticazione ASP.NET](http://msdn.microsoft.com/library/fc10b0ef-4ce4-4a7f-9174-886325221ee1)   
 [Gestione delle autorizzazioni tramite ruoli](http://msdn.microsoft.com/library/01954ce4-39a2-487f-8153-a69f6f6f3195)    
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../docs/framework/winforms/advanced/application-settings-overview.md)
