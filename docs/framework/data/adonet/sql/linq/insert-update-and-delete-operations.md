---
title: "Operazioni Insert, Update e Delete | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 26a43a4f-83c9-4732-806d-bb23aad0ff6b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Operazioni Insert, Update e Delete
In `Insert` le operazioni `Update`, `Delete`e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono eseguite aggiungendo, modificando e rimuovendo oggetti nel modello a oggetti.  Per impostazione predefinita, le azioni vengono convertite da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in SQL e le modifiche vengono inviate al database.  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene offerta la massima flessibilità per quanto riguarda la modifica e il salvataggio in modo permanente delle modifiche apportate agli oggetti.  Non appena gli oggetti entità sono disponibili, recuperandoli tramite una query o costruendoli di nuovo, è possibile modificarli nell'applicazione come oggetti normali.  In altre parole, è possibile modificarne i valori e aggiungerli o rimuoverli dalle raccolte.  In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene tenuta traccia delle modifiche, che verranno trasmesse di nuovo al database quando si chiama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  
  
> [!NOTE]
>  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non supporta o non riconosce operazioni di eliminazione a catena.  Se si desidera eliminare una riga di una tabella contenente vincoli, è necessario impostare la regola `ON DELETE CASCADE` nel vincolo di chiave esterna del database o usare il proprio codice per eliminare innanzitutto gli oggetti figlio che impediscono l'eliminazione dell'oggetto padre. In caso contrario, viene generata un'eccezione.  Per altre informazioni, vedere [Procedura: eliminare righe dal database](../../../../../../docs/framework/data/adonet/sql/linq/how-to-delete-rows-from-the-database.md).  
  
 Nei frammenti di codice riportati di seguito vengono usate le classi `Customer`e `Order` del database di esempio Northwind.  Le definizioni di classe non sono illustrate per brevità.  
  
 [!code-csharp[DLinqCRUDOps#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCRUDOps/cs/Program.cs#1)]
 [!code-vb[DLinqCRUDOps#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCRUDOps/vb/Module1.vb#1)]  
  
 Quando si chiama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] genera automaticamente ed esegue i comandi SQL necessari per trasmettere di nuovo le modifiche al database.  
  
> [!NOTE]
>  È possibile eseguire l'override di questo comportamento usando una logica personalizzata, in genere mediante una stored procedure.  Per altre informazioni, vedere [Responsabilità dello sviluppatore nell'eseguire l'override del comportamento predefinito](../../../../../../docs/framework/data/adonet/sql/linq/responsibilities-of-the-developer-in-overriding-default-behavior.md).  
>   
>  Gli sviluppatori che usano [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] possono adoperare [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per sviluppare stored procedure a questo scopo.  
  
## Vedere anche  
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [Personalizzazione delle operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)