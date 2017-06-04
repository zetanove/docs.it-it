---
title: "Host servizio WCF (WcfSvcHost.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8643a63d-a357-4c39-bd6c-cdfdf71e370e
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# Host servizio WCF (WcfSvcHost.exe)
Host servizio di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] \(WcfSvcHost.exe\) consente di avviare il debugger \(F5\) di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per avviare automaticamente funzioni di host e test di un servizio implementato.È quindi possibile testare il servizio mediante Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(WcfTestClient.exe\) o un client specifico per trovare e correggere qualsiasi errore potenziale.  
  
## Host servizio WCF  
 Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] enumera i servizi in un progetto di servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], carica la configurazione del progetto e crea un'istanza di un host per ciascun servizio che trova.Lo strumento è integrato in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] tramite il modello Servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e viene richiamato quando si avvia eseguire il debug del progetto.  
  
 Mediante Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], è possibile ospitare un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(in un progetto della libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]\) senza scrivere codice aggiuntivo o eseguire il commit di un host specifico durante lo sviluppo.  
  
> [!NOTE]
>  L'host del servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] non supporta il trust parziale.Se si desidera utilizzare un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in modalità di trust parziale, non utilizzare il modello Progetto Libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per compilare il servizio.Creare invece un nuovo sito Web in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], scegliendo il modello Sito Web servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], che possa ospitare il servizio in un server Web su cui è supportato il trust parziale di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
## Tipi di progetto ospitati da Host servizio WCF  
 Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] può fungere da host per i seguenti tipi di progetto di libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]: Libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], Libreria di servizi flusso di lavoro sequenziale, Libreria di servizi flusso di lavoro macchina a stati e Libreria d servizi con pubblicazione via RSS.Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] può anche fungere da host per i servizi che possono essere aggiunti a un progetto di libreria di servizi mediante la funzionalità **Aggiungi elemento**.Questo include Servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], Servizio macchina a stati WF, Servizio sequenziale WF, Servizio macchina a stati WF XAML Servizio sequenziale WF XAML.  
  
 Tuttavia, è necessario notare che lo strumento non consentirà di configurare un host.Per questa attività, è necessario modificare manualmente il file App.config.Lo strumento non convalida nemmeno i file di configurazione definiti dall'utente.  
  
> [!CAUTION]
>  Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] non deve essere utilizzato per l'hosting di servizi in un ambiente di produzione in quanto non è stato codificato per questo scopo.Servizio host [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] non supporta i requisiti di affidabilità, sicurezza e gestibilità di un tale ambiente.Utilizzare invece IIS in quanto fornisce migliori funzionalità di affidabilità e monitoraggio ed è la soluzione preferita per i servizi di hosting.Dopo avere completato lo sviluppo dei servizi, è necessario eseguirne la migrazione dal Servizio host [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] a IIS.  
  
## Scenari per l'utilizzo di Host servizio WCF in Visual Studio  
 Nella tabella seguente sono elencati tutti i parametri nella finestra di dialogo **Argomenti della riga di comando** che è accessibile facendo clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], selezionando **Proprietà**, quindi la scheda **Debug** e scegliendo **Avvia progetto**.Questi parametri sono utili nella configurazione di Host servizio[!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
|Parametro|Significato|  
|---------------|-----------------|  
|`/client`|Un parametro facoltativo che specifica il percorso di un file eseguibile da eseguire dopo l'hosting dei servizi.Dopo l'hosting viene avviato il Client test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].|  
|`/clientArg`|Consente di specificare una stringa come argomento che viene passato all'applicazione client personalizzata.|  
|`/?`|Visualizza il testo della Guida.|  
  
#### Utilizzo di Client di test WCF  
 Dopo avere creato un nuovo progetto di servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e avere premuto F5 per avviare il debugger, Servizio Host [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] avvia l'hosting di tutti i servizi che trova nel progetto.Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene aperto automaticamente e visualizza un elenco degli endpoint di servizio definiti nel file di configurazione.Dalla finestra principale, è possibile testare i parametri e richiamare il servizio.  
  
 Per garantire che venga utilizzato Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], selezionare **Proprietà**, quindi selezionare la scheda **Debug**.Fare clic su **Avvia progetto** e assicurarsi nella finestra di dialogo **Argomenti della riga di comando** sia visualizzato quanto segue.  
  
 `/client:WcfTestClient.exe`  
  
#### Utilizzo di un client personalizzato  
 Per utilizzare un client personalizzato, fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], selezionare **Proprietà**, quindi selezionare la scheda **Debug**.Scegliere **Avvia progetto** e modificare il parametro `/client` nella finestra di dialogo **Argomenti della riga di comando** per puntare al client personalizzato, come indicato nell'esempio seguente.  
  
 `/client:"path/CustomClient.exe"`  
  
 Quando si preme F5 per avviare nuovamente il servizio, Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] avvia automaticamente il client personalizzato quando si avvia il debugger.  
  
 È anche possibile utilizzare il parametro `/clientArg:` per specificare una stringa come argomento passato all'applicazione client personalizzata, come indicato nell'esempio seguente.  
  
 `/client:"path/CustomClient.exe" /clientArg:"arguments that are passed to Client"`  
  
 Ad esempio, se si utilizza il modello Libreria di servizi di diffusione, sarà possibile utilizzare gli argomenti della riga di comando seguenti:  
  
 `/client:iexplore.exe /clientArgs:http://localhost:8731/Design_Time_Addresses/Feed1/`  
  
#### Specifica nessuno client  
 Per specificare che non verrà utilizzato alcun client dopo l'hosting del servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], selezionare **Proprietà**, quindi selezionare la scheda **Debug**.Scegliere **Avvia progetto** e lasciare vuota la finestra di dialogo **Argomenti della riga di comando**.  
  
#### Utilizzo di un host personalizzato  
 Per utilizzare un host personalizzato, fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], selezionare **Proprietà**, quindi selezionare la scheda **Debug**.Scegliere **Avvia programma esterno** e immettere il percorso completo dell'host personalizzato.È anche possibile utilizzare la finestra di dialogo **Argomenti della riga di comando** per specificare argomenti da passare al host.  
  
## Interfaccia utente dell'Host servizio WCF  
 Quando si richiama inizialmente l'Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(premendo F5 in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]\), viene aperta automaticamente la finestra **Host servizio WCF**.Quando Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è in esecuzione, nell'area della notifica viene visualizzata l'icona del programma.Fare doppio clic sull'icona per aprire la finestra **Host servizio WCF**  
  
 Quando si verificano gli errori durante l'hosting del servizio, verrà aperta la finestra Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per visualizzare informazioni rilevanti.  
  
 La finestra principale **Host servizio WCF** contiene due menu:  
  
-   **File**: contiene i comandi **Chiudi** ed **Esci**.Quando si fa clic **Chiudi**, viene chiusa la finestra di dialogo **Host servizio WCF**, ma prosegue l'hosting dei servizi.Quando si fa clic su **Esci**, viene chiuso anche Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Questo arresta anche tutti i servizi in hosting.  
  
-   **Guida**: contiene il comando **Informazioni su** che visualizza informazioni sulla versione.Contiene anche il comando **Guida** che consente di aprire un file della Guida.  
  
 La finestra principale **Host servizio WCF** contiene due aree:  
  
-   La prima area è **Servizio**.Contiene un elenco che visualizza informazioni di base su tutti i servizi.Le informazioni includono:  
  
    -   **Servizio**: elenca tutti i servizi.  
  
    -   **Stato**: elenca lo stato del servizio.I valori validi sono "Avviato", "Arrestato" ed "Errore."  
  
    -   **Indirizzo metadati**: visualizza l'indirizzo dei metadati dei servizi.  
  
-   La seconda area è **Informazioni aggiuntive**.Visualizza una spiegazione dettagliata dello stato del servizio quando la riga del servizio specifica è selezionata nell'area **Servizio**.Se lo stato è Errore, è possibile visualizzare il messaggio di errore completo sullo schermo.  
  
## Interruzione dell'Host servizio WCF  
 È possibile arrestare Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] nei quattro modi seguenti:  
  
-   Arrestare la sessione di debug in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
-   Selezionare **Esci** dal menu **File** nella finestra **Host servizio WCF**.  
  
-   Selezionare **Esci** dal menu di scelta rapida dell'icona della barra delle applicazioni Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] nell'area di notifica del sistema.  
  
-   Uscire da Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] se è utilizzato.  
  
## Utilizzo di Host servizio senza privilegio di amministratore  
 Per consentire agli utenti senza privilegio di amministratore di sviluppare servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], viene creato un ACL \(Elenco di controllo di accesso\) per lo spazio dei nomi "http:\/\/\+:8731\/Design\_Time\_Addresses" durante l'installazione di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].L'ACL viene impostato su \(UI\) che include tutti gli utenti interattivi che hanno eseguito l'accesso al computer.Gli amministratori possono aggiungere o rimuovere utenti da questo ACL oppure aprire porte aggiuntive. Questo ACL consente agli utenti di utilizzare Host automatico servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(wcfSvcHost.exe\) senza disporre dei privilegi di amministratore.  
  
 È anche possibile modificare l'accesso utilizzando lo strumento netsh.exe in [!INCLUDE[wv](../../../includes/wv-md.md)] con l'account di amministratore con privilegi elevati.Di seguito è riportato un esempio dell'utilizzo di netsh.exe.  
  
```  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 Per ulteriori informazioni su netsh.exe, vedere la pagina relativa alle[modalità di utilizzo dello strumento Netsh.exe e delle relative opzioni della riga di comando](http://go.microsoft.com/fwlink/?LinkId=97877)".  
  
## Vedere anche  
 [Client di test WCF \(WcfTestClient.exe\)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)