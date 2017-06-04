---
title: "&lt;serviceActivations&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97e665b6-1c51-410b-928a-9bb42c954ddb
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;serviceActivations&gt;
Elemento di configurazione che consente di aggiungere impostazioni che definiscono impostazioni per l'attivazione di servizi virtuali che eseguono il mapping a tipi di servizi [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  In questo modo è possibile attivare servizi ospitati in WAS\/IIS senza un file con estensione svc.  
  
## Sintassi  
  
```  
  
<serviceHostingEnvironment>   
   <serviceActivations>  
      <add factory="String"  
           service="String"/>  
   </serviceActivations>  
</serviceHostingEnvironment>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-serviceactivations.md)|Aggiunge un elemento di configurazione che specifica l'attivazione di un'applicazione di servizio.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<serviceHostingEnvironment\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|Definisce il tipo del quale l'ambiente host del servizio crea un'istanza per un determinato trasporto.|  
  
## Note  
 Nell'esempio seguente viene illustrato come configurare le impostazioni di attivazione all'interno del file web.config.  
  
```  
<configuration>  
  <system.serviceModel>  
    <serviceHostingEnvironment>  
      <serviceActivations>  
        <add service="GreetingService"/>  
      </serviceActivations>  
    </serviceHostingEnvironment>  
  </system.serviceModel>  
</configuration>  
```  
  
 L'utilizzo di questa configurazione consente di attivare GreetingService senza usare un file con estensione svc.  
  
 Si noti che `<serviceHostingEnvironment>` è una configurazione a livello di applicazione.  È necessario posizionare il file `web.config` contenente la configurazione nella radice dell'applicazione virtuale.  Inoltre, `serviceHostingEnvironment` è una sezione ereditabile di machinetoApplication.  Se si registra un servizio nella radice del computer, ogni servizio dell'applicazione erediterà tale servizio.  
  
 L'attivazione basata sulla configurazione supporta l'attivazione sul protocollo http e non http.  A tale scopo sono necessarie le estensioni in relatativeAddress, ossia  svc, xoml o xamlx.  È possibile eseguire il mapping di estensioni personalizzate ai provider di compilazione noti, consentendo in tal modo l'attivazione di servizi su qualsiasi estensione.  In caso di conflitto, la sezione `<serviceActivations>` esegue l'override delle registrazioni nel file con estensione svc.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceActivationElementCollection>   
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>