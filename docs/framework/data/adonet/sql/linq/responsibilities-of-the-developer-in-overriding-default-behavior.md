---
title: "Responsabilit&#224; dello sviluppatore nell&#39;eseguire l&#39;override del comportamento predefinito | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6909ddd-e053-46a8-980c-0e12a9797be1
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Responsabilit&#224; dello sviluppatore nell&#39;eseguire l&#39;override del comportamento predefinito
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non vengono applicati i requisiti seguenti, tuttavia il comportamento sarà indefinito se tali requisiti non vengono soddisfatti.  
  
-   Il metodo di override non deve chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A> o <xref:System.Data.Linq.Table%601.Attach%2A>.  Se questi metodi vengono chiamati in un metodo di override, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] genera un'eccezione.  
  
-   Non è possibile usare i metodi di override per avviare, eseguire il commit o interrompere una transazione.  L'operazione <xref:System.Data.Linq.DataContext.SubmitChanges%2A> viene eseguita in una transazione.  Una transazione annidata interna può interferire con la transazione esterna.  I metodi di override del caricamento possono avviare una transazione solo dopo avere determinano che l'operazione non viene eseguita in <xref:System.Transactions.Transaction>.  
  
-   È previsto che i metodi di override seguano il mapping di concorrenza ottimistica applicabile.  Il metodo di override dovrebbe generare un'eccezione <xref:System.Data.Linq.ChangeConflictException> quando si verifica un conflitto di concorrenza ottimistica.  Questa eccezione viene rilevata da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in modo da consentire la corretta elaborazione dell'opzione <xref:System.Data.Linq.DataContext.SubmitChanges%2A> disponibile in <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  
  
-   I metodi di creazione \(`Insert`\) e di override `Update` dovrebbero trasferire di nuovo i valori per le colonne generate dal database ai corrispondenti membri dell'oggetto quando l'operazione viene completata correttamente.  
  
     Ad esempio, se viene eseguito il mapping di `Order.OrderID` a una colonna di identità \(chiave primaria di *incremento automatico*\), il metodo di override `InsertOrder()` dovrà recuperare l'ID generato dal database e impostare il membro `Order.OrderID` su ID.  In modo analogo i membri del timestamp dovranno essere aggiornati in base ai valori di timestamp generati dal database per assicurarsi che gli oggetti aggiornati sono coerenti.  La mancata propagazione dei valori generati dal database potrebbe comportare un'incoerenza tra il database e gli oggetti registrati da <xref:System.Data.Linq.DataContext>.  
  
-   È compito dell'utente richiamare l'API dinamica corretta.  Ad esempio, nel metodo di override dell'aggiornamento è possibile chiamare solo <xref:System.Data.Linq.DataContext.ExecuteDynamicUpdate%2A>.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non rileva né verifica se il metodo dinamico richiamato corrisponde all'operazione applicabile.  Se viene chiamato un metodo non applicabile, ad esempio <xref:System.Data.Linq.DataContext.ExecuteDynamicDelete%2A> per un oggetto da aggiornare, i risultati sono indefiniti.  
  
-   Infine, il metodo di override dovrebbe eseguire l'operazione specificata.  La semantica delle operazioni [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], ad esempio il caricamento eager, il caricamento posticipato e il metodo <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, richiedono la fornitura del servizio specificato da parte degli override. Ad esempio, un override di caricamento che restituisce solo una raccolta vuota, senza controllare il contenuto nel database, causerà probabilmente la restituzione di dati incoerenti.  
  
## Vedere anche  
 [Personalizzazione delle operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)