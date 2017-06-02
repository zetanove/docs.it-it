---
title: "ServiceDescription e riferimento a WSDL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eedc025d-abd9-46b1-bf3b-61d2d5c95fd6
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# ServiceDescription e riferimento a WSDL
In questo argomento viene descritto come [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] esegue il mapping di documenti WSDL \(Web Services Description Language\) da e verso istanze <xref:System.ServiceModel.Description.ServiceDescription>.  
  
## Mapping di ServiceDescription a WSDL 1.1  
 È possibile usare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per esportare documenti WSDL da un'istanza <xref:System.ServiceModel.Description.ServiceDescription> per il servizio .  I documenti WSDL vengono generati automaticamente per il servizio quando si pubblicano endpoint di metadati.  
  
 È inoltre possibile importare istanze <xref:System.ServiceModel.Description.ServiceEndpoint>, <xref:System.ServiceModel.Description.ContractDescription> e <xref:System.ServiceModel.Channels.Binding> da documenti WSDL usando il tipo `WsdlImporter`.  
  
 I documenti WSDL, esportati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], importano tutti i dati XSD \(XML Schema Definition\) usati da documenti XSD esterni.  Per ogni spazio dei nomi di destinazione che i tipi di dati usano nel servizio viene esportato un documento XSD separato.  Analogamente, per ogni spazio dei nomi di destinazione usato dai contratti di servizio viene esportato un documento WSDL separato.  
  
### ServiceDescription  
 Un'istanza <xref:System.ServiceModel.Description.ServiceDescription> esegue il mapping a un elemento `wsdl:service`.  Un'istanza <xref:System.ServiceModel.Description.ServiceDescription> contiene una raccolta di istanze <xref:System.ServiceModel.Description.ServiceEndpoint>, ognuna delle quali esegue il mapping a singoli elementi `wsdl:port`.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Name`|Valore `wsdl:service`\/@name per il servizio.|  
|`Namespace`|Valore targetNamespace per la definizione `wsdl:service` del servizio.|  
|`Endpoints`|Definizioni di `wsdl:port` per il servizio.|  
  
### ServiceEndpoint  
 Un'istanza <xref:System.ServiceModel.Description.ServiceEndpoint> esegue il mapping a un elemento `wsdl:port`.  Un'istanza <xref:System.ServiceModel.Description.ServiceEndpoint> contiene un indirizzo, un'associazione e un contratto.  
  
 I comportamenti dell'endpoint che implementano l'interfaccia <xref:System.ServiceModel.Description.IWsdlExportExtension> possono modificare l'elemento `wsdl:port` per l'endpoint al quale sono associati.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Name`|Valore `wsdl:port`\/@name per l'endpoint e valore `wsdl:binding`\/@name per l'associazione all'endpoint.|  
|`Address`|Indirizzo per la definizione di `wsdl:port` per l'endpoint.<br /><br /> Il trasporto per l'endpoint determina il formato dell'indirizzo.  Per i trasporti supportati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ad esempio, può essere un indirizzo SOAP o un riferimento a un endpoint.|  
|`Binding`|Definizione di `wsdl:binding` per l'endpoint.<br /><br /> A differenza delle definizioni di `wsdl:binding`, le associazioni in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non vengono associate ad alcun contratto.|  
|`Contract`|Definizione di `wsdl:portType` per l'endpoint.|  
|`Behaviors`|I comportamenti dell'endpoint che implementano l'interfaccia <xref:System.ServiceModel.Description.IWsdlExportExtension> possono modificare l'elemento `wsdl:port` per l'endpoint.|  
  
### Associazioni  
 L'istanza di associazione per un'istanza `ServiceEndpoint` esegue il mapping a una definizione di `wsdl:binding`.  A differenza delle definizioni di `wsdl:binding`, che devono essere associate a una definizione di `wsdl:portType` specifica, le associazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono indipendenti da qualsiasi contratto.  
  
 Un'associazione è costituita da una raccolta di elementi di associazione.  Ogni elemento descrive alcuni aspetti relativi alla modalità di comunicazione tra l'endpoint e i client.  Un'associazione comprende inoltre una classe <xref:System.ServiceModel.Channels.MessageVersion> che indica le classi <xref:System.ServiceModel.EnvelopeVersion> e <xref:System.ServiceModel.Channels.AddressingVersion> per l'endpoint.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Name`|Utilizzato nel nome predefinito di un endpoint, ovvero il nome dell'associazione seguito dal nome del contratto separati da un carattere di sottolineatura.|  
|`Namespace`|`targetNamespace` per la definizione di `wsdl:binding`.<br /><br /> Se alla porta WSDL è associato un criterio, al momento dell'importazione viene eseguito il mapping dello spazio dei nomi di associazione importato a `targetNamespace` per la definizione di `wsdl:port`.|  
|Elemento `BindingElementCollection` restituito dal metodo `CreateBindingElements`\(\).|Varie estensioni specifiche del dominio alla definizione di `wsdl:binding`, in genere asserzioni di criteri.|  
|`MessageVersion`|`EnvelopeVersion` e `AddressingVersion` per l'endpoint.<br /><br /> Quando viene specificato `MessageVersion.None`, l'associazione WSDL non contiene un'associazione SOAP e la porta WSDL non include il contenuto WS\-Addressing.  Questa impostazione viene in genere usata per endpoint XML \(POX\) obsoleti.|  
  
#### BindingElements  
 Gli elementi di associazione per un endpoint eseguono il mapping a varie estensioni WSDL nell'elemento `wsdl:binding`, ad esempio asserzioni di criteri.  
  
 La classe <xref:System.ServiceModel.Channels.TransportBindingElement> per l'associazione determina l'URI \(Uniform Resource Identifier\) per un'associazione SOAP.  
  
#### AddressingVersion  
 L'oggetto `AddressingVersion` in un'associazione esegue il mapping alla versione di indirizzamento usata in `wsd:port`.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta indirizzi SOAP 1.1 e SOAP 1.2 e riferimenti a endpoint WS\-Addressing 08\/2004 e WS\-Addressing 1.0.  
  
#### EnvelopeVersion  
 L'oggetto `EnvelopeVersion` in un'associazione esegue il mapping alla versione di SOAP usata in `wsdl:binding`.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta associazioni SOAP 1.1 e SOAP 1.2.  
  
### Contratti  
 L'istanza <xref:System.ServiceModel.Description.ContractDescription> di un'istanza `ServiceEndpoint` esegue il mapping a `wsdl:portType`.  Un'istanza `ContractDescription` descrive tutte le operazioni per un determinato contratto.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Name`|Valore `wsdl:portType`\/@name per il contratto.|  
|`Namespace`|Valore targetNamespace per la definizione di `wsdl:portType`.|  
|`SessionMode`|Valore `wsdl:portType`\/@msc:usingSession per il contratto.  Questo attributo è un'estensione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per WSDL 1.1.|  
|`Operations`|Definizioni di `wsdl:operation` per il contratto.|  
  
### Operazioni  
 Un'istanza <xref:System.ServiceModel.Description.OperationDescription> esegue il mapping a `wsdl:portType`\/`wsdl:operation`.  Un elemento `OperationDescription` contiene una raccolta di istanze `MessageDescription` che descrivono i messaggi per l'operazione.  
  
 La modalità di esecuzione del mapping di `OperationDescription` a un documento WSDL è fortemente influenzata dai comportamenti di due operazioni: `DataContractSerializerOperationBehavior` e `XmlSerializerOperationBehavior`.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Name`|Valore `wsdl:portType`\/`wsdl:operation`\/@name per l'operazione.|  
|`ProtectionLevel`|Asserzioni di protezione in un criterio di sicurezza associato ai messaggi `wsdl:binding/wsdl:operation` per questa operazione.|  
|`IsInitiating`|Valore `wsdl:portType`\/`wsdl:operation`\/@msc:isInitiating per l'operazione.  Questo attributo è un'estensione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per WSDL 1.1.|  
|`IsTerminating`|Valore `wsdl:portType`\/`wsdl:operation`\/@msc:isTerminating per l'operazione.  Questo attributo è un'estensione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per WSDL 1.1.|  
|`Messages`|Messaggi `wsdl:portType`\/`wsdl:operation`\/`wsdl:input` e `wsdl:portType`\/`wsdl:operation`\/`wsdl:output` per l'operazione.|  
|`Faults`|Definizioni di `wsdl:portType`\/`wsdl:operation`\/`wsdl:fault` per l'operazione.|  
|`Behaviors`|`DataContractSerializerOperationBehavior` e `XmlSerializerOperationBehavior` si riferiscono all'associazione e ai messaggi dell'operazione.|  
  
#### DataContractSerializerOperationBehavior  
 L'elemento `DataContractSerializerOperationBehavior` per un'operazione è un'implementazione dell'interfaccia `IWsdlExportExtension` che esporta i messaggi e l'associazione WSDL per tale operazione.  I tipi XML Schema vengono esportati usando `XsdDataContractExporter`.  L'elemento `DataContractSerializerOperationBehavior` determina inoltre l'uso, lo stile e l'utilità di esportazione e importazione dello schema da usare per l'operazione.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`DataContractFormatAttribute`|La proprietà `Style` per questo attributo esegue il mapping al valore `wsdl:binding`\/`wsdl:operation`\/`soap:operation`\/@style per l'operazione.<br /><br /> `DataContractSerializerOperationBehavior` supporta soltanto l'uso letterale dei tipi di schema in WSDL.|  
  
#### XmlSerializerOperationBehavior  
 L'elemento `XmlSerializerOperationBehavior` per un'operazione è un'implementazione dell'interfaccia `IWsdlExportExtension` che esporta i messaggi e l'associazione WSDL per tale operazione.  I tipi XML Schema vengono esportati usando `XmlSchemaExporter`.  L'elemento `XmlSerializerOperationBehavior` determina inoltre l'uso, lo stile e l'utilità di esportazione e importazione dello schema da usare per l'operazione.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`XmlSerializerFormatAttribute`|La proprietà `Style` per questo attributo esegue il mapping al valore `wsdl:binding`\/`wsdl:operation`\/`soap:operation`\/@style per l'operazione.<br /><br /> La proprietà `Use` per questo attributo esegue il mapping ai valori `wsdl:binding`\/`wsdl:operation`\/`soap:operation`\/\*\/@use per tutti i messaggi inclusi nell'operazione.|  
  
### Messaggi  
 Un'istanza `MessageDescription` esegue il mapping a un elemento `wsdl:message` al quale fa riferimento un messaggio `wsdl:portType`\/`wsdl:operation`\/`wsdl:input` o `wsdl:portType`\/`wsdl:operation`\/`wsdl:output` in un'operazione.  Un elemento `MessageDescription` è costituito da un corpo e da intestazioni.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Action`|Azione SOAP o WS\-Addressing per il messaggio.<br /><br /> Le operazioni che usano la stringa di azione "\*" non sono rappresentate in WSDL.|  
|`Direction`|`MessageDirection.Input` esegue il mapping a `wsdl:input`.<br /><br /> `MessageDirection.Output` esegue il mapping a `wsdl:output`.|  
|`ProtectionLevel`|Asserzioni di protezione in un criterio di sicurezza associato alla definizione di `wsdl:message` per questo messaggio.|  
|`Body`|Corpo del messaggio.|  
|`Headers`|Intestazioni del messaggio.|  
|`ContractDescription.Name`, `OperationContract.Name`|Utilizzato per derivare il valore `wsdl:message`\/@name al momento dell'esportazione.|  
  
#### Corpo del messaggio  
 Un'istanza `MessageBodyDescription` esegue il mapping alle definizioni di `wsdl:message`\/`wsdl:part` per il corpo di un messaggio.  Il corpo del messaggio può essere wrapped o bare.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`WrapperName`|Se lo stile non è RPC, `WrapperName` esegue il mapping al nome dell'elemento a cui fa riferimento `wsdl:message`\/`wsdl:part` con il valore @name impostato su "parameters".|  
|`WrapperNamespace`|Se lo stile non è RPC, `WrapperNamespace` esegue il mapping allo spazio dei nomi dell'elemento per `wsdl:message`\/`wsdl:part` con il valore @name impostato su "parameters".|  
|`Parts`|Parti del messaggio per questo corpo del messaggio.|  
|`ReturnValue`|Elemento figlio dell'elemento wrapper se un elemento wrapper esiste \(stile incapsulato da documenti o stile RPC\). In caso contrario, il primo elemento `wsdl:message`\/`wsdl:part` nel messaggio.|  
  
#### Parti del messaggio  
 Un'istanza `MessagePartDescription` esegue il mapping a un elemento `wsdl:message`\/`wsdl:part` e al tipo di XML Schema o elemento a cui fa riferimento la parte del messaggio.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Name`|Valore `wsd:message`\/`wsdl:part`\/@name per la parte del messaggio e il nome dell'elemento a cui fa riferimento la parte del messaggio.|  
|`Namespace`|Spazio dei nomi dell'elemento al quale fa riferimento la parte del messaggio.|  
|`Index`|Indice dell'elemento `wsdl:message`\/`wsdl:part` per il messaggio.|  
|`ProtectionLevel`|Asserzioni di protezione in un criterio di sicurezza associato alla definizione di `wsdl:message` per questa parte del messaggio.  Nel criterio vengono impostati parametri per fare riferimento alla parte del messaggio specifica.|  
|`MessageType`|Tipo di XML Schema dell'elemento al quale fa riferimento la parte del messaggio.|  
  
#### Intestazioni del messaggio  
 Un'istanza `MessageHeaderDescription` è una parte del messaggio che esegue il mapping a un'associazione `soap:header` per la parte del messaggio.  
  
### Errori  
 Un'istanza `FaultDescription` esegue il mapping a una definizione di `wsdl:portType`\/`wsdl:operation`\/`wsdl:fault` e alla relativa definizione di `wsdl:message` associata.  L'elemento `wsdl:message` viene aggiunto allo stesso spazio dei nomi di destinazione del tipo di porta WSDL associato.  L'elemento `wsdl:message` ha una sola parte di messaggio denominata "detail" che fa riferimento all'elemento XML Schema che corrisponde al valore della proprietà `DefaultType` per l'istanza `FaultDescription`.  
  
|Proprietà|Mapping WSDL|  
|---------------|------------------|  
|`Name`|Valore `wsdl:portType`\/`wsdl:operation`\/`wsdl:fault`\/@name dell'errore.|  
|`Namespace`|Spazio dei nomi dell'elemento XML Schema al quale fa riferimento il messaggio di dettaglio dell'errore.|  
|`Action`|Azione SOAP o WS\-Addressing per l'errore.|  
|`ProtectionLevel`|Asserzioni di protezione in un criterio di sicurezza associato alla definizione di `wsdl:message` per questo errore.|  
|`DetailType`|Tipo XML Schema dell'elemento al quale fa riferimento il messaggio dettagliato.|  
|`Name, ContractDescription.Name, OperationDescription.Name,`|Utilizzato per derivare il valore `wsdl:message`\/@name per il messaggio di errore.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description>