---
title: "Procedura: sviluppare un servizio WCF in esecuzione in IIS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, distribuzione"
  - "WCF Data Services, sviluppo"
  - "WCF Data Services, hosting"
ms.assetid: f6f768c5-4989-49e3-a36f-896ab4ded86e
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Procedura: sviluppare un servizio WCF in esecuzione in IIS
In questo esempio viene illustrato come usare [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per creare un servizio dati basato sul database di esempio Northwind ospitato in un'applicazione Web ASP.NET in esecuzione in Internet Information Services \(IIS\).  Per un esempio relativo alla creazione dello stesso servizio dati Northwind come applicazione Web ASP.NET in esecuzione nel server di sviluppo ASP.NET, vedere la [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
> [!NOTE]
>  Per creare il servizio dati Northwind, è necessario installare il database di esempio Northwind nel computer locale.  Per scaricare questo database di esempio, vedere la pagina di download dei [database di esempio per SQL Server](http://go.microsoft.com/fwlink/?linkid=24758).  
  
 In questo argomento viene illustrato come creare un servizio dati tramite il provider di Entity Framework.  Sono disponibili altri provider di servizi dati.  Per altre informazioni, vedere [Provider di servizi dati](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md).  
  
 Dopo aver creato il servizio, è necessario fornire in modo esplicito l'accesso alle risorse del servizio dati.  Per altre informazioni, vedere [Procedura: abilitare l'accesso al servizio dati](../../../../docs/framework/data/wcf/how-to-enable-access-to-the-data-service-wcf-data-services.md).  
  
### Per creare l'applicazione Web ASP.NET in esecuzione in IIS  
  
1.  In Visual Studio scegliere **Nuovo** dal menu **File**, quindi selezionare **Progetto**.  
  
2.  Nella finestra di dialogo **Nuovo progetto** selezionare Visual Basic o Visual C\# come linguaggio di programmazione.  
  
3.  Nel riquadro **Modelli** selezionare **Applicazione Web ASP.NET**.  Nota: se si usa Visual Studio Web Developer, sarà necessario creare un nuovo sito Web anziché una nuova applicazione Web.  
  
4.  Digitare `NorthwindService` come nome del progetto.  
  
5.  Fare clic su **OK**.  
  
6.  Scegliere **Proprietà NorthwindService** dal menu **Progetto**.  
  
7.  Selezionare la scheda **Web**, quindi **Usa server Web IIS locale**.  
  
8.  Fare clic su **Crea directory virtuale**, quindi su **OK**.  
  
9. Dal prompt dei comandi aperto con privilegi di amministratore, eseguire uno dei comandi seguenti \(a seconda del sistema operativo\):  
  
    -   sistemi a 32 bit:  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i  
        ```  
  
    -   sistemi a 64 bit:  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework64\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i  
        ```  
  
     In questo modo viene effettuata la registrazione di Windows Communication Foundation \(WCF\) nel computer.  
  
10. Dal prompt dei comandi aperto con privilegi di amministratore, eseguire uno dei comandi seguenti \(a seconda del sistema operativo\):  
  
    -   sistemi a 32 bit:  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe" -i -enable  
        ```  
  
    -   sistemi a 64 bit:  
  
        ```ms-dos  
        "%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe" -i -enable  
        ```  
  
     In questo modo viene verificato che l'esecuzione di IIS dopo che WCF è stato installato nel computer sia corretta.  Può essere necessario inoltre riavviare IIS.  
  
11. Quando l'applicazione ASP.NET è in esecuzione in IIS7, è necessario eseguire inoltre i passaggi seguenti:  
  
    1.  Aprire Gestione IIS e passare all'applicazione PhotoService in **Sito Web predefinito**.  
  
    2.  In **Visualizzazione funzionalità** fare doppio clic su **Autenticazione**.  
  
    3.  Nella pagina **Autenticazione** selezionare **Autenticazione anonima**.  
  
    4.  Nel riquadro **Azioni** fare clic su **Modifica** per impostare l'entità di sicurezza in base alla quale gli utenti anonimi si connetteranno al sito.  
  
    5.  Nella finestra di dialogo **Modifica credenziali di autenticazione anonima** selezionare **Identità pool di applicazioni**.  
  
    > [!IMPORTANT]
    >  Quando si usa l'account Servizio di rete, agli utenti anonimi viene concesso l'accesso completo alla rete interna associato a tale account.  
  
12. Tramite SQL Server Management Studio, l'utilità sqlcmd.exe o l'Editor Transact\-SQL eseguire il comando Transact\-SQL seguente sull'istanza di SQL Server cui è collegato il database Northwind:  
  
    ```sql  
    CREATE LOGIN [NT AUTHORITY\NETWORK SERVICE] FROM WINDOWS;  
    GO   
    ```  
  
     In questo modo nell'istanza di SQL Server viene creato un account di accesso per l'account di Windows usato per eseguire IIS.  Ciò rende possibile la connessione di IIS all'istanza di SQL Server.  
  
13. Con il database Northwind collegato eseguire i comandi Transact\-SQL seguenti:  
  
    ```sql  
    USE Northwind  
    GO  
    CREATE USER [NT AUTHORITY\NETWORK SERVICE]   
    FOR LOGIN [NT AUTHORITY\NETWORK SERVICE] WITH DEFAULT_SCHEMA=[dbo];  
    GO  
    ALTER LOGIN [NT AUTHORITY\NETWORK SERVICE]   
    WITH DEFAULT_DATABASE=[Northwind];   
    GO  
    EXEC sp_addrolemember 'db_datareader', 'NT AUTHORITY\NETWORK SERVICE'  
    GO  
    EXEC sp_addrolemember 'db_datawriter', 'NT AUTHORITY\NETWORK SERVICE'  
    GO   
    ```  
  
     Vengono concessi i diritti al nuovo account di accesso per consentire a IIS la lettura e la scrittura dei dati nel database Northwind.  
  
### Per definire il modello di dati  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto ASP.NET, quindi scegliere **Aggiungi nuovo elemento**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **ADO.NET Entity Data Model**.  
  
3.  Digitare `Northwind.edmx` come nome del modello di dati.  
  
4.  Nella Procedura guidata Entity Data Model selezionare **Genera da database**, quindi fare clic su **Avanti**.  
  
5.  Connettere il modello di dati al database effettuando uno dei passaggi seguenti, quindi fare clic su **Avanti**:  
  
    -   Se non si dispone di una connessione al database già configurata, fare clic su **Nuova connessione** e creare una nuova connessione.  Per altre informazioni, vedere [Procedura: creare connessioni a database di SQL Server](http://go.microsoft.com/fwlink/?LinkId=123631).  A questa istanza di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] deve essere collegato il database Northwind di esempio.  
  
         \- oppure \-  
  
    -   Se si dispone di una connessione al database già configurata per connettersi al database Northwind, selezionarla dall'elenco delle connessioni.  
  
6.  Nella pagina finale della procedura guidata, selezionare le caselle di controllo relative a tutte le tabelle nel database e deselezionare le caselle di controllo relative a visualizzazioni e stored procedure.  
  
7.  Fare clic su **Fine** per chiudere la procedura guidata.  
  
    > [!NOTE]
    >  Questo modello di dati generato espone le proprietà della chiave esterna sui tipi di entità.  I modelli di dati creati usando Visual Studio 2008 non includono tali proprietà della chiave esterna.  Per questo motivo è necessario aggiornare le classi del servizio dati client di qualsiasi applicazione client creata per accedere al servizio dati Northwind creato usando Visual Studio 2008 prima di tentare di accedere alla versione corrente del servizio dati Northwind.  
  
### Per creare il servizio dati  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto ASP.NET, quindi scegliere **Aggiungi nuovo elemento**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **ADO.NET Data Services**.  
  
3.  Digitare `Northwind` come nome del servizio.  
  
     In Visual Studio verranno creati i file del markup XML e del codice per il nuovo servizio.  Per impostazione predefinita, verrà visualizzata la finestra dell'editor del codice.  In **Esplora soluzioni** il servizio risulterà denominato Northwind con estensione svc.cs o svc.vb.  
  
4.  Nel codice per il servizio dati sostituire il commento `/* TODO: put your data source class name here */` nella definizione della classe che definisce il servizio dati con il tipo del contenitore di entità del modello di dati, che in questo caso corrisponde a `NorthwindEntities`.  La definizione di classe dovrà essere analoga alla seguente:  
  
     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#servicedefinition)]  
  
## Vedere anche  
 [Esposizione dei dati come servizio](../../../../docs/framework/data/wcf/exposing-your-data-as-a-service-wcf-data-services.md)