---
title: "Integrazione di WPF e WF in XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4f53b48-fc90-4315-bca0-ba009562f488
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Integrazione di WPF e WF in XAML
In questo esempio viene illustrato come creare un'applicazione che utilizza le funzionalità [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] e [!INCLUDE[wf](../../../../includes/wf-md.md)] in un unico documento XAML.Per eseguire questa operazione, nell'esempio vengono utilizzati [!INCLUDE[wf](../../../../includes/wf-md.md)] e l'estensibilità XAML.  
  
## Dettagli dell'esempio  
 Il file ShowWindow.xaml viene deserializzato in un'attività <xref:System.Activities.Statements.Sequence> con due variabili di stringa modificate dalle attività della sequenza: `ShowWindow` e `WriteLine`.L'attività <xref:System.Activities.Statements.WriteLine> invia come output alla finestra della console l'espressione che assegna alla proprietà <xref:System.Activities.Statements.WriteLine.Text%2A>.L'attività `ShowWindow` visualizza una finestra [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] come parte della relativa logica di esecuzione.La proprietà <xref:System.Activities.ActivityContext.DataContext%2A> della finestra include le variabili dichiarate nella sequenza.I controlli della finestra dichiarati nell'attività `ShowWindow` utilizzano l'associazione dati per modificare tali variabili.Infine, nella finestra è contenuto un controllo pulsante.L'evento `Click` per il pulsante viene gestito da un oggetto <xref:System.Activities.ActivityDelegate> denominato `MarkupExtension` che contiene un'attività `CloseWindow`.`MarkUpExtension` richiama l'attività esterna che fornisce come contesto tutti gli oggetti identificati da un oggetto `x:Name` nonché l'oggetto <xref:System.Activities.ActivityContext.DataContext%2A> della finestra contenitore.Pertanto, l'oggetto `CloseWindow.InArgument<Window>` può essere associato utilizzando un'espressione che fa riferimento al nome della finestra.  
  
 L'attività `ShowWindow` deriva dalla classe <xref:System.Activities.AsyncCodeActivity%601> per visualizzare una finestra [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] e viene completata quando la finestra viene chiusa.La proprietà `Window` è di tipo `Func<Window>`, il quale consente la creazione della finestra su richiesta per ogni esecuzione dell'attività.La proprietà `Window` utilizza un oggetto <xref:System.Xaml.XamlDeferringLoader> per abilitare questo modello di valutazione posticipato.L'oggetto `FuncFactoryDeferringLoader` consente di acquisire un oggetto `XamlReader` durante la serializzazione e di leggerlo durante l'esecuzione di attività.  
  
 Un'attività scritta in modo corretto non blocca mai il thread dell'utilità di pianificazione.Tuttavia, l'attività `ShowWindow` non può essere completata finché non viene chiusa la finestra in corso di visualizzazione.L'attività `ShowWindow` realizza questo comportamento derivando dall'oggetto <xref:System.Activities.AsyncCodeActivity>, chiamando il metodo <xref:System.Activities.WorkflowInvoker.BeginInvoke%2A> nel metodo <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e visualizzando come modale la finestra.Il delegato viene richiamato tramite la proprietà <xref:System.ServiceModel.InstanceContext.SynchronizationContext%2A> di WPF.L'attività `ShowWindow` assegna la proprietà <xref:System.Activities.ActivityContext.DataContext%2A> alla proprietà `Window.DataContext` per fornire qualsiasi accesso ai controlli associati a dati alle variabili dell'ambito.  
  
 L'ultimo punto di interesse di questo esempio è un oggetto <xref:System.Workflow.ComponentModel.Serialization.MarkupExtension> denominato `DelegateActivityExtension`.Il metodo `ProvideValue` di questa estensione di markup restituisce un delegato che richiama un'attività incorporata.Questa attività viene eseguita in un ambiente che include il contesto dati [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] e qualsiasi valore `x:Name` nell'ambito.Nel metodo `GenericInvoke`, questo ambiente viene fornito all'attività tramite un'estensione <xref:System.Activities.Hosting.SymbolResolver>.Questa estensione viene aggiunta a un oggetto <xref:System.Activities.WorkflowInvoker> che viene quindi utilizzato per richiamare l'attività incorporata ogni volta che viene richiamato il delegato dell'estensione di markup.  
  
> [!NOTE]
>  La finestra di progettazione predefinita non supporta l'attività ShowWindow; pertanto, il file ShowWindow.Xaml non viene visualizzato correttamente nella finestra di progettazione.  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione WPFWFIntegration.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
4.  Digitare il proprio nome e cognome nella finestra di dialogo.  
  
5.  Chiudere la finestra di dialogo; la console restituirà il nome.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\WPFWFIntegration`  
  
## Vedere anche