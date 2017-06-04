---
title: "Attivazione basata sulla configurazione in IIS e WAS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6a927e1f-b905-4ee5-ad0f-78265da38238
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Attivazione basata sulla configurazione in IIS e WAS
In genere, quando si ospita un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] in Internet Information Services \(IIS\) o nel servizio Attivazione processo Windows \(WAS\), è necessario fornire un file con estensione svc.Il file con estensione svc contiene il nome del servizio e una factory di host del servizio personalizzata facoltativa.Quest'ulteriore file comporta un sovraccarico ai fini della gestibilità.Con la funzionalità di attivazione basata sulla configurazione non è più necessario disporre di un file con estensione svc e quindi tale sovraccarico viene evitato.  
  
## Attivazione basata sulla configurazione  
 L'attivazione basata sulla configurazione acquisisce i metadati posizionati nel file con estensione svc e li sposta nel file Web.config.Nell'elemento \<`serviceHostingEnvironment`\> si trova un elemento \<`serviceActivations`\>.Nell'elemento \<`serviceActivations`\> si trovano uno o più elementi \<`add`\>, uno per ogni servizio ospitato.L'elemento \<`add`\> contiene attributi che consentono di impostare il relativo indirizzo per il servizio e il tipo di servizio o una factory di host del servizio.Nell'esempio di codice di configurazione riportato di seguito viene illustrato come utilizzare questa sezione.  
  
> [!NOTE]
>  Ogni elemento \<`add`\> deve specificare un servizio o un attributo della factory.È consentita la specifica sia degli attributi del servizio che della factory.  
  
```  
<serviceHostingEnvironment>  
  <serviceActivations>  
    <add relativeAddress="MyServiceAddress" service="Service" factory=”MyServiceHostFactory”/>  
  </serviceActivations>  
</serviceHostingEnvironment>  
```  
  
 Con questa situazione nel file Web.config è possibile posizionare il codice sorgente del servizio nella directory App\_Code dell'applicazione o un assembly compilato nella directory bin dell'applicazione.  
  
> [!NOTE]
>  -   Quando si utilizza l'attivazione basata sulla configurazione, il codice inline presente nei file con estensione svc non è supportato.  
> -   È necessario impostare l'attributo `relativeAddress` su un indirizzo relativo quale “\<sottodirectory\>\/service.svc” o “~\/\<sottodirectory\/service.svc”.  
> -   Se si registra un indirizzo relativo che non dispone di un'estensione nota associata a WCF, viene generata un'eccezione di configurazione.  
> -   L'indirizzo specificato è relativo alla radice dell'applicazione virtuale.  
> -   A causa del modello gerarchico della configurazione, gli indirizzi relativi registrati a livello del computer e del sito vengono ereditati dalle applicazioni virtuali.  
> -   Le registrazioni in un file di configurazione hanno priorità rispetto alle impostazioni in un file con estensione svc, xamlx, xoml o di un altro tipo.  
> -   Qualsiasi simbolo '\\' \(barra rovesciata\) in un URI inviato a IIS\/WAS viene convertito in modo automatico in un simbolo '\/' \(barra\).Se viene aggiunto un indirizzo relativo che contiene un simbolo '\\' e viene inviato a IIS un URI che utilizza l'indirizzo relativo, la barra rovesciata viene convertita in una barra normale e IIS non è in grado di associarla all'indirizzo relativo.IIS invia informazioni di traccia a indicare che non è stata rilevata alcuna corrispondenza.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection.ServiceActivations%2A>   
 [Servizi host](../../../../docs/framework/wcf/hosting-services.md)   
 [Panoramica dell'hosting dei servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md)   
 [\<serviceHostingEnvironment\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)   
 [Funzionalità di hosting di AppFabric](http://go.microsoft.com/fwlink/?LinkId=201276)