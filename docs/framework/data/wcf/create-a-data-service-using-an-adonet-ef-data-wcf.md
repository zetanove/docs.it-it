---
title: "Procedura: creare un servizio dati utilizzando un&#39;origine dati ADO.NET Entity Framework (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, Entity framework"
  - "WCF Data Services, provider"
ms.assetid: 6d11fec8-0108-42f5-8719-2a7866d04428
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Procedura: creare un servizio dati utilizzando un&#39;origine dati ADO.NET Entity Framework (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] espone i dati di entità come servizio dati.  Tali dati vengono forniti da [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] quando l'origine dati è un database relazionale.  In questo argomento viene illustrato come creare un modello di dati basato su [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] in un'applicazione Web [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] in base a un database esistente e come usarlo per creare un nuovo servizio dati.  
  
 In [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] è disponibile inoltre uno strumento da riga di comando che può generare un modello di [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] all'esterno di un progetto [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  Per altre informazioni, vedere [Procedura: utilizzare EdmGen.exe per generare i file di modello e di mapping](../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  
  
### Per aggiungere un modello di Entity Framework basato su un database esistente a un'applicazione Web esistente  
  
1.  Nel menu **Progetto** fare clic su **Aggiungi nuovo elemento**.  
  
2.  Nel riquadro **Modelli** fare clic sulla categoria **Dati**, quindi selezionare **ADO.NET Entity Data Model**.  
  
3.  Digitare il nome del modello, quindi fare clic su **Aggiungi**.  
  
     Verrà visualizzata la prima pagina della Procedura guidata [!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)].  
  
4.  Nella finestra di dialogo **Scegli contenuto Model** selezionare **Genera da database**.  Scegliere quindi **Avanti**.  
  
5.  Fare clic sul pulsante **Nuova connessione**.  
  
6.  Nella finestra di dialogo **Proprietà connessione** digitare il nome del server, selezionare il metodo di autenticazione, digitare il nome del database, quindi scegliere **OK**.  
  
     La finestra di dialogo **Scegliere la connessione dati** verrà aggiornata con le impostazioni di connessione al database.  
  
7.  Verificare che la casella di controllo **Salva impostazioni stringa di connessione entity in App.Config come** sia selezionata.  Scegliere quindi **Avanti**.  
  
8.  Nella finestra di dialogo **Seleziona oggetti di database** selezionare tutti di oggetti di database che si intende esporre nel servizio dati.  
  
    > [!NOTE]
    >  Gli oggetti inclusi nel modello di dati non vengono esposti automaticamente dal servizio dati.  Devono essere esposti in modo esplicito mediante il servizio stesso.  Per altre informazioni, vedere [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md).  
  
9. Fare clic su **Fine** per completare la procedura guidata.  
  
     Verrà creato un modello di dati predefinito in base al database specifico.  [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] consente di personalizzare il modello di dati.  Per altre informazioni, vedere [Tasks](http://msdn.microsoft.com/it-it/7166f1f1-4de8-4bd4-86b5-5e20a2ebaccb).  
  
### Per creare il servizio dati usando il nuovo modello di dati  
  
1.  In [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] aprire il file con estensione edmx che rappresenta il modello di dati.  
  
2.  In **Browser modello** fare clic con il pulsante destro del mouse sul modello, scegliere **Proprietà**, quindi prendere nota del nome del contenitore di entità.  
  
3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], quindi scegliere **Aggiungi nuovo elemento**.  
  
4.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Servizio dati WCF**.  
  
5.  Specificare un nome per il servizio, quindi fare clic su **OK**.  
  
     In [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] verranno creati i file del markup XML e del codice per il nuovo servizio.  Per impostazione predefinita, verrà visualizzata la finestra dell'editor del codice.  
  
6.  Nel codice per il servizio dati sostituire il commento `/* TODO: put your data source class name here */` nella definizione della classe che definisce il servizio dati con il tipo che eredita dalla classe <xref:System.Data.Objects.ObjectContext> e che rappresenta il contenitore di entità del modello di dati annotato nel passaggio 2.  
  
7.  Nel codice per il servizio dati consentire ai client autorizzati di accedere ai set di entità esposti dal servizio dati.  Per altre informazioni, vedere [Creazione del servizio dati](../../../../docs/framework/data/wcf/creating-the-data-service.md).  
  
8.  Per testare il servizio dati Northwind.svc tramite un browser, seguire le istruzioni riportate nell'argomento [Accesso al servizio da un browser](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md).  
  
## Vedere anche  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Provider di servizi dati](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)   
 [Procedura: creare un servizio dati utilizzando il provider di reflection](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md)   
 [Procedura: creare un servizio dati utilizzando un'origine dati LINQ to SQL](../../../../docs/framework/data/wcf/create-a-data-service-using-linq-to-sql-wcf.md)