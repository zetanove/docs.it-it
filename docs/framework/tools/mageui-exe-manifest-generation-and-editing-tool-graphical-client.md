---
title: MageUI.exe (Strumento per la generazione e la modifica di manifesti, client grafico) | Documentazione Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Manifest Generation and Editing tool
- MageUI.exe
ms.assetid: f9e130a6-8117-49c4-839c-c988f641dc14
caps.latest.revision: 38
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: acd994c4b36200a924c537750f7e8b14a24d06c8
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="mageuiexe-manifest-generation-and-editing-tool-graphical-client"></a>MageUI.exe (Strumento per la generazione e la modifica di manifesti, client grafico)
MageUI.exe supporta le stesse funzionalità dello strumento da riga di comando Mage.exe, ma con un'interfaccia utente basata su Windows. Con questo strumento è possibile creare, modificare e firmare manifesti di distribuzione e di applicazione. I nuovi manifesti creati con MageUI.exe sono destinati a [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)]. È necessario usare versioni precedenti di MageUI.exe per le versioni precedenti di .NET Framework. In caso di aggiunta o rimozione di assembly da un manifesto o di apposizione di una nuova firma a manifesti esistenti, MageUI.exe non aggiorna il manifesto per destinarlo a [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)]. Per altre informazioni, vedere [Mage.exe (Strumento per la generazione e la modifica di manifesti)](../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md).  
  
 Viene installato automaticamente con Visual Studio. Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7. Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Due versioni di Mage.exe e MageUI.exe sono incluse come componenti del pacchetto d'installazione di [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)]. Per visualizzare le informazioni sulla versione, eseguire MageUI.exe, scegliere **?**, quindi **Informazioni su**. In questa documentazione viene descritta la versione 4.0.x.x di Mage.exe e MageUI.exe.  
  
> [!NOTE]
>  MageUI.exe non supporta l'elemento [compatibleFrameworks](/visualstudio/deployment/compatibleframeworks-element-clickonce-deployment) nel salvataggio di un manifesto di applicazione che è già stato firmato con un certificato usando MageUI.exe. È invece necessario usare [Mage.exe](../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md).  
  
## <a name="uielement-list"></a>Elenco UIElement  
 Nella tabella riportata di seguito vengono elencate le voci disponibili nei menu e sulla barra degli strumenti.  
  
|Comando|Menu|Collegamento|Descrizione|  
|-------------|----------|--------------|-----------------|  
|**Manifesto dell'applicazione**|**File, Nuovo**||Crea un nuovo manifesto di applicazione.|  
|**Manifesto di distribuzione**|**File, Nuovo**||Crea un nuovo manifesto di distribuzione.|  
|**Apri**|**File**|CTRL+O|Apre un manifesto di distribuzione, un manifesto di applicazione o una licenza di attendibilità esistente per consentirne la modifica.|  
|**Chiudi**|**File**|CTRL+F4|Chiude un file aperto.<br /><br /> Se si modifica un file prima di chiuderlo, verrà chiesto di firmarlo nuovamente con una chiave pubblica, una coppia di chiavi o un certificato archiviato.|  
|**Salva**|**File**|CTRL+S|Salva su disco il documento attualmente con lo stato attivo per l'input dell'utente.|  
|**Salva con nome**|**File**||Salva un file su disco consentendo di specificare un nuovo nome e/o un nuovo percorso.|  
|**Salva tutto**|**File**||Salva le modifiche apportate a tutti i file attualmente aperti in MageUI.exe.|  
|**Preferenze**|**File**||Apre la finestra di dialogo **Preferenze**. Per altre informazioni, vedere la sezione successiva.|  
|**File**|**File**|ALT + F4|Chiude MageUI.exe.|  
|**Taglia**|**Modifica**|CTRL+X|Rimuove il testo attualmente selezionato dall'applicazione e lo sposta negli Appunti di sistema.|  
|**Copia**|**Modifica**|CTRL+C|Copia negli Appunti di sistema il testo attualmente selezionato.|  
|**Incolla**|**Modifica**|CTRL+V|Incolla il testo dagli Appunti di sistema nell'elemento di testo attualmente attivo.|  
|**Eliminazione**|**Modifica**||Elimina un elemento attualmente selezionato in un elenco, ad esempio una licenza di attendibilità nella scheda **Manifesto di distribuzione**.|  
|**Chiudi tutto**|**Finestra**||Chiude tutti i file attualmente aperti in MageUI.exe. Se è necessario salvare uno o più file, verrà chiesto di effettuare il salvataggio. Verrà inoltre chiesto di selezionare una chiave di firma per ogni file non firmato o modificato.|  
|**Informazioni su**|**Guida**||Visualizza le informazioni sulla versione e sul copyright relative a MageUI.exe.|  
  
## <a name="preferences-dialog-box"></a>Finestra di dialogo Preferenze  
 Nella finestra di dialogo **Preferenze** sono inclusi i seguenti elementi.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Firma al salvataggio**|Visualizza la richiesta di firma di un file ogni volta che si salvano le modifiche.|  
|**Usa certificato di firma predefinito**|Usa la chiave specificata nella casella di testo **File di certificato** per firmare tutti i file. In questo modo viene eliminata la richiesta di firma visualizzata quando si salva un file ed è selezionata l'opzione **Firma al salvataggio**. Usare il pulsante con i puntini di sospensione (**…**) accanto alla casella di testo **File di certificato** per selezionare un file di chiave.|  
|Algoritmo digest|Specifica l'algoritmo con cui generare i digest di dipendenza. Il valore deve essere "sha256RSA" o "sha1RSA". Usa SHA1 come predefinito. Usato sia nei manifesti di applicazione che di distribuzione. Se l'utente fornisce un certificato quando salva il manifesto, usa gli algoritmi nel certificato con cui generare i digest di dipendenza.|  
  
## <a name="signing-options-dialog-box"></a>Finestra di dialogo Opzioni di firma  
 La finestra di dialogo **Opzioni di firma** viene visualizzata quando si salva per la prima o quando si modifica un manifesto o una licenza di attendibilità. Viene visualizzata solo se l'opzione **Firma al salvataggio** nella finestra di dialogo **Preferenze** è selezionata. È necessario essere connessi a Internet quando si firma un manifesto che specifica un valore nella casella di testo **TimeStamp URI**.  
  
 In questa finestra di dialogo sono inclusi i seguenti elementi:  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Firma con file di certificato**|Firma il manifesto con un certificato digitale archiviato nel file system.|  
|**File**|Fornisce un'area per digitare il percorso del file .pfx che rappresenta il certificato.|  
|**...**|Apre la finestra di dialogo **Scegli File** per la selezione di un file .pfx esistente.|  
|**Nuovo**|Genera un nuovo file .pfx non verificabile tramite un'Autorità di certificazione (CA). Per altre informazioni sui tipi di certificati usati per firmare le distribuzioni di [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)], vedere [Panoramica della distribuzione di applicazioni attendibili](/visualstudio/deployment/trusted-application-deployment-overview).|  
|**Password**|Fornisce un'area per digitare la password usata per la firma con il certificato. Se la password non è applicabile, il campo può essere lasciato vuoto.|  
|**Firma con certificato archiviato**|Visualizza un elenco selezionabile di certificati digitali presenti nell'archivio certificati del computer.|  
|**TimeStamp URI**|Visualizza l'URI (Uniform Resource Locator) di un servizio di aggiunta di timestamp digitale. L'aggiunta di timestamp nei manifesti evita la necessità di firmarli nuovamente in caso di scadenza del certificato digitale prima della distribuzione della versione successiva dell'applicazione. Per altre informazioni, vedere [Membri del programma Root Certificate di Windows](http://go.microsoft.com/fwlink/?LinkId=159000) e [ClickOnce e Authenticode](/visualstudio/deployment/clickonce-and-authenticode).|  
|**Non firmare**|Consente di salvare il manifesto senza aggiungere una firma da un certificato digitale.|  
  
## <a name="tab-and-panel-descriptions"></a>Descrizioni di schede e pannelli  
 Un documento che viene aperto con MageUI.exe viene visualizzato all'interno della propria scheda. In ciascuna scheda è incluso un set di pannelli di proprietà in cui sono riportati i dati del documento, raggruppati in subset.  
  
### <a name="application-manifest-tab"></a>Scheda Manifesto dell'applicazione  
 La scheda **Manifesto dell'applicazione** visualizza i contenuti di un manifesto dell'applicazione. Il manifesto dell'applicazione descrive tutti i file inclusi nella distribuzione e le autorizzazioni necessarie per eseguire l'applicazione nel client.  
  
 La scheda **Manifesto dell'applicazione** contiene le seguenti schede.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Nome**|Specifica le informazioni di identificazione relative a questa distribuzione.|  
|**Descrizione**|Specifica le informazioni relative a editore, prodotto e supporto.|  
|**Opzioni dell'applicazione**|Specifica se è un'applicazione browser e se il manifesto è l'origine delle informazioni di attendibilità.|  
|**File**|Specifica tutti i file che costituiscono la distribuzione.|  
|**Autorizzazioni necessarie**|Specifica il set di autorizzazioni minimo richiesto per eseguire l'applicazione in un client.|  
  
### <a name="name-tab"></a>Scheda Nome  
 La scheda **Nome** viene visualizzata quando si crea o si apre un manifesto dell'applicazione per la prima volta. Identifica in modo univoco la distribuzione e facoltativamente specifica una piattaforma di destinazione valida.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Nome**|Obbligatorio. Il nome del manifesto dell'applicazione. In genere coincide con il nome del file.|  
|**Version**|Obbligatorio. Il numero di versione della distribuzione nel formato *N.N.N.N*. È necessario solo il primo numero della build principale. Ad esempio, per la versione 1.0 di un'applicazione, i valori validi sono `1`, `1.0`, `1.0.0` e `1.0.0.0`.|  
|**Processore**|Facoltativo. L'architettura del computer in cui è possibile eseguire la distribuzione. Il valore predefinito è `msil`, ossia Microsoft Intermediate Language, che rappresenta il formato predefinito di tutti gli assembly gestiti. Modificare questo campo se gli assembly nell'applicazione sono stati precompilati per un'architettura specifica. Per altre informazioni sulla precompilazione, vedere [Ngen.exe (Native Image Generator)](../../../docs/framework/tools/ngen-exe-native-image-generator.md).|  
|**Impostazioni cultura**|Parametro facoltativo. Il codice ISO di paese e area in due parti in cui viene eseguita l'applicazione. Il valore predefinito è `neutral`.|  
|**Token di chiave pubblica**|Parametro facoltativo. La chiave pubblica con cui è stato firmato il manifesto dell'applicazione. Se si tratta di un manifesto nuovo o non firmato, questo campo verrà visualizzato come `Unsigned`.|  
  
### <a name="description-tab"></a>Scheda Descrizione  
 Queste informazioni sono generalmente disponibili all'interno del manifesto della distribuzione. Questi campi possono essere modificati solo se la casella di controllo **Usa manifesto applicazione per informazioni sull'attendibilità** è selezionata nella scheda **Opzioni applicazione**.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Server di pubblicazione**|Il nome della persona o dell'organizzazione responsabile dell'applicazione. Questo valore viene usato come nome della cartella del menu Start.|  
|**Prodotto**|Il nome del prodotto completo. Se si seleziona **Installazione locale** per l'elemento **Tipo di applicazione** nella scheda **Opzioni di distribuzione** del manifesto della distribuzione, questo nome sarà quello visualizzato nel collegamento del menu **Start** e in **Installazione applicazioni** per questa applicazione.|  
|**Percorso del supporto**|L'URL tramite cui i clienti possono ottenere assistenza e supporto per l'applicazione.|  
  
### <a name="application-options-tab"></a>Scheda Opzioni applicazione  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Applicazione browser di Windows Presentation Foundation**|Specifica se si tratta di un'applicazione WPF eseguita nel browser come applicazione browser XAML (XBAP).|  
|**Usa manifesto applicazione per informazioni sull'attendibilità**|Specifica se il manifesto contiene informazioni sull'attendibilità.|  
  
### <a name="files-tab"></a>Scheda File  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Directory dell'applicazione**|La directory in cui si trovano i file dell'applicazione. Usare il pulsante con i puntini di sospensione (**…**) per selezionare la directory.|  
|**Popola**|Aggiunge tutti i file nella directory dell'applicazione e le sottodirectory nel manifesto dell'applicazione. Se MageUI.exe rileva un unico file eseguibile nella directory, questo viene contrassegnato automaticamente come Punto di ingresso, ovvero il file eseguito per primo quando viene avviata l'applicazione ClickOnce nel client.|  
|**File dell'applicazione**|Elenca tutti i file nell'applicazione. Ogni file ha tre attributi modificabili, descritti di seguito.|  
|**Tipo di file**|Il tipo di file può avere uno dei quattro valori seguenti:<br /><br /> -   Nessuno.<br />-   Punto di ingresso. Il file eseguibile principale dell'applicazione. Un solo file eseguibile può essere contrassegnato come punto di ingresso.<br />-   File di dati. Un file, ad esempio un file XML, che fornisce i dati all'applicazione.<br />-   File icona. L'icona di un'applicazione, come viene visualizzata nel desktop o nell'angolo di una finestra di un'applicazione.|  
|**Optional**|I file contrassegnati come facoltativi non vengono scaricati durante l'aggiornamento o l'installazione iniziale, ma possono essere scaricati in fase di esecuzione usando l'API su richiesta System.Deployment. Per altre informazioni, vedere [Procedura dettagliata: Download di assembly su richiesta con l'API della distribuzione ClickOnce tramite la finestra di progettazione](/visualstudio/deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer).|  
|**Gruppo**|Etichetta per un set di file facoltativi. È possibile applicare un'etichetta Gruppo a un set di file e usare l'API su richiesta per scaricare un gruppo di file con una singola chiamata API.|  
  
### <a name="permissions-required-tab"></a>Scheda Autorizzazioni necessarie  
 Usare la scheda **Autorizzazioni necessarie** per concedere all'applicazione un accesso più esteso al computer locale rispetto a quello concesso per impostazione predefinita. Per altre informazioni, vedere [Protezione di applicazioni ClickOnce](/visualstudio/deployment/securing-clickonce-applications).  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Tipo di set di autorizzazioni**|Il set di autorizzazioni minimo richiesto per eseguire l'applicazione nel client. Per una descrizione di questi set di autorizzazioni e delle autorizzazioni obbligatorie o facoltative, vedere [NIB: Set di autorizzazioni denominati](http://msdn.microsoft.com/en-us/08250d67-c99d-4ab0-8d2b-b0e12019f6e3).|  
|**Dettagli**|Il file XML creato per il manifesto dell'applicazione al fine di rappresentare il set di autorizzazioni. Se non si è esperti del formato XML del manifesto dell'applicazione, è consigliabile non modificare manualmente il file XML. Per altre informazioni, vedere [Manifesto dell'applicazione ClickOnce](/visualstudio/deployment/clickonce-application-manifest).|  
  
### <a name="deployment-manifest-tab"></a>Scheda Manifesto della distribuzione  
 La scheda **Manifesto della distribuzione** contiene le schede seguenti.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Nome**|Specifica le informazioni di identificazione relative a questa distribuzione.|  
|**Descrizione**|Specifica le informazioni relative a editore, prodotto e supporto.|  
|**Opzioni di distribuzione**|Specifica informazioni aggiuntive sulla distribuzione, ad esempio il tipo di applicazione e il percorso iniziale.|  
|**Opzioni aggiornamento**|Specifica la frequenza con cui [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] controlla la disponibilità degli aggiornamenti dell'applicazione.|  
|**Riferimento all'applicazione**|Specifica il manifesto dell'applicazione per la distribuzione.|  
  
### <a name="name-tab"></a>Scheda Nome  
 La scheda **Nome** viene visualizzata quando si crea o si apre un manifesto della distribuzione per la prima volta. Identifica in modo univoco la distribuzione e facoltativamente specifica una piattaforma di destinazione valida.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Nome**|Obbligatorio. Il nome del manifesto della distribuzione. In genere coincide con il nome del file.|  
|**Version**|Obbligatorio. Il numero di versione della distribuzione nel formato *N.N.N.N*. È necessario solo il primo numero della build principale. Ad esempio, per la versione 1.0 di un'applicazione, i valori validi sono `1`, `1.0`, `1.0.0` e `1.0.0.0`.|  
|**Processore**|Facoltativo. L'architettura del computer in cui è possibile eseguire la distribuzione. Il valore predefinito è `msil`, ossia Microsoft Intermediate Language, il formato predefinito di tutti gli assembly gestiti. Modificare questo campo se gli assembly nell'applicazione sono stati compilati per un'architettura specifica.|  
|**Impostazioni cultura**|Facoltativo. Il codice ISO di paese e area in due parti in cui viene eseguita l'applicazione. Il valore predefinito è `neutral`.|  
|**Token di chiave pubblica**|Parametro facoltativo. La chiave pubblica con cui è stato firmato il manifesto della distribuzione. Se si tratta di un manifesto nuovo o non firmato, questo campo verrà visualizzato come `Unsigned`.|  
  
### <a name="description-tab"></a>Scheda Descrizione  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Server di pubblicazione**|Obbligatorio. Il nome della persona o dell'organizzazione responsabile dell'applicazione. Questo valore viene usato come nome della cartella del menu Start.|  
|**Prodotto**|Obbligatorio. Il nome del prodotto completo. Se è stato selezionato **Installazione locale** per l'elemento **Tipo di applicazione** nella scheda **Opzioni di distribuzione**, questo nome sarà quello visualizzato nel collegamento del menu **Start** e in **Installazione applicazioni** di questa applicazione.|  
|**Percorso del supporto**|Parametro facoltativo. L'URL tramite cui i clienti possono ottenere assistenza e supporto per l'applicazione.|  
  
### <a name="deployment-options-tab"></a>Scheda Opzioni di distribuzione  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Tipo di applicazione**|Parametro facoltativo. Specifica se l'applicazione esegue l'installazione automatica nel computer client (**Installazione locale**), viene eseguita online (**Solo in linea**) oppure è un'applicazione WPF eseguita nel browser (**Applicazione browser WPF**). Il valore predefinito è **Installazione locale**.|  
|**Posizione iniziale**|Parametro facoltativo. L'URL da cui deve essere effettivamente avviata l'applicazione. È utile quando si distribuisce un'applicazione da un CD che deve aggiornarsi automaticamente dal Web.|  
|**Includi il percorso iniziale (ProviderURL) nel manifesto**|Parametro facoltativo. Specifica l'URL esaminato da [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] per gli aggiornamenti dell'applicazione.|  
|**Esegui automaticamente l'applicazione dopo l'installazione**|Obbligatorio. Specifica che l'applicazione [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] deve essere eseguita subito dopo l'installazione iniziale da un URL. Il valore predefinito prevede che la casella di controllo sia selezionata.|  
|**Consenti passaggio di parametri URL all'applicazione**|Obbligatorio. Consente il trasferimento dei dati di parametro nell'applicazione [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] tramite una stringa di query aggiunta all'URL del manifesto della distribuzione. Il valore predefinito prevede che la casella di controllo sia deselezionata.|  
|**Usa l'estensione di file .deploy**|Obbligatorio. Se è selezionato, tutti i file nel manifesto dell'applicazione devono avere l'estensione .deploy. Il valore predefinito prevede che la casella di controllo sia deselezionata.|  
  
### <a name="update-options-tab"></a>Scheda Opzioni aggiornamento  
 La scheda **Opzioni aggiornamento** contiene le opzioni sopra indicate solo quando la casella di selezione **Tipo di applicazione** nella scheda **Nome** è impostata su **Installazione locale**.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**L'applicazione deve controllare la disponibilità di aggiornamenti**|Specifica se [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] deve controllare disponibilità di aggiornamenti per l'applicazione. Se questa casella di controllo non è selezionata, l'applicazione non controllerà gli aggiornamenti a meno che non venga aggiornata a livello di codice tramite le API nello spazio dei nomi <xref:System.Deployment.Application>.|  
|**Scegliere quando controllare la disponibilità di aggiornamenti**|Fornisce due opzioni per i controlli degli aggiornamenti:<br /><br /> -   **Prima dell'avvio dell'applicazione**. Il controllo degli aggiornamenti viene eseguito prima dell'esecuzione dell'applicazione.<br />-   **Dopo l'avvio dell'applicazione**. Il controllo degli aggiornamenti viene avviato subito dopo l'inizializzazione del form principale dell'applicazione e viene eseguito al successivo avvio dell'applicazione.|  
|**Frequenza controllo disponibilità aggiornamenti**|Determina la frequenza con cui [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] controlla gli aggiornamenti:<br /><br /> -   **Controlla sempre all'avvio dell'applicazione**. [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] eseguirà un controllo degli aggiornamenti ogni volta che l'utente apre l'applicazione.<br />-   **Controlla ogni**: Seleziona un intervallo di tempo e un'unità (ore, giorni o settimane) che deve trascorrere prima del controllo degli aggiornamenti.|  
|**Specificare la versione minima richiesta per l'applicazione**|Parametro facoltativo. Specifica che è necessario installare una determinata versione dell'applicazione, impedendo agli utenti di usare una versione precedente.|  
|**Version**|Obbligatorio se la casella di controllo **Specificare la versione minima richiesta per l'applicazione** è selezionata. Il numero di versione specificato deve essere nel formato *N.N.N.N*. È necessario solo il primo numero della build principale. Ad esempio, per la versione 1.0 di un'applicazione, i valori validi sono `1`, `1.0`, `1.0.0` e `1.0.0.0`.|  
  
### <a name="application-reference-tab"></a>Scheda Riferimento all'applicazione  
 La scheda **Riferimento all'applicazione** contiene gli stessi campi della scheda **Nome** descritta precedentemente in questo argomento. L'unica eccezione è il campo seguente.  
  
|Elemento dell'interfaccia utente|Descrizione|  
|----------------|-----------------|  
|**Seleziona manifesto**|Consente di scegliere il manifesto dell'applicazione. Tutti gli altri campi in questa pagina verranno popolati quando si sceglie un manifesto dell'applicazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza e distribuzione di ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment)   
 [Procedura dettagliata: Distribuzione manuale di un'applicazione ClickOnce](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)   
 [Mage.exe (Strumento per la generazione e la modifica di manifesti)](../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md)
