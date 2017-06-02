---
title: "Procedura: utilizzare il provider di ruoli ASP.NET con un servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 88d33a81-8ac7-48de-978c-5c5b1257951e
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: utilizzare il provider di ruoli ASP.NET con un servizio
Il provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] \(insieme al provider di appartenenza [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]\) è una funzionalità grazie alla quale gli sviluppatori [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] sono in grado di creare siti Web che consentono agli utenti di creare un account in un sito e di acquisire ruoli a scopo di autorizzazione.Con questa funzionalità qualsiasi utente può stabilire un account nel sito e accedere in modo esclusivo al sito e ai relativi servizi.Si tratta di una funzionalità in contrasto con la protezione di Windows, in base alla quale è necessario che gli utenti dispongano di un account in un dominio Windows.Qualsiasi utente che fornisca le credenziali \(ovvero nome utente e password\) può utilizzare il sito e i relativi servizi.  
  
 Per un'applicazione di esempio, vedere [Provider di appartenenza e di ruoli](../../../../docs/framework/wcf/samples/membership-and-role-provider.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] funzione del provider di appartenenza [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], vedere [Procedura: utilizzare provider di appartenenza ASP.NET](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md).  
  
 La funzionalità del provider di ruoli utilizza un database SQL Server per archiviare informazioni utente.Gli sviluppatori [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] possono sfruttare queste funzionalità a fini di sicurezza.Dopo l'integrazione in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], gli utenti devono fornire nome utente e password all'applicazione client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Per attivare l'utilizzo del database in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è necessario creare un'istanza della classe <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>, impostare la proprietà <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A> su <xref:System.ServiceModel.Description.PrincipalPermissionMode> e aggiungere l'istanza alla raccolta dei comportamenti nella classe <xref:System.ServiceModel.ServiceHost> in cui risiede il servizio.  
  
### Per configurare il provider di ruoli  
  
1.  Nel file Web.config file, nell'elemento \<`system.web`\> aggiungere un elemento \<`roleManager`\> e impostarne l'attributo `enabled` su `true`.  
  
2.  Impostare l'attributo `defaultProvider` su `SqlRoleProvider`.  
  
3.  Aggiungere un elemento \<`providers`\> come figlio dell'elemento \<`roleManager`\>.  
  
4.  Aggiungere un elemento \<`add`\> come figlio dell'elemento \<`providers`\>, con gli attributi seguenti impostati sui valori appropriati: `name`, `type`, `connectionStringName` e `applicationName`, come mostrato nell'esempio seguente.  
  
    ```  
    <!-- Configure the Sql Role Provider. -->  
    <roleManager enabled ="true"   
     defaultProvider ="SqlRoleProvider" >  
       <providers>  
         <add name ="SqlRoleProvider"   
           type="System.Web.Security.SqlRoleProvider"   
           connectionStringName="SqlConn"   
           applicationName="MembershipAndRoleProviderSample"/>  
       </providers>  
    </roleManager>  
    ```  
  
### Per configurare il servizio per l'utilizzo del provider di ruoli  
  
1.  Nel file Web.config aggiungere un elemento [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md).  
  
2.  Aggiungere un elemento [\<comportamenti\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)\< `all'elemento system.ServiceModel`\>.  
  
3.  Aggiungere una sezione [\<comportamentiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) all'elemento \<`behaviors`\>.  
  
4.  Aggiungere un elemento [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) e impostare l'attributo `name` su un valore appropriato.  
  
5.  Aggiungere un [\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)\<`behavior all'elemento` \>.  
  
6.  Impostare l'attributo `principalPermissionMode` su `UseAspNetRoles`.  
  
7.  Impostare l'attributo `roleProviderName` su `SqlRoleProvider`.Nell'esempio seguente viene illustrata una parte della configurazione.  
  
    ```  
    <behaviors>  
     <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
       <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                             roleProviderName ="SqlRoleProvider" />  
      </behavior>  
     </serviceBehaviors>  
    </behaviors>  
    ```  
  
## Vedere anche  
 [Provider di appartenenza e di ruoli](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)   
 [Procedura: utilizzare provider di appartenenza ASP.NET](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)