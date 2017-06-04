---
title: "Confronto di transazioni in COM+ e ServiceModel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e493bcdd-b91a-4486-853f-83dbcd1931b7
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Confronto di transazioni in COM+ e ServiceModel
In questo argomento viene illustrato come simulare il comportamento di un servizio COM\+ transazionale usando gli attributi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] forniti dallo spazio dei nomi <xref:System.ServiceModel>.  
  
## Emulazione di COM\+ mediante attributi ServiceModel  
 Nella tabella seguente viene confrontata l'enumerazione <xref:System.EnterpriseServices.TransactionOption> usata per creare una transazione `EnterpriseServices` e la modalità di correlazione agli attributi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] forniti dallo spazio dei nomi <xref:System.ServiceModel>.  
  
|Attributo COM\+|Attributi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]|  
|---------------------|-----------------------------------------------------------------------|  
|RequiresNew|<xref:System.ServiceModel.TransactionFlowAttribute> è impostato su <xref:System.ServiceModel.TransactionFlowOption>.<br /><br /> <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> è `true`.<br /><br /> L'attributo `TransactionFlow` nell'elemento di associazione è `false`.|  
|Obbligatorio|<xref:System.ServiceModel.TransactionFlowAttribute> è impostato su <xref:System.ServiceModel.TransactionFlowOption>.<br /><br /> <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> è `true`.<br /><br /> L'attributo `TransactionFlow` nell'elemento di associazione è `true`.|  
|Supportato|Non esiste alcun equivalente diretto.  In generale, è necessario adottare il comportamento specificato per `Required`.|  
|NotSupported|<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> è `false`.<br /><br /> L'attributo `TransactionFlow` nell'elemento di associazione è `false`.|  
|Disabled|Non esiste alcun equivalente diretto.  In generale, è necessario adottare il comportamento specificato per `NotSupported`.|