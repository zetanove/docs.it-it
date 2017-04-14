---
title: "Procedura: risolvere conflitti mediante la sovrascrittura dei valori di database | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd6db0b8-c29c-48ff-b768-31d28e7a148c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: risolvere conflitti mediante la sovrascrittura dei valori di database
Per risolvere le differenze tra i valori del database previsti ed effettivi prima del tentativo di inviare di nuovo le modifiche, è possibile usare <xref:System.Data.Linq.RefreshMode> per sovrascrivere i valori del database.  Per altre informazioni, vedere [Cenni preliminari sulla concorrenza ottimistica](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md).  
  
> [!NOTE]
>  In tutti i casi, viene innanzitutto aggiornato il record sul client recuperando i dati aggiornati dal database.  Questa azione assicura che il successivo tentativo di aggiornamento non avrà esito negativo durante gli stessi controlli di concorrenza.  
  
## Esempio  
 In questo scenario viene generata un'eccezione <xref:System.Data.Linq.ChangeConflictException> quando User1 tenta di inviare le modifiche, in quanto nel frattempo User2 ha modificato le colonne Assistant e Department.  Nella tabella seguente è illustrata questa situazione.  
  
||Manager|Assistant|Department|  
|------|-------------|---------------|----------------|  
|Stato del database originale quando viene eseguita una query da User1 e User2.|Alfreds|Maria|Sales|  
|User1 si prepara a inviare queste modifiche.|Alfred||Marketing|  
|User2 ha già inviato queste modifiche.||Mary|Servizio|  
  
 User1 decide di risolvere questo conflitto sovrascrivendo i valori del database con i valori del membro client corrente.  
  
 Quando User1 risolve il conflitto usando <xref:System.Data.Linq.RefreshMode>, il risultato nel database sarà come nella tabella seguente:  
  
||Manager|Assistant|Department|  
|------|-------------|---------------|----------------|  
|Nuovo stato dopo la risoluzione dei conflitti.|Alfred<br /><br /> \(da User1\)|Maria<br /><br /> \(originale\)|Marketing<br /><br /> \(da User1\)|  
  
 Nel codice di esempio seguente viene illustrato come sovrascrivere i valori del database con i valori del membro client corrente.  Non si verificano conflitti di ispezione o gestione personalizzata dei singoli membri.  
  
 [!code-csharp[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#2)]  
  
## Vedere anche  
 [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)