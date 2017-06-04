---
title: "Configurazione dei servizi tramite file di configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "configurazione dei servizi [WCF]"
ms.assetid: c9c8cd32-2c9d-4541-ad0d-16dff6bd2a00
caps.latest.revision: 29
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Configurazione dei servizi tramite file di configurazione
La configurazione di un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] con un file di configurazione assicura la possibilità di fornire dati sul comportamento di endpoint e servizi al momento della distribuzione invece che in fase di progettazione. In questo argomento vengono delineate le principali tecniche disponibili.  
  
 Un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] può essere configurato mediante la tecnologia di configurazione [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. In genere, gli elementi XML vengono aggiunti al file Web.config per un sito Internet Information Services \(IIS\) che ospita un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Gli elementi consentono di modificare dettagli, quali gli indirizzi degli endpoint \(gli indirizzi effettivi usati per comunicare con il servizio\), per i singoli computer.[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] include inoltre diversi elementi forniti dal sistema che consentono di selezionare rapidamente la maggior parte delle funzionalità di base per un servizio. A partire da [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)], [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene fornito con un nuovo modello di configurazione predefinito che semplifica i requisiti di configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Se non si specifica alcuna configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per un determinato servizio, il runtime configura automaticamente il servizio con alcuni endpoint standard e con comportamento\/associazione predefinito. In pratica, la creazione della configurazione è un fattore essenziale della programmazione di applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Configurazione di associazioni per servizi](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md).[!INCLUDE[crlist](../../../includes/crlist-md.md)] degli elementi più comunemente usati, vedere [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)] endpoint, associazioni e comportamenti predefiniti, vedere [Configurazione semplificata](../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
> [!IMPORTANT]
>  Nel caso di distribuzione di scenari affiancati in cui vengono implementate due versioni diverse di un servizio, è necessario specificare nomi parziali di assembly a cui viene fatto riferimento nei file di configurazione. Questa operazione è necessaria perché il file di configurazione è condiviso tra tutte le versioni di un servizio che potrebbero essere in esecuzione in versioni diverse di .NET Framework.  
  
## System.Configuration: Web.config e App.config  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] usa il sistema di configurazione System.Configuration di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Quando si configura un servizio in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], usare un file Web.config o App.config per specificare le impostazioni. La scelta del nome del file di configurazione è determinata dall'ambiente host scelto per il servizio. Se si sta usando IIS per ospitare il servizio, usare un file Web.config. Se si sta usando un altro ambiente host, usare un file App.config.  
  
 In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], il file denominato App.config viene usato per creare il file di configurazione finale. Il nome finale effettivamente usato per la configurazione dipende dal nome dell'assembly. Ad esempio, un assembly denominato "Cohowinery.exe" ha un file di configurazione finale denominato "Cohowinery.exe.config". Tuttavia, è sufficiente modificare il file App.config. Le modifiche apportate al file vengono automaticamente apportate al file di configurazione finale dell'applicazione in fase di compilazione.  
  
 Quando si usa un file App.config, il sistema di configurazione unisce il file App.config al contenuto del file Machine.config, al momento dell'avvio dell'applicazione e dell'applicazione della configurazione. Questo meccanismo consente di definire impostazioni a livello di computer nel file Machine.config. Il file App.config può essere usato per eseguire l'override del file Machine.config; è inoltre possibile bloccare le impostazioni nel file Machine.config in modo che vengano usate. Nel caso di Web.config, il sistema di configurazione esegue il merge dei file Web.config in tutte le directory che conducono alla directory dell'applicazione nella configurazione che viene applicata.[!INCLUDE[crabout](../../../includes/crabout-md.md)]lla configurazione e sulle priorità delle impostazioni, vedere gli argomenti nello spazio dei nomi <xref:System.Configuration>.  
  
## Principali sezioni del file di configurazione  
 Le sezioni principali del file di configurazione includono gli elementi seguenti.  
  
```  
<system.ServiceModel>  
  
   <services>  
   <!—- Define the service endpoints. This section is optional in the new  
    default configuration model in .NET Framework 4. -->  
      <service>  
         <endpoint/>  
      </service>  
   </services>  
  
   <bindings>  
   <!-- Specify one or more of the system-provided binding elements,  
    for example, <basicHttpBinding> -->   
   <!-- Alternatively, <customBinding> elements. -->  
      <binding>  
      <!-- For example, a <BasicHttpBinding> element. -->  
      </binding>  
   </bindings>  
  
   <behaviors>  
   <!-- One or more of the system-provided or custom behavior elements. -->  
      <behavior>  
      <!-- For example, a <throttling> element. -->  
      </behavior>  
   </behaviors>  
  
</system.ServiceModel>  
```  
  
> [!NOTE]
>  Le sezioni di associazioni e comportamenti sono facoltative e vengono incluse solo se necessario.  
  
### Elemento \<services\>  
 L'elemento `services` contiene le specifiche per tutti i servizi ospitati dall'applicazione. A partire dal modello di configurazione semplificato in [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)], questa sezione è facoltativa.  
  
 [\<servizi\>](../../../docs/framework/configure-apps/file-schema/wcf/services.md)  
  
### Elemento \<service\>  
 Ogni servizio ha gli attributi seguenti:  
  
-   `name`. Specifica il tipo che fornisce un'implementazione di un contratto di servizio. Si tratta di un nome completo costituito dallo spazio dei nomi, seguito da un punto e quindi dal nome del tipo. Ad esempio, `"MyNameSpace.myServiceType"`.  
  
-   `behaviorConfiguration`. Specifica il nome di uno degli elementi `behavior` presenti nell'elemento `behaviors`. Il comportamento specificato regola azioni, stabilendo, ad esempio, se il servizio consente la rappresentazione. Se il valore è il nome vuoto o se non viene specificato alcun attributo `behaviorConfiguration`, viene aggiunto al servizio il set predefinito di comportamenti del servizio.  
  
-   [\<service\>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)  
  
### Elemento \<endpoint\>  
 Ogni endpoint richiede un indirizzo, un'associazione e un contratto, rappresentati dagli attributi seguenti:  
  
-   `address`. Specifica l'URI \(Uniform Resource Identifier\) del servizio, che può essere un indirizzo assoluto o uno relativo all'indirizzo di base del servizio. Se impostato su una stringa vuota, indica che l'endpoint è disponibile all'indirizzo di base specificato durante la creazione di <xref:System.ServiceModel.ServiceHost> per il servizio.  
  
-   `binding`. In genere, specifica un'associazione fornita dal sistema come <xref:System.ServiceModel.WsHttpBinding>, ma può specificare anche un'associazione definita dall'utente. L'associazione specificata determina il tipo di trasporto, sicurezza e codifica usato e se sono supportati o attivati flussi, sessioni affidabili o transazioni.  
  
-   `bindingConfiguration`. Se i valori predefiniti di un'associazione devono essere modificati, è possibile farlo configurando l'elemento `binding` appropriato nell'elemento `bindings`. A questo attributo deve essere assegnato lo stesso valore dell'attributo `name` dell'elemento `binding` usato per modificare le impostazioni predefinite. Se non viene assegnato alcun nome o non si specifica alcun attributo `bindingConfiguration` nell'associazione, nell'endpoint viene usata l'associazione predefinita del tipo di associazione.  
  
-   `contract`. Specifica l'interfaccia che definisce il contratto. Si tratta dell'interfaccia implementata nel tipo CLR \(Common Language Runtime\) specificato dall'attributo `name` dell'elemento `service`.  
  
-   [\<endpoint\> element reference](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017)  
  
### Elemento \<bindings\>  
 L'elemento `bindings` contiene le specifiche per tutte le associazioni usabili da qualsiasi endpoint definito in qualsiasi servizio.  
  
 [\<associazioni\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)  
  
### Elemento \<binding\>  
 L'elemento `binding` contenuto nell'elemento `bindings` può essere una delle associazioni fornite dal sistema \(vedere [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md)\) o un'associazione personalizzata \(vedere [Associazioni personalizzate](../../../docs/framework/wcf/extending/custom-bindings.md)\). L'elemento `binding` ha un attributo `name` che mette in correlazione l'associazione e l'endpoint specificato nell'attributo `bindingConfiguration` dell'elemento `endpoint`. Se non è specificato alcun nome, l'associazione corrisponde all'impostazione predefinita del tipo di associazione.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] come configurare servizi e client, vedere [Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/it-it/13cb368e-88d4-4c61-8eed-2af0361c6d7a).  
  
 [\<associazione\>](../../../docs/framework/misc/binding.md)  
  
### Elemento \<behaviors\>  
 Si tratta di un elemento contenitore per gli elementi `behavior` che definiscono i comportamenti di un servizio.  
  
 [\<comportamenti\>](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)  
  
### Elemento \<behavior\>  
 Ogni elemento `behavior` è identificato da un attributo `name` e specifica un comportamento fornito dal sistema, ad esempio \<`throttling`\>, o un comportamento personalizzato. Se non viene assegnato alcun nome, l'elemento relativo al comportamento corrisponde al comportamento del servizio o dell'endpoint predefinito.  
  
 [\<comportamento\>](../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md)  
  
## Come usare configurazioni di associazioni e comportamenti  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] semplifica la condivisione delle configurazioni tra endpoint usando un sistema di riferimento nella configurazione. Invece di assegnare direttamente valori di configurazione a un endpoint, i valori di configurazione relativi all'associazione vengono raggruppati in elementi `bindingConfiguration` nella sezione `<binding>`. Una configurazione di associazione è un gruppo denominato di impostazioni su un'associazione. Gli endpoint possono quindi fare riferimento a `bindingConfiguration` in base al nome.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
 <system.serviceModel>  
  <bindings>  
    <basicHttpBinding>  
     <binding name="myBindingConfiguration1" closeTimeout="00:01:00" />  
     <binding name="myBindingConfiguration2" closeTimeout="00:02:00" />  
     <binding closeTimeout="00:03:00" />  <!—- Default binding for basicHttpBinding -->  
    </basicHttpBinding>  
     </bindings>  
     <services>  
      <service name="MyNamespace.myServiceType">  
       <endpoint   
          address="myAddress" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration1"  
          contract="MyContract"  />  
       <endpoint   
          address="myAddress2" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration2"  
          contract="MyContract" />  
       <endpoint   
          address="myAddress3" binding="basicHttpBinding"   
          contract="MyContract" />  
       </service>  
      </services>  
    </system.serviceModel>  
</configuration>  
```  
  
 L'attributo `name` di `bindingConfiguration` è impostato nell'elemento `<binding>`.`name` deve essere una stringa univoca all'interno dell'ambito del tipo di associazione, in questo caso [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) o un valore vuoto per fare riferimento all'associazione predefinita. L'endpoint si collega alla configurazione impostando l'attributo `bindingConfiguration` su questa stringa.  
  
 Un attributo `behaviorConfiguration` viene implementato nello stesso modo, come illustrato nell'esempio seguente.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myBehavior">  
           <callbackDebug includeExceptionDetailInFaults="true" />  
         </behavior>  
      </endpointBehaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="true" />  
        </behavior>  
      </serviceBehaviors>  
  
    </behaviors>  
    <services>  
     <service name="NewServiceType">  
       <endpoint   
          address="myAddress3" behaviorConfiguration="myBehavior"  
          binding="basicHttpBinding"  
          contract=”MyContract” />  
      </service>  
    </services>  
   </system.serviceModel>  
</configuration>  
```  
  
 Si noti che al servizio viene aggiunto il set predefinito di comportamenti del servizio. Questo sistema consente agli endpoint di condividere configurazioni comuni senza ridefinire le impostazioni. Se è necessario un ambito a livello di computer, creare la configurazione di associazione o comportamento in Machine.config. Le impostazioni di configurazione sono disponibili in tutti i file App.config.[Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) semplifica la creazione di configurazioni.  
  
## Unione di comportamenti  
 La funzionalità di unione dei comportamenti semplifica la gestione di questi ultimi quando si desidera un set di comportamenti comuni da usare in modo coerente. Tale funzionalità consente di specificare i comportamenti a livelli diversi della gerarchia di configurazione e consente altresì ai servizi di ereditare i comportamenti da più livelli della gerarchia di configurazione. Per illustrare questo funzionamento, si presupponga di disporre del layout di directory virtuale seguente in IIS:  
  
 ~\\Web.config~\\Service.svc~\\Child\\Web.config~\\Child\\Service.svc  
  
 Il file ~\\Web.config contiene gli elementi seguenti:  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceDebug includeExceptionDetailInFaults="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 Un figlio Web.config è situato in ~\\Child\\Web.config con il contenuto seguente:  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 Il servizio presente in ~\\Child\\Service.svc si comporterà come se disponesse di entrambi i comportamenti di serviceDebug e serviceMetadata, mentre il servizio in ~ \\Service.svc disporrà solo del comportamento di serviceDebug. In pratica vengono unite le due raccolte di comportamenti con lo stesso nome \(in questo caso la stringa vuota\).  
  
 È anche possibile cancellare raccolte di comportamenti tramite il tag \<clear\> e rimuovere comportamenti individuali dalla raccolta tramite il tag \<remove\>. Le due configurazioni seguenti, ad esempio, determinano il solo comportamento di serviceMetadata per il servizio figlio:  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <remove name="serviceDebug"/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <clear/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 L'unione di comportamenti può essere eseguita per raccolte di comportamenti anonimi, come illustrato in precedenza, e raccolte di comportamenti denominati.  
  
 Tale unione funziona non solo nell'ambiente di hosting IIS, in cui i file Web.config si uniscono gerarchicamente con il file Web.config radice e con machine.config, ma anche nell'ambiente dell'applicazione, in cui machine.config può unirsi con il file App.config.  
  
 L'unione di comportamenti si applica sia comportamenti dell'endpoint che a comportamenti del servizio nella configurazione.  
  
 Se una raccolta di comportamenti figlio contiene un comportamento già presente nella raccolta di comportamenti padre, il comportamento figlio sostituisce quello del padre. Di conseguenza, se a una raccolta di comportamenti padre fosse associato `<serviceMetadata httpGetEnabled="False" />` e alla raccolta di comportamenti figlio fosse associato `<serviceMetadata httpGetEnabled="True" />`, il comportamento figlio sostituirebbe il comportamento padre nella raccolta di comportamenti e httpGetEnabled sarebbe impostato su true.  
  
## Vedere anche  
 [Configurazione semplificata](../../../docs/framework/wcf/simplified-configuration.md)   
 [Configuring Windows Communication Foundation Applications](http://msdn.microsoft.com/it-it/13cb368e-88d4-4c61-8eed-2af0361c6d7a)   
 [\<service\>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)   
 [\<associazione\>](../../../docs/framework/misc/binding.md)