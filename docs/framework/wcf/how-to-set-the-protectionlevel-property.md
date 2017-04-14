---
title: "Procedura: impostare la propriet&#224; ProtectionLevel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Proprietà ProtectionLevel"
  - "WCF, protezione"
ms.assetid: 3d4e8f80-0f9e-4a26-9899-beb6584e78df
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Procedura: impostare la propriet&#224; ProtectionLevel
È possibile impostare il livello di protezione applicando un attributo appropriato e impostando la proprietà.È possibile impostare la protezione a livello di servizio su tutte le parti di ogni messaggio. In alternativa, è possibile impostare la protezione a livelli granulari in modo crescente, dai metodi alle parti del messaggio.[!INCLUDE[crabout](../../../includes/crabout-md.md)] proprietà `ProtectionLevel`, vedere [Informazioni sul livello di protezione](../../../docs/framework/wcf/understanding-protection-level.md).  
  
> [!NOTE]
>  È possibile impostare i livelli di protezione solo nel codice, non nella configurazione.  
  
### Per firmare tutti i messaggi per un servizio  
  
1.  Creare un'interfaccia per il servizio.  
  
2.  Applicare l'attributo <xref:System.ServiceModel.ServiceContractAttribute> al servizio e impostare la proprietà <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> su <xref:System.Net.Security.ProtectionLevel>, come illustrato nel codice seguente \(il livello predefinito è <xref:System.Net.Security.ProtectionLevel>\).  
  
     [!code-csharp[C_ProtectionLevel#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#1)]
     [!code-vb[C_ProtectionLevel#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#1)]  
  
### Per firmare tutte le parti del messaggio per un'operazione  
  
1.  Creare un'interfaccia per il servizio e applicarvi l'attributo <xref:System.ServiceModel.ServiceContractAttribute>.  
  
2.  Aggiungere una dichiarazione di metodo all'interfaccia.  
  
3.  Applicare l'attributo <xref:System.ServiceModel.OperationContractAttribute> al metodo e impostare la proprietà <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> su <xref:System.Net.Security.ProtectionLevel>, come illustrato nel codice seguente.  
  
     [!code-csharp[C_ProtectionLevel#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#2)]
     [!code-vb[C_ProtectionLevel#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#2)]  
  
## Protezione dei messaggi di errore  
 È possibile inviare le eccezioni generate in un servizio a un client come errori SOAP.[!INCLUDE[crabout](../../../includes/crabout-md.md)] creazione di errori fortemente tipizzati, vedere [Specifica e gestione di errori in contratti e servizi](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md) e [Procedura: dichiarare errori nei contratti di servizio](../../../docs/framework/wcf/how-to-declare-faults-in-service-contracts.md).  
  
#### Per proteggere i messaggi di errore  
  
1.  Creare un tipo che rappresenta il messaggio di errore.Nell'esempio seguente viene creata una classe denominata `MathFault` con due campi.  
  
2.  Applicare l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> al tipo e un attributo <xref:System.Runtime.Serialization.DataMemberAttribute> a ogni campo che deve essere serializzato, come illustrato nel codice seguente.  
  
     [!code-csharp[C_ProtectionLevel#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#3)]
     [!code-vb[C_ProtectionLevel#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#3)]  
  
3.  Nell'interfaccia che restituirà l'errore, applicare l'attributo <xref:System.ServiceModel.FaultContractAttribute> al metodo che restituirà l'errore e impostare il parametro `detailType` sul tipo della classe di errore.  
  
4.  Nel costruttore, inoltre, impostare la proprietà <xref:System.ServiceModel.FaultContractAttribute.ProtectionLevel%2A> su <xref:System.Net.Security.ProtectionLevel>, come illustrato nel codice seguente.  
  
     [!code-csharp[C_ProtectionLevel#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#4)]
     [!code-vb[C_ProtectionLevel#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#4)]  
  
## Protezione delle parti del messaggio  
 Utilizzare un contratto di messaggio per proteggere le parti di un messaggio.[!INCLUDE[crabout](../../../includes/crabout-md.md)] contratti di messaggio, vedere [Utilizzo dei contratti di messaggio](../../../docs/framework/wcf/feature-details/using-message-contracts.md).  
  
#### Per proteggere il corpo del messaggio  
  
1.  Creare un tipo che rappresenta il messaggio.Nell'esempio seguente viene creata una classe `Company` con due campi, `CompanyName` e `CompanyID`.  
  
2.  Applicare l'attributo <xref:System.ServiceModel.MessageContractAttribute> alla classe e impostare la proprietà <xref:System.ServiceModel.MessageContractAttribute.ProtectionLevel%2A> su <xref:System.Net.Security.ProtectionLevel>.  
  
3.  Applicare l'attributo <xref:System.ServiceModel.MessageHeaderAttribute> a un campo che verrà espresso come intestazione del messaggio e impostare la proprietà `ProtectionLevel` su <xref:System.Net.Security.ProtectionLevel>.  
  
4.  Applicare l'elemento <xref:System.ServiceModel.MessageBodyMemberAttribute> a qualsiasi campo che sarà espresso come parte del corpo del messaggio e impostare la proprietà `ProtectionLevel` su <xref:System.Net.Security.ProtectionLevel>, come illustrato nell'esempio seguente.  
  
     [!code-csharp[C_ProtectionLevel#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#5)]
     [!code-vb[C_ProtectionLevel#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#5)]  
  
## Esempio  
 Nell'esempio seguente viene impostata la proprietà `ProtectionLevel` di diverse classi Attribute in varie posizioni di un servizio.  
  
 [!code-csharp[C_ProtectionLevel#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#6)]
 [!code-vb[C_ProtectionLevel#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#6)]  
  
## Compilazione del codice  
 Nel codice seguente vengono illustrati gli spazi dei nomi necessari per compilare il codice di esempio.  
  
 [!code-csharp[C_ProtectionLevel#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#0)]
 [!code-vb[C_ProtectionLevel#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#0)]  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 <xref:System.ServiceModel.FaultContractAttribute>   
 <xref:System.ServiceModel.MessageContractAttribute>   
 <xref:System.ServiceModel.MessageBodyMemberAttribute>   
 [Informazioni sul livello di protezione](../../../docs/framework/wcf/understanding-protection-level.md)