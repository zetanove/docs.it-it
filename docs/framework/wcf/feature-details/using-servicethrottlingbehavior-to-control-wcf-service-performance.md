---
title: "Uso di ServiceThrottlingBehavior per controllare le prestazioni dei servizi WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "comportamento [WCF], le prestazioni del servizio"
ms.assetid: f9dc120c-dc24-49d5-930e-b22f5bc73423
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Uso di ServiceThrottlingBehavior per controllare le prestazioni dei servizi WCF
Il <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> classe espone proprietà che è possibile utilizzare per limitare il numero di istanze o sessioni create a livello di applicazione. Usando questo comportamento è possibile ottimizzare le prestazioni dell'applicazione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## <a name="controlling-service-instances-and-concurrent-calls"></a>Controllo delle istanze di servizio e delle chiamate contemporanee  
 Utilizzare il <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> proprietà per specificare il numero massimo di messaggi elaborati attivamente in un <xref:System.ServiceModel.ServiceHost> (classe) e <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> proprietà per specificare il numero massimo di <xref:System.ServiceModel.InstanceContext> oggetti nel servizio.  
  
 Poiché la determinazione di impostazioni di queste proprietà in genere avviene dopo l'esperienza in scenari reali eseguendo l'applicazione con carichi, le impostazioni per il <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> proprietà è in genere specificato in un file di configurazione dell'applicazione mediante la [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/servicethrottling.md) elemento.  
  
 Esempio di codice seguente viene illustrato l'utilizzo di <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> classe da un file di configurazione che imposta il <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A>, <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>, e <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> proprietà da 1 a scopo di esempio. L'esperienza in scenari reali determina le impostazioni ottimali per qualsiasi applicazione specifica.  
  
 [!code-csharp[ServiceThrottlingBehavior#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/servicethrottlingbehavior/cs/hostapplication.exe.config#3)]  
  
 Il comportamento in fase di esecuzione dipende dai valori di <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> e <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> proprietà, che controllano il numero di messaggi possono essere eseguiti in un'operazione in una sola volta e la durata del servizio <xref:System.ServiceModel.InstanceContext> relativo in ingresso sessioni del canale, rispettivamente.  
  
 Per informazioni dettagliate, vedere <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>, e <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>   
 <xref:System.ServiceModel.NetTcpBinding.MaxConnections%2A>