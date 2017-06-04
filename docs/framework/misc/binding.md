---
title: "&lt;associazione&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 666183d6-4d1f-45c7-ac64-bdf93ee8f36f
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;associazione&gt;
È possibile usare l'elemento di `binding` per configurare differenti tipi di associazione predefiniti forniti da Windows Communication Foundation \(WCF\).  
  
## Binding fornito dal sistema  
 Le associazioni fornite dal sistema nascondono la complessità dello stack di messaggistica WCF.  Le applicazioni che usano associazioni fornite dal sistema non richiedono il controllo completo sullo stack.  Gli attributi esposti in ciascuna associazione fornita dal sistema sono quelli più appropriati per lo scenario di utilizzo gestito dall'associazione.  
  
 La sezione di configurazione di ciascuna associazione fornita dal sistema può definire varie configurazioni usate per configurare l'associazione.  Ogni configurazione è identificata da un nome univoco.  
  
 Non è possibile aggiungere elementi o attributi a un'associazione fornita dal sistema.  A tal scopo, è necessario implementare un'associazione personalizzata come descritto nella sezione "Associazione personalizzata" di questo argomento.  È possibile definire un'associazione personalizzata che riproduce perfettamente un'associazione fornita dal sistema e aggiunge alcune impostazioni sulle quali è desiderabile che l'applicazione utente abbia il controllo.  
  
## Associazione personalizzata  
 Le associazioni personalizzate forniscono il controllo completo dello stack dei messaggi WCF.  Un'associazione singola definisce lo stack dei messaggi specificando gli elementi di configurazione per gli elementi dello stack nell'ordine in cui vengono visualizzati nello stack.  Ogni elemento definisce e configura un elemento dello stack.  In ogni associazione personalizzata deve essere presente un solo elemento `transport`.  Senza questo elemento, lo stack dei messaggi è incompleto.  
  
 L'ordine in cui gli elementi vengono visualizzati nello stack è importante, perché è l'ordine in cui le operazioni vengono applicate al messaggio.  L'ordine consigliato per gli elementi dello stack è il seguente:  
  
1.  Transazioni \(facoltativo\)  
  
2.  Messaggistica affidabile \(facoltativo\)  
  
3.  Sicurezza \(facoltativo\)  
  
4.  Codificatore  
  
5.  Trasporto  
  
 Le associazioni personalizzate sono identificate dal relativo attributo `name`.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.BindingsSection>   
 <xref:System.ServiceModel.Channels.Binding>   
 <xref:System.ServiceModel.Channels.BindingElement>   
 [Associazioni](../../../docs/framework/wcf/bindings.md)   
 [Associazioni personalizzate](../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)