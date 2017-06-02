---
title: "Procedura: utilizzare il provider di ruoli ASP.NET di Gestione autorizzazioni con un servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f21deb81-91ef-49ef-94d6-494785143271
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: utilizzare il provider di ruoli ASP.NET di Gestione autorizzazioni con un servizio
Quando [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] ospita un servizio Web, è possibile integrare Gestione autorizzazioni nell'applicazione per fornire l'autorizzazione al servizio.  Gestione autorizzazioni consente a uno sviluppatore di applicazioni di definire singole operazioni che possono essere raggruppate per formare attività.  Un amministratore può quindi autorizzare ruoli a eseguire attività specifiche o singole operazioni.  Gestione autorizzazioni fornisce uno strumento di amministrazione come uno snap\-in MMC \(Microsoft Management Console\) per gestire ruoli, attività, operazioni e utenti.  Gli amministratori configurano un archivio criteri di Gestione autorizzazioni in un file XML, in Active Directory o in un archivio ADAM \(Active Directory Application Mode\).  
  
 Gestione autorizzazioni viene integrato nell'applicazione configurando il provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] di Gestione autorizzazioni per l'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] che ospita il servizio Web.  Come altri provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], il provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] di Gestione autorizzazioni viene configurato con l'elemento \<`providers`\>.  
  
 L'esempio di codice seguente costituisce una parte di un file di configurazione per un servizio Web che sta integrando Gestione autorizzazioni nell'applicazione.  
  
```  
<system.web>  
    <roleManager enabled="true" defaultProvider="AzManRoleProvider">  
      <providers>  
        <add name="AzManRoleProvider"  
             type="System.Web.Security.AuthorizationStoreRoleProvider, System.Web, Version=2.0.0.0, Culture=neutral, publicKeyToken=b03f5f7f11d50a3a"  
             connectionStringName="AzManPolicyStoreConnectionString"   
             applicationName="SecureService"/>  
      </providers>  
    </roleManager>  
</system.web>  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'integrazione di un provider di ruoli [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] con un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Procedura: utilizzare il provider di ruoli ASP.NET con un servizio](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'uso di Gestione autorizzazioni con [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], vedere la [procedura relativa all'uso di Gestione autorizzazioni \(AzMan\) con ASP.NET 2.0](http://go.microsoft.com/fwlink/?LinkId=71303).  
  
## Vedere anche  
 [Procedura: utilizzare il provider di ruoli ASP.NET con un servizio](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)