---
title: "Procedura: eseguire il debug di applicazioni e servizi in grado di riconoscere attestazioni mediante traccia WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d51ba59-3adb-4ca4-bd33-5027531af687
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# Procedura: eseguire il debug di applicazioni e servizi in grado di riconoscere attestazioni mediante traccia WIF
## Si applica a  
  
-   Microsoft® Windows® Identity Foundation \(WIF\)  
  
-   Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)  
  
-   Risoluzione dei problemi e debug di applicazioni WIF  
  
## Riepilogo  
 Questa procedura descrive i passaggi necessari per configurare le funzionalità di traccia di WIF, raccogliere i log di traccia e analizzarli mediante lo strumento visualizzatore di tracce dei servizi.  Fornisce un mapping generale delle voci di traccia alle azioni necessarie per la risoluzione dei problemi correlati a WIF.  
  
## Sommario  
  
-   Obiettivi  
  
-   Riepilogo dei passaggi  
  
-   Passaggio 1 \- Configurare le funzionalità di traccia di WIF usando il file Web.config  
  
-   Passaggio 2 \- Analizzare i file di traccia di WIF usando lo strumento visualizzatore di tracce dei servizi  
  
-   Passaggio 3 \- Identificare soluzioni per la risoluzione dei problemi correlati a WIF  
  
-   Elementi correlati  
  
## Obiettivi  
  
-   Configurare le funzionalità di traccia WIF.  
  
-   Visualizzare i log di traccia nello strumento visualizzatore di tracce dei servizi.  
  
-   Identificare i problemi relativi a WIF nei log di traccia.  
  
-   Applicare azioni correttive ai problemi correlati a WIF riscontrati nei log di traccia.  
  
## Riepilogo dei passaggi  
  
-   Passaggio 1 \- Configurare le funzionalità di traccia di WIF usando il file Web.config  
  
-   Passaggio 2 \- Analizzare i file di traccia di WIF usando lo strumento visualizzatore di tracce dei servizi  
  
-   Passaggio 3 \- Identificare soluzioni per la risoluzione dei problemi correlati a WIF  
  
## Passaggio 1 \- Configurare le funzionalità di traccia di WIF usando il file Web.config  
 In questo passaggio si aggiungeranno modifiche alle sezioni di configurazione del file *Web.config* in modo da abilitare la traccia e la registrazione degli eventi WIF in un log di traccia.  
  
#### Per configurare le funzionalità di traccia di WIF usando il file Web.config  
  
1.  Aprire il file di configurazione radice **Web.config** o **App.config** nell'editor di Visual Studio facendo doppio clic su di esso in **Esplora soluzioni**.  Se la soluzione non dispone di un file di configurazione **Web.config** o **App.config**, aggiungerlo facendo clic con il pulsante destro del mouse sulla soluzione in **Esplora soluzioni** e scegliendo **Aggiungi**, quindi **Nuovo elemento**.  Nella finestra di dialogo **Nuovo elemento** selezionare **File di configurazione dell'applicazione** per **App.config** o **File di configurazione Web** per **Web.config** dall'elenco e fare clic su **OK**.  
  
2.  Aggiungere le voci di configurazione simili alla seguente al file di configurazione all'interno del nodo **\<configuration\>** alla fine del file di configurazione:  
  
    ```xml  
    <system.diagnostics>  
        <sources>  
            <source name="System.IdentityModel" switchValue="Verbose">  
                <listeners>  
                    <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="WIFTrace.e2e"/>  
                </listeners>  
            </source>  
        </sources>  
        <trace autoflush="true"/>  
    </system.diagnostics>  
    ```  
  
3.  La configurazione precedente indica a WIF di generare eventi di traccia dettagliati e registrarli nel file *WIFTrace.e2e*.  Per un elenco completo dei valori per lo switch **switchValue**, fare riferimento alla tabella Livello di traccia nell'argomento [Configurazione delle funzionalità di traccia](http://msdn.microsoft.com/library/ms733025.aspx).  
  
## Passaggio 2 \- Analizzare i file di traccia di WIF usando lo strumento visualizzatore di tracce dei servizi  
 In questo passaggio si userà lo strumento visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\) per analizzare i log di traccia di WIF.  
  
#### Per analizzare i log di traccia di WIF con lo strumento visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)  
  
1.  Lo strumento visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\) è incluso in Windows SDK.  Se Windows SDK non è ancora installato, è possibile scaricarlo qui: [Windows SDK](http://www.microsoft.com/download/en/details.aspx?id=8279).  
  
2.  Eseguire lo strumento visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)  In genere è disponibile nella cartella **Bin** del percorso di installazione.  
  
3.  Aprire il file di log di traccia di WIF, ad esempio, WIFTrace.e2e scegliendo **Apri** dal menu **File** oppure usando la scelta rapida da tastiera **CTRL\+O**.  Il file di log di traccia verrà aperto nel visualizzatore di tracce dei servizi.  
  
4.  Esaminare le voci nella scheda **Attività**.  Ogni voce contiene un numero di attività, il numero di tracce registrate, la durata dell'attività e i timestamp di inizio e fine.  
  
5.  Fare clic sulla scheda **Attività**.  Nell'area principale dello strumento saranno visibili le voci di traccia dettagliate.  Usare l'elenco a discesa del menu **Livello** per filtrare in base a specifici livelli di traccia, ad esempio: **Tutto**, **Avviso**, **Errori**, **Informazioni** e così via.  
  
6.  Fare clic sulle specifiche voci di traccia per esaminare i dettagli nell'area inferiore dello strumento.  I dettagli sono disponibili nelle visualizzazioni **Formattato** e **XML** scegliendo le schede corrispondenti.  
  
## Passaggio 3 \- Identificare soluzioni per la risoluzione dei problemi correlati a WIF  
 Questo passaggio illustra come individuare soluzioni per i problemi correlati a WIF identificati mediante il log di traccia WIF e lo strumento visualizzatore di tracce dei servizi.  Illustra inoltre il mapping generale delle eccezioni correlate a WIF alle possibili soluzioni o alle azioni necessarie per risolvere il problema.  
  
#### Per identificare soluzioni per correggere i problemi correlati a WIF  
  
1.  Esaminare la tabella seguente di eccezioni WIF e le azioni necessarie per correggere i problemi.  
  
||||  
|-|-|-|  
|**ID errore**|**Messaggio di errore**|**Azione necessaria per correggere l'errore**|  
|ID4175|L'emittente del token di sicurezza non è stato riconosciuto da IssuerNameRegistry.  Per accettare token di sicurezza da questa autorità emittente, configurare IssuerNameRegistry per restituire un nome valido per l'emittente.|L'errore può essere causato dall'aver copiato un'identificazione personale dallo snap\-in MMC e averla poi incollata nel file *Web. config*.  In particolare, copiando dalla finestra delle proprietà del certificato è possibile ottenere un carattere aggiuntivo non stampabile nella stringa di testo.  Questo carattere aggiuntivo provoca un errore di mancata corrispondenza dell'identificazione personale. La procedura per copiare correttamente l'identificazione personale è disponibile qui: [http:\/\/msdn.microsoft.com\/library\/ff359102.aspx](http://msdn.microsoft.com/library/ff359102.aspx)|  
  
## Elementi correlati  
  
-   [Uso di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](http://msdn.microsoft.com/library/aa751795.aspx)