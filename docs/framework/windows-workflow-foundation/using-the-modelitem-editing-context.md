---
title: "Utilizzo del contesto di modifica ModelItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7f9f1ea5-0147-4079-8eca-be94f00d3aa1
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Utilizzo del contesto di modifica ModelItem
Il contesto di modifica <xref:System.Activities.Presentation.Model.ModelItem> è l'oggetto utilizzato dall'applicazione host per comunicare con la finestra di progettazione.<xref:System.Activities.Presentation.EditingContext> espone due metodi utilizzabili, <xref:System.Activities.Presentation.EditingContext.Items%2A> e <xref:System.Activities.Presentation.EditingContext.Services%2A>.  
  
## La raccolta Items  
 La raccolta <xref:System.Activities.Presentation.EditingContext.Items%2A> viene utilizzata per accedere ai dati condivisi tra l'host e la finestra di progettazione o ai dati disponibili a tutte le finestre di progettazione.La raccolta dispone delle seguenti funzionalità, accessibili tramite la classe <xref:System.Activities.Presentation.ContextItemManager>:  
  
1.  <xref:System.Activities.Presentation.ContextItemManager.GetValue%2A>  
  
2.  <xref:System.Activities.Presentation.ContextItemManager.Subscribe%2A>  
  
3.  <xref:System.Activities.Presentation.ContextItemManager.Unsubscribe%2A>  
  
4.  <xref:System.Activities.Presentation.ContextItemManager.SetValue%2A>  
  
## La raccolta Services  
 La raccolta <xref:System.Activities.Presentation.EditingContext.Services%2A> viene utilizzata per accedere ai servizi usati dalla finestra di progettazione per interagire con l'host o ai servizi usati da tutte le finestre di progettazione.Questa raccolta dispone dei principali metodi seguenti:  
  
1.  <xref:System.Activities.Presentation.ServiceManager.Publish%2A>  
  
2.  <xref:System.Activities.Presentation.ServiceManager.Subscribe%2A>  
  
3.  <xref:System.Activities.Presentation.ServiceManager.Unsubscribe%2A>  
  
4.  <xref:System.Activities.Presentation.ServiceManager.GetService%2A>  
  
## Assegnazione di un'attività a una finestra di progettazione  
 Per specificare quale finestra di progettazione viene utilizzata da un'attività, viene utilizzato l'attributo Designer.  
  
```  
[Designer(typeof(MyClassDesigner))]  
public sealed class MyClass : CodeActivity  
{  
  
```  
  
## Creazione di un servizio  
 Per creare un servizio con la funzione di condotto di informazioni tra la finestra di progettazione e l'host, è necessario creare un'interfaccia e un'implementazione.L'interfaccia viene utilizzata dal metodo <xref:System.Activities.Presentation.ServiceManager.Publish%2A> per definire i membri del servizio e l'implementazione contiene la logica del servizio.Nell'esempio di codice seguente vengono create l'interfaccia e l'implementazione di un servizio.  
  
```  
public interface IMyService  
    {  
        IEnumerable<string> GetValues(string DisplayName);  
    }  
  
    public class MyServiceImpl : IMyService  
    {  
        public IEnumerable<string> GetValues(string DisplayName)  
        {  
            return new string[]  {   
                DisplayName + " One",   
                DisplayName + " Two",  
                "Three " + DisplayName  
            } ;  
        }  
    }  
  
```  
  
## Pubblicazione di un servizio  
 Affinché una finestra di progettazione utilizzi un servizio, questo deve essere prima pubblicato dal host utilizzando il metodo <xref:System.Activities.Presentation.ServiceManager.Publish%2A>.  
  
```  
this.Context.Services.Publish<IMyService>(new MyServiceImpl);  
```  
  
## Sottoscrizione di un servizio  
 La finestra di progettazione ottiene accesso al servizio utilizzando il metodo <xref:System.Activities.Presentation.ServiceManager.Subscribe%2A> nel metodo <xref:System.Activities.Presentation.WorkflowViewElement.OnModelItemChanged%2A>.Nel frammento di codice seguente viene mostrato come sottoscrivere un servizio.  
  
```  
protected override void OnModelItemChanged(object newItem)  
{  
    if (!subscribed)  
    {  
        this.Context.Services.Subscribe<IMyService>(  
            servInstance =>  
            {  
                listBox1.ItemsSource = servInstance.GetValues(this.ModelItem.Properties["DisplayName"].ComputedValue.ToString());  
            }  
            );  
        subscribed = true;   
    }  
}  
  
```  
  
## Condivisione di dati tramite la raccolta Items  
 L'utilizzo della raccolta Items è simile all'utilizzo della raccolta Services, tranne che si usa <xref:System.Activities.Presentation.ContextItemManager.SetValue%2A> anziché Publish.Questa raccolta è più adatta per la condivisione di dati semplici tra le finestre di progettazione e l'host che per funzionalità complesse.  
  
## Elementi e servizi host di EditingContext  
 .NET Framework fornisce una serie di elementi e servizi incorporati accessibili tramite il contesto di modifica.  
  
 Elementi:  
  
-   <xref:System.Activities.Presentation.Hosting.AssemblyContextControlItem>: gestisce l'elenco degli assembly locali di riferimento che verranno utilizzati nel flusso di lavoro per i controlli \(ad esempio l'editor espressioni\).  
  
-   <xref:System.Activities.Presentation.Hosting.ReadOnlyState>: indica se la finestra di progettazione è in stato di sola lettura.  
  
-   <xref:System.Activities.Presentation.View.Selection>: definisce la raccolta di oggetti attualmente selezionati.  
  
-   <xref:System.Activities.Presentation.Hosting.WorkflowCommandExtensionItem>:  
  
-   <xref:System.Activities.Presentation.WorkflowFileItem>: fornisce informazioni sul file su cui si basa la sessione di modifica corrente.  
  
 Servizi:  
  
-   <xref:System.Activities.Presentation.Model.AttachedPropertiesService>: consente l'aggiunta di proprietà all'istanza corrente tramite <xref:System.Activities.Presentation.Model.AttachedPropertiesService.AddProperty%2A>.  
  
-   <xref:System.Activities.Presentation.View.DesignerView>: consente l'accesso alle proprietà del Canvas della finestra di progettazione.  
  
-   <xref:System.Activities.Presentation.IActivityToolboxService>: consente l'aggiornamento del contenuto della casella degli strumenti.  
  
-   <xref:System.Activities.Presentation.Hosting.ICommandService>: utilizzato per integrare i comandi della finestra di progettazione \(quale Menu di scelta rapida\) con implementazioni del servizio personalizzate.  
  
-   <xref:System.Activities.Presentation.Debug.IDesignerDebugView>: fornisce funzionalità per il debugger della finestra di progettazione.  
  
-   <xref:System.Activities.Presentation.View.IExpressionEditorService>: fornisce l'accesso alla finestra di dialogo dell'Editor espressioni.  
  
-   <xref:System.Activities.Presentation.IIntegratedHelpService>: fornisce funzionalità integrate di Guida alla finestra di progettazione.  
  
-   <xref:System.Activities.Presentation.Validation.IValidationErrorService>: fornisce l'accesso agli errori di convalida tramite <xref:System.Activities.Presentation.Validation.IValidationErrorService.ShowValidationErrors%2A>.  
  
-   <xref:System.Activities.Presentation.IWorkflowDesignerStorageService>: fornisce un servizio interno per l'archiviazione e il recupero dei dati.Il servizio viene utilizzato internamente da .Net Framework e non è destinato all'uso esterno.  
  
-   <xref:System.Activities.Presentation.IXamlLoadErrorService>: fornisce l'accesso alla raccolta di errori di caricamento XAML tramite <xref:System.Activities.Presentation.IXamlLoadErrorService.ShowXamlLoadErrors%2A>.  
  
-   <xref:System.Activities.Presentation.Services.ModelService>: utilizzato dalla finestra di progettazione per interagire con il modello del flusso di lavoro modificato.  
  
-   <xref:System.Activities.Presentation.Model.ModelTreeManager>: fornisce l'accesso alla radice dell'albero dell'elemento del modello tramite <xref:System.Activities.Presentation.Model.ModelItem.Root%2A>.  
  
-   <xref:System.Activities.Presentation.UndoEngine>: fornisce funzionalità di rollback e rollforward.  
  
-   <xref:System.Activities.Presentation.Services.ViewService>: esegue il mapping degli elementi visivi agli elementi del modello sottostante.  
  
-   <xref:System.Activities.Presentation.View.ViewStateService>: archivia gli stati di visualizzazione per gli elementi del modello.  
  
-   <xref:System.Activities.Presentation.View.VirtualizedContainerService>: utilizzato per personalizzare il comportamento dell'interfaccia utente del contenitore virtuale.  
  
-   <xref:System.Activities.Presentation.Hosting.WindowHelperService>: utilizzato per registrare e annullare la registrazione dei delegati per le notifiche degli eventi.Consente inoltre l'impostazione del proprietario di una finestra.