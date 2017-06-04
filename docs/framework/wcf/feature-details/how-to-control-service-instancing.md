---
title: "Procedura: controllare l&#39;istanza del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: e0b12b34-8004-443a-a46d-83a5c00f2601
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Procedura: controllare l&#39;istanza del servizio
L'impostazione della modalità di istanza di un servizio consente di specificare quando vengono creati una classe <xref:System.ServiceModel.InstanceContext?displayProperty=fullName> e il relativo oggetto servizio definito dall'utente associato.  Per un elenco delle modalità possibili, vedere l'enumerazione <xref:System.ServiceModel.InstanceContextMode>.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]i comportamenti, vedere [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  Per alcuni esempi funzionanti, vedere [Comportamenti](../../../../docs/framework/wcf/samples/behaviors.md).  
  
### Per controllare la durata dell'istanza del servizio tramite codice  
  
1.  Applicare la classe <xref:System.ServiceModel.ServiceBehaviorAttribute> alla classe di servizi.  
  
2.  Impostare la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> su uno dei valori seguenti: <xref:System.ServiceModel.InstanceContextMode>, <xref:System.ServiceModel.InstanceContextMode> o <xref:System.ServiceModel.InstanceContextMode>.  
  
     [!code-csharp[C_ControlServiceInstancing#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#1)]
     [!code-vb[C_ControlServiceInstancing#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#1)]  
  
## Esempio  
 Nell'esempio di codice seguente, la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> dell'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute> viene impostata su <xref:System.ServiceModel.InstanceContextMode>.  
  
 [!code-csharp[c_ControlServiceInstancing#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#2)]
 [!code-vb[c_ControlServiceInstancing#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#2)]  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceBehaviorAttribute>   
 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>   
 <xref:System.ServiceModel.InstanceContextMode>   
 [Service: Behaviors Samples](http://msdn.microsoft.com/it-it/4e3c6513-a7ff-4b35-8dcf-b5506c6f39a7)