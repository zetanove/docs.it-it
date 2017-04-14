---
title: "Contratti dati compatibili con versioni successive | Microsoft Docs"
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
helpviewer_keywords: 
  - "contratti dati [WCF], compatibilità con versioni successive"
ms.assetid: 413c9044-26f8-4ecb-968c-18495ea52cd9
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Contratti dati compatibili con versioni successive
Una caratteristica del sistema di contratti dati di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consiste nel fatto che i contratti possono evolversi nel tempo in modo da non determinare interruzioni.Ovvero, un client con una versione precedente di un contratto dati può comunicare con un servizio dotato di una versione più recente dello stesso contratto dati, oppure un client con una versione più recente di un contratto dati può comunicare con un client dotato di una versione precedente dello stesso contratto dati.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedure consigliate: controllo delle versioni del contratto dati](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md).  
  
 È possibile applicare, in base alle esigenze, la maggior parte delle funzionalità di controllo delle versioni quando vengono create versioni nuove di un contratto dati esistente.Per funzionare correttamente, tuttavia, la funzionalità di controllo delle versioni *sequenza di andata e ritorno* deve essere generata nel tipo della prima versione.  
  
## Sequenze di andata e ritorno  
 Le sequenze di andata e ritorno si verificano quando i dati passano da una versione nuova a una versione precedente e di nuovo alla versione nuova di un contratto dati.Le sequenze di andata e ritorno garantiscono che non vi sarà perdita di dati.L'attivazione delle sequenze di andata e ritorno rende il tipo compatibile con versioni successive con eventuali modifiche future supportate dal modello di controllo delle versioni del contratto dati.  
  
 Per consentire sequenze di andata e ritorno per un particolare tipo, quest'ultimo deve implementare l'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject>.L'interfaccia contiene una proprietà, <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>, che restituisce il tipo <xref:System.Runtime.Serialization.ExtensionDataObject>.La proprietà archivia qualsiasi dato da versioni future del contratto dati che è sconosciuto alla versione corrente.  
  
### Esempio  
 Il contratto dati seguente non è compatibile con modifiche future.  
  
 [!code-csharp[C_DataContract#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#7)]
 [!code-vb[C_DataContract#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#7)]  
  
 Per rendere il tipo compatibile con le modifiche future, ad esempio l'aggiunta di un nuovo membro dati denominato "phoneNumber", implementare l'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject>.  
  
 [!code-csharp[C_DataContract#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#8)]
 [!code-vb[C_DataContract#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#8)]  
  
 Quando l'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rileva dati che non fanno parte del contratto dati originale, questi vengono archiviati nella proprietà e conservati.Tali dati non vengono elaborati in nessun altro modo a parte l'archiviazione temporanea.Se l'oggetto viene restituito di nuovo all'origine, anche i dati originali \(sconosciuti\) vengono restituiti.I dati, pertanto, hanno eseguito sequenze di andata e ritorno dall'endpoint di origine senza perdite.Si noti che se l'endpoint di origine, tuttavia, ha richiesto l'elaborazione dei dati, questa aspettativa rimane insoddisfatta e l'endpoint deve in qualche modo rilevare e accogliere la modifica.  
  
 Il tipo <xref:System.Runtime.Serialization.ExtensionDataObject> non contiene metodi o proprietà pubblici.Di conseguenza, è impossibile ottenere accesso diretto ai dati archiviati all'interno della proprietà <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>.  
  
 La funzionalità delle sequenze di andata e ritorno può essere disattivata, impostando `ignoreExtensionDataObject` su `true` nel costruttore <xref:System.Runtime.Serialization.DataContractSerializer> o impostando la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> su `true` in <xref:System.ServiceModel.ServiceBehaviorAttribute>.Quando questa funzionalità è disattivata, il deserializzatore non popolerà la proprietà <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> e il serializzatore non creerà il contenuto della proprietà.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.IExtensibleDataObject>   
 <xref:System.Runtime.Serialization.ExtensionDataObject>   
 [Controllo delle versioni dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)   
 [Procedure consigliate: controllo delle versioni del contratto dati](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)