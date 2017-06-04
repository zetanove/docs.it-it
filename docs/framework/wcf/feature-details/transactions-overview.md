---
title: "Panoramica sulle transazioni di Windows Communication Foundation | Microsoft Docs"
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
  - "transazioni [WCF]"
  - "WCF, transazioni"
  - "Windows Communication Foundation, transazioni"
ms.assetid: c7757854-1207-4019-8b31-552578b7d570
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Panoramica sulle transazioni di Windows Communication Foundation
Le transazioni consentono di radunare un set di azioni o operazioni in un'unica unità di esecuzione indivisibile.  Una transazione è una raccolta di operazioni con le proprietà seguenti:  
  
-   Atomicità.  Questo aspetto assicura che tutti gli aggiornamenti completati in una transazione specifica vengano sottoposti a commit e resi durevoli oppure vengono tutti interrotti e sottoposti a rollback allo stato precedente.  
  
-   Coerenza.  Questa caratteristica garantisce che le modifiche eseguita in una transazione rappresentano una trasformazione da uno stato coerente a un altro.  Ad esempio, una transazione che trasferisce denaro da un conto corrente a un conto di risparmio non modifica il quantità di denaro nel conto generale.  
  
-   Isolamento.  Questo aspetto impedisce a una transazione di applicare modifiche di cui non è stato eseguito il commit ad altre transazioni simultanee.  L'isolamento garantisce l'astrazione della concorrenza mentre assicura che una transazione non abbia un impatto imprevisto sull'esecuzione di un'altra transazione.  
  
-   Durabilità.  Implica che, quando è stato eseguito il commit, gli aggiornamenti alle risorse gestite \(ad esempio un record di database\) verranno resi persistenti rispetto agli errori.  
  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce un vasta gamma di funzionalità che consentono di creare transazioni distribuite nell'applicazione di servizio Web.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa il supporto per il protocollo WS\-AtomicTransaction \(WS\-AT\) che consente alle applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di propagare transazioni alle applicazioni interoperative, ad esempio i servizi Web interoperativi creati usando tecnologia di terze parti.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa anche il supporto per il protocollo delle transazioni OLE che può essere usato negli scenari in cui non è necessaria la funzionalità di interoperabilità per abilitare il flusso delle transazioni.  
  
 È possibile usare un file di configurazione dell'applicazione per configurare associazioni che abilitano o disabilitano il flusso delle transazioni, nonché impostare il protocollo delle transazioni desiderato su un'associazione.  È inoltre possibile impostare timeout delle transazioni a livello di servizio usando il file di configurazione.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Attivazione del flusso delle transazioni](../../../../docs/framework/wcf/feature-details/enabling-transaction-flow.md).  
  
 Gli attributi delle transazioni nello spazio dei nomi <xref:System.ServiceModel> consentono di eseguire le operazioni seguenti:  
  
-   Configurare timeout delle transazioni e filtri a livello di isolamento usando l'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute>.  
  
-   Abilitare la funzionalità delle transazioni e configurare il comportamento di completamento delle transazioni usando l'attributo <xref:System.ServiceModel.OperationBehaviorAttribute>.  
  
-   Usare gli attributi <xref:System.ServiceModel.ServiceContractAttribute> e <xref:System.ServiceModel.OperationContractAttribute> su un metodo del contratto per richiedere, consentire o negare il flusso delle transazioni.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Attributi della transazione di ServiceModel](../../../../docs/framework/wcf/feature-details/servicemodel-transaction-attributes.md).  
  
## Vedere anche  
 [Attributi della transazione di ServiceModel](../../../../docs/framework/wcf/feature-details/servicemodel-transaction-attributes.md)   
 [Attivazione del flusso delle transazioni](../../../../docs/framework/wcf/feature-details/enabling-transaction-flow.md)