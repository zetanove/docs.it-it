---
title: "Pubblicazione servizio WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c806b253-cd47-4b96-b831-e73cbf08808f
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Pubblicazione servizio WCF
Pubblicazione servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] assiste l'utente nel passaggio dall'ambiente di sviluppo iniziale fornito da Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] fino all'effettiva distribuzione dell'applicazione in un ambiente di produzione a scopo di test.  Prima di impegnarsi in un piano di distribuzione finale, è possibile usare Pubblicazione servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] per verificare che il servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] venga eseguito correttamente e sia pronto per la pubblicazione.  È inoltre possibile scegliere di distribuire le librerie dei servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in diverse posizioni di destinazione per il test.  
  
## Servizi supportati e posizioni di destinazione  
 Pubblicazione servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] supporta la pubblicazione di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] creati dal set di modelli delle librerie dei servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e dei modelli di elementi corrispondenti, tra cui:  
  
-   Modello della libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con modello di elemento.  
  
-   Modello della libreria di servizi del flusso di lavoro sequenziale con modello di elemento.  
  
-   Modello della libreria di servizi del flusso di lavoro di una macchina a stati con modello di elemento.  
  
-   Libreria di servizi di diffusione.  
  
 È possibile trovare questi modelli di servizi scegliendo **File** \-\> **Nuovo progetto** \-\> **Visual Basic** r **Visual C\#** \-\> **WCF**.  
  
 È possibile pubblicare il servizio nelle posizioni di destinazione seguenti.  
  
-   IIS locale.  
  
-   File system.  
  
-   Sito FTP.  
  
-   Sito remoto.  
  
## Uso di Pubblicazione servizio WCF  
 Per distribuire un'implementazione del servizio, eseguire la procedura seguente:  
  
1.  Aprire Visual Studio con privilegi elevati. A tale scopo, fare clic con il pulsante destro del mouse sul file eseguibile, quindi scegliere Esegui come amministratore per avviarlo.  Se si usa IIS 7.0 o versioni successive, verificare che sia stato installato il componente "Compatibilità metabase di IIS e configurazione di IIS 6" tramite l'opzione Attiva o disattiva le funzionalità Windows nel Pannello di controllo.  
  
2.  Aprire un progetto del servizio, selezionare **Compila**\-\>**Pubblica \<Nome progetto\>** dal menu principale oppure fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Pubblica**.  
  
3.  Verrà visualizzata la finestra **Pubblica**.  Fare clic su **…**.  per specificare la posizione di destinazione in cui distribuire il servizio.  È possibile scegliere di distribuire l'applicazione in un sito Web IIS locale, nel file system, in un sito FTP o in un sito remoto.  Se si distribuisce l'applicazione in un sito Web IIS locale, è possibile selezionare il sito Web e crearvi l'applicazione Web. A tale scopo, fare clic sull'icona **Crea nuova applicazione Web** nell'angolo superiore destro.  
  
4.  Dopo aver fatto clic su **Pubblica** nella finestra principale, l'applicazione verrà distribuita nel percorso di destinazione specificato e nella directory di destinazione verranno copiati il file Web.config, il file con estensione svc e i file di assembly.  .  Il nome del file con estensione svc sarà “ProjectName.ServiceName.svc”.  Dopo la pubblicazione del servizio, è possibile che nella finestra di output di Visual Studio venga visualizzato un collegamento attivo analogo a "Connessione a http:\/\/localhost\/WebApplicationFolderName... ".  Premere CTRL e fare clic sul collegamento per aprire una pagina del browser in Visual Studio per visualizzare la struttura di directory del servizio.  
  
     Se non è possibile collegarsi al sito, è possibile che il browser di directory non sia abilitato in IIS.  Per abilitarlo, seguire i suggerimenti disponibili nella sezione "Possibili operazioni".  In alternativa, digitare direttamente "http:\/\/localhost\/WebApplicationFolderName\/ProjectName.ServiceName.svc" per visualizzare la pagina del servizio.  
  
 È possibile usare **Pubblica** per specificare se si desidera copiare nel percorso di destinazione i file di assembly, il file di configurazione e il file con estensione svc definiti nel progetto e sovrascrivere i file esistenti in tale percorso.  
  
 Se si sceglie di distribuire l'applicazione nel sito Web IIS locale, è possibile rilevare errori correlati all'installazione di IIS.  Verificare che IIS sia installato in modo corretto.  È possibile digitare "http:\/\/localhost" nel browser e controllare se viene visualizzata la pagina predefinita di IIS.  In alcuni casi i problemi potrebbero essere causati dalla registrazione non corretta di ASP.NET o [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in IIS.  In questo caso, aprire il prompt dei comandi di Visual Studio ed eseguire il comando "aspnet\_regiis.exe \- ir" per correggere problemi di registrazione di ASP.NET o eseguire il comando "ServiceModelReg.exe \-ia" per correggere problemi di registrazione di WCF.  
  
## File generati per la pubblicazione  
 Prima che una libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] possa essere ospitata sul Web, devono essere generati automaticamente i file di assembly, il file Web.config e il file con estensione svc.  Tutti i file vengono copiati nella posizione di destinazione specificata.  Il servizio viene quindi pubblicato.  
  
### File di assembly  
 Quando si pubblica un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] usando questo strumento, viene innanzitutto compilato automaticamente il servizio, mentre i file di assembly vengono generati nel progetto di servizio dopo la compilazione.  
  
### File SVC  
 L'operazione di pubblicazione determina la creazione di un file con estensione svc per ogni servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], indipendentemente dal fatto che il file esista o meno, per garantire la validità della versione.  Esistono due tipi diversi di file svc: uno per la libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e la libreria di servizi di diffusione e un altro per la libreria di servizi del flusso di lavoro sequenziale e la libreria di servizi del flusso di lavoro di una macchina a stati.  Il file con estensione svc generato viene copiato nella cartella radice nella posizione di destinazione.  
  
### File Web.config  
 Ogni volta che un progetto di servizio viene pubblicato in una posizione di destinazione specifica, viene creato un file Web.config.  
  
 Il file Web.config generato include sezioni Web utili per l'hosting Web, nonché il contenuto del file App.config per la libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con le modifiche seguenti:  
  
-   L'indirizzo di base è escluso.  
  
-   Le impostazioni nell'elemento `<diagnostics>` vengono escluse per mantenere le impostazioni di traccia della piattaforma di destinazione.  
  
## Pubblicazione di servizi WCF con associazioni non HTTP a IIS  
 Se si usa IIS7.0 o versione successiva, è possibile pubblicare servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con associazioni a IIS non HTTP.  È necessario tuttavia eseguire alcune configurazioni preliminari.  Per altre informazioni, vedere gli argomenti in [Hosting nel servizio di attivazione dei processi di Windows](../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md).  
  
## Sicurezza  
 Per la pubblicazione su un sito Web IIS locale sono necessari i privilegi di amministratore, poiché IIS deve essere eseguito con un account di questo tipo.  Se Pubblicazione servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene aperto da un utente che non dispone dei privilegi di amministratore, IIS non sarà disponibile come posizione di destinazione.  La pubblicazione nel File system, su un sito FTP o su un sito remoto può essere eseguita senza i privilegi di amministratore.  
  
## Vedere anche  
 [Modelli di Visual Studio WCF](../../../docs/framework/wcf/wcf-vs-templates.md)   
 [Host servizio WCF \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)   
 [Client di test WCF \(WcfTestClient.exe\)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)