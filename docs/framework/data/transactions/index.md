---
title: "Elaborazione della transazione  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: effdc8e6-accf-41eb-98a5-431603ba218b
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Elaborazione della transazione 
Quando si acquista un libro da una libreria online si offre denaro \(tramite carta di credito\) in cambio di un libro.Se la carta di credito è valida, una serie di operazioni correlate garantisce che l'acquirente riceva il libro e che la libreria riceva il denaro.Se tuttavia durante lo scambio si verifica un errore in una delle operazioni della serie, l'intero scambio ha esito negativo.L'acquirente non riceve il libro e la libreria non riceve il denaro.  
  
 La tecnologia responsabile dell'equità e della prevedibilità dello scambio è detta elaborazione delle transazioni.Le transazioni garantiscono che le risorse orientate ai dati vengano aggiornate in via definitiva solo dopo che tutte le operazioni all'interno dell'unità transazionale siano state completate correttamente.La combinazione di un set di operazioni correlate in un'unità in cui tutte le operazioni hanno lo stesso esito, sia esso positivo o negativo, consente di semplificare il ripristino in caso di errore e di rendere l'applicazione più affidabile.  
  
 I sistemi di elaborazione delle transazioni si basano sull'hosting in componenti hardware e software di un'applicazione orientata alle transazioni che esegue le transazioni di routine necessarie allo svolgimento di attività aziendali.Alcuni esempi di tale applicazione sono i sistemi che gestiscono la registrazione degli ordini di vendita, la prenotazione di biglietti aerei, le retribuzioni, i record degli impiegati, la lavorazione e la spedizione di merci.  
  
 Questa sezione fornisce sia informazioni di carattere generale sull'elaborazione delle transazioni sia informazioni specifiche su come scrivere applicazioni transazionali e gestori di risorse tramite Microsoft .NET Framework.  
  
## In questa sezione  
 [Transaction Fundamentals](http://msdn.microsoft.com/it-it/2a476b63-b94f-443f-992d-53943fdf4e5d)  
 Introduce i termini e in concetti fondamentali relativi all'elaborazione delle transazioni.  
  
 [Funzionalità Fornite da System.Transactions ](../../../../docs/framework/data/transactions/features-provided-by-system-transactions.md)  
 Descrive come utilizzare le funzionalità di System.Transactions per scrivere un'applicazione transazionale personalizzata.  
  
## Riferimenti  
 <xref:System.Transactions>  
 Fornisce le classi che consentono al codice di partecipare alle transazioni.Tali classi supportano le transazioni con più partecipanti distribuiti, le notifiche a fase multipla e le integrazioni durevoli.  
  
## Sezioni correlate