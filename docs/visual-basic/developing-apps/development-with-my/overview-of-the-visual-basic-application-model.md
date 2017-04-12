---
title: Panoramica del modello di applicazione Visual Basic | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My.Application object, Visual Basic application model
- Visual Basic application model
ms.assetid: 17538984-84fe-43c9-82c8-724c9529fe8b
caps.latest.revision: 30
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 0925bb102c148480d82128b91cbf1762de24e7ec
ms.lasthandoff: 03/13/2017

---
# <a name="overview-of-the-visual-basic-application-model"></a>Cenni preliminari sul modello di applicazione Visual Basic
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce un modello ben definito per il controllo del comportamento delle applicazioni Windows Forms: il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] modello di applicazione. Questo modello include eventi per la gestione dell'applicazione avvio e arresto, nonché gli eventi di rilevamento delle eccezioni non gestito. Fornisce inoltre il supporto per lo sviluppo di applicazioni a istanza singola. Il modello di applicazione è estensibile, pertanto gli sviluppatori che necessita di maggiore controllo possono personalizzare i metodi sottoponibili a override.  
  
## <a name="uses-for-the-application-model"></a>Viene utilizzato per il modello di applicazione  
 Una tipica applicazione deve effettuare le attività quando viene avviato e arrestato. Ad esempio, all'avvio, l'applicazione può visualizzare una schermata, creare connessioni di database, caricare uno stato salvato e così via. Quando l'applicazione viene chiusa, è possibile chiudere le connessioni di database, salvare lo stato corrente e così via. Inoltre, l'applicazione può eseguire codice specifico quando l'applicazione si arresta improvvisamente, ad esempio durante un'eccezione non gestita.  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] modello applicativo consente di creare facilmente un *a istanza singola* dell'applicazione. Un'applicazione a istanza singola differisce da un'applicazione normale che è possibile eseguire solo un'istanza dell'applicazione alla volta. Un tentativo di avviare un'altra istanza di un'applicazione a istanza singola risulta nell'istanza originale viene inviata una notifica, per mezzo di `StartupNextInstance` eventi, che è stato effettuato un altro tentativo di avvio. La notifica include argomenti della riga di comando dell'istanza successiva. La seconda istanza dell'applicazione viene quindi chiusa prima di poter eseguire le operazioni di inizializzazione.  
  
 Un'applicazione a istanza singola avvia e controlla se è la prima istanza o la seconda istanza dell'applicazione:  
  
-   Se è la prima istanza, inizia come di consueto.  
  
-   Ogni successivo tentativo di avviare l'applicazione, mentre la prima istanza in esecuzione, comporta un comportamento molto diverso. Il tentativo successivo notifica la prima istanza sugli argomenti della riga di comando e quindi chiude immediatamente. La prima istanza gestisce il `StartupNextInstance` evento per individuare gli argomenti della riga di comando della seconda istanza e continua l'esecuzione.  
  
     Questo diagramma viene mostrato come una seconda istanza comunica con la prima istanza.  
  
     ![Immagine di applicazione a istanza singola](../../../visual-basic/developing-apps/development-with-my/media/singleinstance.gif "SingleInstance")  
  
 Gestendo le `StartupNextInstance` evento, è possibile controllare il comportamento dell'applicazione a istanza singola. Ad esempio Microsoft Outlook viene in genere eseguita come un'applicazione a istanza singola. Quando Outlook è in esecuzione e si tenta di avviare Outlook anche in questo caso, lo stato attivo passa all'istanza originale ma non si apre un'altra istanza.  
  
## <a name="events-in-the-application-model"></a>Eventi del modello di applicazione  
 Nel modello di applicazione sono disponibili i seguenti eventi:  
  
-   **Avvio dell'applicazione**. L'applicazione genera il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>evento all'avvio.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> La gestione dell'evento, è possibile aggiungere codice che inizializza l'applicazione prima di carica il form principale. Il `Startup` eventi consente anche di annullare l'esecuzione dell'applicazione durante la fase del processo di avvio, se necessario.  
  
     È possibile configurare l'applicazione per visualizzare una schermata durante l'esecuzione di codice di avvio dell'applicazione. Per impostazione predefinita, il modello di applicazione elimina la schermata iniziale quando sia il `/nosplash` o `-nosplash` viene utilizzato l'argomento della riga di comando.  
  
-   **Applicazioni a istanza singola**. Il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>evento viene generato quando viene avviata una seconda istanza di un'applicazione a istanza singola.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> L'evento passa gli argomenti della riga di comando della seconda istanza.  
  
-   **Le eccezioni non gestite**. Se l'applicazione rileva un'eccezione non gestita, genera il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>eventi.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> Il gestore dell'evento è possibile esaminare l'eccezione e determinare se continuare l'esecuzione.  
  
     Il `UnhandledException` in alcune circostanze non viene generato l'evento. Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>  
  
-   **Modifiche di connettività di rete**. Se viene modificata la disponibilità della rete del computer, l'applicazione genera il <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>eventi.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>  
  
     Il `NetworkAvailabilityChanged` in alcune circostanze non viene generato l'evento. Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>  
  
-   **Chiusura dell'applicazione**. L'applicazione fornisce la <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>evento per segnalare quando è in fase di chiusura.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> In tal caso gestore, è possibile assicurarsi che le operazioni che l'applicazione deve eseguire, ovvero la chiusura e il salvataggio, ad esempio, vengono completate. È possibile configurare l'applicazione chiuso alla chiusura del form principale, o l'arresto solo quando tutti i form chiuso.  
  
## <a name="availability"></a>Disponibilità  
 Per impostazione predefinita, il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] modello applicativo è disponibile per i progetti Windows Form. Se si configura l'applicazione per utilizzare un diverso oggetto di avvio o avviare il codice dell'applicazione con un oggetto personalizzato `Sub Main`, oggetto o potrebbe essere necessario fornire un'implementazione della classe di <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>classe per utilizzare il modello di applicazione.</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> Per informazioni sulla modifica dell'oggetto di avvio, vedere [pagina applicazione, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [Estensione del modello di applicazione Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)
