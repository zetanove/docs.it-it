---
title: "Procedura: inserire righe nel database | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 44d99680-69c7-4879-a732-f6771b334211
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: inserire righe nel database
Per inserire righe in un database, aggiungere oggetti alla raccolta [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Table%601> associata, quindi inviare le modifiche al database. Le modifiche vengono convertite da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] nei comandi SQL `INSERT` corretti.  
  
> [!NOTE]
>  È possibile eseguire l'override dei metodi predefiniti [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per le operazioni di database `Insert`, `Update`e `Delete`.  Per altre informazioni, vedere [Personalizzazione delle operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md).  
>   
>  Gli sviluppatori che usano [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] possono adoperare [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per sviluppare stored procedure allo stesso scopo.  
  
 Per l'esecuzione dei passaggi seguenti si presuppone l'uso di un oggetto <xref:System.Data.Linq.DataContext> valido per la connessione al database Northwind.  Per altre informazioni, vedere [Procedura: connettersi a un database](../../../../../../docs/framework/data/adonet/sql/linq/how-to-connect-to-a-database.md).  
  
### Per inserire una riga nel database  
  
1.  Creare un nuovo oggetto contenente i dati della colonna da inviare.  
  
2.  Aggiungere il nuovo oggetto alla raccolta [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] `Table` associata alla tabella di destinazione nel database.  
  
3.  Inviare le modifiche al database.  
  
## Esempio  
 L'esempio di codice seguente consente di creare un nuovo oggetto di tipo `Order` e di popolarlo con i valori corretti.  Il nuovo oggetto viene quindi aggiunto alla raccolta `Order`.  Infine viene inviata la modifica al database come una nuova riga nella tabella `Orders`.  
  
 [!code-csharp[System.Data.Linq.Table#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.table/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.Table#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.table/vb/module1.vb#1)]  
  
## Vedere anche  
 [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)   
 [Metodi DataContext \(Progettazione relazionale oggetti\)](../Topic/DataContext%20Methods%20\(O-R%20Designer\).md)   
 [Procedura: assegnare stored procedure per l'esecuzione dei comandi di aggiornamento, inserimento ed eliminazione \(Progettazione relazionale oggetti\)](../Topic/How%20to:%20Assign%20stored%20procedures%20to%20perform%20updates,%20inserts,%20and%20deletes%20\(O-R%20Designer\).md)   
 [Scrittura e invio di modifiche di dati](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)