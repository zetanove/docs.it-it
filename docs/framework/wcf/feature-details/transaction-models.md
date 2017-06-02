---
title: "Modelli di transazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 48a8bc1b-128b-4cf1-a421-8cc73223c340
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Modelli di transazione
In questo argomento viene descritta la relazione tra i modelli di programmazione della transazione e i componenti dell'infrastruttura forniti da Microsoft.  
  
 Quando si utilizzano transazioni in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], è importante comprendere che non si sta selezionando tra modelli transazionali differenti ma piuttosto si sta operando a livelli differenti di un modello integrato e coerente.  
  
 Nelle sezioni seguenti vengono descritti i tre componenti primari della transazione.  
  
## Transazioni Windows Communication Foundation  
 Il supporto delle transazioni in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di scrivere servizi transazionali.Le applicazioni inoltre, con il supporto per il protocollo WS\-AtomicTransaction \(WS\-AT\), possono propagare transazioni a servizi Web generati tramite [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] o tecnologia di terze parti.  
  
 In un servizio o in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], le funzionalità delle transazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] forniscono attributi e configurazione per specificare in modo dichiarativo come e quando l'infrastruttura deve creare, propagare e sincronizzare transazioni.  
  
## Transazioni System.Transactions  
 Lo spazio dei nomi <xref:System.Transactions> fornisce sia un modello di programmazione esplicito basato sulla classe <xref:System.Transactions.Transaction> sia un modello di programmazione implicito che utilizza la classe <xref:System.Transactions.TransactionScope>, in cui le transazioni vengono gestite automaticamente dall'infrastruttura.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] su come creare un'applicazione transazionale utilizzando questi due modelli, vedere l'articolo sulla [scrittura di un'applicazione transazionale](http://go.microsoft.com/fwlink/?LinkId=94947) \(la pagina potrebbe essere in inglese\).  
  
 In un servizio o in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], <xref:System.Transactions> fornisce il modello di programmazione per la creazione di transazioni all'interno di un'applicazione client e per l'interazione esplicita con una transazione, se necessario, all'interno di un servizio.  
  
## Transazioni MSDTC  
 MSDTC \(Microsoft Distributed Transaction Coordinator\) è un gestore transazioni che fornisce supporto per transazioni distribuite.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'articolo sui [riferimenti del programmatore DTC](http://go.microsoft.com/fwlink/?LinkId=94948) \(la pagina potrebbe essere in inglese\).  
  
 In un servizio o in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], MSDTC fornisce l'infrastruttura per il coordinamento di transazioni create all'interno di un client o di un servizio.