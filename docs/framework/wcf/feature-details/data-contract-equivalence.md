---
title: "Equivalenza dei contratti dati | Microsoft Docs"
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
  - "contratti dati [WCF], equivalenza"
ms.assetid: f06f3c7e-c235-4ec1-b200-68142edf1ed1
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Equivalenza dei contratti dati
Perché un client possa inviare correttamente dati di un certo tipo a un servizio o perché un servizio possa inviare correttamente dati a un client, non è necessario che il tipo inviato sia presente nell'estremità ricevente.  L'unico requisito è che i contratti dati di entrambi i tipi siano equivalenti.  In alcuni casi non è necessaria la stretta equivalenza, come descritto in [Controllo delle versioni dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md).  
  
 Perché i contratti dati siano equivalenti devono avere lo stesso spazio dei nomi e lo stesso nome.  Ogni membro dati su uno lato deve inoltre avere un membro dati equivalente sull'altro lato.  
  
 Perché i membri dati siano equivalenti devono avere lo stesso nome.  Devono inoltre rappresentare lo stesso tipo di dati, che significa che i rispettivi contratti dati devono essere equivalenti.  
  
> [!NOTE]
>  Sia per i nomi e gli spazi dei nomi dei contratti dati sia per i nomi dei membri dati viene fatta distinzione tra maiuscole e minuscole.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sui nomi e gli spazi dei nomi dei contratti dati, nonché sui nomi dei membri dati, vedere [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md).  
  
 Se sullo stesso lato \(mittente o ricevitore\) sono presenti due tipi e i contratti dati non sono equivalenti \(ad esempio, hanno membri dati diversi\), è necessario assegnare loro un nome e uno spazio dei nomi differenti.  In caso contrario, è possibile che vengano generate eccezioni.  
  
 I contratti dati per i tipi seguenti sono equivalenti:  
  
 [!code-csharp[C_DataContractNames#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#5)]
 [!code-vb[C_DataContractNames#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#5)]  
  
## Ordine dei membri dati ed equivalenza dei contratti dati  
 L'utilizzo della proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> della classe <xref:System.Runtime.Serialization.DataMemberAttribute> può influire sull'equivalenza dei contratti dati.  Per essere equivalenti, i contratti dati devono avere membri disposti nello stesso ordine.  L'ordine predefinito è quello alfabetico.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Ordine dei membri dati](../../../../docs/framework/wcf/feature-details/data-member-order.md).  
  
 Il codice seguente, ad esempio, comporta contratti dati equivalenti.  
  
 [!code-csharp[C_DataContractNames#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#6)]
 [!code-vb[C_DataContractNames#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#6)]  
  
 Il codice seguente non comporta invece contratti dati equivalenti.  
  
 [!code-csharp[C_DataContractNames#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#7)]
 [!code-vb[C_DataContractNames#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#7)]  
  
## Ereditarietà, interfacce ed equivalenza dei contratti dati  
 Quando viene determinata l'equivalenza, un contratto dati che eredita da un altro contratto dati viene trattato come se fosse un contratto dati che include tutti i membri dati del tipo di base.  Tenere presente che l'ordine dei membri dati deve corrispondere e che i membri del tipo di base precedono nell'ordine i membri del tipo derivato.  Inoltre, se due membri dati hanno lo stesso valore di ordine, come nell'esempio di codice seguente, l'ordinamento di questi membri dati è alfabetico.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Ordine dei membri dati](../../../../docs/framework/wcf/feature-details/data-member-order.md).  
  
 Nell'esempio seguente il contratto dati per il tipo `Employee` è equivalente al contratto dati per il tipo `Worker`.  
  
 [!code-csharp[C_DataContractNames#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#8)]
 [!code-vb[C_DataContractNames#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#8)]  
  
 Quando vengono passati parametri e restituiti valori tra un client e un servizio, non è possibile inviare un contratto dati relativo a una classe di base se l'endpoint ricevente prevede un contratto dati relativo a una classe derivata.  Questo comportamento è conforme ai principi di base della programmazione orientata a oggetti.  Nell'esempio precedente non è possibile inviare un oggetto di tipo `Person` se è previsto un oggetto di tipo `Employee` .  
  
 Un contratto dati relativo a una classe derivata può essere inviato quando è previsto un contratto dati relativo a una classe di base soltanto se l'endpoint ricevente "riconosce" il tipo derivato usando la classe <xref:System.Runtime.Serialization.KnownTypeAttribute>.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  Nell'esempio precedente un oggetto di tipo `Employee` può essere inviato se è previsto un oggetto di tipo `Person`, ma solo se il codice del ricevitore usa la classe <xref:System.Runtime.Serialization.KnownTypeAttribute> per includerlo nell'elenco dei tipi noti.  
  
 Quando vengono passati parametri e restituiti valori tra applicazioni, se il tipo previsto è un'interfaccia è come se fosse di tipo <xref:System.Object>.  Poiché ogni tipo deriva in fondo da <xref:System.Object>, ogni contratto dati deriva in ultima istanza dal contratto dati relativo a <xref:System.Object>.  Quando è prevista un'interfaccia è pertanto possibile passare qualsiasi tipo di contratto dati.  Per usare correttamente le interfacce sono necessari ulteriori passaggi. Per altre informazioni, vedere [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 [Ordine dei membri dati](../../../../docs/framework/wcf/feature-details/data-member-order.md)   
 [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [Nomi di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-names.md)