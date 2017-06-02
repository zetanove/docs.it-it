---
title: "Strumento Editor di configurazione (SvcConfigEditor.exe) | Microsoft Docs"
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
  - "File di configurazione"
  - "schema dei file di configurazione"
  - "file di configurazione"
  - "file di configurazione, creazione"
ms.assetid: 2db21a57-5f64-426f-89df-fb0dc2d2def5
caps.latest.revision: 45
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 45
---
# Strumento Editor di configurazione (SvcConfigEditor.exe)
L'Editor di configurazione dei servizi \(SvcConfigEditor.exe\) di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] consente ad amministratori e sviluppatori di creare e modificare le impostazioni di configurazione per i servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] tramite un'interfaccia utente grafica.Con questo strumento è possibile gestire le impostazioni di associazioni, comportamenti, servizi e diagnostica [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] senza la necessità di modificare direttamente i file di configurazione XML.  
  
 L'Editor di configurazione dei servizi si trova nella cartella C:\\Programmi\\Microsoft SDKs\\Windows\\v6.0\\Bin.  
  
## Editor di configurazione dei servizi di WCF  
 L'Editor di configurazione dei servizi dispone di una procedura guidata che descrive le fasi per configurare un servizio o un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Si consiglia di utilizzare direttamente la procedura guidata anziché l'editor.  
  
 Se si dispone già di alcuni file di configurazione conformi allo schema System.Configuration standard, tramite l'interfaccia utente è possibile gestire impostazioni specifiche relative ad associazioni, comportamenti, servizi e diagnostica.Oltre alle impostazioni dei file di configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] esistenti, l'Editor di configurazione dei servizi consente di gestire file eseguibili, servizi COM\+ e servizi ospitati su Web.Quando si apre un servizio ospitato su Web con l'Editor di configurazione dei servizi, vengono visualizzate sia la configurazione del servizio stesso che le sezioni di configurazione ereditate dei nodi di livello superiore.  
  
 Dato che le impostazioni di configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] si trovano nella sezione `<system.serviceModel>` del file di configurazione, l'editor opera esclusivamente sul contenuto di questo elemento e non accede gli altri elementi nello stesso file.È possibile accedere direttamente ai file di configurazione esistenti oppure selezionare un assembly contenente un servizio, una directory virtuale o un servizio COM\+.L'editor carica il file di configurazione per quel particolare servizio e consente all'utente di aggiungere elementi nuovi o di modificare elementi esistenti annidati nella sezione `<system.serviceModel>` del file di configurazione.  
  
 L'editor supporta IntelliSense e richiede la conformità con lo schema.L'editor garantisce che l’output risultante sia conforme con lo schema del file di configurazione e che i valori dei dati siano sintatticamente corretti.Tuttavia, l'editor non garantisce che il file di configurazione siano semanticamente validi.In altre parole, l'editor non garantisce che il file di configurazione pussa funzionare con il servizio che configura.  
  
> [!CAUTION]
>  L'editor non può cancellare un elemento di configurazione dal file di configurazione una volta che l’elemento è stato modificato.Ad esempio, se si utilizza l'editor per impostare il nome dell'endpoint su una stringa non vuota e per salvarlo, il file di configurazione avrà il contenuto mostrato nell'esempio seguente:  
>   
>  `<endpoint binding="basicHttpBinding" name="somename" />`  
>   
>  Se si tenta di rimuovere il nome impostandolo su una stringa vuota e salvando il file, il file di configurazione contiene ancora l'attributo `name`, come mostrato nell'esempio seguente.  
>   
>  `<endpoint binding="basicHttpBinding" name="" />`  
>   
>  Per cancellare l'attributo è necessario modificare manualmente l'elemento utilizzando un altro editor di testo.  
>   
>  È necessario prestare particolare attenzione a questo problema quando si utilizza l'elemento `issueToken` del comportamento dell’endpoint `clientCredential`.In particolare, l'attributo `address` del sottoelemento `localIssuer` non deve essere una stringa vuota.Se si è modificato l'attributo `address` utilizzando l'Editor di configurazione e si desidera rimuoverlo completamente, è necessario utilizzare uno strumento diverso dall'Editor.In caso contrario, l'attributo conterrà una stringa vuota e l'applicazione genererà un'eccezione.  
  
## Utilizzo dell'Editor di configurazione  
 L'Editor di configurazione dei servizi si trova nel seguente percorso di installazione di Windows SDK:  
  
 C:\\Programmi\\Microsoft SDKs\\Windows\\v6.0\\Bin\\SvcConfigEditor.exe  
  
 Dopo avere avviato l'Editor di configurazione dei servizi, è possibile utilizzare il menu **File\/Apri** per cercare il servizio o l’assembly che si desidera gestire.È possibile aprire direttamente file di configurazione, cercare i servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] \/COM \+ e aprire i file di configurazione per i servizi ospitati su Web.  
  
 L'interfaccia utente dell'Editor di configurazione dei servizi è suddivisa nelle aree seguenti:  
  
-   Il riquadro di visualizzazione struttura ad albero, in cui gli elementi di configurazione sono visualizzati in una struttura ad albero a sinistra.Per eseguire operazioni sulla struttura ad albero è possibile fare clic con il pulsante destro del mouse sui nodi.  
  
-   Il riquadro attività, in cui le attività comuni degli elementi correnti sono visualizzate nell'angolo inferiore sinistro della finestra.  
  
-   Il riquadro dettagli, in cui vengono visualizzate le impostazioni dettagliate del nodo di configurazione selezionato nella visualizzazione struttura ad albero a destra.  
  
### Apertura di un file di configurazione  
  
1.  Avviare l'Editor di configurazione dei servizi. A tale scopo, utilizzare una finestra di comando per passare al percorso di installazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e quindi digitare `SvcConfigEditor.exe`.  
  
2.  Scegliere **Apri** dal menu **File** e fare clic sul tipo di file che si desidera gestire.  
  
3.  Nella finestra di dialogo **Apri**, passare al file specifico che si desidera gestire e fare doppio clic su di esso.  
  
 Il visualizzatore segue automaticamente il percorso dell'unione delle configurazioni e crea una visualizzazione della configurazione unita.Ad esempio, la configurazione effettiva di un servizio non ospitato è una combinazione di Machine.config e App.config.Le modifiche vengono apportate al file attivo nell'editor SvcConfigEditor.Se si desidera modificare un file specifico all'interno del percorso di unione delle configurazioni, è necessario aprirlo direttamente.  
  
> [!NOTE]
>  L'Editor di configurazione ricarica il file di configurazione attualmente aperto quando quest’ultimo è stato modificato fuori dell'Editor.Quando si verifica questa condizione, tutte le modifiche che non sono state salvate in modo durevole nell'Editor verranno perse.Se il nuovo caricamento si verifica costantemente, la causa più probabile è un servizio che accede continuamente al file di configurazione, ad esempio un software antivirus in esecuzione in background.Per risolvere questo problema, assicurarsi che l'Editor di configurazione sia l'unico processo che può accedere al file quando è aperto.  
  
### Services  
 Nel nodo **Servizi** vengono visualizzati tutti i servizi attualmente assegnati presenti nel file di configurazione.Ogni sottonodo della struttura ad albero corrisponde a un sottoelemento dell'elemento \<`services`\> del file di configurazione.  
  
 Quando si fa clic sul nodo **Servizi** viene visualizzata la Pagina di riepilogo del servizio. Nel **Riquadro dettagli** disponibile in tale pagina è possibile visualizzare o eseguire attività.  
  
#### Creazione di una nuova configurazione di un servizio  
 Per creare una nuova configurazione di un servizio, è possibile procedere nei modi seguenti:  
  
-   Utilizzo di una procedura guidata: fare clic sul collegamento **Crea un nuovo servizio** nel Riquadro attività o nella Pagina di riepilogo per avviare la procedura guidata.Questa operazione può inoltre essere eseguita scegliendo **File** \-\> **Aggiungi nuovo elemento**.  
  
-   Creazione manuale: è possibile fare clic con il pulsante destro del mouse sul nodo **Servizi** e scegliere **Nuovo servizio**.  
  
#### Creazione di una nuova configurazione di endpoint di servizio  
 Per creare una nuova configurazione di endpoint di servizio, è possibile procedere nei modi seguenti:  
  
-   Creazione tramite una procedura guidata: fare clic sul collegamento **Crea un nuovo endpoint del servizio** nel Riquadro attività o nella Pagina di riepilogo per avviare la procedura guidata.Questa operazione può inoltre essere eseguita scegliendo **File** \-\> **Aggiungi nuovo elemento**.  
  
-   Creazione manuale: dopo aver creato un servizio è possibile fare clic con il pulsante destro del mouse sul nodo **Endpoint** e scegliere “**Nuovo endpoint del servizio**”.  
  
#### Modifica della configurazione di un servizio  
  
1.  Fare clic su un nodo **Servizio**.  
  
2.  Modificare le impostazioni nelle griglie delle proprietà.  
  
#### Modifica della configurazione di un endpoint di servizio  
  
1.  Fare clic su un nodo **Endpoint di servizio**.  
  
2.  Modificare le impostazioni nelle griglie delle proprietà.  
  
#### Aggiunta di un indirizzo di base  
  
1.  Fare clic sul nodo **Host**.  
  
2.  Fare clic sul pulsante **Nuovo** nella sezione **Indirizzi di base**.  
  
3.  Immettere l'indirizzo URI di base nella finestra di dialogo.  
  
4.  Scegliere **OK**.  
  
> [!NOTE]
>  Non è possibile modificare il valore di [\<FiltriPrefissoIndirizzoBase\>](../../../docs/framework/configure-apps/file-schema/wcf/baseaddressprefixfilters.md) in questo strumento.Per aggiungere o modificare questo elemento è necessario utilizzare un editor di testo o [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
### Client  
 Nel nodo **Client** vengono visualizzati tutti gli endpoint client contenuti nel file di configurazione.Ogni sottonodo della struttura ad albero corrisponde a un sottoelemento dell'elemento \<`client`\> del file di configurazione.  
  
 Quando si fa clic sul nodo **Client** viene visualizzata la **Pagina di riepilogo** del client. Nel **Riquadro dettagli** disponibile in questa pagina è possibile visualizzare o eseguire attività.  
  
#### Creazione di una nuova configurazione di endpoint client  
 Per creare una nuova configurazione di endpoint client, è possibile procedere nei modi seguenti:  
  
-   Creazione tramite procedura guidata: fare clic sul collegamento **Crea un nuovo client** nel **Riquadro attività** nella parte inferiore sinistra della finestra o nella **Pagina di riepilogo** per avviare la procedura guidata.Questa operazione può inoltre essere eseguita scegliendo **File** \-\> **Aggiungi nuovo elemento**.Verrà richiesto di individuare la posizione della configurazione del servizio, da cui viene generata la configurazione client.A questo punto è possibile specificare l'endpoint del servizio a cui connettersi.  
  
-   Creazione manuale: fare clic con il pulsante destro del mouse sul nodo **Endpoint** in **Client**, quindi scegliere **Nuovo endpoint client**.  
  
#### Modifica di una configurazione di endpoint client  
  
1.  Fare clic su un nodo **Endpoint client**.  
  
2.  Modificare le impostazioni nelle griglie delle proprietà.  
  
### Endpoint standard  
 Gli endpoint standard sono endpoint specializzati in cui uno o più aspetti dell'indirizzo, del contratto e dell'associazione sono impostati sui valori predefiniti.  
  
 Tali impostazioni di configurazione sono archiviate nel nodo **Endpoint standard**.Nel nodo **Endpoint standard** vengono visualizzate tutte le impostazioni dell'endpoint standard del file di configurazione.Ogni sottonodo della struttura ad albero corrisponde a un sottoelemento dell'elemento `<standardEndpoints>` del file di configurazione.  
  
 Quando si fa clic sul nodo **Endpoint standard**, viene visualizzata la **Pagina di riepilogo** dell'endpoint standard. Nel **Riquadro dettagli** disponibile in tale pagina è possibile visualizzare o eseguire attività.  
  
#### Creazione di una nuova configurazione di endpoint standard  
 Per creare una nuova configurazione di endpoint standard, è possibile procedere nei modi seguenti:  
  
-   Fare clic con il pulsante destro del mouse sul nodo **Endpoint standard** e scegliere **Configurazione nuovo endpoint standard**. Selezionare il tipo di associazione nella finestra di dialogo e fare clic su **OK**.  
  
-   Selezionare il nodo **Endpoint standard** e fare clic su **Configurazione nuovo endpoint standard** nel **riquadro attività** in basso a sinistra nella finestra.  
  
 Verrà visualizzata la finestra di dialogo **Crea un nuovo endpoint standard** in cui sono elencati tutti i tipi di endpoint standard registrati.  
  
#### Visualizzazione e modifica di una configurazione di endpoint standard  
 Per aprire una configurazione di endpoint standard per la visualizzazione e la modifica, è possibile procedere nei modi seguenti:  
  
-   Fare clic per espandere il nodo **Endpoint standard** e fare clic sul rispettivo sottonodo dell'endpoint.  
  
-   Fare clic sul nodo **Endpoint standard** e sul rispettivo endpoint nel riquadro dei dettagli.  
  
 Gli attributi dell'endpoint vengono visualizzati nel riquadro di destra per la modifica.  
  
#### Eliminazione di una configurazione di endpoint standard  
 Per eliminare una configurazione di endpoint standard, è possibile procedere nei modi seguenti:  
  
-   Fare clic per espandere il nodo **Endpoint standard** e fare clic con il pulsante destro del mouse sul rispettivo sottonodo dell'endpoint.Utilizzare il comando di contesto **Elimina configurazione endpoint standard** per eliminare l'endpoint.  
  
-   Fare clic sul nodo **Endpoint standard**.Nel riquadro **Attività** fare clic su **Elimina configurazione endpoint standard**.  
  
 Se si utilizza l'endpoint standard, viene visualizzato un messaggio di avviso quando si tenta di eliminarlo: **Endpoint standard in uso. Se lo si elimina ora, assicurarsi di eliminare tutti i relativi riferimenti presenti in altre parti della configurazione \(ad esempio, nell'endpoint del servizio\). In caso contrario la configurazione non sarà valida e non potrà essere aperta in seguito. Eliminare l'endpoint standard?”**  
  
### Associazione  
 Le configurazioni di associazione consentono di configurare le associazioni sugli endpoint.Tali impostazioni di configurazione vengono archiviate nel nodo **Associazione**.Gli endpoint fanno riferimento alle configurazioni di associazione in base al nome. Inoltre, più endpoint possono fare riferimento a una stessa configurazione di associazione.  
  
 Nel nodo **Associazioni** vengono visualizzate tutte le impostazioni di associazione contenute nel file di configurazione.Ogni sottonodo della struttura ad albero corrisponde a un sottoelemento dell'elemento \<`bindings`\> del file di configurazione.  
  
 Quando si fa clic sul nodo **Associazioni** viene visualizzata la **Pagina di riepilogo** dell’associazione. Nel **Riquadro dettagli** disponibile in questa pagina è possibile visualizzare o eseguire attività.  
  
#### Creazione di una nuova configurazione di associazione  
 Per creare una nuova configurazione dell’associazione, è possibile procedere nei modi seguenti.  
  
-   Fare clic con il pulsante destro del mouse sul nodo **Associazioni** e scegliere **Nuova configurazione dell’associazione**… Selezionare il tipo di associazione nella finestra di dialogo e fare clic su **OK**.  
  
-   Selezionare il nodo **Associazioni**, quindi fare clic su **Nuova configurazione dell'associazione** nel **riquadro attività** nella parte inferiore sinistra della finestra.  
  
-   Nella pagina di riepilogo del servizio o del client, scegliere **Fare clic per creare** nel campo **Configurazione dell'associazione** per creare una configurazione di associazione per l'endpoint corrispondente.  
  
#### Aggiunta di estensioni degli elementi di associazione a un'associazione personalizzata  
  
1.  Selezionare l'associazione a cui si desidera aggiungere un elemento di estensione.  
  
2.  Scegliere **Aggiungi**.  
  
3.  Nell'elenco di estensioni disponibili, selezionare l'estensione degli elementi di associazione che si desidera aggiungere.Per selezionare più elementi, premere contemporaneamente CTRL.  
  
4.  Scegliere **Aggiungi**.  
  
#### Impostazione della posizione dell'estensione in un'associazione personalizzata  
 Un'associazione personalizzata è una raccolta di elementi di associazione organizzati in uno stack.Ogni elemento di associazione dello stack può essere configurato in modo specifico.L'ordine delle estensioni degli elementi di associazione in un'associazione personalizzata indica la posizione occupata da ogni estensione nello stack.Gli elementi all'inizio dello stack vengono applicati per primi.Per modificare l'ordine:  
  
1.  Selezionare il nodo dell'associazione personalizzata.  
  
2.  Selezionare un elemento di estensione dell'associazione nella sezione **Posizione dell'estensione degli elementi di associazione**.  
  
3.  Utilizzare il pulsante **Su** o **Giù** a sinistra dell'elenco per modificare la posizione dell'elemento selezionato.  
  
#### Modifica della configurazione di estensioni degli elementi di associazione in un'associazione personalizzata  
  
1.  Selezionare il nodo dell'associazione nella struttura ad albero.  
  
2.  Selezionare l'associazione personalizzata contenente l'elemento che si desidera modificare.  
  
3.  Selezionare l'estensione degli elementi di associazione che si desidera modificare.Le impostazioni dell'elemento verranno visualizzate nel riquadro di destra, in cui è inoltre possibile modificarle.  
  
### Diagnostica  
 Nel nodo **Diagnostica** vengono visualizzate tutte le impostazioni di diagnostica contenute nel file di configurazione.Consente di attivare e disattivare i contatori delle prestazioni, abilitare o disabilitare Strumentazione gestione Windows \(WMI\), nonché di configurare le funzionalità di traccia [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e di registrazione dei messaggi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Le impostazioni del nodo **Diagnostica** corrispondono alla sezione \<`system.diagnostics`\> e alla sezione `<diagnostics>` in `<system.serviceModel>`del file di configurazione.  
  
 Quando si fa clic sul nodo **Diagnostica** viene visualizzata la **Pagina di riepilogo** della diagnostica. Nel **Riquadro dettagli** disponibile in tale pagina è possibile visualizzare o eseguire attività.  
  
#### Configurazione dei contatori delle prestazioni e di WMI  
  
1.  Fare clic sul nodo **Diagnostica**.  
  
2.  Fare clic su **Attiva\/Disattiva contatori delle prestazioni**.Il contatore delle prestazioni prevede tre stati: Disattivo \(predefinito\), Solo servizio e Tutto.Il collegamento consente di attivare\/disattivare l'impostazione degli stati.  
  
#### Configurazione del provider WMI  
  
1.  Fare clic sul nodo **Diagnostica**.  
  
2.  Per abilitare il provider WMI, fare clic sul collegamento **Abilita Provider WMI**.  
  
#### Abilitazione della traccia WCF  
 È possibile creare un file di traccia [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con le proprietà standard oppure configurare un file di traccia personalizzato.  
  
1.  Fare clic sul nodo **Diagnostica**.  
  
2.  Fare clic su **Abilita Traccia**.  
  
3.  Fare clic sul collegamento **Livello traccia** per modificare il livello di traccia.Esistono sei livelli di traccia: Disattivo, Critico, Errore, Avviso, Informazioni e Dettagliato.Le opzioni **Traccia attività** e **Propaga attività** consentono di utilizzare la funzionalità di traccia delle attività di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
4.  Fare clic sul nome del listener di traccia per specificare il file e le opzioni di traccia.  
  
#### Abilitazione della registrazione WCF  
 È possibile creare un file di traccia [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con le proprietà standard oppure configurare un file di traccia personalizzato.  
  
1.  Fare clic sul nodo **Diagnostica**.  
  
2.  Fare clic su **Abilita Registrazione messaggi**.  
  
3.  Fare clic sul collegamento **Livello log** per regolare il livello.Esistono tre livelli di log: Messaggi in formato non valido, Messaggi servizio e Messaggi trasporto.  
  
4.  Fare clic sul nome del listener per specificare le opzioni e il file di log.  
  
> [!NOTE]
>  Se si desidera scaricare automaticamente i log dei messaggi e dei file di traccia alla chiusura dell'applicazione, abilitare l'opzione **Cancellazione automatica registro**.  
  
 Nella **Pagina di riepilogo** della **Diagnostica** è possibile eseguire le attività di configurazione di diagnostica più comuni.Se tuttavia si desidera modificare manualmente le impostazioni Listener e Origini, è necessario espandere il nodo **Diagnostica** e modificare le impostazioni dei nodi **Registrazione messaggi**, **Listener** e **Origini**.  
  
#### Abilitazione della tracciatura o della registrazione dei messaggi personalizzata di WCF  
  
1.  Fare clic sul nodo **Diagnostica** e quindi espanderlo.  
  
2.  Fare clic con il pulsante destro del mouse sul nodo **Listener** e scegliere **Nuovo listener**.  
  
3.  Immettere il nome del file di traccia nel campo **InitData**.È possibile fare clic sul pulsante con i puntini di sospensione \(…\) per selezionare un percorso specifico.  
  
4.  Se si fa clic sulla riga **TypeName** viene visualizzato un pulsante con i puntini di sospensione “…”.Fare clic su questo pulsante per aprire il **Browser dei tipi di listener di traccia**, in cui è possibile cercare i listener di traccia preconfigurati già installati.  
  
5.  Nella sezione **Origine**,fare clic su **Aggiungi** per aprire una finestra di dialogo contenente un menu a discesa in cui sono elencate le origini di traccia disponibili.Scegliere un'origine di traccia e quindi fare clic su **OK**.  
  
6.  Per modificare le impostazioni di registrazione dei messaggi, fare clic sul nodo **Registrazione messaggi**.Le impostazioni possono essere modificate nella griglia delle proprietà.  
  
### Avanzate  
  
#### Comportamenti  
 Nel nodo **Comportamenti** vengono visualizzati i comportamenti attualmente definiti nel file di configurazione.  
  
 Le configurazioni dei comportamenti consentono di impostare i comportamenti di endpoint e servizi.Tali impostazioni di configurazione sono archiviate nel nodo **Avanzate** in **Comportamenti del servizio** e **Comportamenti endpoint**.I comportamenti del servizio sono utilizzati dai servizi, mentre i comportamenti degli endpoint sono utilizzati dagli endpoint.  
  
 I comportamenti sono una raccolta di elementi di estensione organizzati in uno stack.L'elemento all'inizio dello stack viene applicato per primo.Ogni elemento di estensione può essere configurato in modo specifico.  
  
##### Creazione di una nuova configurazione di un comportamento  
 Per creare una nuova configurazione di un comportamento, è possibile procedere nei due modi seguenti:  
  
-   Fare clic con il pulsante destro del mouse su uno dei nodi dei comportamenti e scegliere “**Nuova configurazione del comportamento…**  
  
-   Selezionare uno dei nodi dei comportamenti e fare clic su **Nuova configurazione del comportamento** nel **riquadro attività** nella parte inferiore sinistra della finestra.  
  
##### Aggiunta di estensioni degli elementi del comportamento a un comportamento  
  
1.  Selezionare uno dei nodi dei comportamenti.  
  
2.  Selezionare il comportamento che si desidera modificare.  
  
3.  Scegliere **Aggiungi**.  
  
4.  Nell'elenco di estensioni disponibili, selezionare l'estensione degli elementi del comportamento che si desidera aggiungere.  
  
5.  Scegliere **Aggiungi**.  
  
##### Impostazione della posizione dell'estensione in un Comportamento  
 I comportamenti sono raccolte di elementi organizzati in uno stack.Ogni elemento dello stack può essere configurato in modo specifico.L'ordine delle estensioni degli elementi di comportamento in un comportamento indica la posizione occupata da ogni estensione nello stack.Gli elementi all'inizio dello stack vengono applicati per primi.Per modificare l'ordine:  
  
1.  selezionare uno dei nodi dei comportamenti.  
  
2.  Selezionare il comportamento che si desidera modificare.  
  
3.  Selezionare un elemento di estensione del comportamento nella sezione **Posizione dell'estensione degli elementi di comportamento**.  
  
4.  Utilizzare il pulsante **Su** o **Giù** a sinistra dell'elenco per modificare la posizione dell'elemento selezionato.  
  
##### Modifica della configurazione delle estensioni degli elementi del comportamento  
  
1.  Selezionare uno dei nodi dei comportamenti nella struttura ad albero.  
  
2.  Selezionare il comportamento contenente l'elemento che si desidera modificare.  
  
3.  Selezionare l'estensione dell'elemento del comportamento che si desidera modificare.Le impostazioni dell'elemento sono visualizzate nel riquadro a destra, in cui è inoltre possibile modificarle.  
  
#### ProtocolMapping  
 In questa sezione è possibile impostare i tipi di associazione predefiniti per i vari protocolli, quali http, tcp, MSMQ e net.pipe, tramite il mapping definito tra gli schemi di indirizzi dei protocolli e le possibili associazioni.È inoltre possibile aggiungere nuovi mapping ad altri protocolli.  
  
#### Estensioni  
 Le nuove estensioni delle associazioni, degli elementi delle associazioni, degli endpoint standard e dei comportamenti possono essere registrate per essere utilizzate nella configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Ogni estensione è costituita da una coppia nome\/tipo.Il primo elemento della coppia definisce il nome dell'estensione nella configurazione, mentre il secondo implementa l'estensione.Esistono quattro tipi di estensione:  
  
-   Le estensioni delle associazioni definiscono un intero tipo di associazione.Esempio: `basicHttpBinding`.  
  
-   Le estensioni degli elementi di associazione definiscono un elemento di un'associazione.Esempio: `textMessageEncoding`.  
  
-   Le estensioni degli endpoint standard definiscono un endpoint standard intero.Esempio: `discoveryEndpoint`.  
  
-   Le estensioni degli elementi di comportamento definiscono un elemento di un comportamento.Esempio: `clientVia`.  
  
 Le estensioni registrate nella configurazione possono essere utilizzate come qualsiasi altro componente [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] dello stesso tipo.  
  
##### Aggiunta di una nuova estensione  
 Selezionare uno dei nodi delle estensioni nei nodi avanzati:  
  
1.  fare clic su **Nuovo**.  
  
2.  Immettere un nome e un tipo.  
  
3.  Scegliere **OK**.  
  
4.  L'estensione verrà quindi visualizzata nella sezione appropriata dell'editor.Se ad esempio si aggiunge un'estensione di un elemento di un comportamento, questa verrà visualizzata nell'elenco delle estensioni disponibili.  
  
#### Ambiente host  
 Questa sezione consente di definire le impostazioni di creazione delle istanze per l'ambiente host del servizio.  
  
### Creazione di un file di configurazione utilizzando la procedura guidata  
 Uno dei sistemi disponibili per la creazione di nuovo file di configurazione consiste nell'utilizzo della Creazione guidata nuovo elemento del servizio.La procedura guidata consente di individuare i tipi di servizio e gli altri elementi compatibili con [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] installati nel computer, incluse le applicazioni COM\+ e le directory virtuali ospitate su Web, e quindi carica tali elementi in modo da semplificare notevolmente la creazione della configurazione.  
  
#### Creazione di un file di configurazione  
  
1.  Avviare l'Editor di configurazione dei servizi. A tale scopo, utilizzare una finestra di comando per passare al percorso di installazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e quindi digitare `SvcConfigEditor.exe`.  
  
2.  Scegliere **Apri** dal menu **File**, quindi, a seconda del tipo di file di configurazione che si desidera creare, fare clic su **Eseguibile**, **Servizio COM\+** o **Servizio WebHosted**.  
  
3.  Nella finestra di dialogo **Apri**, passare al file specifico per cui si desidera creare un file di configurazione e quindi fare doppio clic su di esso.  
  
4.  Scegliere **Aggiungi nuovo elemento** dal menu **File** e fare clic su **Servizio**.Verrà avviata la Creazione guidata nuovo elemento del servizio.  
  
5.  Attenersi alle istruzioni fornite nella procedura guidata per creare il nuovo servizio.  
  
> [!NOTE]
>  Se si desidera utilizzare NetPeerTcpBinding dal file di configurazione creato tramite la Procedura guidata, si deve aggiungere manualmente un elemento di configurazione dell’associazione e modificare l'attributo `mode` dell’elemento `security` in “None”.  
  
## Configurazione di COM\+  
 L'Editor di configurazione dei servizi consente di creare un nuovo file di configurazione per un'applicazione COM\+ esistente o di modificare una configurazione COM\+ esistente.Il nodo **Contratto COM** è visibile solo quando il file di configurazione contiene la sezione \<`comContract`\>.  
  
### Creazione di una nuova configurazione COM\+  
 Prima di creare una nuova configurazione COM\+, verificare che l'applicazione COM\+ sia stata installata in Servizi componenti e registrata nella Global Assembly Cache \(GAC\).  
  
1.  Scegliere **File** \-\> **Integra** \-\> **Applicazione COM\+**. Questa operazione determina la chiusura del file attualmente aperto.Se il file corrente contiene dati non salvati, verrà visualizzata la finestra di dialogo Salva.Verrà quindi avviata l'**Integrazione guidata COM\+**.  
  
2.  Nella prima pagina, selezionare l'applicazione COM\+ nella struttura ad albero.Se risulta impossibile individuare l'applicazione COM\+ nella struttura ad albero, verificare che sia stata installata in Servizi componenti e registrata nella Global Assembly Cache \(GAC\).  
  
3.  Nella pagina successiva, selezionare i metodi che si desidera esporre come servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Tutti i metodi supportati dell'applicazione COM\+ sono visualizzati e selezionati per impostazione predefinita.  
  
4.  Scegliere un metodo di hosting.  
  
5.  Configurare le altre impostazioni secondo le istruzioni della procedura guidata.  
  
6.  L'Editor di configurazione dei servizi utilizza in background ComSvcConfig.exe per generare un file di configurazione.Al termine di questa operazione sarà possibile esaminare un riepilogo e quindi uscire dalla procedura guidata.Verrà automaticamente aperto il file di configurazione in modo da consentirne la modifica diretta.  
  
### Modifica di una configurazione COM\+ esistente  
  
1.  Nel menu **File** \-\> scegliere **Apri** \-\> **COM\+ Service**…  
  
2.  Selezionare nell'elenco il servizio COM\+ che si desidera modificare.  
  
3.  Modificare le impostazioni di configurazione nel nodo **Contratti COM**.  
  
    > [!NOTE]
    >  È inoltre possibile aprire e modificare direttamente un file di configurazione contenente contratti COM.  
  
## Sicurezza  
 Un file di configurazione del servizio generato dall'Editor di configurazione non è necessariamente protetto.Fare riferimento alla documentazione [Sicurezza](../../../docs/framework/wcf/feature-details/security.md) per verificare come proteggere i servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 L’Editor di Configurazione, inoltre, può essere utilizzato solo per leggere e scrivere elementi di configurazione  [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] validi.Lo strumento ignora elementi conformi allo schema, definiti dall'utente.Inoltre, non tenta di rimuovere questi elementi dal file di configurazione o di determinarne gli effetti sugli elementi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] conosciuti.L’utente è tenuto a determinare se questi elementi possono costituire una minaccia per l'applicazione o il sistema.