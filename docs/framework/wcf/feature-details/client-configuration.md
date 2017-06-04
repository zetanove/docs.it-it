---
title: "Configurazione del client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5da5bd3b-65d9-43b7-91b9-cc9e989b1350
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Configurazione del client
La configurazione client di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] può essere utilizzata per specificare l'indirizzo, l'associazione, il comportamento e il contratto, ovvero le proprietà di base dell'endpoint client utilizzate dai client per connettersi agli endpoint di servizio.  L'elemento [\<client\>](../../../../docs/framework/configure-apps/file-schema/wcf/client.md) presenta un elemento [\<endpoint\>](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017) i cui attributi consentono di configurare le proprietà di base dell'endpoint.  Questi attributi sono descritti nella sezione "Configurazione degli endpoint" di questo argomento.  
  
 L'elemento [\<endpoint\>](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017) contiene inoltre un elemento [\<metadati\>](../../../../docs/framework/configure-apps/file-schema/wcf/metadata.md) utilizzato per specificare le impostazioni relative all'importazione e all'esportazione di metadati, un elemento [\<intestazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md) che contiene una raccolta di intestazioni di indirizzo personalizzate e un elemento  [\<identità\>](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md) che consente all'endpoint di essere autenticato dagli altri endpoint con cui scambia messaggi.  Gli elementi [\<intestazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md) e [\<identità\>](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md) sono parte di <xref:System.ServiceModel.EndpointAddress> e sono descritti nell'argomento [Indirizzi](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md).  I collegamenti agli argomenti che spiegano l'utilizzo delle estensioni di metadati sono riportati nella sottosezione "Configurazione di metadati" di questo argomento.  
  
## Configurazione degli endpoint  
 La configurazione client è progettata per consentire al client di specificare uno o più endpoint e di definire per ognuno di essi nome, indirizzo e contratto. Ognuno di questi elementi di endpoint fa riferimento agli elementi [\<associazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) e [\<comportamenti\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) della configurazione client da utilizzare per configurare tale endpoint.  Il file di configurazione client deve essere denominato con il nome previsto dal runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ovvero "App.config".  Nell'esempio seguente viene illustrato un file di configurazione client.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
        <client>  
          <endpoint  
            name="endpoint1"  
            address="http://localhost/ServiceModelSamples/service.svc"  
            binding="wsHttpBinding"  
            bindingConfiguration="WSHttpBinding_IHello"  
            behaviorConfiguration="IHello_Behavior"  
            contract="IHello" >  
  
            <metadata>  
              <wsdlImporters>  
                <extension  
                  type="Microsoft.ServiceModel.Samples.WsdlDocumentationImporter, WsdlDocumentation"/>  
              </wsdlImporters>  
            </metadata>  
  
            <identity>  
              <servicePrincipalName value="host/localhost" />  
            </identity>  
          </endpoint>  
// Add another endpoint by adding another <endpoint> element.  
          <endpoint  
            name="endpoint2">  
           //Configure another endpoint here.  
          </endpoint>  
        </client>  
  
//The bindings section references by the bindingConfiguration endpoint attribute.  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_IHello"   
                 bypassProxyOnLocal="false"   
                 hostNameComparisonMode="StrongWildcard">  
          <readerQuotas maxDepth="32"/>  
          <reliableSession ordered="true"   
                           enabled="false" />  
          <security mode="Message">  
           //Security settings go here.  
          </security>  
        </binding>  
        <binding name="Another Binding"  
        //Configure this binding here.  
        </binding>  
          </wsHttpBinding>  
        </bindings>  
  
//The behavior section references by the behaviorConfiguration endpoint attribute.  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name=" IHello_Behavior ">  
                    <clientVia />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
  
    </system.serviceModel>  
</configuration>  
```  
  
 L'attributo `name` facoltativo identifica in modo univoco un endpoint per un dato contratto.  In particolare, tale attributo viene utilizzato dal costruttore <xref:System.ServiceModel.ChannelFactory%601.%23ctor%2A> o dal costruttore <xref:System.ServiceModel.ClientBase%601.%23ctor%2A> per specificare l'endpoint della configurazione client da configurare e da caricare quando viene creato un canale per il servizio.  È possibile scegliere come nome di configurazione di endpoint il carattere jolly "\*". In questo caso, il metodo <xref:System.ServiceModel.ChannelFactory.ApplyConfiguration%2A> carica qualsiasi configurazione di endpoint contenuta nel file, purché ne sia presente soltanto una. Se sono presenti più configurazioni di endpoint, viene generata un'eccezione.  Se questo attributo viene omesso, l'endpoint corrispondente viene utilizzato come endpoint predefinito associato al tipo di contratto specificato.  Il valore predefinito dell'attributo `name` è una stringa vuota a cui si fa riferimento con le stesse modalità utilizzate per qualsiasi altro nome.  
  
 Affinché possa essere individuato e identificato, ogni endpoint deve presentare un indirizzo.  L'attributo `address` può essere utilizzato per specificare l'URL che indica la posizione dell'endpoint.  Tuttavia, l'indirizzo di un endpoint di servizio può anche essere specificato in codice creando un Uniform Resource Identifier \(URI\) e aggiungendo tale identificatore all'elemento <xref:System.ServiceModel.ServiceHost> tramite uno dei metodi <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Indirizzi](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md).  Come già menzionato nell'introduzione, gli elementi [\<intestazioni\>](../../../../docs/framework/configure-apps/file-schema/wcf/headers.md) e [\<identità\>](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md) sono parte di <xref:System.ServiceModel.EndpointAddress> e pertanto sono anch'essi descritti nell'argomento [Indirizzi](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md).  
  
 L'attributo `binding` indica il tipo di associazione che l'endpoint prevede di utilizzare per la connessione a un servizio.  Se si prevede di fare riferimento al tipo occorre registrare per quest'ultimo una sezione di configurazione.  Nell'esempio precedente questa sezione corrisponde alla sezione [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) in cui si indica che l'endpoint utilizza <xref:System.ServiceModel.WSHttpBinding>.  È tuttavia possibile che l'endpoint utilizzi più di un'associazione di un determinato tipo.  Ogni associazione presenta un proprio elemento [\<associazione\>](../../../../docs/framework/misc/binding.md) all'interno dell'elemento di tipo \(dell'associazione\).  L'attributo `bindingconfiguration` viene utilizzato per distinguere le associazioni dello stesso tipo.  Il valore di tale attributo fa riferimento all'attributo `name` dell'elemento [\<associazione\>](../../../../docs/framework/misc/binding.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come configurare un'associazione client nella configurazione, vedere [Procedura: specificare un'associazione client nella configurazione](../../../../docs/framework/wcf/how-to-specify-a-client-binding-in-configuration.md).  
  
 L'attributo `behaviorConfiguration` viene utilizzato per specificare l'elemento [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) dell'elemento [\<comportamentiEndpoint\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md) che l'endpoint deve utilizzare.  Il valore di tale attributo fa riferimento all'attributo `name` dell'elemento [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md).  Per un esempio di come utilizzare la configurazione per specificare i comportamenti dei client, vedere [Configurazione dei comportamenti client](../../../../docs/framework/wcf/configuring-client-behaviors.md).  
  
 L'attributo `contract` specifica il contratto esposto dall'endpoint.  Questo valore fa riferimento alla proprietà <xref:System.ServiceModel.ServiceContractAttribute.ConfigurationName%2A> dell'attributo <xref:System.ServiceModel.ServiceContractAttribute>.  Il valore predefinito è il nome di tipo completo della classe che implementa il servizio.  
  
### Configurazione di metadati  
 L'elemento [\<metadati\>](../../../../docs/framework/configure-apps/file-schema/wcf/metadata.md) viene utilizzato per specificare le impostazioni utilizzate per registrare le estensioni di importazione di metadati.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'estensione del sistema di metadati, vedere [Estensione del sistema di metadati](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md).  
  
## Vedere anche  
 [Endpoint: indirizzi, associazioni e contratti](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)   
 [Configurazione dei comportamenti client](../../../../docs/framework/wcf/configuring-client-behaviors.md)