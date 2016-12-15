---
title: "Extending the Visual Basic Application Model | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic Application Model, extending"
ms.assetid: e91d3bed-4c27-40e3-871d-2be17467c72c
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Extending the Visual Basic Application Model
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile aggiungere funzionalità al modello di applicazione eseguendo l'override dei membri `Overridable` della classe <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>.  In tal modo sarà possibile personalizzare il comportamento del modello di applicazione e aggiungere chiamate ai metodi personalizzati al momento dell'avvio e della chiusura dell'applicazione.  
  
## Panoramica visiva del modello di applicazione  
 In questa sezione viene presentata la sequenza visiva delle chiamate di funzione nel modello di applicazione Visual Basic.  Nella sezione successiva verrà fornita una descrizione dettagliata dello scopo di ciascuna funzione.  
  
 Nell'immagine seguente viene illustrata la sequenza di chiamata del modello di applicazione in una normale applicazione Windows Form in Visual Basic.  La sequenza viene avviata quando la routine `Sub Main` esegue la chiamata al metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>.  
  
 ![Modello di applicazioni Visual Basic &#45;&#45; Esecuzione](../../../visual-basic/developing-apps/customizing-extending-my/media/vb_modelrun.gif "VB\_ModelRun")  
  
 Il modello applicativo di Visual Basic include anche gli eventi <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> e <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>.  Nell'immagine seguente viene illustrato il meccanismo di generazione di tali eventi.  
  
 ![Modello di applicazioni Visual Basic &#45;&#45; Istanza successiva](../../../visual-basic/developing-apps/customizing-extending-my/media/vb_modelnext.gif "VB\_ModelNext")  
  
 ![Eccezione non gestita del modello di applicazioni Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/media/vb_unhandex.gif "VB\_UnhandEx")  
  
## Override dei metodi di base  
 Il metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> definisce l'ordine di esecuzione dei metodi `Application`.  Per impostazione predefinita, mediante la procedura `Sub Main` per un'applicazione Windows Form viene chiamato il metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>.  
  
 Se l'applicazione è un'applicazione normale, ovvero un'applicazione a più istanze, o è la prima istanza di un'applicazione a istanza singola, il metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> esegue i metodi `Overridable` nel seguente ordine:  
  
1.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A>.  Per impostazione predefinita, questo metodo imposta gli stili di visualizzazione e di visualizzazione del testo, l'oggetto Principal corrente del thread principale dell'applicazione \(se l'applicazione utilizza l'autenticazione di Windows\) e chiama il metodo `ShowSplashScreen` se non è stato utilizzato `/nosplash` o `-nosplash` nell'argomento della riga di comando.  
  
     La sequenza di avvio dell'applicazione viene annullata se la funzione restituisce `False`.  Questa funzionalità risulta particolarmente utile nei casi in cui non è necessario eseguire l'applicazione.  
  
     Il metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> chiama i metodi seguenti:  
  
    1.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A>.  Determina se nell'applicazione è stata definita una schermata iniziale e, in tal caso, visualizza la schermata iniziale in un thread distinto.  
  
         Il metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A> contiene il codice per la visualizzazione della schermata iniziale per almeno il numero di millisecondi specificati dalla proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A>.  Per utilizzare la funzionalità, è necessario aggiungere la schermata iniziale all'applicazione mediante **Progettazione progetti** \(che imposta la proprietà `My.Application.MinimumSplashScreenDisplayTime` su due secondi\), o impostare la proprietà `My.Application.MinimumSplashScreenDisplayTime` su un metodo che esegue l'override del metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> o <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A>.  
  
    2.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>.  Consente l'emissione di codice in una finestra di progettazione per l'inizializzazione della schermata iniziale.  
  
         Per impostazione predefinita, questo metodo non effettua alcuna operazione.  Se si seleziona una schermata iniziale per l'applicazione in **Progettazione progetti** in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], viene eseguito l'override del metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A> con un metodo che imposta la proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A> su una nuova istanza del form della schermata iniziale.  
  
2.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartup%2A>.  Fornisce un punto di estensibilità per la generazione dell'evento `Startup`.  La sequenza di avvio dell'applicazione viene interrotta se la funzione restituisce `False`.  
  
     Per impostazione predefinita, questo metodo genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>.  Se tramite il gestore eventi la proprietà <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> dell'argomento di evento viene impostata su `True`, il metodo restituisce `False` per annullare l'avvio dell'applicazione.  
  
3.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnRun%2A>.  Fornisce il punto iniziale utilizzato dall'applicazione principale quando è pronta ad avviare l'esecuzione, al termine dell'inizializzazione.  
  
     Per impostazione predefinita, prima che immetta il ciclo di messaggi di Windows Form, questo metodo chiama i metodi `OnCreateMainForm` \(per la creazione del form principale dell'applicazione\) e `HideSplashScreen` \(per la chiusura della schermata iniziale\):  
  
    1.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>.  Fornisce una soluzione per l'emissione di codice per l'inizializzazione del form principale.  
  
         Per impostazione predefinita, questo metodo non effettua alcuna operazione.  Tuttavia, quando si seleziona un form principale per l'applicazione in **Progettazione progetti**°di°[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], la finestra di progettazione esegue l'override del metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A> con un metodo che imposta la proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> su una nuova istanza del form principale.  
  
    2.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.HideSplashScreen%2A>.  Se nell'applicazione è definita e aperta una schermata iniziale, il metodo consente di chiuderla.  
  
         Per impostazione predefinita, il metodo chiude la schermata iniziale.  
  
4.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A>.  Fornisce una soluzione per personalizzare il comportamento di un'applicazione a istanza singola quando viene avviata un'altra istanza dell'applicazione.  
  
     Per impostazione predefinita, questo metodo genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>.  
  
5.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnShutdown%2A>.  Fornisce un punto di estensibilità per la generazione dell'evento `Shutdown`.  Il metodo non viene eseguito se nell'applicazione principale viene generata un'eccezione non gestita.  
  
     Per impostazione predefinita, questo metodo genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>.  
  
6.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnUnhandledException%2A>.  Eseguito se in uno dei metodi elencati in precedenza viene generata un'eccezione non gestita.  
  
     Per impostazione predefinita, questo metodo genera l'evento <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> se non è connesso un debugger e se l'applicazione gestisce l'evento `UnhandledException`.  
  
 Se l'applicazione è un'applicazione a istanza singola ed è già in esecuzione, la successiva istanza dell'applicazione esegue la chiamata al metodo <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A> sull'istanza originale dell'applicazione, quindi chiude l'applicazione.  
  
 Il costruttore <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> chiama la proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> per stabilire quale motore di rendering del testo utilizzare per i form dell'applicazione.  Per impostazione predefinita, la proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> restituisce `False`, che indica che verrà utilizzato il motore di rendering del testo GDI, corrispondente all'impostazione predefinita in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)].  È possibile eseguire l'override della proprietà <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> per restituire `True`, che indica che verrà utilizzato il motore di rendering del testo GDI\+, corrispondente all'impostazione predefinita in Visual Basic .NET 2002 e Visual Basic .NET 2003.  
  
## Configurazione dell'applicazione  
 Nell'ambito del modello applicativo di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] la classe <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> fornisce proprietà protette per la configurazione dell'applicazione.  Queste proprietà devono essere impostate nel costruttore della classe di implementazione.  
  
 In un progetto Windows Form predefinito, **Progettazione progetti** consente di creare codice per impostare le proprietà con le impostazioni di progettazione.  Le proprietà sono utilizzate solo all'avvio dell'applicazione. Se si impostano successivamente all'avvio dell'applicazione, non avranno alcun effetto.  
  
||||  
|-|-|-|  
|Proprietà|Determina|Impostazione nel riquadro dell'applicazione di progettazione progetti|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.IsSingleInstance%2A>|Se l'applicazione viene eseguita come applicazione a istanza singola o a più istanze.|Casella di controllo**Eseguire l'applicazione a istanza singola**|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.EnableVisualStyles%2A>|Se l'applicazione utilizzerà gli stili di visualizzazione che corrispondono a Windows XP.|Casella di controllo**Abilitare gli stili visivi XP**|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SaveMySettingsOnExit%2A>|Se l'applicazione salva automaticamente le modifiche apportate alle impostazioni utente dell'applicazione alla chiusura dell'applicazione.|Casella di controllo**Salvare My.Settings all'arresto**|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShutdownStyle%2A>|Le cause che inducono l'interruzione dell'applicazione, ad esempio quando il form di avvio o la chiusura del form ultimo viene chiusa.|Elenco di**Modalità di chiusura**|  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [Overview of the Visual Basic Application Model](../../../visual-basic/developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)   
 [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)