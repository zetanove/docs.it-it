---
title: "Procedura: creare un contratto dati di base per una classe o una struttura | Microsoft Docs"
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
  - "contratti dati [WCF], creazione per una classe o una struttura"
  - "Classe DataContractAttribute"
  - "DataMemberAttribute"
ms.assetid: bc464889-3070-4a2f-91d2-e788a0f686a7
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Procedura: creare un contratto dati di base per una classe o una struttura
In questo argomento vengono illustrati i passaggi di base per creare un contratto dati usando una classe o una struttura.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]i contratti dati e su come vengono usati, vedere [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md).  
  
 Per un'esercitazione in cui vengono illustrati i passaggi della creazione di un servizio e di un client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] di base, vedere [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md).  Per un'applicazione di esempio funzionante costituita da un servizio di base e un client, vedere [Contratto dati di base](../../../../docs/framework/wcf/samples/basic-data-contract.md).  
  
### Per creare un contratto dati di base per una classe o una struttura  
  
1.  Dichiarare che il tipo è associato a un contratto dati applicando l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> alla classe.  Si noti che tutti i tipi pubblici, inclusi quelli senza attributi, sono serializzabili.  Tramite <xref:System.Runtime.Serialization.DataContractSerializer> viene dedotto un contratto dati se è assente l'attributo <xref:System.Runtime.Serialization.DataContractAttribute>.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)], vedere [Tipi serializzabili](../../../../docs/framework/wcf/feature-details/serializable-types.md).  
  
2.  Definire i membri \(proprietà, campi o eventi\) serializzati applicando l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> a ogni membro.  Questi membri vengono definiti membri dati.  Per impostazione predefinita, tutti i tipi pubblici sono serializzabili.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)], vedere [Tipi serializzabili](../../../../docs/framework/wcf/feature-details/serializable-types.md).  
  
    > [!NOTE]
    >  È possibile applicare l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> ai campi privati, per esporre i dati ad altri utenti.  Assicurarsi che il membro non contenga dati riservati.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come creare un contratto dati per il tipo `Person` applicando gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute> alla classe e ai relativi membri.  
  
 [!code-csharp[DataContractAttribute#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#2)]
 [!code-vb[DataContractAttribute#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#2)]  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md)   
 [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md)