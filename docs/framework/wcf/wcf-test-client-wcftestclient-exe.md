---
title: "Client di test WCF (WcfTestClient.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d4302855-677f-4640-aa90-c5d785d72fb7
caps.latest.revision: 45
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 45
---
# Client di test WCF (WcfTestClient.exe)
Client di test [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] \(WcfTestClient.exe\) è un strumento GUI che consente agli utenti di immettere parametri di test, inviare l'input immesso al servizio e visualizzare la risposta restituita dal servizio.  In combinazione con Host servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] offre una funzione di test del servizio trasparente.  
  
 Client di prova [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(WcfTestClient.exe\) è disponibile nel percorso seguente: C:\\Programmi\\Microsoft Visual Studio 9.0\\Common7\\IDE\\  
  
## Scenari per l'uso di Client di test  
 Nelle sezioni seguenti sono illustrati gli scenari più comuni nei quali è possibile usare Client di prova [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per semplificare il processo di sviluppo.  
  
### All'interno di Visual Studio  
  
#### Host servizio WCF avvia Client di test WCF con un solo servizio  
 Dopo avere creato un nuovo progetto di servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e avere premuto F5 per avviare il debugger, Servizio Host [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] avvia l'hosting del servizio nel progetto.  Quindi, Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] apre e visualizza un elenco degli endpoint di servizio definiti nel file di configurazione.  È possibile testare i parametri e richiamare il servizio e ripetere il processo per testare e convalidare continuamente il servizio.  
  
#### Host servizio WCF avvia Client di test WCF con più servizi  
 È inoltre possibile usare Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per il debug di un progetto di servizio contenente più servizi.  All'apertura, Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] esegue automaticamente l'iterazione dell'elenco dei servizi nel progetto e li apre per il test.  
  
### All'esterno di Visual Studio  
 È inoltre possibile richiamare Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \(WcfTestClient.exe\) dall'esterno di Visual Studio per eseguire il test di un servizio arbitrario su Internet.  Per individuare lo strumento, passare al percorso seguente:  
  
 C:\\Programmi\\Microsoft Visual Studio 9.0\\Common7\\IDE\\  
  
 Per usare lo strumento, fare doppio clic sul nome del file per aprirlo da questo percorso oppure avviarlo da una riga di comando.  
  
 Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] usa un numero arbitrario di URI come argomenti della riga di comando.  Di seguito sono riportati gli URI dei servizi che è possibile sottoporre a test.  
  
 `wcfTestClient.exe URI1 URI2 …`  
  
 Con la finestra Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] aperta, fare clic su **File**\-\>**Aggiungi servizio** e immettere l'indirizzo endpoint del servizio da aprire.  
  
## Interfaccia utente di Client di test WCF  
 È possibile usare Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con uno o più servizi.  
  
### Operazioni di servizio  
 Nel riquadro di sinistra della finestra principale di Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] sono elencati tutti i servizi disponibili, insieme ai rispettivi endpoint e operazioni.  
  
 Quando si fa doppio clic su un'operazione, è possibile visualizzare il relativo contenuto nel riquadro di destra all'interno di una nuova scheda con il nome dell'operazione.  
  
 Nel riquadro di sinistra sono elencati i anche file di configurazione client.  Fare doppio clic sugli elementi per visualizzare il contenuto del file in una nuova finestra a schede nel riquadro di destra.  
  
### Immissione dei parametri del test  
 Per visualizzare i parametri del test, fare doppio clic su un'operazione per aprirla nel riquadro di destra.  Per impostazione predefinita, i parametri vengono mostrati nella visualizzazione **Formattato** ed è possibile immettere valori arbitrari dei parametri per il test del servizio.  
  
 Per visualizzare il codice XML del messaggio, scegliere **XML**.  Per inviarli al servizio, scegliere **Richiama**.  
  
 Per un parametro DataSet, fare clic sul pulsante con i puntini di sospensione \(**…**\) accanto a **Modifica** per modificarlo in una nuova finestra in cui è visualizzato il DataGrid.  Verranno visualizzati i pulsanti **Copia DataSet** e **Incolla DataSet**.  Se lo schema dell'oggetto the DataSet non è noto alla prima modifica, il DataGrid sarà vuoto.  È necessario incollare un oggetto DataSet object con lo stesso schema nell'oggetto corrente nel DataGrid  \(tenere presente che è necessario copiare lo schema da un'altra posizione prima di incollare\). È inoltre possibile copiare un oggetto Dataset da usare in un secondo momento facendo clic sul pulsante **Copia DataSet**.  
  
 La risposta del servizio viene visualizzata sotto i parametri del test.  
  
> [!NOTE]
>  Se il valore restituito previsto è una stringa, il risultato verrà visualizzato come una stringa tra virgolette anche se l'input fornito non era tra virgolette.  
  
 Se una particolare operazione viene specificata come unidirezionale quando si crea il contratto per il servizio, non viene visualizzata alcuna risposta del servizio.  Non appena il messaggio viene accodato per il recapito, viene visualizzata una finestra di dialogo per notificare che il messaggio è stato inviato correttamente.  
  
### Supporto della sessione  
 La casella di controllo **Avvia un nuovo proxy** nella scheda di un'operazione di servizio consente abilitare o disabilitare il supporto della sessione.  Per impostazione predefinita, la casella è deselezionata.  
  
 Quando si immettono parametri di test per un'operazione specifica, o per un'altra operazione nello stesso endpoint del servizio, e si fa clic più volte su **Richiama** con la casella di controllo deselezionata, tali operazioni condividono un unico proxy e lo stato del servizio risulta persistente tra più operazioni.  
  
 Se la casella di controllo **Avvia un nuovo proxy** viene selezionata, verrà avviato un nuovo proxy ogni volta che si fa clic su **Richiama**, lo scenario della sessione precedente verrà terminato e lo stato del servizio reimpostato.  
  
### Modifica della configurazione client  
 Nel riquadro di sinistra della finestra principale del Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] sono elencati i file di configurazione client.  Fare doppio clic su uno degli elementi per visualizzare il contenuto del file nel riquadro di destra.  
  
#### Apportare modifiche con l'Editor configurazione servizi  
 Fare clic con il pulsante destro del mouse su **File di configurazione** nel riquadro di sinistra e selezionare il menu di scelta rapida **Modifica con SvcConfigEditor**.  Editor configurazione servizi verrà avviato con il contenuto della configurazione client.  Sarà possibile modificare la configurazione e salvarla all'interno dello strumento.  
  
 Dopo avere salvato il file nell'Editor di configurazione dei servizi, Client di prova [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] visualizzerà un messaggio di avviso per informare che il file è stato modificato all'esterno e chiedere se si desidera ricaricarlo.  
  
 Se si seleziona **Sì**, il contenuto della configurazione nella scheda "Client.dll.config" rifletterà le modifiche apportate nell'editor.  
  
 Se si seleziona **No**, il contenuto della configurazione nella scheda "Client.dll.config" rimarrà invariato e il contenuto modificato verrà salvato automaticamente nel file di origine.  
  
#### Ripristinare la configurazione predefinita  
 Se si desidera annullare tutte le modifiche apportate e ripristinare la configurazione client predefinita, fare clic con il pulsante destro del mouse su **File di configurazione** nel riquadro di sinistra e scegliere **Ripristina configurazione predefinita** dal menu di scelta rapida.  Il valore della configurazione predefinita verrà caricato e il contenuto nella scheda "Client.dll.config" verrà ripristinato.  
  
#### Convalidare le modifiche  
 Quando le modifiche salvate vengono caricate in Client di prova [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], viene verificata la validità della configurazione rispetto allo schema [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Se vengono rilevati errori, verrà visualizzata una finestra di dialogo contenente i dettagli degli errori.  
  
 Durante il processo di generazione proxy, di compilazione binaria o di richiamo del servizio, le voci di menu che supportano la modifica, ad esempio "Modifica", "Ripristina" e così via, risultano disabilitate.  La chiamata del servizio risulta inoltre disattivata durante il caricamento della configurazione aggiornata in Client di prova [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
#### Rendere persistente la configurazione client  
 La scheda **Strumenti**\-\>**Opzioni**\-\>**Configurazione client** contiene l'opzione **Rigenera sempre la configurazione all'avvio dei servizi** abilitata per impostazione predefinita.  Questa opzione specifica che ogni volta che Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] carica un servizio, il file di configurazione viene rigenerato automaticamente in base ai file App.config del contratto di servizio e del servizio più recenti.  
  
 Se è stata modificata la configurazione client per il servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e si desidera usare sempre il file aggiornato per eseguire il debug del servizio, sarà possibile deselezionare l'opzione **Rigenera**.  In tal modo, anche quando si aggiorna il servizio e si riapre Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], il file Client.dll.config corrisponderà a quello aggiornato in precedenza dall'utente anziché a un file rigenerato in base al servizio aggiornato.  
  
 Potrebbe tuttavia essere necessario modificare il file di configurazione per renderlo coerente con il proxy rigenerato.  Se il proxy e file di configurazione rigenerati non corrispondono perché un servizio è stato aggiornato, si verificheranno errori quando il servizio viene richiamato.  
  
> [!CAUTION]
>  Se il file di configurazione client è stato modificato e si è scelto di riusarlo in futuro, il file sarà disponibile nel percorso seguente:  
>   
>  \\Documents and Settings\\\[Account utente\]\\Documenti\\Test Client Projects.  
>   
>  Le informazioni sulle credenziali aggiornate archiviate nel file di configurazione client sono protette dall'elenco di controllo dell'accesso \(ACL\) di questa cartella.  
  
### Aggiunta, rimozione e aggiornamento di servizi  
  
#### Aggiungere un servizio  
 Fare clic su **File**\-\>**Aggiungi servizio** per aggiungere un servizio a Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Verrà quindi richiesto di digitare l'URI \(indirizzo endpoint\) del servizio da aggiungere.  L'indirizzo del servizio può corrispondere a un indirizzo mex o a un indirizzo WSDL.  
  
 Nel sottomenu **Servizi recenti** è inoltre disponibile un elenco di 10 endpoint di servizio aggiunti recentemente.  Se si seleziona uno di questi endpoint, il servizio specificato verrà aggiunto a Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 Per ottenere lo stesso risultato, è inoltre possibile fare clic con il pulsante destro del mouse sulla radice dell'albero del servizio **Progetti di servizi** e scegliere **Aggiungi servizio**.  
  
 Durante il processo di generazione proxy, di compilazione binaria o di richiamo del servizio, le voci di menu che supportano l'aggiunta di un servizio risultano disabilitate.  Anche la chiamata del servizio è disabilitata.  
  
#### Rimuovere un servizio  
 Fare clic con il pulsante destro del mouse sulla radice del servizio da rimuovere e scegliere **Rimuovi servizio** per rimuovere un servizio da Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 Durante il processo di generazione proxy, di compilazione binaria o di richiamo del servizio, le voci di menu che supportano la rimozione di un servizio risultano disabilitate.  Anche la chiamata del servizio è disabilitata.  
  
#### Aggiornare un servizio  
 Se si apporta una modifica al servizio mentre Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è in esecuzione e si desidera essere certi che l'implementazione di Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per tale servizio sia aggiornata, fare clic con il pulsante destro del mouse sulla radice del servizio e scegliere **Aggiorna servizio**.  Si noti che dopo l'aggiornamento lo stato del servizio viene reimpostato.  
  
 Durante il processo di generazione proxy, di compilazione binaria o di richiamo del servizio, le voci di menu che supportano l'aggiornamento di un servizio risultano disabilitate.  Anche la chiamata del servizio è disabilitata.  
  
## Percorso dei file generati da Client di test  
 Per impostazione predefinita, Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] archivia il codice client e file di configurazione generati nella cartella "%appdata%\\Local\\temp\\Test Client Projects".  Questa cartella viene eliminata dopo la chiusura di Client di prova [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Se un file di configurazione viene modificato in Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e l'opzione **Rigenera sempre la configurazione all'avvio dei servizi** è disabilitata, il file modificato verrà copiato nella cartella "Cached Config" nel percorso "Documenti\\Test Client Projects Documents\\Test Client Projects" con un file XML di mapping \(dall'indirizzo dei metadati al nome del file\) come indice.  
  
 È inoltre possibile avviare Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in una riga di comando, usare l'opzione `/ProjectPath` per specificare il percorso desiderato per l'archiviazione dei file generati oppure usare l'opzione `/RestoreProjectPath` per ripristinare il percorso predefinito.  La sintassi è la seguente:  
  
 `wcfTestClient.exe /ProjectPath [desired location]`  
  
 L'esecuzione di questo comando non determina l'apertura di Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)],  ma solo la modifica del percorso della cartella.  È possibile eseguire questo comando indipendentemente dal fatto che Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] sia o meno in esecuzione.  Il nuovo percorso verrà applicato al riavvio di Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Le informazioni sul percorso possono essere salvate nel Registro di sistema oppure nel file WcfTestClient.exe.option nella cartella "%appdata%\\Local\\temp\\Test Client Projects".  
  
## Funzioni supportate da Client di prova WCF  
 Nell'elenco seguente sono incluse le funzionalità supportate da Client di prova [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]:  
  
-   Chiamata al servizio: messaggio di richiesta\/risposta e unidirezionale.  
  
-   Associazioni: tutte le associazioni supportate da Svcutil.exe.  
  
-   Controllo della sessione.  
  
-   Contratto di messaggio.  
  
-   Serializzazione XML.  
  
 Nell'elenco seguente sono incluse le funzionalità non supportate da Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]:  
  
-   Tipi: <xref:System.IO.Stream>, <xref:System.ServiceModel.Channels.Message>, <xref:System.Xml.XmlElement>, <xref:System.Xml.XmlAttribute>, <xref:System.Xml.XmlNode>, tipi che implementano l'interfaccia <xref:System.Xml.Serialization.IXmlSerializable>, tra cui l'attributo <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> correlato, i tipi <xref:System.Xml.Linq.XDocument> e <xref:System.Xml.Linq.XElement> e il tipo <xref:System.Data.DataTable> di ADO.NET.  
  
-   Contratto duplex.  
  
-   Transazione.  
  
-   Sicurezza: [!INCLUDE[infocard](../../../includes/infocard-md.md)], certificato e nome utente\/password.  
  
-   Associazioni: WSFederationbinding, qualsiasi associazione Context e associazione Https, WebHttpbinding \(supporto per messaggi di riposta Json\).  
  
## Chiusura di Client di test WCF  
 È possibile chiudere CLient di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] nei seguenti modi:  
  
-   Scegliere **Esci** dal menu **File**.  In alternativa, nella finestra principale del Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], scegliere **Chiudi**.  Entrambe le azioni determinano inoltre l'arresto di Host automatico servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e l'interruzione del processo di debug di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] se Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è stato avviato da [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
-   Fare clic con il pulsante destro del mouse nell'icona **Host servizio WCF** nell'area di notifica, quindi scegliere **Esci**. Questo chiude sia Host automatico servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] che Client di test [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e arresta il processo di debug di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## Vedere anche  
 [Host servizio WCF \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)