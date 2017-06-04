---
title: "Download dei database di esempio (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb42a7af-d410-4b7f-b4a8-13c72ce6fd09
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Download dei database di esempio (LINQ to DataSet)
Negli esempi e nelle procedure dettagliate riportate nella documentazione di [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] viene usato il database di esempio AdventureWorks.  È possibile scaricare gratuitamente questo prodotto dal sito di download Microsoft. Negli esempi e nelle procedure dettagliate riportate nella documentazione di [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] viene usato SQL Server come archivio dati.  Anziché SQL Server è tuttavia possibile usare come archivio dati SQL Server Express Edition, disponibile gratuitamente.  
  
## Download e installazione del database AdventureWorks  
  
#### Per scaricare e installare il database di esempio AdventureWorks per SQL Server  
  
1.  Aprire Internet Explorer.  
  
2.  Passare al sito Web relativo agli [esempi di SQL Server 2005 e ai database di esempio](http://go.microsoft.com/fwlink/?linkid=31046).  
  
3.  Attenersi alle istruzioni per scaricare il database di esempio AdventureWorks corretto per il tipo di processore in utilizzo, ad esempio AdventureWorksDB.msi, quindi salvare il file MSI nel computer locale.  
  
4.  Se è già stata installata una versione precedente di AdventureWorks, tramite download o durante l'installazione di SQL Server, è necessario rimuoverla prima di eseguire AdventureWorks.msi.  
  
#### Per rimuovere un download precedente di un database di esempio AdventureWorks  
  
1.  Eliminare il database AdventureWorks o AdventureWorksDW.  
  
2.  In **Installazione applicazioni** selezionare **AdventureWorksDB** o **AdventureWorksBI**, quindi fare clic su **Rimuovi**.  
  
#### Per rimuovere un database di esempio AdventureWorks installato in precedenza tramite il programma di installazione  
  
1.  Eliminare il database AdventureWorks o AdventureWorksDW.  
  
2.  In **Installazione applicazioni** selezionare **Microsoft SQL Server 2005** e fare clic su **Cambia**.  
  
3.  In **Selezione componenti** selezionare **Componenti workstation** e quindi fare clic su **Avanti**.  
  
4.  In **Installazione guidata di Microsoft SQL Server** fare clic su **Avanti**.  
  
5.  In **Controllo configurazione sistema** fare clic su **Avanti**.  
  
6.  In **Cambia o rimuovi istanza** fare clic su **Modifica componenti installati**.  
  
7.  In **Selezione funzionalità** espandere il nodo **Documentazione, esempi e database di esempio**.  
  
8.  Selezionare **Codice e applicazioni di esempio**.  Espandere **Database di esempio**, selezionare il database di esempio da rimuovere e selezionare **La funzionalità completa non sarà disponibile**.  Scegliere **Avanti**.  
  
9. Fare clic su **Installa** per completare l'installazione guidata.  
  
#### Per collegare i file del database di esempio AdventureWorks a un'istanza di SQL Server  
  
1.  Dopo aver installato il file del programma di installazione del database di esempio, fare doppio clic su file **AdventureWorksDB.msi** \(o sul file scaricato\) per installare il database.  Per impostazione predefinita, il database viene installato in C:\\Programmi\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data.  
  
2.  Per collegare il file del database AdventureWorks a un'istanza di SQL Server, eseguire il seguente script SQLCMD o SQL Server Management Studio:  
  
    ```  
    exec sp_attach_db @dbname=N'AdventureWorks', @filename1=N'C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\AdventureWorks_Data.mdf', @filename2=N'C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\AdventureWorks_log.ldf'  
    ```  
  
     Se i file sono stati installati in un'unità o una directory diversa, è necessario modificare i percorsi prima di eseguire la stored procedure `sp_attach_db`.  
  
## Download di SQL Server Express Edition  
 Negli esempi e nelle procedure dettagliate della sezione [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] viene usato SQL Server 2005 come archivio dati, sebbene sia comunque possibile usare SQL Server Express Edition.  SQL Server Express Edition è disponibile gratuitamente e può essere ridistribuito con le applicazioni.  Se si usa [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], SQL Server Express Edition è incluso nelle edizioni Pro e superiori.  
  
#### Per scaricare e installare SQL Server Express Edition  
  
1.  Avviare Internet Explorer.  
  
2.  Passare alla pagina di download di [Microsoft SQL Server 2005 Express Edition](http://go.microsoft.com/fwlink/?LinkID=31070).  
  
3.  Attenersi alle istruzioni di installazione visualizzate nel sito Web.  
  
## Vedere anche  
 [Guida introduttiva](../../../../docs/framework/data/adonet/getting-started-linq-to-dataset.md)