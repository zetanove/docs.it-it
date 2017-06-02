---
title: "Elaborazione di messaggi ordinata in modalit&#224; di concorrenza singola | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a90f5662-a796-46cd-ae33-30a4072838af
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Elaborazione di messaggi ordinata in modalit&#224; di concorrenza singola
WCF non fornisce alcuna garanzia sull'ordine in cui i messaggi vengono elaborati, a meno che il canale sottostante sia con sessione. Ad esempio, un servizio di WCF che utilizza MsmqInputChannel, che non è un canale con sessione, non riuscirà a elaborare i messaggi in ordine. Esistono alcune condizioni in cui uno sviluppatore desidera il comportamento di elaborazione in ordine, ma non desidera utilizzare sessioni.In questo argomento viene descritto come configurare questo comportamento quando un servizio è in esecuzione in modalità di concorrenza singola.  
  
## Elaborazione di messaggi in ordine  
 All'oggetto  <xref:System.ServiceModel.ServiceBehaviorAttribute> è stata aggiunto un nuovo attributo denominato <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A>.Quando la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> è impostata su True e la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> è impostata sul campo <xref:System.ServiceModel.ConcurrencyMode>, i messaggi inviati al servizio verranno elaborati in ordine.Nel frammento di codice seguente viene illustrato come impostare questi attributi.  
  
```  
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, EnsureOrderedDispatch = true )]  
    class Service : IService  
    {  
         // ...  
    }  
  
```  
  
 Se la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> è impostata su qualsiasi altro valore, viene generata un'eccezione <xref:System.InvalidOperationException>.  
  
## Vedere anche  
 [Sessioni, istanze e concorrenza](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)   
 [Concorrenza](../../../../docs/framework/wcf/samples/concurrency.md)