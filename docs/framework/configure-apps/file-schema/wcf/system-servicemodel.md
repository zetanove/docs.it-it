---
title: "&lt;system.serviceModel&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#system.ServiceModel"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.ServiceModel"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "elemento <system.serviceModel>"
  - "system.serviceModelelement"
ms.assetid: 78519531-ad7a-40d3-b3e7-42f1103d8854
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# &lt;system.serviceModel&gt;
Questa sezione di configurazione contiene tutti gli elementi di configurazione del modello ServiceModel di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Sintassi  
  
```  
  
<system.serviceModel>  
    <behaviors>  
    </behaviors>  
    <bindings>  
    </bindings>  
    <client>  
    </client>  
    <comContracts>  
    </comContracts>  
    <commonBehaviors>  
    </commonBehaviors>  
    <diagnostics>  
    </diagnostics>  
    <extensions>  
    </extensions>  
    <protocolMapping>  
    </protocolMapping>  
    <routing>  
    </routing>  
    <serviceHostingEnvironment>  
    </serviceHostingEnvironment>  
    <services>  
    </services>  
    <standardEndpoints>  
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 None  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamenti\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)|Questa sezione definisce due raccolte figlio denominate `endpointBehaviors` e `serviceBehaviors`.  Ogni raccolta definisce elementi di comportamento usati rispettivamente da endpoint e servizi.  Ogni elemento di comportamento è identificato dal relativo attributo `name` univoco.|  
|[\<associazioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Questa sezione contiene una raccolta di associazioni standard e personalizzate.  Ogni voce è identificata dal relativo attributo `name` univoco.  I servizi usano le associazioni collegandole mediante l'oggetto `name`.|  
|[\<client\>](../../../../../docs/framework/configure-apps/file-schema/wcf/client.md)|Questa sezione include un elenco degli endpoint usati da un client per connettersi a un servizio.|  
|[\<comContracts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontracts.md)|Questa sezione definisce i contratti COM che consentono l'interoperabilità tra WCF e COM.|  
|[\<comportamentiComuni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)|Il contenuto di questa sezione può essere definito solo nel file machine.config.  e definisce due raccolte figlio denominate `endpointBehaviors` e `serviceBehaviors`.  Ogni raccolta definisce elementi di comportamento usati rispettivamente da tutti gli endpoint [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] e dai servizi del computer.  Se un comportamento viene definito in entrambe le sezioni `<commonBehaviors>` e `<behaviors>`, viene data la preferenza al comportamento nelle sezioni \<behaviors\>.|  
|[\<estensioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/extensions-section.md)|Questa sezione include una raccolta di estensioni che consentono di creare associazioni definite dall'utente, comportamenti e altri aspetti relativi alle estensioni.|  
|[\<diagnostica\>](../../../../../docs/framework/configure-apps/file-schema/wcf/diagnostics.md)|Questa sezione include le impostazioni per le funzionalità di diagnostica di WCF.  L'utente può abilitare o disabilitare tracce, contatori di prestazioni e il provider WMI e può aggiungere filtri dei messaggi personalizzati.|  
|[\<protocolMapping\>](../../../../../docs/framework/configure-apps/file-schema/wcf/protocolmapping.md)|Questa sezione definisce un set di mapping dei protocolli predefiniti tra gli schemi dei protocolli di trasporto \(ad esempio http, net.tcp, net.pipe e così via\) e le associazioni di WCF.|  
|[\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing.md)|Questa sezione definisce un set di filtri di routing che determinano il tipo di <xref:System.ServiceModel.Dispatcher.MessageFilter> di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] da usare durante la valutazione di messaggi in arrivo, nonché tabelle di routing che definiscono gli endpoint di destinazione ai quali inviare i messaggi quando viene trovata una corrispondenza.|  
|[\<serviceHostingEnvironment\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|Questa sezione definisce il tipo del quale l'ambiente host del servizio crea un'istanza per un determinato trasporto.  Se questa sezione è vuota, viene usato il tipo predefinito.|  
|[\<servizi\>](../../../../../docs/framework/configure-apps/file-schema/wcf/services.md)|Questa sezione include una raccolta di servizi.  Per ogni servizio definito nell'assembly, questo elemento contiene un elemento `service` nel quale vengono specificate le impostazioni per il servizio.|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|Questa sezione definisce una raccolta di endpoint standard rappresentati da endpoint preconfigurati riusabili.  Un endpoint standard disporrà di uno o più indirizzi, attributi di associazione e del contratto impostati su un valore fisso.  Ad esempio, nell'endpoint di individuazione il contratto è fisso.  È inoltre possibile usare endpoint standard per estendere endpoint servizio con nuove proprietà in modo analogo alla definizione di associazioni personalizzate.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\<configuration\>|Elemento radice di tutti gli elementi di configurazione contenuti in un file di configurazione .NET.|  
  
## Note  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] non aggiunge elementi alle sezioni di configurazione di altri prodotti.  
  
 I servizi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] vengono definiti nella sezione `services` del file di configurazione.  Un assembly può contenere un numero qualsiasi di servizi.  Ogni servizio dispone di una propria sezione di configurazione `service`.  La sezione e il relativo contenuto definiscono in modo specifico il contratto, il comportamento e gli endpoint del servizio.  
  
 Fra gli attributi di un servizio, solo `name` è obbligatorio.  Per impostazione predefinita, il nome di un servizio descrive il tipo CLR sottostante usato per implementare un servizio. È tuttavia possibile modificare la proprietà ConfigurationName di un attributo <xref:System.ServiceModel.ServiceContractAttribute> per eseguire l'override del requisito del tipo CLR.  
  
 L'attributo `behaviorConfiguration` è facoltativo.  identifica il comportamento usato dal servizio.  Il comportamento specificato da questo attributo deve essere collegato a un comportamento di servizio definito nell'ambito dello stesso file di configurazione, ad esempio  lo stesso file o un file padre.  
  
 Ogni servizio espone uno o più endpoint definiti in un elemento `endpoint`.  Ogni endpoint presenta indirizzo e associazione propri.  Tutte le associazioni usate all'interno del file di configurazione devono essere definite nell'ambito del file.  
  
 Le associazioni sono collegate agli endpoint tramite la combinazione di attributi `name` e `bindingConfiguration`.  L'attributo `binding` definisce la sezione in cui è definita l'associazione.  L'attributo `bindingConfiguration` definisce quale associazione configurata viene usata fra quelle contenute nella sezione di associazione.  Una sezione di associazione può infatti definire varie associazioni configurate.  
  
## Esempio  
 Segue un esempio di file di configurazione di WCF.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
           <!-- List of Behaviors -->  
        </behaviors>  
        <client>  
           <!-- List of Endpoints -->  
        </client>  
        <diagnostics wmiProviderEnabled="false" performanceCountersEnabled="false" tracingEnabled="false">  
        </diagnostics>  
        <serviceHostingEnvironment>  
           <!-- List of entries -->  
        </serviceHostingEnvironment>  
        <comContracts>  
           <!-- List of COM+ Contracts -->  
        </comContracts>          
        <services>  
           <!-- List of Services -->  
        </services>  
        <bindings>  
           <!-- List of Bindings -->  
        </bindings>  
    </system.serviceModel>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceModelSectionGroup>