---
title: "Procedura: specificare quando vengono generate le eccezioni di concorrenza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 344ae068-ff63-4a2e-8b00-af22e143675f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: specificare quando vengono generate le eccezioni di concorrenza
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] un'eccezione <xref:System.Data.Linq.ChangeConflictException> viene generata quando gli oggetti non vengono aggiornati a causa di conflitti di concorrenza ottimistici.  Per altre informazioni, vedere [Cenni preliminari sulla concorrenza ottimistica](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md).  
  
 Prima di inviare le modifiche al database, è possibile specificare quando dovranno essere generate le eccezioni di concorrenza:  
  
-   Generare l'eccezione al primo errore \(<xref:System.Data.Linq.ConflictMode>\).  
  
-   Completare tutti i tentativi di aggiornamento, accumulare tutti gli errori e segnalare gli errori accumulati nell'eccezione \(<xref:System.Data.Linq.ConflictMode>\).  
  
 Quando viene generata, l'eccezione <xref:System.Data.Linq.ChangeConflictException> fornisce l'accesso a una raccolta <xref:System.Data.Linq.ChangeConflictCollection>.  In questa raccolta vengono forniti i dettagli per ogni conflitto \(associato a un unico tentativo di aggiornamento non riuscito\), nonché l'accesso alla raccolta <xref:System.Data.Linq.ObjectChangeConflict.MemberConflicts%2A>.  Per ogni conflitto fra membri viene eseguito il mapping a un unico membro nell'aggiornamento che non ha superato il controllo della concorrenza.  
  
## Esempio  
 Nel codice riportato di seguito vengono illustrati esempi di entrambi i valori.  
  
 [!code-csharp[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/vb/module1.vb#1)]  
  
## Vedere anche  
 [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)   
 [Scrittura e invio di modifiche di dati](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)