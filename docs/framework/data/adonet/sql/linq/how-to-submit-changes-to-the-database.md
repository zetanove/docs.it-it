---
title: "Procedura: inviare le modifiche al database | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: inviare le modifiche al database
Indipendentemente da quante modifiche si apportano agli oggetti, queste vengono applicate solo alle repliche in memoria.  Le modifiche non vengono apportate ai dati effettivi nel database  e non saranno trasmesse al server finché non si chiama in modo esplicito <xref:System.Data.Linq.DataContext.SubmitChanges%2A> su <xref:System.Data.Linq.DataContext>.  
  
 Quando si effettua questa chiamata, <xref:System.Data.Linq.DataContext> tenta di convertire le modifiche in comandi SQL equivalenti.  È possibile usare logica personalizzata per eseguire l'override di queste azioni, tuttavia l'ordine di invio viene gestito da un servizio di <xref:System.Data.Linq.DataContext> detto *processore delle modifiche*.  Di seguito viene riportata la sequenza degli eventi:  
  
1.  Quando si chiama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] esamina il set di oggetti conosciuti per determinare se a tali oggetti sono state associate nuove istanze.  In caso affermativo, queste nuove istanze vengono aggiunte al set di oggetti registrati.  
  
2.  Tutti gli oggetti con modifiche in sospeso vengono ordinati in una sequenza di oggetti in base alle reciproche dipendenze.  Gli oggetti le cui modifiche dipendono da altri oggetti vengono ordinati in sequenza dopo le relative dipendenze.  
  
3.  Immediatamente prima della trasmissione di una qualsiasi modifica effettiva, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] avvia una transazione per incapsulare la serie di singoli comandi.  
  
4.  Le modifiche agli oggetti vengono convertite una alla volta in comandi SQL e inviate al server.  
  
 Qualsiasi errore rilevato dal database in questa fase causa l'interruzione del processo di invio e la generazione di un'eccezione.  Viene eseguito il rollback di tutte le modifiche al database come se non fosse mai stato eseguito alcun invio.  In <xref:System.Data.Linq.DataContext> è tuttavia ancora presente una registrazione completa di tutte le modifiche,  pertanto è possibile tentare di correggere il problema e chiamare nuovamente <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, come nell'esempio di codice che segue.  
  
## Esempio  
 Quando la transazione relativa alla sottomissione viene completata correttamente, <xref:System.Data.Linq.DataContext> accetta le modifiche agli oggetti ignorando le informazioni di rilevamento delle modifiche.  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## Vedere anche  
 [Procedura: rilevare e risolvere gli invii in conflitto](../../../../../../docs/framework/data/adonet/sql/linq/how-to-detect-and-resolve-conflicting-submissions.md)   
 [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)   
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [Scrittura e invio di modifiche di dati](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)