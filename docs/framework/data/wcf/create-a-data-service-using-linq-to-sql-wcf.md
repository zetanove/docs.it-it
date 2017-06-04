---
title: "Procedura: creare un servizio dati utilizzando un&#39;origine dati LINQ to SQL (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, LINQ to SQL"
  - "WCF Data Services, provider"
ms.assetid: 3b01c2fd-8c6e-4bf5-b38f-9e61bdc3c328
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: creare un servizio dati utilizzando un&#39;origine dati LINQ to SQL (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] espone i dati di entità come servizio dati.  Il provider di reflection consente di definire un modello di dati basato su una classe che espone membri che restituiscono un'implementazione di <xref:System.Linq.IQueryable%601>.  Per essere in grado di apportare aggiornamenti ai dati nell'origine dati, queste classi devono inoltre implementare l'interfaccia <xref:System.Data.Services.IUpdatable>.  Per altre informazioni, vedere [Provider di servizi dati](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md).  In questo argomento viene illustrato come creare classi LINQ to SQL per l'accesso al database Northwind di esempio tramite il provider di reflection, nonché come creare il servizio dati basato su queste classi di dati.  
  
### Per aggiungere classi LINQ to SQL a un progetto  
  
1.  Nel menu **Progetto** all'interno di un'applicazione Visual Basic o C\#, scegliere **Aggiungi nuovo elemento**.  
  
2.  Fare clic sul modello **Classi LINQ to SQL**.  
  
3.  Modificare il nome in Northwind.dbml.  
  
4.  Fare clic su **Aggiungi**.  
  
     Il file Northwind.dbml verrà aggiunto al progetto e verrà visualizzato Progettazione relazionale oggetti.  
  
5.  In **Esplora server**\/**database** sotto Northwind espandere **Tabelle** e trascinare la tabella `Customers` in Progettazione relazionale oggetti.  
  
     Verrà creata una classe di entità `Customer` che verrà visualizzata nell'area di progettazione.  
  
6.  Ripetere il passaggio 6 per le tabelle `Orders`, `Order_Details` e `Products`.  
  
7.  Fare clic con il pulsante destro del mouse sul nuovo file con estensione dbml che rappresenta le classi LINQ to SQL e scegliere **Visualizza codice**.  
  
     Verrà creata una nuova pagina code\-behind denominata Northwind.cs contenente una definizione di classe parziale per la classe che eredita dalla classe <xref:System.Data.Linq.DataContext>, che in questo caso corrisponde a `NorthwindDataContext`.  
  
8.  Sostituire il contenuto del file di codice Northwind.cs con il codice riportato di seguito.  Questo codice implementa il provider di reflection mediante l'estensione di <xref:System.Data.Linq.DataContext> e delle classi di dati generate da LINQ to SQL:  
  
     [!code-csharp[Astoria Linq Provider#Linq2SqlProvider](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria linq provider/cs/northwind.cs#linq2sqlprovider)]
     [!code-vb[Astoria Linq Provider#Linq2SqlProvider](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria linq provider/vb/northwind.vb#linq2sqlprovider)]  
  
### Per creare un servizio dati tramite un modello di dati basato su LINQ to SQL  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto ASP.NET, quindi scegliere **Aggiungi nuovo elemento**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Servizio dati WCF**.  
  
3.  Specificare un nome per il servizio, quindi fare clic su **OK**.  
  
     In Visual Studio verranno creati i file del markup XML e del codice per il nuovo servizio.  Per impostazione predefinita, verrà visualizzata la finestra dell'editor del codice.  
  
4.  Nel codice per il servizio dati sostituire il commento `/* TODO: put your data source class name here */` nella definizione della classe che definisce il servizio dati con il tipo del contenitore di entità del modello di dati, che in questo caso corrisponde a `NorthwindDataContext`.  
  
5.  Nel codice per il servizio dati sostituire il codice segnaposto nella funzione `InitializeService` con il codice seguente:  
  
     [!code-csharp[Astoria Linq Provider#EnableAccess](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria linq provider/cs/northwind.svc.cs#enableaccess)]
     [!code-vb[Astoria Linq Provider#EnableAccess](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria linq provider/vb/northwind.svc.vb#enableaccess)]  
  
     In questo modo i client autorizzati saranno in grado di accedere alle risorse per i tre set di entità specificati.  
  
6.  Per testare il servizio dati Northwind.svc tramite un browser, seguire le istruzioni riportate nell'argomento [Accesso al servizio da un browser](../../../../docs/framework/data/wcf/accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md).  
  
## Vedere anche  
 [Procedura: creare un servizio dati utilizzando un'origine dati ADO.NET Entity Framework](../../../../docs/framework/data/wcf/create-a-data-service-using-an-adonet-ef-data-wcf.md)   
 [Procedura: creare un servizio dati utilizzando il provider di reflection](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md)   
 [Provider di servizi dati](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)