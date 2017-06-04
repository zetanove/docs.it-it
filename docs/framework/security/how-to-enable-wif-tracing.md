---
title: "Procedura: Abilitare la traccia WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 271b6889-3454-46ff-96ab-9feb15e742ee
caps.latest.revision: 3
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 3
---
# Procedura: Abilitare la traccia WIF
## Si applica a  
  
-   Foundation \(WIF\) di identità di Microsoft® Windows®  
  
-   ASP.NET® Web Form  
  
## Riepilogo  
 In questa procedura vengono fornite le procedure dettagliate per abilitare l'analisi di WIF in un'applicazione ASP.NET.  Fornisce inoltre le istruzioni che testano l'applicazione per verificare che il listener di traccia e il registro funzionino correttamente.  In questa procedura non ha dettagliato le istruzioni per creare un servizio token di sicurezza \(STS\) e si utilizza lo sviluppo servizio token di sicurezza fornite dallo strumento di accesso e di identità.  Lo sviluppo servizio token di sicurezza non esegue l'autenticazione reale ed è destinata a scopo di test.  È necessario configurare l'identità e di accesso per completare questa procedura.  Può essere scaricato dal seguente percorso: [Strumento di accesso e di identità](http://go.microsoft.com/fwlink/?LinkID=245849)  
  
> [!IMPORTANT]
>  Abilitare l'analisi di WIF per le applicazioni passive, ovvero, applicazioni che utilizzano il protocollo di WS\- federazione, può essere esposto l'applicazione agli attacchi Denial of Service \(DoS\) o la diffusione di informazioni a una parte dannoso.  Inclusi il secondo \(RPS\) passivo che STSes passivo.  Per questo motivo, è consigliabile di non abilitare l'analisi di WIF per il secondo \(RPS\) passivo o STSes in un ambiente di produzione.  
  
## Contenuto  
  
-   Obiettivi  
  
-   Panoramica  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice e abilitare l'analisi  
  
-   Passaggio 2 \- verificare la soluzione  
  
## Obiettivi  
  
-   Creare un'applicazione ASP.NET semplice che utilizza WIF e lo sviluppo servizio token di sicurezza dall'identità e accedere allo strumento  
  
-   Abilitare l'analisi e verificare che sia funzionante  
  
## Panoramica  
 La tracciatura consente di eseguire il debug e la risoluzione di molti tipi di problemi con WIF, inclusi i token, i cookie, richieste, i messaggi di protocollo e così via.  L'analisi di WIF è simile all'analisi di WCF; ad esempio, è possibile scegliere il livello di traccia per visualizzare tutti i messaggi critici a tutti i messaggi.  Le analisi di WIF possono essere generate in file **xml** o in file **.svclog** che sono visualizzabili tramite lo strumento del Service visualizzatore di traccia.  Tale strumento si trova nella directory **bin** di Windows SDK il percorso di installazione nel computer, ad esempio: **C:\\Program Files\\Microsoft sdks \\ Windows \\ v7.1 \\ bin \\ SvcTraceViewer.exe**.  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice e abilitare l'analisi  
  
-   Passaggio 2 \- verificare la soluzione  
  
## Passaggio 1 \- creare un'applicazione Web Form ASP.NET semplice e abilitare l'analisi  
 In questo passaggio, verrà creata una nuova applicazione Web Form ASP.NET e si modifica *il file Web.config* per abilitare la tracciatura.  
  
#### Per creare un'applicazione ASP.NET semplice  
  
1.  Avviare Visual Studio e **File**, **Nuovo**quindi **Progetto**.  
  
2.  Nella finestra **Nuovo progetto**, fare clic **Applicazione Web Form ASP.NET**.  
  
3.  In **Nome**, immettere `TestApp` e premere **OK**.  
  
4.  Fare clic con il pulsante destro del mouse sul progetto **TestApp** in **Esplora soluzioni**, quindi selezionare **Identità e accesso**.  
  
5.  Verrà visualizzata la finestra **Identità e accesso**.  In **Provider**, selezionare **Esegui test dell'applicazione con l'STS di sviluppo locale**, quindi **Applica**.  
  
6.  Creare una nuova cartella in **log** denominato nella radice dell'unità **C:**, come indicato: **C:\\logs**  
  
7.  Aggiungere il seguente elemento **\<system.diagnostics\>** *al file di configurazione Web.config* immediatamente dopo l'elemento chiusura **\<\/configSections\>**, come indicato:  
  
    ```  
    <configuration>  
        <configSections>  
        …  
        </configSections>  
        <system.diagnostics>  
            <sources>  
                <source name="System.IdentityModel" switchValue="Verbose">  
                    <listeners>  
                        <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="C:\logs\WIF.xml" />  
                    </listeners>  
                </source>  
            </sources>  
            <trace autoflush="true" />  
        </system.diagnostics>  
    ```  
  
    > [!NOTE]
    >  Il percorso della directory specificata nell'attributo **initializeData** deve essere presenti prima di registrare possa iniziare.  Se la posizione non esiste, alcun log verrà creato.  
  
     Le impostazioni di configurazione delle precedenti consentiranno **Dettagliati** la tracciatura per WIF e salveranno il gruppo di risultati nel file **C:\\logs\\WIF.xml**.  
  
## Passaggio 2 \- verificare la soluzione  
 In questo passaggio, è consigliabile testare l'applicazione ASP.NET WIF\- abilitata verificare che i registri vengano registrandi.  
  
#### Per testare l'applicazione ASP.NET WIF\- attivata l'operazione di analisi  
  
1.  Eseguire la soluzione premendo il tasto **F5**.  Dovrebbe essere visualizzata la home page ASP.NET predefinito e automaticamente essere autenticati con il nome utente *Terry*, che corrisponde all'utente predefinito restituito dallo sviluppo servizio token di sicurezza.  
  
2.  Chiudere la finestra del browser e passare alla cartella **C:\\logs**.  Aprire il file **C:\\logs\\WIF.xml** utilizzando un editor di testo.  
  
3.  Archiviare il file **WIF.xml** e verificare che contenga le voci che iniziano con **\<E2ETraceEvent\>**.  Queste traccia contiene gli elementi **\<TraceRecord\>** con descrizioni per l'attività analizzata, come **Convalida di SecurityToken**.