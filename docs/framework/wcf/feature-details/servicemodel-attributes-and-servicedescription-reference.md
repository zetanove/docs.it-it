---
title: "Attributi ServiceModel e riferimento a ServiceDescription | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ab86b17-eab9-4846-a881-0099f9a7cc64
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Attributi ServiceModel e riferimento a ServiceDescription
L'*albero di descrizione* è la gerarchia di tipi, che iniziano dall'oggetto <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=fullName>, che descrivono ogni aspetto di un servizio.[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilizza un albero di descrizione per compilare un runtime di servizio valido, per pubblicare Web Services Description Language \(WSDL\), XML Schema Definition Language \(XSD\) e asserzioni di criteri \(metadati\) sul servizio che i client possono utilizzare per connettersi al servizio e utilizzarlo, nonché per generare varie rappresentazioni di codici e di file di configurazione dei valori dell'albero di descrizione.  
  
 In questo argomento viene illustrato come le proprietà relative al contratto vengono ottenute dal contratto di servizio e come vengono implementate e aggiunte alla struttura di descrizione.In alcuni casi, i valori dell'attributo vengono convertiti in proprietà di comportamento e il comportamento viene quindi inserito nell'albero di descrizione.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] su come i valori della struttura di descrizione vengono convertiti in metadati, vedere [ServiceDescription e riferimento a WSDL](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md).  
  
## Operazioni di mapping alla struttura di descrizione  
 Nelle applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], i contratti di servizio vengono modellati da interfacce \(o classi\) che utilizzano attributi per contrassegnare l'interfaccia o la classe e i relativi metodi come raggruppamento di operazioni.Quando una classe <xref:System.ServiceModel.ServiceHost> viene aperta, eventuali implementazioni e contratti di servizio vengono analizzati e vengono uniti alle informazioni di configurazione in una struttura di descrizione.  
  
 Esistono due tipi di modelli dell'operazione: il modello *parametro* e il modello *contratto di messaggio*.Il modello parametro utilizza metodi gestiti che non dispongono di un parametro o di un tipo di valore restituito contrassegnato dalla classe <xref:System.ServiceModel.MessageContractAttribute?displayProperty=fullName>.In questo modello gli sviluppatori controllano la serializzazione di parametri e di valori restituiti ma [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera i valori utilizzati per popolare la struttura di descrizione per il servizio e il relativo contratto.  
  
 Le associazioni specificate nei file di configurazione vengono caricate direttamente nella proprietà <xref:System.ServiceModel.Description.ServiceEndpoint.Binding%2A?displayProperty=fullName>.  
  
|Proprietà ServiceBehaviorAttribute|Valore della struttura di descrizione interessato|  
|----------------------------------------|-------------------------------------------------------|  
|Name|<xref:System.ServiceModel.Description.ServiceDescription.Name%2A>|  
|Namespace|<xref:System.ServiceModel.Description.ServiceDescription.Namespace%2A>|  
|ConfigurationName|<xref:System.ServiceModel.Description.ServiceDescription.ConfigurationName%2A>|  
|IgnoreExtensionDataObject|Imposta la proprietà <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.IgnoreExtensionDataObject%2A> per tutte le operazioni.|  
|MaxItemsInObjectGraph|Imposta la proprietà <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.MaxItemsInObjectGraph%2A> per tutte le operazioni.|  
  
|Proprietà ServiceContractAttribute|Valore della struttura di descrizione interessato|  
|----------------------------------------|-------------------------------------------------------|  
|CallbackContract|<xref:System.ServiceModel.Description.ContractDescription.CallbackContractType%2A>, <xref:System.ServiceModel.Description.MessageDescription> aggiunti a tutte le operazioni <xref:System.ServiceModel.Description.OperationDescription.Messages%2A>.|  
|ConfigurationName|<xref:System.ServiceModel.Description.ContractDescription.ConfigurationName%2A>|  
|ProtectionLevel|Proprietà <xref:System.ServiceModel.Description.ContractDescription.ProtectionLevel%2A> ed eventuali livelli di protezione figlio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] gerarchia del livello di protezione, vedere [Informazioni sul livello di protezione](../../../../docs/framework/wcf/understanding-protection-level.md).|  
|SessionMode|<xref:System.ServiceModel.Description.ContractDescription.SessionMode%2A>|  
  
|Valore ServiceKnownTypesAttribute|Valore della struttura di descrizione interessato|  
|---------------------------------------|-------------------------------------------------------|  
|MethodName|<xref:System.ServiceModel.Description.OperationDescription.KnownTypes%2A>|  
  
|Valore OperationContractAttribute|Valore della struttura di descrizione interessato|  
|---------------------------------------|-------------------------------------------------------|  
|Action|<xref:System.ServiceModel.Description.MessageDescription.Action%2A> per il messaggio di output o di input, a seconda del contratto o del contratto callback.|  
|AsyncPattern|Se true, <xref:System.ServiceModel.Description.OperationDescription.BeginMethod%2A> e <xref:System.ServiceModel.Description.OperationDescription.EndMethod%2A>|  
|IsOneWay|Esegue il mapping a un solo <xref:System.ServiceModel.Description.MessageDescription> in <xref:System.ServiceModel.Description.OperationDescription.Messages%2A>|  
|IsInitiating|<xref:System.ServiceModel.Description.OperationDescription.IsInitiating%2A>|  
|IsTerminating|<xref:System.ServiceModel.Description.OperationDescription.IsTerminating%2A>|  
|Nome|<xref:System.ServiceModel.Description.OperationDescription.Name%2A>|  
|ProtectionLevel|Proprietà <xref:System.ServiceModel.Description.OperationDescription.ProtectionLevel%2A> ed eventuali livelli di protezione figlio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] gerarchia del livello di protezione, vedere [Informazioni sul livello di protezione](../../../../docs/framework/wcf/understanding-protection-level.md).|  
|ReplyAction|<xref:System.ServiceModel.Description.MessageDescription.Action%2A> per il messaggio di output o di input, a seconda del contratto o del contratto callback.|  
  
|Valore FaultContractAttribute|Valore della struttura di descrizione interessato|  
|-----------------------------------|-------------------------------------------------------|  
|Azione|<xref:System.ServiceModel.Description.FaultDescription.Action%2A> a seconda del contratto o del contratto callback.|  
|DetailType|<xref:System.ServiceModel.Description.FaultDescription.DetailType%2A>|  
|Nome|<xref:System.ServiceModel.Description.FaultDescription.Name%2A>|  
|Spazio dei nomi|<xref:System.ServiceModel.Description.FaultDescription.Namespace%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.FaultDescription.ProtectionLevel%2A>|  
  
|Valore DataContractFormatAttribute|Valore della struttura di descrizione interessato|  
|----------------------------------------|-------------------------------------------------------|  
|Use|Il valore <xref:System.ServiceModel.DataContractFormatAttribute.Style%2A> è impostato su <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> per l'operazione.|  
  
|Valore XmlSerializerFormatAttribute|Valore della struttura di descrizione interessato|  
|-----------------------------------------|-------------------------------------------------------|  
|Style|Questa proprietà <xref:System.ServiceModel.XmlSerializerFormatAttribute> è impostata su <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> per l'operazione.|  
|Utilizzo|<xref:System.ServiceModel.XmlSerializerFormatAttribute> è impostato su <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> per l'operazione.|  
  
|Valore TransactionFlowAttribute|Valore della struttura di descrizione interessato|  
|-------------------------------------|-------------------------------------------------------|  
|TransactionFlowOption|<xref:System.ServiceModel.TransactionFlowAttribute> viene aggiunto come comportamento dell'operazione alla proprietà <xref:System.ServiceModel.Description.OperationDescription.Behaviors%2A>.|  
  
|Valore MessageContractAttribute|Valore della struttura di descrizione interessato|  
|-------------------------------------|-------------------------------------------------------|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessageDescription.ProtectionLevel%2A>|  
|WrapperName|<xref:System.ServiceModel.Description.MessageBodyDescription.WrapperName%2A>|  
|WrapperNamespace|<xref:System.ServiceModel.Description.MessageBodyDescription.WrapperNamespace%2A>|  
  
|Valore MessageHeaderAttribute|Valore della struttura di descrizione interessato|  
|-----------------------------------|-------------------------------------------------------|  
|Actor|<xref:System.ServiceModel.Description.MessageHeaderDescription.Actor%2A> per l'intestazione corrispondente in <xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|MustUnderstand|<xref:System.ServiceModel.Description.MessageHeaderDescription.MustUnderstand%2A> per l'intestazione corrispondente in <xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|Nome|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A> per l'intestazione corrispondente in <xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|Spazio dei nomi|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A> per l'intestazione corrispondente in <xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A> per l'intestazione corrispondente in <xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|Relay|<xref:System.ServiceModel.Description.MessageHeaderDescription.Relay%2A> per l'intestazione corrispondente in <xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
  
|Valore MessageBodyMemberAttribute|Valore della struttura di descrizione interessato|  
|---------------------------------------|-------------------------------------------------------|  
|Nome|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A> per la parte corrispondente in <xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|Spazio dei nomi|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A> per la parte corrispondente in <xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|Order|<xref:System.ServiceModel.Description.MessagePartDescription.Index%2A> per la parte corrispondente in <xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A> per la parte corrispondente in <xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
  
|Valore MessageHeaderArrayAttribute|Valore della struttura di descrizione interessato|  
|----------------------------------------|-------------------------------------------------------|  
|Actor|<xref:System.ServiceModel.Description.MessageHeaderDescription.Actor%2A>|  
|MustUnderstand|<xref:System.ServiceModel.Description.MessageHeaderDescription.MustUnderstand%2A>|  
|Nome|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>|  
|Spazio dei nomi|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A>|  
|Relay|<xref:System.ServiceModel.Description.MessageHeaderDescription.Relay%2A>|  
  
|Valore MessagePropertyAttribute|Valore della struttura di descrizione interessato|  
|-------------------------------------|-------------------------------------------------------|  
|Nome|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>|  
  
|Valore MessageParameterAttribute|Valore della struttura di descrizione interessato|  
|--------------------------------------|-------------------------------------------------------|  
|Nome|<xref:System.ServiceModel.Description.MessagePartDescription.name%2A> per la parte corrispondente in <xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] su come i valori della struttura di descrizione vengono convertiti in metadati, vedere [ServiceDescription e riferimento a WSDL](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md).  
  
## Vedere anche  
 [ServiceDescription e riferimento a WSDL](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md)