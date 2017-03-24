---
title: Estensione del modello di applicazione Visual Basic | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic Application Model, extending
ms.assetid: e91d3bed-4c27-40e3-871d-2be17467c72c
caps.latest.revision: 21
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9752cdfa79d3db4c8b07daa95aea2c842e06cc36
ms.lasthandoff: 03/13/2017

---
# <a name="extending-the-visual-basic-application-model"></a>Estensione del modello di applicazione Visual Basic
È possibile aggiungere funzionalità al modello dell'applicazione eseguendo l'override di `Overridable` i membri di <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>classe.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> Questa tecnica consente di personalizzare il comportamento del modello di applicazione e aggiungere chiamate a metodi personalizzati, come l'applicazione viene avviato e arrestato.  
  
## <a name="visual-overview-of-the-application-model"></a>Panoramica visiva del modello di applicazione  
 In questa sezione sono visivamente la sequenza di chiamate di funzione nel modello di applicazione Visual Basic. La prossima sezione descrive lo scopo di ogni funzione in modo dettagliato.  
  
 La figura seguente illustra la sequenza di chiamate del modello di applicazione in una normale applicazione Windows Form di Visual Basic. La sequenza inizia quando il `Sub Main` chiamate di procedure di <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>(metodo).</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>  
  
 ![Modello di applicazione Visual Basic-- Eseguire](../../../visual-basic/developing-apps/customizing-extending-my/media/vb_modelrun.gif "VB_ModelRun")  
  
 Il modello di applicazione Visual Basic fornisce inoltre il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>e <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>gli eventi.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> </xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> Le immagini che seguono viene illustrato il meccanismo per la generazione di questi eventi.  
  
 ![Modello di applicazione Visual Basic-- Istanza successivamente](../../../visual-basic/developing-apps/customizing-extending-my/media/vb_modelnext.gif "VB_ModelNext")  
  
 ![Eccezione non gestita del modello di applicazione Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/media/vb_unhandex.gif "VB_UnhandEx")  
  
## <a name="overriding-the-base-methods"></a>L'override dei metodi Base  
 Il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>metodo definisce l'ordine in cui il `Application` metodi di esecuzione.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A> Per impostazione predefinita, il `Sub Main` procedure per un'applicazione Windows Form chiama il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>(metodo).</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>  
  
 Se l'applicazione è un'applicazione normale (applicazione di più istanze) o la prima istanza di un'applicazione a istanza singola, il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>il metodo viene eseguito il `Overridable` metodi nell'ordine seguente:</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Run%2A>  
  
1.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> Per impostazione predefinita, questo metodo imposta gli stili di visualizzazione, gli stili di visualizzazione di testo ed entità corrente per il thread principale dell'applicazione (se l'applicazione utilizza l'autenticazione di Windows) e chiama `ShowSplashScreen` se non si specifica `/nosplash` né `-nosplash` viene utilizzato come un argomento della riga di comando.  
  
     La sequenza di avvio dell'applicazione viene annullata se la funzione restituisce `False`. Questo può essere utile se vi sono circostanze in cui l'applicazione non deve essere eseguita.  
  
     Il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A>metodo chiama i metodi seguenti:</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A>  
  
    1.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A> Determina se l'applicazione dispone di una schermata iniziale e in caso affermativo, viene visualizzata la schermata iniziale in un thread separato.  
  
         Il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A>metodo contiene il codice che consente di visualizzare la schermata iniziale di schermata per almeno il numero di millisecondi specificato dalla <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A>proprietà.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A> </xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShowSplashScreen%2A> Per utilizzare questa funzionalità, è necessario aggiungere la schermata iniziale per l'applicazione utilizzando il **Progettazione progetti** (che imposta il `My.Application.MinimumSplashScreenDisplayTime` proprietà su due secondi), o impostare il `My.Application.MinimumSplashScreenDisplayTime` proprietà in un metodo che esegue l'override di <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A>o <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>(metodo).</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A> </xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnInitialize%2A> Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MinimumSplashScreenDisplayTime%2A>  
  
    2.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A> Consente di generare il codice che inizializza la schermata iniziale.  
  
         Per impostazione predefinita, questo metodo non esegue alcuna operazione. Se si seleziona una schermata dell'applicazione nel [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] **Progettazione progetti**, la finestra di progettazione esegue l'override di <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>con un metodo che imposta il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A>proprietà in una nuova istanza del form schermata iniziale.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SplashScreen%2A> </xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateSplashScreen%2A>  
  
2.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartup%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartup%2A> Fornisce un punto di estensibilità per la generazione di `Startup` eventi. La sequenza di avvio dell'applicazione viene interrotta se questa funzione restituisce `False`.  
  
     Per impostazione predefinita, questo metodo genera il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>eventi.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> Se il gestore dell'evento imposta il @System.ComponentModel.CancelEventArgs.Cancel proprietà dell'argomento dell'evento per `True`, il metodo restituisce `False` per annullare l'avvio dell'applicazione.  
  
3.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnRun%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnRun%2A> Fornisce il punto di partenza per quando è pronto per avviare l'esecuzione, dopo l'inizializzazione viene eseguita l'applicazione principale.  
  
     Per impostazione predefinita, prima che immetta il ciclo di messaggi Windows Form, questo metodo chiama il `OnCreateMainForm` (per la creazione del form principale dell'applicazione) e `HideSplashScreen` (per chiudere la schermata iniziale) metodi:  
  
    1.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A> Fornisce un modo per una finestra di progettazione generare il codice che inizializza il form principale.  
  
         Per impostazione predefinita, questo metodo non esegue alcuna operazione. Tuttavia, quando si seleziona un form principale dell'applicazione nel [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] **Progettazione progetti**, la finestra di progettazione esegue l'override il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>con un metodo che imposta il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A>proprietà in una nuova istanza del form principale.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.MainForm%2A> </xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnCreateMainForm%2A>  
  
    2.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.HideSplashScreen%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.HideSplashScreen%2A> Se l'applicazione ha una schermata iniziale e è aperto, questo metodo chiude la schermata iniziale.  
  
         Per impostazione predefinita, questo metodo chiude la schermata iniziale.  
  
4.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A> Fornisce un modo per personalizzare il comportamento di un'applicazione a istanza singola quando viene avviata un'altra istanza dell'applicazione.  
  
     Per impostazione predefinita, questo metodo genera il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>eventi.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>  
  
5.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnShutdown%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnShutdown%2A> Fornisce un punto di estensibilità per la generazione di `Shutdown` eventi. Questo metodo non viene eseguito se si verifica un'eccezione non gestita nell'applicazione principale.  
  
     Per impostazione predefinita, questo metodo genera il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>eventi.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>  
  
6.  <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnUnhandledException%2A>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnUnhandledException%2A> Eseguito se si verifica un'eccezione non gestita in uno dei metodi sopra elencati.  
  
     Per impostazione predefinita, questo metodo genera il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>eventi fino a quando non è collegato un debugger e l'applicazione gestisce il `UnhandledException` eventi.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>  
  
 Se l'applicazione è un'applicazione a istanza singola e l'applicazione è già in esecuzione, l'istanza successiva dell'applicazione chiama il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A>(metodo) nell'istanza originale di applicazione e quindi viene chiusa.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.OnStartupNextInstance%2A>  
  
 Il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>costruttore chiama il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A>proprietà per determinare quale motore di rendering di testo da utilizzare per i form dell'applicazione.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> </xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> Per impostazione predefinita, il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A>restituisce proprietà `False`, che indica che il motore di rendering del testo GDI utilizzabile, ossia l'impostazione predefinita in [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)].</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A> È possibile eseguire l'override di <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A>proprietà da restituire `True`, che indica che verrà utilizzato il motore di rendering di testo GDI+, ossia l'impostazione predefinita in Visual Basic .NET 2002 e Visual Basic .NET 2003.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UseCompatibleTextRendering%2A>  
  
## <a name="configuring-the-application"></a>Configurazione dell'applicazione  
 Come parte di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] modello di applicazione, la <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>classe offre proprietà protette che consentono di configurare l'applicazione.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> Queste proprietà devono essere impostate nel costruttore della classe di implementazione.  
  
 In un progetto Windows Form predefinito, il **progettazione** consente di creare codice per impostare le proprietà con le impostazioni della finestra di progettazione. Le proprietà vengono utilizzate solo all'avvio dell'applicazione; la loro impostazione dopo l'avvio dell'applicazione non ha alcun effetto.  
  
|Proprietà|Determina|L'impostazione nel riquadro di progettazione dell'applicazione|  
|---|---|---|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.IsSingleInstance%2A></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.IsSingleInstance%2A>|Se l'applicazione viene eseguito come applicazione a istanza singola o a più istanze.|**Rendi a istanza singola** casella di controllo|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.EnableVisualStyles%2A></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.EnableVisualStyles%2A>|Se l'applicazione utilizzerà gli stili di visualizzazione che corrispondono a Windows XP.|**Abilitare gli stili visivi XP** casella di controllo|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SaveMySettingsOnExit%2A></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.SaveMySettingsOnExit%2A>|Se l'applicazione salva le modifiche delle impostazioni utente dell'applicazione automaticamente alla chiusura dell'applicazione.|**Salva My. Settings in fase di arresto** casella di controllo|  
|<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShutdownStyle%2A></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.ShutdownStyle%2A>|La causa l'interruzione, ad esempio quando si chiude il form di avvio o quando si chiude l'ultimo modulo dell'applicazione.|**Modalità di arresto** elenco|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [Panoramica del modello di applicazione Visual Basic](../../../visual-basic/developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)   
 [Pagina Applicazione, Creazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)
