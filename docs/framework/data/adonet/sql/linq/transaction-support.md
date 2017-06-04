---
title: "Supporto di transazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8cceb26e-8d36-4365-8967-58e2e89e0187
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Supporto di transazioni
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono supportati tre modelli di transazione distinti.  Di seguito sono elencati tali modelli nell'ordine di esecuzione dei controlli.  
  
## Transazione locale esplicita  
 Quando si chiama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, se la proprietà <xref:System.Data.Linq.DataContext.Transaction%2A> è impostata su una transazione \(`IDbTransaction`\), la chiamata <xref:System.Data.Linq.DataContext.SubmitChanges%2A> viene eseguita nel contesto della stessa transazione.  
  
 È compito del programmatore eseguire il commit o il rollback della transazione dopo che ne è stata completata l'esecuzione.  La connessione corrispondente alla transazione deve essere la stessa usata per costruire <xref:System.Data.Linq.DataContext>.  Se si usa una connessione diversa, viene generata un'eccezione.  
  
## Transazione distribuibile esplicita  
 È possibile chiamare le API [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] \(incluso, senza limitazione, l'oggetto <xref:System.Data.Linq.DataContext.SubmitChanges%2A>\) nell'ambito di un oggetto <xref:System.Transactions.Transaction> attivo.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] rileva che la chiamata si trova nell'ambito di una transazione e non ne crea una nuova.  Inoltre, in questo caso, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] la connessione non viene chiusa.  Nel contesto di tale transazione è possibile eseguire query ed esecuzioni di <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  
  
## Transazione implicita  
 Quando si chiama l'oggetto <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene controllato se la chiamata si trova nell'ambito di una transazione <xref:System.Transactions.Transaction> o se la proprietà `Transaction` \(`IDbTransaction`\) è impostata su una transazione locale avviata dall'utente.  Se non viene trovata alcuna transazione, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene avviata una transazione locale \(`IDbTransaction`\) che verrà usata per eseguire i comandi SQL generati.  Dopo aver completato correttamente l'esecuzione di tutti i comandi SQL, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene eseguito il commit della transazione locale e restituito un valore.  
  
## Vedere anche  
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [Procedura: raggruppare gli invii dei dati mediante le transazioni](../../../../../../docs/framework/data/adonet/sql/linq/how-to-bracket-data-submissions-by-using-transactions.md)