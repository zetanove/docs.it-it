---
title: "Strumento Visualizzatore di tracce dei servizi (SvcTraceViewer.exe) | Microsoft Docs"
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
ms.assetid: 9027efd3-df8d-47ed-8bcd-f53d55ed803c
caps.latest.revision: 55
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 55
---
# Strumento Visualizzatore di tracce dei servizi (SvcTraceViewer.exe)
Lo strumento Visualizzatore di tracce dei servizi [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] consente di analizzare le tracce di diagnostica create da [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Il Visualizzatore di tracce dei servizi offre funzionalità per unire, visualizzare e filtrare facilmente i messaggi di traccia nel log che consentono di diagnosticare, risolvere e controllare i problemi relativi ai servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
## Configurazione delle funzionalità di traccia  
 Le tracce di diagnostica forniscono informazioni che mostrano quello si sta verificando in tutta l'operazione dell'applicazione.Come si intuisce dal nome, è possibile seguire le operazioni dall'origine alla destinazione e tramite punti intermedi.  
  
 È possibile configurare la funzionalità di traccia utilizzando il file di configurazione dell'applicazione, Web.config per applicazioni ospitate sul Web o *Appname*.config per applicazioni indipendenti.Di seguito è riportato un esempio:  
  
```  
<system.diagnostics>  
    <trace autoflush="true" />  
    <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
            <listeners>  
               <add name="sdt"   
                   type="System.Diagnostics.XmlWriterTraceListener"   
                   initializeData= "SdrConfigExample.e2e" />  
            </listeners>  
         </source>  
    </sources>  
</system.diagnostics>  
  
```  
  
 In questo esempio vengono specificati il nome e il tipo del listener di traccia.Il listener viene denominato `sdt` e come tipo viene aggiunto il listener di traccia standard di .NET Framework, ovvero System.Diagnostics.XmlWriterTraceListener.Viene utilizzato l'attributo `initializeData` per impostare il nome del file di log del listener su `SdrConfigExample.e2e`.Per il file di log è possibile sostituire un percorso completo con un semplice nome file.  
  
 In questo esempio viene creato un file nella directory radice denominato SdrConfigExample.e2e.Quando si utilizza il visualizzatore di tracce per aprire il file come descritto nella sezione “Apertura e visualizzazione di file di traccia WCF”, è possibile visualizzare tutti i messaggi che sono stati inviati.  
  
 Il livello di traccia viene controllato in base all'impostazione `switchValue`.Nella tabella seguente viene fornita una descrizione dei livelli di traccia disponibili.  
  
|Livello di traccia|Descrizione|  
|------------------------|-----------------|  
|Critico|-   Registra voci del registro eventi e Fail\-Fast e informazioni sulla correlazione tra tracce.Di seguito sono indicati alcuni esempi di quando è possibile utilizzare il livello Critico:<br />-   AppDomain non disponibile a causa di un'eccezione non gestita.<br />-   Impossibile avviare l’applicazione.<br />-   Il messaggio che ha causato l’errore ha origine nel processo MyApp.exe.|  
|Errore|-   Registra tutte le eccezioni.È possibile utilizzare il Livello di errore nei casi seguenti:<br />-   Si è verificato l’arresto anomalo del codice a causa di un’eccezione di cast non valido.<br />-   Avvio dell’applicazione non riuscito a causa dell’eccezione “impossibile creare l’endpoint”.|  
|Avviso|-   È stata rilevata una condizione che in seguito può dare luogo a un errore standard o critico.È possibile utilizzare questo livello nei casi seguenti:<br />-   L'applicazione riceve più richieste di quanto sia consentito dalle impostazioni di limitazione.<br />-   La coda di ricezione ha raggiunto il 98 percento della capacità massima configurata.|  
|Info|-   Il sistema genera messaggi informativi che semplificano il monitoraggio e la diagnosi dello stato di sistema, la valutazione delle prestazioni o il profiling.È possibile utilizzare queste informazioni durante la pianificazione delle capacità e la gestione delle prestazioni.È possibile utilizzare questo livello nei casi seguenti:<br />-   Errore dopo che il messaggio ha raggiunto l'AppDomain ed è stato deserializzato.<br />-   Errore durante la creazione dell'associazione HTTP.|  
|Dettagliata|-   Traccia a livello di debug per codice utente e manutenzione.Impostare questo livello quando:<br />-   non si sa con certezza quale metodo nel codice è stato chiamato quando si è verificato l'errore.<br />-   È stato configurato un endpoint errato ed è stato impossibile avviare il servizio perché la voce nell'archivio prenotazioni è bloccata.|  
|ActivityTracing|Eventi di flusso tra attività di elaborazione e componenti.<br /><br /> Questo livello consente ad amministratori e sviluppatori di mettere in correlazione applicazioni nello stesso dominio applicazione.<br /><br /> -   Tracce per limiti di attività: avvio\/interruzione.<br />-   Tracce per trasferimenti.|  
  
 È possibile utilizzare l'istruzione `add` per specificare il nome e il tipo del listener di traccia da utilizzare.Nella configurazione dell'esempio il listener viene denominato `sdt` e come tipo viene aggiunto il listener di traccia standard di .NET Framework, ovvero `System.Diagnostics.XmlWriterTraceListener`.Utilizzare l'istruzione `initializeData` per impostare il nome del file di log del Listener.È inoltre possibile sostituire un percorso completo con un semplice nome file.  
  
## Utilizzo dello strumento Visualizzatore di tracce dei servizi  
  
### Apertura e visualizzazione di file di traccia WCF  
 Il Visualizzatore di tracce dei servizi supporta tre tipi di file:  
  
-   [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] File di traccia, con estensione .svcLog  
  
-   File di traccia eventi, con estensione etl  
  
-   File di traccia Crimson  
  
 Mediante lo strumento Visualizzatore di tracce dei servizi è possibile aprire i file di traccia supportati, aggiungere e integrare file aggiuntivi e aprire e unire simultaneamente un gruppo di file di traccia.  
  
##### Per aprire un file di traccia  
  
1.  Avviare lo strumento Visualizzatore di tracce dei servizi. A tale scopo, utilizzare una finestra di commando per passare al percorso di installazione [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(C:\\Program Files\\Microsoft SDKs\\Windows\\v6.0\\Bin\) e quindi digitare `SvcTraceViewer.exe`.  
  
> [!NOTE]
>  Lo strumento Visualizzatore di tracce dei servizi può essere associato a due tipi di file: svclog e stvproj.Per eseguire e annullare la registrazione delle estensioni di file è possibile utilizzare due parametri nella riga di comando.  
>   
>  \/register: consente di registrare l'associazione delle estensioni di file "svclog" e "stvproj" a SvcTraceViewer.exe  
>   
>  \/unregister: consente di annullare la registrazione dell'associazione delle estensioni di file "svclog" e "stvproj" a SvcTraceViewer.exe  
  
1.  All'avvio dello strumento Visualizzatore di tracce dei servizi, scegliere **Apri** dal menu **File**.Passare al percorso in cui sono archiviati i file di traccia.  
  
2.  Fare doppio clic sul file di traccia che si desidera aprire.  
  
    > [!NOTE]
    >  Premere MAIUSC mentre si fa clic su più file di traccia per selezionarli e aprirli simultaneamente.Lo strumento Visualizzatore di tracce dei servizi consente di unire e visualizzare il contenuto di tutti i file in una visualizzazione unificata.È ad esempio possibile aprire i file di traccia sia del client sia del servizio.Ciò è utile quando nella configurazione sono state abilitate le funzionalità di registrazione dei messaggi e di propagazione delle attività.In questo caso la visualizzazione unificata dei contenuti dei file consente infatti di analizzare lo scambio dei messaggi fra client e servizio.È inoltre possibile trascinare più file nel visualizzatore, oppure utilizzare la scheda **Progetto**.Per ulteriori dettagli, vedere la sezione riguardante la gestione dei progetti.  
  
3.  Per aggiungere ulteriori file di traccia alla raccolta aperta, fare clic su **File** e quindi scegliere **Aggiungi**.Nella finestra visualizzata, spostarsi al percorso dei file di traccia e fare doppio clic sul file che si desidera aggiungere.  
  
> [!CAUTION]
>  Non è consigliabile caricare un file di log di traccia di dimensioni superiori a 200 MB.Se si tenta di caricare un file di dimensioni superiori, il processo di caricamento può richiedere molto tempo, a seconda delle risorse del computer.Lo strumento Visualizzatore di tracce dei servizi può non rispondere per molto tempo o può esaurire la memoria del computer.Per evitare che ciò avvenga, è consigliabile configurare la funzionalità di caricamento parziale.Per ulteriori informazioni su questa procedura, vedere la sezione "Caricamento di file di traccia di grandi dimensioni”.  
  
#### Formati di traccia eventi e di traccia Crimson  
 Il formato nativo del visualizzatore è il formato di traccia di attività generato da [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Le tracce generate in un altro formato devono essere convertite affinché il visualizzatore sia in grado di leggerle.Attualmente, oltre al formato di traccia delle attività, il visualizzatore supporta i formati di traccia eventi e di traccia Crimson.  
  
 Quando si apre un file che non contiene tracce di attività, il visualizzatore prova a convertirlo.Occorre quindi specificare il nome e il percorso del file in cui salvare i dati di traccia convertiti.Dopo aver eseguito la conversione dei dati, il visualizzatore mostra il contenuto del nuovo file.  
  
> [!NOTE]
>  Al termine della conversione, i dati di traccia convertiti vengono salvati nel disco rigido.Prima di avviare la conversione è pertanto necessario verificare che lo spazio disponibile sul disco sia sufficiente a contenere tali dati.In caso contrario, la conversione avrà esito negativo.  
  
### Gestione di progetti  
 Per visualizzare simultaneamente più file di traccia è possibile utilizzare la funzionalità di gestione di progetti del visualizzatore.Se ad esempio si dispone del file di traccia di un client e del file di traccia di un servizio, è possibile aggiungerli a un progetto.Ogni volta che si apre il progetto, tutti i relativi file di traccia verranno quindi caricati simultaneamente.  
  
 Esistono due modalità per gestire i progetti:  
  
-   dal menu **File** è possibile aprire, salvare e chiudere progetti.  
  
-   Nella scheda **Progetto** è possibile aggiungere file a un progetto.  
  
### Visualizzazione di tracce WCF  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] genera tracce utilizzando il formato di traccia di attività.Nel modello delle tracce delle attività, le singole tracce vengono raggruppate in attività in base al loro scopo.Il flusso di controllo logico viene trasferito tra le attività.Durante il periodo di attività di un'applicazione, ad esempio, iniziano e terminano molte attività di trasmissione di messaggi.Per ulteriori informazioni sulla visualizzazione di tracce e attività e sull'interfaccia utente del Visualizzatore di tracce dei servizi, vedere [Utilizzo di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
#### Passaggio a una visualizzazione specifica  
 Nel Visualizzatore di tracce dei servizi sono disponibili le visualizzazioni distinte seguenti,disponibili come schede nel riquadro sinistro dello strumento. Tali schede, accessibili anche dal menu **Visualizza**, sono:  
  
-   Visualizzazione Attività  
  
-   Visualizzazione Progetto  
  
-   Visualizzazione Messaggio  
  
-   Visualizzazione Grafico  
  
##### Visualizzazione Attività  
 Dopo aver aperto i file di traccia, nella finestra **Attività** del riquadro a sinistra vengono visualizzate le tracce raggruppate per attività.  
  
 Nella visualizzazione **Attività** vengono riportati I nomi delle attività, il numero di trace contenute nell’attività, la durata nonché l’ora di inizio e fine.  
  
 Se si fa clic su una delle attività elencate, nel riquadro delle tracce a destra vengono visualizzate le tracce contenute in tale attività.È quindi possibile selezionare una traccia per visualizzarne i dettagli.  
  
 Per selezionare più attività è possibile premere **CTRL** o **MAIUSC** e quindi fare clic sulle attività desiderate.Nel riquadro delle tracce vengono visualizzate tutte le tracce contenute nelle attività selezionate.  
  
 Per visualizzare un'attività nella visualizzazione **Grafico**, fare doppio clic su di essa.In alternativa, selezionare un'attività e passare alla visualizzazione **Grafico**.  
  
> [!NOTE]
>  L'attività “000000000000” è un'attività speciale che non può essere visualizzata nella visualizzazione Grafico.Poiché a tale attività sono collegate tutte le altre attività, la visualizzazione di questa attività comporta una notevole riduzione delle prestazioni.  
  
 Per ordinare l'elenco delle attività è possibile fare clic sul titolo della colonna.Le attività che contengono tracce di avviso presentano uno sfondo giallo, mentre quelle che contengono tracce di errore presentano uno sfondo rosso.  
  
 Esistono tre tipi distinti di attività, ognuno di essi caratterizzato da un'icona visualizzata a sinistra di ogni attività.Per conoscere il significato delle icone, consultare la sezione relativa alla descrizione delle icone di traccia.  
  
##### Visualizzazione Progetto  
 Questa visualizzazione consente di gestire i file di traccia del progetto corrente.Per ulteriori dettagli, vedere la sezione riguardante la gestione dei progetti.  
  
##### Visualizzazione Grafico  
 Una delle funzionalità più potenti dello strumento Visualizzatore di tracce dei servizi è la visualizzazione **Grafico**, in cui i dati di traccia di una determinata attività sono presentati sotto forma di grafico.Questo tipo di visualizzazione consente di esaminare l'esecuzione sequenziale dei passaggi degli eventi e le interrelazioni tra più attività dovute allo spostamento di dati fra tali file.  
  
 Per passare alla visualizzazione **Grafico**, selezionare un'attività nella visualizzazione **Attività**. Fare quindi clic sulla scheda **Attività** o su una traccia del log dei messaggi riportata nella visualizzazione **Messaggio**.Se sono stati caricati più file di traccia e l'attività contiene tracce ricavate da più di un file, tutte le tracce attinenti sono visualizzate nella visualizzazione **Grafico**.Per accedere alla visualizzazione **Grafico** è inoltre possibile fare doppio clic sulle attività e sulle tracce del log dei messaggi.  
  
 Nella visualizzazione **Grafico** ogni colonna verticale rappresenta un'attività e ogni blocco di una determinata colonna rappresenta una traccia.Le attività sono raggruppate per processo \(o thread\).Le frecce piccole tra le attività rappresentano i trasferimenti.Le frecce grandi tra i processi rappresentano lo scambio di messaggi.L'attività attualmente selezionata è sempre visualizzata in giallo.  
  
###### Selezione di Tracce nel Grafico  
  
1.  Fare clic su un blocco del grafico.  
  
2.  Utilizzare i tasti SU e GIÙ per selezionare le tracce adiacenti.  
  
3.  Osservare le informazioni di traccia riportate nel Riquadro delle tracce e nel Riquadro dettagli.  
  
###### Espansione o compressione dei trasferimenti delle attività  
 Quando l'attività attualmente selezionata trasferisce l'esecuzione a un'altra attività è possibile espandere i trasferimenti delle attività.Ciò consente di seguire i trasferimenti.  
  
 Per espandere o comprimere i trasferimenti delle attività,  
  
1.  individuare la traccia di trasferimento contrassegnata da un segno "\+" a sinistra dell'icona di trasferimento.  
  
2.  Fare clic su "\+" oppure premere **CTRL** e "\+".  
  
3.  Nel grafico verrà visualizzata l'attività successiva.  
  
4.  A sinistra dell'icona di trasferimento verrà visualizzato un segno "\-".Fare clic sul segno "\-" o premere CTRL e "\-" per comprimere il trasferimento dell'attività.  
  
> [!NOTE]
>  Quando esistono più trasferimenti verso una determinata attività e si espande uno di essi, il sistema visualizza le attività che portano alla nuova attività a partire dall'attività radice.Queste nuove attività sono visualizzate in forma compressa.Per esaminare i dettagli di queste attività è possibile espanderle verticalmente facendo clic sull'icona di espansione posta nell'intestazione del grafico.  
  
###### Espansione o compressione verticale delle attività  
 Al fine di nascondere i dettagli superflui, il visualizzatore consente di comprimere le attività riportate nel grafico delle attività.Quando un'attività è compressa, le tracce specifiche in essa contenute non vengono visualizzate.Vengono riportati soltanto i trasferimenti di traccia.Per visualizzare tutte le tracce di un'attività è possibile espandere verticalmente l'attività. A tale scopo, fare clic sul simbolo di espansione dell'attività posto nell'intestazione del grafico.  
  
 Per espandere o comprimere verticalmente le attività  
  
1.  Per espandere verticalmente un'attività, fare clic sull'icona "\+" visualizzata nell'intestazione dell'attività.  
  
2.  Si noti che nel grafico vengono visualizzate tutte le tracce.  
  
3.  Per comprimere verticalmente un'attività, fare clic sull'icona "\-" visualizzata nell'intestazione dell'attività.  
  
4.  Si noti che nell'attività sono riportati solo i trasferimenti, i log dei messaggi, le tracce di avviso e di eccezione di maggiore importanza.  
  
###### Opzioni  
 Nel menu **Opzione** della visualizzazione Grafico è possibile selezionare due opzioni.  
  
-   Mostra tracce del limite delle attività. Tale opzione, se deselezionata, consente di escludere dal grafico le tracce di limite attività.  
  
-   Mostra tracce dettagliate che non appartengono a messaggi. Tale opzione, se deselezionata, consente di escludere dal grafico le tracce di livello dettagliato, tranne nel caso di tracce di messaggio.Nella maggior parte dei casi le tracce di livello dettagliato sono meno importanti ai fini dell'analisi.Questa opzione è utile quando non si desidera analizzare le tracce di livello dettagliato al fine di concentrarsi esclusivamente sulle tracce più importanti.  
  
###### Modalità di layout  
 Il visualizzatore presenta due modalità di layout: **Processo** e **Thread**.Questa impostazione definisce l'unità massima di organizzazione.La modalità di layout predefinita è **Processo**, in cui le attività riportate nel grafico sono raggruppate per processo.  
  
###### Elenco di esecuzione  
 In questo elenco a discesa è possibile selezionare quale processo o thread visualizzare nel grafico.Se ad esempio sono stati aperti i file di traccia di un servizio e di due client \(A e B\), per visualizzare nel grafico solo il servizio e il client A è possibile deselezionare nell'elenco il client B.  
  
#### Visualizzazione dei dettagli di una traccia  
 Per visualizzare i dettagli di una traccia, selezionarla nel riquadro delle tracce.I dettagli vengono riportati nel Riquadro dettagli.  
  
##### Riquadro delle tracce  
 Il riquadro nell'angolo superiore destro del Visualizzatore di tracce dei servici è il riquadro delle tracce.In questo riquadro sono elencate tutte le tracce contenute nell'attività selezionata, insieme alle relative informazioni aggiuntive, ad esempio livello di traccia, ID del thread e nome del processo.  
  
 Il codice XML non elaborato della traccia può essere copiato negli Appunti. A tale fine, fare clic con il pulsante destro del mouse su una traccia e selezionare l'opzione **Copia la traccia negli Appunti**.  
  
##### Riquadro dettagli  
 Il riquadro nell'angolo inferiore sinistro del Visualizzatore di tracce dei servizi è il Riquadro dettagli.Questo riquadro presenta tre schede che consentono di visualizzare i dettagli di una traccia.  
  
 Nella visualizzazione **Formattato** le informazioni sono presentate in modo più organizzato.Tutti gli elementi XML noti vengono elencati in tabelle e strutture ad albero, semplificando la lettura e la comprensione delle informazioni.  
  
 Nella visualizzazione **XML** viene presentato il codice XML corrispondente alla traccia selezionata.Tale visualizzazione supporta l'evidenziazione e l'utilizzo dei colori per la sintassi.Quando si utilizza la funzione di ricerca delle stringhe **Trova**, i risultati della ricerca vengono evidenziati.  
  
 Nella visualizzazione **Messaggio** viene riportata la parte di messaggio del codice XML contenuta nelle tracce del log dei messaggi.Tale visualizzazione è visibile solo quando si seleziona una traccia di messaggio.  
  
### Filtro delle tracce WCF  
 Per semplificare l'analisi dei file di traccia è possibile filtrarli nei modi seguenti:  
  
-   la barra degli strumenti di filtro consente di accedere ai filtri predefiniti e personalizzati.Tale barra può essere abilitata tramite il menu **Visualizza**.  
  
-   Il filtro predefinito del visualizzatore può essere utilizzato per filtrare in modo selettivo le tracce [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Per impostazione predefinita, tale filtro è impostato in modo da consentire il passaggio di tutte le tracce dell'infrastruttura.Le impostazioni di questo filtro possono essere definite nel sottomenu **Opzioni filtro** del menu **Visualizza**.  
  
-   I filtri XPath personalizzati consentono agli utenti di avere il controllo completo sull'applicazione dei filtri.I filtri possono essere definiti nel menu **Filtro personalizzato** alla voce **Visualizza**.  
  
 Vengono visualizzate solo le tracce che passano attraverso tutti i filtri attivi.  
  
#### Utilizzo della barra degli strumenti di filtro  
 La barra degli strumenti di filtro si trova nella parte superiore dello strumento.Se non è presente, è possibile attivarla nel menu **Visualizza**.La barra è costituita da tre componenti:  
  
-   Cerca: il campo **Cerca** consente di definire l'oggetto da ricercare nell'operazione di filtro.Se ad esempio si desidera individuare tutte le tracce generate nel contesto del processo X, impostare questo campo su X e il campo **Cerca in** su "Nome processo".Quando si sceglie un filtro basato su tempo, questo campo diventa un controllo di selezione Datetime.  
  
-   Cerca in: questo campo definisce il tipo di filtro da applicare.  
  
-   Livello: questa impostazione definisce il livello minimo di traccia consentito dal filtro.Ad esempio, se il livello è impostato su Errore e successivi, consente di visualizzare soltanto le tracce di livello Errore e Critico.I criteri di questo filtro vengono applicati insieme ai criteri specificati in Cerca e Cerca in.  
  
 Il pulsante **Filtra ora** consente di avviare l'operazione di filtro.L'applicazione di alcuni filtri, specialmente quando riguarda set di dati di grandi dimensioni, richiede molto tempo.Per annullare l'operazione di filtro è possibile fare clic sul pulsante **Interrompi** visualizzato nella barra di stato del menu **Operazioni**.  
  
 Il pulsante **Cancella** consente di reimpostare i filtri predefiniti e standard in modo da consentire il passaggio di tutte le tracce.  
  
#### Opzioni di filtro  
 Il visualizzatore è in grado di rimuovere automaticamente dalla visualizzazione le tracce [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].La rimozione può riguardare in modo selettivo le tracce generate da aree specifiche di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], ad esempio le tracce relative alle transazioni.  
  
 Le impostazioni di questo filtro possono essere definite nel sottomenu **Opzioni filtro** del menu **Visualizza**.  
  
#### Filtri personalizzati  
 Se si ha familiarità con il linguaggio Xpath \(XML Path\) è possibile utilizzarlo per creare filtri personalizzati finalizzati alla ricerca di dati di traccia correlati a qualsiasi elemento XML di interesse.I filtri sono accessibili tramite la barra degli strumenti di filtro.  
  
 I filtri personalizzati possono includere parametri.È inoltre possibile importare filtri personalizzati già esistenti.  
  
##### Creazione di un filtro personalizzato  
 I filtri possono essere creati in due modi:  
  
###### Creazione di un filtro personalizzato tramite la Creazione guidata modelli  
 È possibile fare clic su una traccia esistente e creare un filtro basato sulla struttura della traccia.Questo esempio illustra la creazione di un filtro personalizzato basato sull'ID del thread.  
  
1.  Nel riquadro di traccia che si trova nella parte superiore destra del visualizzatore, selezionare la traccia contenente l'elemento su cui si desidera basare il filtro.  
  
2.  Fare clic sul pulsante **Crea filtro personalizzato** nella parte superiore del riquadro della traccia.  
  
3.  Nella finestra di dialogo visualizzata, immettere il nome del filtro.In questo esempio, digitare `ID thread`.È inoltre possibile fornire una descrizione del filtro.  
  
4.  Nella struttura ad albero a sinistra viene visualizzata la struttura del record di traccia selezionato nel passaggio 1.Passare all'elemento per il quale si desidera creare una condizione.In questo esempio, passare all'elemento ThreadID che si trova nel nodo XPath: \/E2ETraceEvent\/System\/Execution\/@ThreadID.Fare doppio clic sull'attributo ThreadID contenuto nella visualizzazione struttura ad albero.Nella parte destra della finestra di dialogo viene creata un'espressione per l'attributo.  
  
5.  Impostare il parametro relativo alla condizione di ThreadID su "{0}".Questo passaggio fa in modo che il valore ThreadID venga configurato quando il filtro viene applicato.Per ulteriori informazioni, consultare la sezione relativa all'applicazione dei filtri. È possibile definire fino a quattro parametri.Le condizioni vengono combinate mediante l'operatore OR.  
  
6.  Fare clic su **OK** per creare il filtro.  
  
> [!NOTE]
>  I filtri creati tramite la Creazione guidata modelli possono essere modificati solo manualmente.Questa procedura guidata non può essere utilizzata su un filtro già esistente.Inoltre, se si utilizza la Creazione guidata modelli per creare un filtro Xpath, le condizioni di tale filtro vengono combinate tramite l'operatore OR.Di conseguenza, se si desidera impostare un operatore AND, l'espressione del filtro deve essere modificata manualmente.  
  
###### Creazione manuale di un filtro personalizzato  
 Il menu Filtri Personalizzati consente di immettere filtri XPath manualmente.  
  
1.  Scegliere **Filtri personalizzati** dal menu Visualizza.  
  
2.  Nella finestra di dialogo visualizzata, fare clic su **Nuovo**.  
  
3.  Specificare almeno il nome e un'espressione Xpath del filtro.  
  
4.  Scegliere **OK**.  
  
###### Applicazione di un filtro personalizzato  
 Una volta creato un filtro personalizzato, tale filtro è accessibile tramite la barra degli strumenti di filtro.Selezionare il filtro che si desidera applicare nel campo **Cerca in** della barra degli strumenti di filtro.Per utilizzare l'esempio precedente, selezionare "ID thread".  
  
1.  Specificare nel campo **Trova** il valore che si desidera trovare.In questo esempio, immettere l'ID del thread da individuare.  
  
2.  Fare clic su **Filtra ora** ed esaminare il risultato dell'operazione.  
  
 Se il filtro da applicare prevede più parametri, immetterli nel campo **Trova** utilizzando ";" come separatore.Ad esempio, nella stringa seguente sono definiti 3 parametri: "1;findValue;text".Il visualizzatore applica "1" al parametro {0} del filtro,mentre "findValue" e "text" sono applicati rispettivamente ai parametri {1} e {2} del filtro.  
  
###### Condivisione di filtri personalizzati  
 I filtri personalizzati possono essere condivisi tra sessioni diverse e utenti diversi.È possibile esportare i filtri in un file di definizione e quindi importare questo file in un altro percorso.  
  
 Per importare un filtro personalizzato:  
  
1.  scegliere **Filtri personalizzati** dal menu **Visualizza**.  
  
2.  Nella finestra di dialogo visualizzata, fare clic sul pulsante **Importa**.  
  
3.  Passare al file del filtro personalizzato \(con estensione stvcf\), fare clic su di esso e quindi sul pulsante **Apri**.  
  
 Per esportare un filtro personalizzato:  
  
1.  scegliere **Filtri personalizzati** dal menu Visualizza.  
  
2.  Nella finestra di dialogo visualizzata, selezionare il filtro che si desidera esportare.  
  
3.  Fare clic sul pulsante **Esporta**.  
  
4.  Specificare il nome e il percorso del file di definizione del filtro personalizzato \(con estensione stvcf\) e quindi fare clic su **Salva**.  
  
> [!NOTE]
>  Questi filtri personalizzati possono essere importati ed esportati solo tramite lo strumento Visualizzatore di tracce dei servizie non possono essere letti con altri strumenti.  
  
### Ricerca dei dati  
 Il visualizzatore offre le modalità seguenti per la ricerca dei dati:  
  
-   La barra degli strumenti Trova consente di accedere rapidamente alle opzioni di ricerca più comuni.  
  
-   La finestra di dialogo Trova offre ulteriori opzioni di ricerca.Tale finestra è accessibile dal menu **Modifica** o mediante la combinazione di tasti CTRL\+F.  
  
 La barra degli strumenti Trova si trova nella parte superiore del visualizzatore.Se non è presente, è possibile attivarla nel menu **Visualizza**.La barra è costituita da due componenti:  
  
-   Trova: consente di immettere una parola chiave di ricerca.  
  
-   Cerca in: consente di definire l'ambito di ricerca.È possibile scegliere se eseguire la ricerca in tutte le attività o soltanto nell'attività corrente.  
  
 Nella finestra di dialogo Trova sono disponibili altre due opzioni:  
  
-   Trova destinazione:  
  
    -   L'opzione "Dati del registro non elaborati" esegue una ricerca della parola chiave in tutti i dati non elaborati.  
  
    -   Le opzioni "Nel testo XML" e "Nell'attributo XML" consentono di eseguire la ricerca soltanto negli elementi XML.  
  
    -   Se si sceglie l'opzione "Messaggio registrato" la ricerca della parola chiave viene eseguita soltanto nei messaggi.  
  
-   Ignora attività radice: la ricerca ignora le tracce dell'attività "000000000000".Ciò consente di migliorare le prestazioni nei file di traccia di grandi dimensioni quando l'attività radice presenta migliaia di tracce, per lo più relative a trasferimenti.  
  
### Esplorazione delle tracce  
 Poiché le tracce vengono registrate in sequenza durante la fase di esecuzione dell'applicazione, l'esplorazione delle tracce può agevolarne il debug.Il Visualizzatore di tracce dei servizi offre varie opzioni di esplorazione delle tracce.  
  
#### Passo avanti o Passo indietro  
 Se si considera ogni traccia come una riga di codice di un programma, il passaggio alla traccia successiva è molto simile alla funzione "Esegui istruzione\/routine" dell'ambiente di sviluppo integrato \(IDE\) di Visual Studio.A differenza di tale funzione, tuttavia, è inoltre possibile passare alla traccia precedente.Queste opzioni consentono di passare alla traccia successiva o precedente dell'attività.  
  
-   Passo avanti: utilizzare il menu **Attività** o premere "F10".È inoltre possibile utilizzare il tasto di direzione "GIÙ" nel riquadro delle tracce.  
  
-   Passo indietro: utilizzare il menu **Attività** o premere "F9".È inoltre possibile utilizzare il tasto di direzione "SU" nel riquadro delle tracce.  
  
> [!NOTE]
>  In questo modo è possibile accedere a un'attività che si verifica in un processo diverso o anche in un computer diverso, dato che i messaggi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] possono contenere ID attività validi su più computer.  
  
#### Trasferimento successivo  
 Le tracce di trasferimento sono tracce speciali del file di tracciache descrivono il trasferimento dell'esecuzione da un'attività a un'altra.Si supponga ad esempio che l'attività A trasferisca l'esecuzione all'attività B.In questo caso nell'attività A viene creata una traccia di trasferimento denominata "A: Attività" insieme alla relativa icona di trasferimento.Questa traccia di trasferimento è un collegamento tra le due tracce.È inoltre possibile che alla fine dell'attività B venga creata un'altra traccia di trasferimento che descrive la restituzione dell'esecuzione all'attività A.Questo funzionamento è simile alle chiamate di funzione dei programmi: A chiama B e quindi B restituisce il risultato.  
  
 Analogamente alla funzione "Esegui istruzione" di un debugger, questa opzioneconsente di seguire il trasferimento dell'esecuzione da A a B,senza influire sulle altre tracce.  
  
 Esistono due modalità per eseguire questo tipo di esplorazione: tramite mouse o mediante tastiera.  
  
-   Tramite mouse: fare doppio clic sulla traccia di trasferimento nel riquadro delle tracce.  
  
-   Mediante tastiera: selezionare una traccia di trasferimento e, nel menu **Attività**, scegliere "Trasferimento successivo". In alternativa, premere "F11"  
  
> [!NOTE]
>  In molti casi, quando l'attività A trasferisce l'esecuzione all'attività B, l'attività A attende che l'attività B restituisca l'esecuzione.Di conseguenza, durante la registrazione di traccia dell'attività B, per l'attività A non viene eseguita alcuna registrazione di traccia.Tuttavia, è anche possibile che l'attività A non attenda l'attività B. In questo caso la registrazione di traccia dell'attività A continua normalmente.Un'altra possibilità è che l'attività B non restituisca l'esecuzione all'attività A.Ciò rappresenta una differenza rispetto alle chiamate di funzione.I trasferimenti fra le attività risultano più comprensibili se esaminati nella visualizzazione Grafico.  
  
#### Vai al trasferimento successivo o Vai al trasferimento precedente  
 Durante l'analisi dell'attività corrente o delle attività selezionate, quando vengono selezionate più attività, può essere utile individuare rapidamente le attività a cui viene trasferita l'esecuzione.L'opzione "Vai al trasferimento successivo" consente di individuare la traccia di trasferimento successiva dell'attività.Dopo aver trovato la traccia di trasferimento è possibile utilizzare l'opzione "Trasferimento successivo" per passare all'attività successiva.  
  
-   Vai al trasferimento successivo: utilizzare il menu **Attività** o premere "CTRL\+F10".  
  
-   Vai al trasferimento precedente: utilizzare il menu **Attività** o premere "CTRL\+F9".  
  
#### Esplorazione tramite la visualizzazione Grafico  
 Anche se la navigazione nel riquadro delle attività e nel riquadro delle tracce è simile all'esecuzione del debug, l'utilizzo della visualizzazione **Grafico** consente di migliorare notevolmente la navigazione.Per ulteriori informazioni, vedere la sezione “Visualizzazione grafico”.  
  
### Caricamento dei file di traccia di grandi dimensioni  
 I file di traccia possono essere di dimensioni notevoli.Se ad esempio si attiva la funzione tracce di livello "Dettagliato", un file di traccia riguardante un'esecuzione di pochi minuti può presentare dimensioni di centinaia di MB o più, a seconda della velocità di rete e del modello di comunicazione.  
  
 L'apertura di un file di traccia di grandi dimensioni nello strumento Visualizzatore di tracce dei servizi può comportare una riduzione delle prestazioni.È possibile che il caricamento risulti lento e che il tempo di risposta dopo il caricamento sia elevato.La velocità effettiva varia da caso a caso e dipende della configurazione hardware del sistema in uso.Nella maggior parte dei PC, il caricamento di un file di traccia più grande di 200 MB comporta una notevole riduzione delle prestazioni.Se il file di traccia presenta dimensioni superiori a 1 GB, è possibile che lo strumento utilizzi tutta la memoria disponibile o che risulti bloccato per un periodo di tempo molto lungo.  
  
 Per evitare problemi durante l'analisi di file di traccia di grandi dimensioni, nello strumento Visualizzatore di tracce dei servizi è disponibile una funzionalità di caricamento parziale dei file di traccia.Si supponga ad esempio di disporre di un file di oltre 1 GB relativo a una traccia in esecuzione sul server da diversi giorni.In questo caso, qualora si verifichino errori, non è necessario aprire l'intero file di traccia.È invece possibile caricare soltanto le tracce relative all'intervallo di tempo in cui si ritiene che si siano verificati gli errori.Poiché l'ambito è ridotto, lo strumento Visualizzatore di tracce dei servizi può caricare il file più velocemente. L'identificazione degli errori può quindi essere svolta a partire da un set minore di dati.  
  
#### Abilitazione della funzionalità di caricamento parziale  
 La funzionalità di caricamento parziale non richiede l'abilitazione manuale.Se si tenta di caricare un set di file di traccia le cui dimensioni complessive sono maggiori di 40 MB, nello strumento Visualizzatore di tracce dei servizi viene aperta automaticamente una finestra di dialogo in cui è possibile selezionare la parte che si desidera caricare.  
  
> [!NOTE]
>  Poiché è possibile che le tracce non siano distribuite uniformemente nell'intervallo di tempo, l'ampiezza del periodo di tempo che si specifica nella barra degli strumenti della funzionalità di caricamento parziale potrebbe non essere proporzionale alle dimensioni di caricamento visualizzate.Le dimensioni di caricamento effettive possono essere minori rispetto alla stima visualizzata nella finestra di dialogo della funzionalità di caricamento parziale.  
  
#### Impostazione dell'intervallo di tempo per il caricamento parziale  
 Dopo aver caricato parte del file di traccia, per modificare l'intervallo di tempo relativo al set di dati caricatoè possibile regolare la barra degli strumenti della funzionalità di caricamento parziale che si trova nella parte superiore del visualizzatore.  
  
1.  Utilizzare il mouse per spostare la barra degli strumenti oppure immettere l'ora di inizio e di fine.  
  
2.  Fare clic sul pulsante **Regola**.  
  
## Descrizione delle icone di traccia  
 Di seguito è riportato un elenco di icone utilizzate dallo strumento Visualizzatore di tracce dei servizi nella visualizzazione **Attività**, nella visualizzazione **Grafico** e nel riquadro **Traccia** per rappresentare elementi diversi.  
  
> [!NOTE]
>  Alcune tracce non suddivise per categoria \(ad esempio "un messaggio è stato chiuso"\) non dispongono di un'icona.  
  
### Tracce Traccia attività  
  
|Icona|Descrizione|  
|-----------|-----------------|  
|![Traccia di avviso](../../../docs/framework/wcf/media/7457c4ed-8383-4ac7-bada-bcb27409da58.gif "7457c4ed\-8383\-4ac7\-bada\-bcb27409da58")|Traccia di avviso: traccia generata al livello di avviso|  
|![Traccia di errore](../../../docs/framework/wcf/media/7d908807-4967-4f6d-9226-d52125db69ca.gif "7d908807\-4967\-4f6d\-9226\-d52125db69ca")|Traccia di errore: traccia generata al livello di errore.|  
|![Traccia di inizio dell'attività](../../../docs/framework/wcf/media/8a728f91-5f80-4a95-afe8-0b6acd6e0317.gif "8a728f91\-5f80\-4a95\-afe8\-0b6acd6e0317")|Traccia di inizio dell’attività: traccia che indica l’inizio di un’attività,contenente il nome dell’attività.I progettisti dell’applicazione e gli sviluppatori devono definire una traccia d’inizio dell’attività per ogni ID attività per processo o thread.<br /><br /> Se l'ID attività viene propagato attraverso origini di traccia per la correlazione tra tracce, è possibile vedere più inizi per lo stesso ID attività \(uno per ogni origine di traccia\).La traccia di inizio viene emessa se è abilitata la funzione ActivityTracing per l'origine di traccia.|  
|![Traccia di arresto dell'attività](../../../docs/framework/wcf/media/a0493e95-653e-4af8-84a4-4d09a400bc31.gif "a0493e95\-653e\-4af8\-84a4\-4d09a400bc31")|Traccia di interruzione dell’attività: traccia che indica l’interruzione di un’attività,.contenente il nome dell’attività.I progettisti dell’applicazione e gli sviluppatori devono definire una traccia d’interruzione dell’attività per ogni ID attività per origine di traccia.Nessuna traccia derivante da una determinata origine di traccia viene visualizzata dopo che venga generata un’interruzione dell’attività da parte dell’origine di traccia, a meno che la granularità del tempo di traccia non sia sufficientemente piccola.In questo caso, durante la visualizzazione, può verificarsi un’esecuzione interleave di due tracce della stessa durata, comprendenti un’interruzione.Se l'ID attività viene propagato attraverso origini di traccia per la correlazione tra tracce, è possibile vedere più Interruzioni per lo stesso ID attività \(una per ogni origine di traccia\).La traccia di interruzione viene emessa se è abilitata la funzione ActivityTracing per l'origine di traccia.|  
|![Traccia di sospensione dell'attività](../../../docs/framework/wcf/media/6f7f4191-df2b-4592-8998-8379769e2d32.gif "6f7f4191\-df2b\-4592\-8998\-8379769e2d32")|Traccia di sospensione dell’attività: traccia che indica il tempo di sospensione di un’attività.Nessuna traccia è generata in un'attività sospesa finché l'attività non riprende.Un'attività sospesa indica che non si sta verificando nessuna elaborazione in quell'attività nell'ambito dell'origine della traccia.Le tracce di Sospensione\/Ripresa sono utili per il profiling.La traccia di sospensione viene emessa se è abilitata la funzione ActivityTracing per l'origine di traccia.|  
|![Traccia di ripresa dell'attività](../../../docs/framework/wcf/media/1060d9d2-c9c8-4e0a-9988-cdc2f7030f17.gif "1060d9d2\-c9c8\-4e0a\-9988\-cdc2f7030f17")|Traccia di ripresa dell'attività: traccia che indica il momento di ripresa di un’attività dopo la sospensione.Le tracce possono essere generate nuovamente in quell'attività.Le tracce di Sospensione\/Ripresa sono utili per il profiling.La traccia di ripresa viene emessa se è abilitata la funzione ActivityTracing per l'origine di traccia.|  
|![Trasferimento](../../../docs/framework/wcf/media/b2d9850e-f362-4ae5-bb8d-9f6f3ca036a5.gif "b2d9850e\-f362\-4ae5\-bb8d\-9f6f3ca036a5")|Trasferimento: traccia generata quando il flusso di controllo logico viene trasferito da un’attività all’altra.L'attività originaria del trasferimento può continuare ad eseguire le operazioni in parallelo con l'attività che riceve il trasferimento.La traccia di trasferimento viene emessa se è abilitata la funzione ActivityTracing per l'origine di traccia.|  
|![Trasferimento da](../../../docs/framework/wcf/media/1df215cb-b344-4f36-a20d-195999bda741.gif "1df215cb\-b344\-4f36\-a20d\-195999bda741")|Trasferimento da: traccia che definisce il trasferimento da un’altra attività all’attività corrente.|  
|![Trasferimento a](../../../docs/framework/wcf/media/74255b6e-7c47-46ef-8e53-870c76b04c3f.gif "74255b6e\-7c47\-46ef\-8e53\-870c76b04c3f")|Trasferimento a: traccia che definisce il trasferimento di un flusso di controllo logico dall’attività corrente a un’altra attività.|  
  
### Tracce WCF  
  
|Icona|Descrizione|  
|-----------|-----------------|  
|![Traccia del log dei messaggi](../../../docs/framework/wcf/media/7c66e994-2476-4260-a0db-98948b9af197.gif "7c66e994\-2476\-4260\-a0db\-98948b9af197")|Traccia Log dei messaggi: traccia generata quando un messaggio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene registrato per mezzo della funzionalità di registrazione dei  messaggi, quando l’origine di traccia `System.ServiceModel.MessageLogging` è abilitata.Facendo clic su questa traccia verrà visualizzato il messaggio.Ci sono quattro punti di registrazione configurabili per un messaggio: ServiceLevelSendRequest, TransportSend, TransportReceive e ServiceLevelReceiveRequest che possono essere specificati anche dall'attributo `messageSource` nella traccia del log dei messaggi.|  
|![Traccia Messaggio ricevuto](../../../docs/framework/wcf/media/de4f586c-c5dd-41ec-b1c3-ac56b4dfa35c.gif "de4f586c\-c5dd\-41ec\-b1c3\-ac56b4dfa35c")|Traccia Messaggio ricevuto: traccia generata quando viene ricevuto un messaggio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], se la l'origine di traccia `System.ServiceModel` è abilitata al livello di traccia Informazioni o Dettagliato.Questa traccia è essenziale per la visualizzazione del tasto di direzione della correlazione tra i messaggi nella visualizzazione  **Grafico** del menu Attività.|  
|![Traccia Messaggio inviato](../../../docs/framework/wcf/media/558943c4-17cf-4c12-9405-677e995ac387.gif "558943c4\-17cf\-4c12\-9405\-677e995ac387")|Traccia Messaggio ricevuto: traccia generata quando viene ricevuto un messaggio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], se la l'origine di traccia `System.ServiceModel` è abilitata al livello di traccia Informazioni o Dettagliato.Questa traccia è essenziale per la visualizzazione del tasto di direzione della correlazione tra i messaggi nella visualizzazione  **Grafico** del menu Attività.|  
  
### Attività  
  
|Icona|Descrizione|  
|-----------|-----------------|  
|![Attività](../../../docs/framework/wcf/media/wcfc-defaultactivityc.gif "wcfc\_defaultActivityc")|Attività: indica che l'attività corrente è un'attività generica.|  
|![Attività radice](../../../docs/framework/wcf/media/5dc8e0eb-1c32-4076-8c66-594935beaee9.gif "5dc8e0eb\-1c32\-4076\-8c66\-594935beaee9")|Attività radice: indica l'attività radice di un processo.|  
  
### Attività WCF  
  
|Icona|Descrizione|  
|-----------|-----------------|  
|![Attività di ambiente](../../../docs/framework/wcf/media/29fa00ac-cf78-46e5-822d-56222fff61d1.gif "29fa00ac\-cf78\-46e5\-822d\-56222fff61d1")|Attività dell'ambiente: attività che crea, apre o chiude un host o un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Gli errori che si sono verificati durante queste fasi verranno visualizzati in questa attività.|  
|![Attività Listen](../../../docs/framework/wcf/media/d7b135f6-ec7d-45d7-9913-037ab30e4c26.gif "d7b135f6\-ec7d\-45d7\-9913\-037ab30e4c26")|Attività Listen: attività che si registra tracce riferita a un listener.In questa attività, si possono visualizzare informazioni e richieste di connessione del listener.|  
|![Attività di ricezione byte](../../../docs/framework/wcf/media/2f628580-b80f-45a7-925b-616c96426c0e.gif "2f628580\-b80f\-45a7\-925b\-616c96426c0e")|Attività ricezione byte: attività che raduna tutte le tracce relative alla ricezione di byte in ingresso su una connessione tra due endpoint.Questa attività è essenziale nelle correlazioni con le attività del trasporto che propagano l'ID attività, ad esempio http.sys.Errori di connessione, quali interruzioni, verranno visualizzati in questa attività.|  
|![Attività messaggio del processo](../../../docs/framework/wcf/media/wcfc-executionactivityiconc.GIF "wcfc\_ExecutionActivityIconc")|Attività Elaborazione messaggi: attività che raduna tracce relative alla creazione di un messaggio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Gli errori causati da envelope errata o da messaggi in formato non valido verranno visualizzati nell'attività.In questa attività, è possibile controllare le intestazioni del messaggio per vedere se un ID attività è stato propagato dal chiamante.In questo caso, quando si passa all’attività di tipo ProcessAction \(icona successiva\), si può inoltre assegnare a tale attività l'ID attività propagato per la correlazione tra tracce di chiamante e chiamato.|  
|![Traccia del log dei messaggi](../../../docs/framework/wcf/media/7c66e994-2476-4260-a0db-98948b9af197.gif "7c66e994\-2476\-4260\-a0db\-98948b9af197")|Attività Elaborazione azione: attività che raduna tutte le tracce relative ad una richiesta [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] tra due endpoint.Se `propagateActivity` è impostato su `true` su entrambi gli endpoint della configurazione, tutte le tracce da entrambi gli endpoint vengono incorporate in un'unica attività per correlazione diretta.Tale attività conterrà errori a causa dell’elaborazione nel trasporto o della sicurezza, che si estendono al limite del codice utente e viceversa \(se esiste una risposta\).|  
|![Attività messaggio del processo](../../../docs/framework/wcf/media/wcfc-executionactivityiconc.GIF "wcfc\_ExecutionActivityIconc")|Attività Esecuzione del codice utente: attività che raduna le tracce del codice utente per l'elaborazione di una richiesta.|  
  
## Risoluzione dei problemi  
 Se non si dispone delle autorizzazioni per scrivere nel Registro di sistema, verrà visualizzato il messaggio di errore seguente "Il Visualizzatore di tracce dei servizi Microsoft non è stato registrato nel sistema" quando si utilizza il comando "`svctraceviewer /register`" per registrare lo strumento.In questo caso è necessario accedere utilizzando un account che abbia accesso in scrittura al Registro di sistema.  
  
 Lo strumento Visualizzatore di tracce dei servizi scrive inoltre alcune impostazioni \(ad esempio, filtri personalizzati e opzioni di filtro\) nel file SvcTraceViewer.exe.settings nella cartella dell'assembly.Se non si dispone dell’autorizzazione in lettura per il file, è comunque possibile avviare lo strumento, ma non è possibile caricare le impostazioni.  
  
 Se, aprendo il file con estensione etl, viene visualizzato il messaggio di errore "Si è verificato un errore sconosciuto durante l'elaborazione di una o più tracce" vuole dire che il formato del file con estensione etl non è valido.  
  
 Se si apre un registro di traccia creato utilizzando un sistema operativo attivato per la lingua araba, è possibile che il filtro dell'ora non funzioni.Ad esempio, l'anno 2005 corrisponde all’anno 1427 del calendario arabo.L'intervallo di tempo supportato dal filtro dello strumento Visualizzatore di tracce dei servizi, tuttavia, non supporta una data antecedente al 1752.Questo può determinare l'impossibilità di selezionare una data corretta nel filtro.Per risolvere questo problema è possibile creare un filtro personalizzato \(**Visualizza\/Filtri personalizzati**\) utilizzando un'espressione XPath per includere un intervallo di tempo specifico.  
  
## Vedere anche  
 [Utilizzo di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)   
 [Configurazione delle funzionalità di traccia](../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)   
 [Activity Tracing and Propagation for End\-To\-End Trace Correlation](http://msdn.microsoft.com/it-it/2c11a905-64f8-47b5-bae5-a74fc666137e)