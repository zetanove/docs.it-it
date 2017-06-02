---
title: "Procedura: creare un client di Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "client [WCF], esecuzione"
  - "Client WCF [WCF], esecuzione"
ms.assetid: a67884cc-1c4b-416b-8c96-5c954099f19f
caps.latest.revision: 64
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 64
---
# Procedura: creare un client di Windows Communication Foundation
Questa è la quarta delle sei attività necessarie per creare un'applicazione [!INCLUDE[indigo1](../../../includes/indigo1-md.md)].Per una panoramica di tutte e sei le attività, vedere l'argomento [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md).  
  
 In questo argomento viene illustrato come recuperare metadati da un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e utilizzarli per creare un proxy [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in grado di accedere al servizio.Questa attività viene completata tramite la funzionalità Aggiungi riferimento al servizio fornita da Visual Studio.Questo strumento ottiene i metadati dall'endpoint MEX del servizio e genera un file di codice sorgente gestito per un proxy client nel linguaggio scelto \(per impostazione predefinita C\#\).Oltre a creare il proxy client, lo strumento crea o aggiorna anche il file di configurazione del client che consente all'applicazione client di connettersi al servizio su uno dei relativi endpoint.  
  
> [!NOTE]
>  È anche possibile utilizzare lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per generare la classe proxy e la configurazione anziché utilizzare Aggiungi riferimento al servizio all'interno di Visual Studio.  
  
> [!WARNING]
>  Quando si esegue la chiamata a un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] da un progetto Libreria di classi in [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], è possibile utilizzare la funzionalità Aggiungi riferimento al servizio per generare automaticamente un proxy e un file di configurazione associato.Il file di configurazione non sarà utilizzato dal progetto Libreria di classi.Sarà necessario aggiungere le impostazioni del file di configurazione generato nel file app.config per il file eseguibile che chiamerà la libreria di classi.  
  
 L'applicazione client utilizza la classe proxy generata per comunicare con il servizio.Questa procedura è descritta in [Procedura: usare un client](../../../docs/framework/wcf/how-to-use-a-wcf-client.md).  
  
### Per creare un client Windows Communication Foundation  
  
1.  Creare un nuovo progetto di applicazione console facendo clic con il pulsante destro del mouse sulla soluzione di introduzione e selezionando **Aggiungi**, **Nuovo progetto**.Sul lato sinistro della finestra di dialogo **Aggiungi nuovo progetto** selezionare **Windows** sotto **C\#** o **VB**.Nella sezione centrale della finestra di dialogo selezionare **Applicazione console**.Assegnare al progetto il nome `GettingStartedClient`.  
  
2.  Impostare il framework di destinazione del progetto GettingStartedClient su .NET Framework 4.5 facendo clic con il pulsante destro del mouse su **GettingStartedClient** in Esplora soluzioni e selezionando **Proprietà**.Nella casella a discesa con etichetta **Framework di destinazione** selezionare **.NET Framework 4.5**.L'operazione di impostazione del framework di destinazione per un progetto VB è leggermente diversa. Nella finestra di dialogo delle proprietà del progetto GettingStartedClient fare clic sulla scheda **Compilazione** sul lato sinistro della schermata, quindi fare clic sul pulsante **Opzioni di compilazione avanzate** nell'angolo inferiore sinistro della finestra di dialogo.Successivamente selezionare **.NET Framework 4.5** nella casella a discesa con etichetta **Framework di destinazione**.  
  
     L'impostazione del framework di destinazione comporterà il ricaricamento della soluzione da parte di Visual Studio 2011. Quando richiesto, premere **OK**.  
  
3.  Aggiungere un riferimento a System.ServiceModel nel progetto GettingStartedClient facendo clic con il pulsante destro del mouse sulla cartella **Riferimento** nel progetto GettingStartedClient in Esplora soluzioni e selezionare **Aggiungi riferimento**.Nella finestra di dialogo **Aggiungi riferimento** selezionare **Framework** sul lato sinistro della finestra di dialogo.Nella casella di testo di ricerca degli assembly digitare `System.ServiceModel`.Nella sezione centrale della finestra di dialogo selezionare **System.ServiceModel**, quindi fare clic sui pulsanti **Aggiungi** e **Chiudi**.Salvare la soluzione facendo clic sul pulsante **Salva tutto** sotto il menu principale.  
  
4.  Successivamente, verrà aggiunto un riferimento al servizio calcolatrice.Prima di poter eseguire questa operazione, è necessario avviare l'applicazione console GettingStartedHost.Una volta che l'host è in esecuzione, è possibile fare clic con il pulsante destro del mouse sulla cartella Riferimenti nel progetto GettingStartedClient in Esplora soluzioni e selezionare Aggiungi riferimento al servizio; digitare l'URL seguente nella casella dell'indirizzo della finestra di dialogo Aggiungi riferimento al servizio: http:\/\/localhost:8000\/ServiceModelSamples\/Service, quindi fare clic sul pulsante **Vai**.CalculatorService deve quindi essere visualizzato nella casella di riepilogo dei servizi. Fare doppio clic su CalculatorService in modo che venga espanso e vengano visualizzati i contratti di servizio implementati dal servizio.Lasciare inalterato lo spazio dei nomi predefinito e fare clic sul pulsante **OK**.  
  
     Quando si aggiunge un riferimento a un servizio utilizzando Visual Studio, nel progetto GettingStartedClient della cartella dei riferimenti al servizio in Esplora soluzioni viene visualizzato un nuovo elemento.Se si utilizza lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md), verranno generati un file di codice sorgente e un file app.config.  
  
     È anche possibile utilizzare lo strumento della riga di comando [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) con le opzioni appropriate per creare il codice client.Nell'esempio seguente viene illustrato un file di codice e un file di configurazione per il servizio.Nel primo esempio viene illustrato come generare il proxy in VB e nel secondo come effettuare la stessa operazione in C\#:  
  
    ```  
    svcutil.exe /language:vb /out:generatedProxy.vb /config:app.config http://localhost:8000/ServiceModelSamples/service  
  
    ```  
  
    ```csharp  
    svcutil.exe /language:cs /out:generatedProxy.cs /config:app.config http://localhost:8000/ServiceModelSamples/service  
  
    ```  
  
 A questo punto è stato creato il proxy che sarà utilizzato dall'applicazione client per chiamare il servizio calcolatrice.Procedere all'argomento successivo: [Procedura: descrizione della configurazione di un client](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md)  
  
## Vedere anche  
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [Guida introduttiva](../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [Servizio indipendente](../../../docs/framework/wcf/samples/self-host.md)   
 [Procedura: pubblicare metadati per un servizio usando un file di configurazione](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [Procedura: utilizzare Svcutil.exe per scaricare documenti di metadati](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)