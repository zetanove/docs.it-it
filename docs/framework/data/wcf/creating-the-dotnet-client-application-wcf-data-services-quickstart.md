---
title: "Creazione dell&#39;applicazione client .NET Framework (Guida rapida di WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 41ade767-eeab-437d-9121-9797e8fb8045
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Creazione dell&#39;applicazione client .NET Framework (Guida rapida di WCF Data Services)
Questa attività è l'attività finale della guida rapida di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  In questa attività si aggiungerà un'applicazione console alla soluzione e un riferimento al feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] in questa nuova applicazione client e si eseguirà l'accesso al feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] dall'applicazione client usando le classi del servizio dati e le librerie client generate.  
  
> [!NOTE]
>  Per accedere a un feed di dati non è necessario disporre di un'applicazione client basata su .NET Framework.  L'accesso al servizio dati può essere eseguito da qualsiasi componente dell'applicazione che usa un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Per altre informazioni, vedere [Utilizzo di un servizio dati in un'applicazione client](../../../../docs/framework/data/wcf/using-a-data-service-in-a-client-application-wcf-data-services.md).  
  
### Per creare l'applicazione client tramite Visual Studio  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla soluzione, scegliere **Aggiungi**, quindi fare clic su **Nuovo progetto**.  
  
2.  In **Tipi progetto** fare clic su **Finestre**, quindi selezionare **Applicazione WPF** nel riquadro **Modelli**.  
  
3.  Immettere `NorthwindClient` come nome del progetto, quindi fare clic su **OK**.  
  
4.  Aprire il file MainWindow.xaml e sostituire il codice XAML con il codice seguente:  
  
     [!code-xml[Astoria Quickstart Client#Window1Xaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml#window1xaml)]  
  
### Per aggiungere un riferimento al servizio dati nel progetto  
  
1.  Fare clic con il pulsante destro del mouse sul progetto NorthwindClient, scegliere **Aggiungi riferimento al servizio**, quindi fare clic su **Individua**.  
  
     Verrà visualizzato il servizio dati Northwind creato nella prima attività.  
  
2.  Nella casella di testo **Spazio dei nomi** digitare `Northwind`, quindi scegliere **OK**.  
  
     Verrà aggiunto un nuovo file di codice al progetto, che contiene le classi di dati usate per accedere e interagire con le risorse del servizio dati come oggetti.  Le classi di dati vengono create nello spazio dei nomi `NorthwindClient.Northwind`.  
  
### Per accedere ai dati del servizio dati nell'applicazione WPF  
  
1.  In **NorthwindClient** in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi riferimento**.  
  
2.  Nella finestra di dialogo Aggiungi riferimento fare clic sulla scheda **.NET**, selezionare l'assembly System.Data.Services.Client.dll, quindi scegliere **OK**.  In **NorthwindClient** in **Esplora soluzioni** aprire la tabella codici per il file MainWindow1.xaml e aggiungere l'istruzione `using` seguente \(`Imports` in Visual Basic\).  
  
     [!code-csharp[Astoria Quickstart Client#Using](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#using)]
     [!code-vb[Astoria Quickstart Client#Using](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#using)]  
  
3.  Inserire il codice seguente che consente di eseguire una query sul servizio dati e di associare il risultato a un oggetto <xref:System.Data.Services.Client.DataServiceCollection%601> nella classe `MainWindow`:  
  
    > [!NOTE]
    >  È necessario sostituire il nome host `localhost:12345` con il server e la porta di hosting dell'istanza del servizio dati Northwind.  
  
     [!code-csharp[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#querycode)]
     [!code-vb[Astoria Quickstart Client#QueryCode](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#querycode)]  
  
4.  Inserire il codice seguente che consente di salvare le modifiche nella classe `MainWindow`:  
  
     [!code-csharp[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart client/cs/window1.xaml.cs#savechanges)]
     [!code-vb[Astoria Quickstart Client#SaveChanges](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart client/vb/window1.xaml.vb#savechanges)]  
  
### Per compilare ed eseguire l'applicazione NorthwindClient  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto NorthwindClient e scegliere **Imposta come progetto di avvio**.  
  
2.  Premere F5 per avviare l’applicazione.  
  
     La soluzione viene compilata e l'applicazione client viene avviata.  I dati vengono richiesti dal servizio e visualizzati nella console.  
  
3.  Modificare un valore nella colonna **Quantità** della griglia dei dati, quindi scegliere **Salva**.  
  
     Le modifiche vengono salvate nel servizio dati.  
  
    > [!NOTE]
    >  Questa versione dell'applicazione NorthwindClient non supporta l'aggiunta e l'eliminazione di entità.  
  
## Passaggi successivi  
 La creazione dell'applicazione client che accede al feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] Northwind di esempio è stata completata.  È stata inoltre completata la guida rapida di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'accesso a un feed di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] da un'applicazione [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], vedere [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md).  
  
## Vedere anche  
 [Guida introduttiva](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)   
 [Risorse](../../../../docs/framework/data/wcf/wcf-data-services-resources.md)