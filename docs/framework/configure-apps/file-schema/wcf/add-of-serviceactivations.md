---
title: "&lt;add&gt; di &lt;serviceActivations&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5b01fc8-ee84-48b7-95fd-95ab54fa871f
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;add&gt; di &lt;serviceActivations&gt;
Elemento di configurazione che consente di definire impostazioni per l'attivazione di servizi virtuali che eseguono il mapping a tipi di servizi [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  In questo modo è possibile attivare servizi ospitati in WAS\/IIS senza un file con estensione svc.  
  
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
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|factory|Stringa che specifica il tipo CLR della factory che genera un elemento di attivazione del servizio.|  
|service|ServiceType che implementa il servizio, ossia il Typename completo o il Typename breve, quando viene inserito nella cartella App\_Code.|  
|relativeAddress|Indirizzo relativo all'interno dell'applicazione IIS corrente, ad esempio “Service.svc".  In WCF 4.0 questo indirizzo relativo deve contenere una delle estensioni di file note \(svc, xamlx, ecc.\).  Nessun file fisico deve esistere per l'URL relativo|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<serviceHostingEnvironment\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|Sezione di configurazione in cui vengono descritte le impostazioni di attivazione.|  
  
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
 <xref:System.ServiceModel.Configuration.ServiceActivationElement>   
 <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>   
 <xref:System.ServiceModel.ServiceHostingEnvironment>