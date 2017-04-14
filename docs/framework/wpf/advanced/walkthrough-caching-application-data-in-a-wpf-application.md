---
title: "Procedura dettagliata: memorizzazione dei dati di un&#39;applicazione nella cache di un&#39;applicazione WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "memorizzazione nella cache [.NET Framework]"
  - "memorizzazione nella cache [WPF]"
  - "procedure dettagliate [WPF], memorizzazione nella cache"
ms.assetid: dac2c9ce-042b-4d23-91eb-28f584415cef
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Procedura dettagliata: memorizzazione dei dati di un&#39;applicazione nella cache di un&#39;applicazione WPF
La memorizzazione nella cache consente di archiviare i dati in memoria per l'accesso rapido.  Quando si accede nuovamente ai dati, le applicazioni possono ottenere i dati dalla cache anziché recuperarli dall'origine.  Ciò può migliorare prestazioni e scalabilità.  Inoltre, la memorizzazione nella cache rende disponibili i dati quando l'origine dati non è temporaneamente disponibile.  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] fornisce classi che consentono di utilizzare la memorizzazione nella cache nelle applicazioni di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] .  Queste classi si trovano nello spazio dei nomi di <xref:System.Runtime.Caching> .  
  
> [!NOTE]
>  Lo spazio dei nomi <xref:System.Runtime.Caching> è nuovo in [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].  Questo spazio dei nomi rende disponibile la memorizzazione nella cache a tutte le applicazioni [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  Nelle versioni precedenti di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] la memorizzazione nella cache è disponibile solo nello spazio dei nomi <xref:System.Web> e pertanto richiede una dipendenza nelle classi ASP.NET.  
  
 In questa procedura dettagliata viene illustrato come utilizzare la funzionalità della memorizzazione nella cache, disponibile in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], come parte di un'applicazione [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Nella procedura dettagliata, viene memorizzato nella cache il contenuto di un file di testo.  
  
 Di seguito vengono illustrate le attività incluse nella procedura dettagliata:  
  
-   Creazione di un progetto di applicazione WPF.  
  
-   Aggiunta di un riferimento a [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].  
  
-   Inizializzazione di una cache.  
  
-   Aggiunta di una voce della cache che include il contenuto di un file di testo.  
  
-   Fornitura di criteri dell'eliminazione per la voce della cache.  
  
-   Monitoraggio del percorso del file memorizzato nella cache e notifica all'istanza della cache delle modifiche dell'elemento monitorato.  
  
## Prerequisiti  
 Per completare questa procedura dettagliata, è necessario disporre di quanto segue:  
  
-   Microsoft [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   Un file di testo contenente una piccola quantità di testo.  Si visualizzerà il contenuto del file di testo in una finestra di messaggio. Nel codice illustrato nella procedura dettagliata si suppone che si utilizzi il file seguente:  
  
     `c:\cache\cacheText.txt`  
  
     Tuttavia, è possibile utilizzare qualsiasi file di testo e apportare piccole modifiche al codice di questa procedura dettagliata.  
  
## Creazione di un progetto di applicazione WPF  
 Si inizierà con la creazione di un progetto di applicazione WPF.  
  
#### Per creare un'applicazione WPF  
  
1.  Avviare [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi **Nuovo progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
3.  In **Modelli installati** selezionare il linguaggio di programmazione da utilizzare \(**Visual Basic** o **Visual C\#**\).  
  
4.  Nella finestra di dialogo **Nuovo progetto** selezionare **Applicazione WPF**.  
  
    > [!NOTE]
    >  Se il modello **Applicazione WPF** non è visualizzato, verificare che sia stata scelta come destinazione una versione di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che supporta WPF.  Nella finestra di dialogo **Nuovo progetto** selezionare [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] dall'elenco.  
  
5.  Nella casella di testo **Nome** immettere un nome per il progetto.  Ad esempio, è possibile immettere WPFCaching.  
  
6.  Selezionare la casella di controllo **Crea directory per soluzione**.  
  
7.  Scegliere **OK**.  
  
     Il file MainWindow.xaml verrà visualizzato nella visualizzazione **Progettazione** in WPF Designer.  In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] vengono creati la cartella **My Project**, il file Application.xaml e il file MainWindow.xaml.  
  
## Scelta di .NET Framework come destinazione e aggiunta di un riferimento agli assembly di cache  
 Per impostazione predefinita, le applicazioni WPF sono destinate a [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)].  Per utilizzare lo spazio dei nomi <xref:System.Runtime.Caching> in un'applicazione WPF, è necessario che l'applicazione sia destinata a [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)], non a [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)], e includa un riferimento allo spazio dei nomi.  
  
 Pertanto, il passaggio seguente consiste nella modifica della destinazione .NET Framework e nell'aggiunta di un riferimento allo spazio dei nomi <xref:System.Runtime.Caching>.  
  
> [!NOTE]
>  La procedura per la modifica della destinazione .NET Framework è diversa in un progetto Visual Basic e in un progetto Visual C\#.  
  
#### Per modificare la versione di .NET Framework di destinazione in Visual Basic  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto, quindi scegliere **Proprietà**.  
  
     Verrà visualizzata la finestra delle proprietà per l'applicazione.  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Nella parte inferiore della finestra, fare clic su **Opzioni di compilazione avanzate ...**.  
  
     Verrà visualizzata la finestra di dialogo **Impostazioni del compilatore avanzate**.  
  
4.  In l ' elenco di **framework di destinazione \(tutte le configurazioni\)** , [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]selezionato.  \(Non selezionare [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]\).  
  
5.  Scegliere **OK**.  
  
     Verrà visualizzata la finestra di dialogo **Modifica versione .NET Framework di destinazione**.  
  
6.  Nella finestra di dialogo **Modifica versione .NET Framework di destinazione** fare clic su **Sì**.  
  
     Il progetto verrà chiuso e riaperto.  
  
7.  Per aggiungere un riferimento all'assembly di cache, effettuare i passaggi seguenti:  
  
    1.  Fare clic con il pulsante destro del mouse sul nome del progetto in **Esplora soluzioni**, quindi scegliere **Aggiungi riferimento**.  
  
    2.  Selezionare la scheda **.NET**, scegliere `System.Runtime.Caching`, quindi fare clic su **OK**.  
  
#### Per modificare la versione di .NET Framework di destinazione in un progetto Visual C\#  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nome del progetto, quindi scegliere **Proprietà**.  
  
     Verrà visualizzata la finestra delle proprietà per l'applicazione.  
  
2.  Fare clic sulla scheda **Applicazione**.  
  
3.  Nell'elenco **Framework di destinazione** selezionare [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].  Non selezionare **.NET Framework 4 Client Profile**.  
  
4.  Per aggiungere un riferimento all'assembly di cache, effettuare i passaggi seguenti:  
  
    1.  Fare clic con il pulsante destro del mouse sulla cartella **Riferimenti**, quindi scegliere **Aggiungi riferimento**.  
  
    2.  Selezionare la scheda **.NET**, scegliere `System.Runtime.Caching`, quindi fare clic su **OK**.  
  
## Aggiunta di un pulsante alla finestra WPF  
 Successivamente, si aggiungerà un controllo pulsante e si creerà un gestore dell'evento per l'evento `Click` del pulsante.  Si aggiungerà quindi codice mediante il quale facendo clic sul pulsante verrà memorizzato nella cache e visualizzato il contenuto del file di testo.  
  
#### Per aggiungere un pulsante  
  
1.  In **Esplora soluzioni** aprire il file MainWindow.xaml facendo doppio clic su di esso.  
  
2.  In **Controlli comuni WPF** nella **Casella degli strumenti** trascinare un controllo `Button` nella finestra `MainWindow`.  
  
3.  Nella finestra **Proprietà** impostare la proprietà `Content` del controllo `Button` su Ottieni cache.  
  
## Inizializzazione della cache e memorizzazione di una voce nella cache  
 Successivamente, si aggiungerà il codice per eseguire le attività seguenti:  
  
-   Creare un'istanza della classe cache \(ossia creare un'istanza di un nuovo oggetto <xref:System.Runtime.Caching.MemoryCache>\).  
  
-   Specificare che la cache utilizza un oggetto <xref:System.Runtime.Caching.HostFileChangeMonitor> per monitorare le modifiche nel file di testo.  
  
-   Leggere il file di testo e memorizzare nella cache il relativo contenuto come voce della cache.  
  
-   Visualizzare il contenuto del file di testo memorizzato nella cache.  
  
#### Per creare l'oggetto cache  
  
1.  Fare doppio clic sul pulsante appena aggiunto per creare un gestore dell'evento nel file MainWindow.Xaml.vb o MainWindow.xaml.cs.  
  
2.  All'inizio del file \(prima della dichiarazione di classe\), aggiungere le istruzioni `Imports` \(Visual Basic\) o `using` \(C\#\) seguenti.  
  
    ```csharp  
    using System.Runtime.Caching;  
    using System.IO;  
    ```  
  
    ```vb  
    Imports System.Runtime.Caching  
    Imports System.IO  
    ```  
  
3.  Nel gestore dell'evento aggiungere il codice riportato di seguito per creare un'istanza dell'oggetto cache.  
  
    ```csharp  
    ObjectCache cache = MemoryCache.Default;  
    ```  
  
    ```vb  
    Dim cache As ObjectCache = MemoryCache.Default  
    ```  
  
     <xref:System.Runtime.Caching.ObjectCache> è una classe incorporata che fornisce una cache dell'oggetto in memoria.  
  
4.  Aggiungere il codice seguente per leggere il contenuto di una voce della cache denominata `filecontents`:  
  
    ```vb  
    Dim fileContents As String = TryCast(cache("filecontents"), String)  
    ```  
  
    ```csharp  
    string fileContents = cache["filecontents"] as string;  
    ```  
  
5.  Aggiungere il codice seguente per verificare se la voce della cache denominata `filecontents` esiste:  
  
    ```vb  
    If fileContents Is Nothing Then  
  
    End If  
    ```  
  
    ```csharp  
    if (fileContents == null)  
    {  
  
    }  
    ```  
  
     Se la voce della cache specificata non esiste, è necessario leggere il file di testo e aggiungerlo alla cache come voce della cache.  
  
6.  Nel blocco `if/then` aggiungere il codice seguente per creare un nuovo oggetto <xref:System.Runtime.Caching.CacheItemPolicy> che specifica che la voce della cache scade dopo 10 secondi.  
  
    ```vb  
    Dim policy As New CacheItemPolicy()  
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0)  
    ```  
  
    ```csharp  
    CacheItemPolicy policy = new CacheItemPolicy();  
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0);  
    ```  
  
     Se non viene fornita alcuna informazione di eliminazione o scadenza, l'impostazione predefinita è <xref:System.Runtime.Caching.ObjectCache.InfiniteAbsoluteExpiration> secondo cui le voci della cache non scadono mai solo in base a un tempo assoluto.  Viceversa, le voci della cache scadono solo in condizioni di pressione della memoria.  Come procedura consigliata, è sempre opportuno fornire esplicitamente una scadenza assoluta o variabile.  
  
7.  All'interno del blocco `if/then`, seguendo il codice aggiunto nel passaggio precedente, aggiungere il codice seguente per creare una raccolta per i percorsi file che si desidera monitorare e aggiungere il percorso del file di testo alla raccolta:  
  
    ```vb  
    Dim filePaths As New List(Of String)()  
    filePaths.Add("c:\cache\cacheText.txt")  
    ```  
  
    ```csharp  
    List<string> filePaths = new List<string>();  
    filePaths.Add("c:\\cache\\cacheText.txt");  
    ```  
  
    > [!NOTE]
    >  Se il file di testo da utilizzare non è `c:\cache\cacheText.txt` specificare il percorso del file di testo da utilizzare.  
  
8.  Seguendo il codice aggiunto nel passaggio precedente, aggiungere il codice seguente per aggiungere un nuovo oggetto <xref:System.Runtime.Caching.HostFileChangeMonitor> alla raccolta di monitoraggio delle modifiche per la voce della cache:  
  
    ```vb  
    policy.ChangeMonitors.Add(New HostFileChangeMonitor(filePaths))  
    ```  
  
    ```csharp  
    policy.ChangeMonitors.Add(new HostFileChangeMonitor(filePaths));  
    ```  
  
     L'oggetto <xref:System.Runtime.Caching.HostFileChangeMonitor> monitora il percorso del file di testo e notifica alla cache se si verificano modifiche.  In questo esempio la voce della cache scadrà se il contenuto del file viene modificato.  
  
9. Seguendo il codice aggiunto nel passaggio precedente, aggiungere il codice seguente per leggere il contenuto del file di testo:  
  
    ```vb  
    fileContents = File.ReadAllText("c:\cache\cacheText.txt") & vbCrLf & DateTime.Now.ToString()  
    ```  
  
    ```csharp  
    fileContents = File.ReadAllText("c:\\cache\\cacheText.txt") + + "\n" + DateTime.Now;   
    ```  
  
     Viene aggiunto il timestamp di data e ora per consentire di vedere la scadenza della voce della cache.  
  
10. Seguendo il codice aggiunto nel passaggio precedente, aggiungere il codice seguente per inserire il contenuto del file nell'oggetto cache come un'istanza di <xref:System.Runtime.Caching.CacheItem>:  
  
    ```vb  
    cache.Set("filecontents", fileContents, policy)  
    ```  
  
    ```csharp  
    cache.Set("filecontents", fileContents, policy);  
    ```  
  
     Specificare informazioni sulla voce della cache da eliminare passando l'oggetto <xref:System.Runtime.Caching.CacheItemPolicy> creato in precedenza come parametro.  
  
11. Dopo il blocco `if/then`, aggiungere il codice seguente per visualizzare il contenuto del file memorizzato nella cache in una finestra del messaggio.  
  
    ```vb  
    MessageBox.Show(fileContents)  
    ```  
  
    ```csharp  
    MessageBox.Show(fileContents);  
    ```  
  
12. Per compilare il progetto scegliere **Compila WPFCaching** dal menu **Compila**.  
  
## Test della memorizzazione nella cache nell'applicazione WPF  
 È ora possibile eseguire il test dell'applicazione.  
  
#### Per sottoporre a test la memorizzazione nella cache nell'applicazione WPF  
  
1.  Premere CTRL\+F5 per eseguire l'applicazione.  
  
     Verrà visualizzata la finestra `MainWindow`.  
  
2.  Fare clic su **Ottieni cache**.  
  
     Il contenuto memorizzato nella cache del file di testo verrà visualizzato in una finestra di messaggio.  Si noti il timestamp nel file.  
  
3.  Chiudere la finestra di messaggio e fare di nuovo clic su **Ottieni cache**.  
  
     Il timestamp è invariato.  Questo indica che viene visualizzato il contenuto memorizzato nella cache.  
  
4.  Attendere 10 secondi o più, quindi fare nuovamente clic su **Ottieni cache**.  
  
     Questa volta viene visualizzato un nuovo timestamp.  Questo indica che i criteri consentono alla voce della cache di scadere e che viene visualizzato il nuovo contenuto della cache.  
  
5.  In un editor di testo aprire il file di testo creato.  Non apportare ancora alcuna modifica.  
  
6.  Chiudere la finestra di messaggio e fare di nuovo clic su **Ottieni cache**.  
  
     Si noti nuovamente il timestamp.  
  
7.  Apportare una modifica al file di testo e salvarlo.  
  
8.  Chiudere la finestra di messaggio e fare di nuovo clic su **Ottieni cache**.  
  
     Questa finestra di messaggio contiene il contenuto aggiornato del file di testo e un nuovo timestamp.  Questo indica che il monitoraggio delle modifiche del file host ha immediatamente eliminato la voce della cache quando si è apportata la modifica, anche se il periodo di timeout assoluto non è scaduto.  
  
    > [!NOTE]
    >  È possibile aumentare il tempo di eliminazione a 20 secondi o più, per disporre di più tempo per apportare la modifica nel file.  
  
## Esempio di codice  
 Dopo avere completato questa procedura dettagliata, l'aspetto del codice per il progetto sarà simile all'esempio seguente.  
  
 [!code-csharp[CachingWPFApplications#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CachingWPFApplications/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[CachingWPFApplications#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CachingWPFApplications/VisualBasic/MainWindow.xaml.vb#1)]  
  
## Vedere anche  
 <xref:System.Runtime.Caching.MemoryCache>   
 <xref:System.Runtime.Caching.ObjectCache>   
 <xref:System.Runtime.Caching>   
 [Memorizzazione nella cache in applicazioni .NET Framework](../../../../docs/framework/performance/caching-in-net-framework-applications.md)