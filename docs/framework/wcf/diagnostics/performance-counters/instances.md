---
title: "Istanze | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8cf3460-0ca1-4411-8262-e9ecaf7f0a31
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Istanze
Nome contatore: istanze.  
  
## Descrizione  
 Numero di contesti di istanza attualmente contenuti dal servizio.  
  
 In genere, il numero di contesti di istanza è identico al numero di istanze.  Tuttavia, gli scenari seguenti rappresenta un'eccezione a questa regola.  
  
-   Un metodo di servizio chiama il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A> in modo esplicito.  
  
-   Viene applicata un'enumerazione <xref:System.ServiceModel.ReleaseInstanceMode> a un'istanza di <xref:System.ServiceModel.OperationBehaviorAttribute>.  
  
## Vedere anche  
 <xref:System.ServiceModel.OperationBehaviorAttribute>