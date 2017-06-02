---
title: "Convalida basata su codice imperativo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae12537c-455e-42b1-82f4-cea4c46c023e
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Convalida basata su codice imperativo
La convalida basata su codice imperativo fornisce un modo semplice per la convalida automatica di un'attività ed è disponibile per le attività che derivano dagli oggetti <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> e <xref:System.Activities.NativeActivity>.Il codice di convalida che determina gli avvisi o gli errori di convalida viene aggiunto all'attività.  
  
## Utilizzo della convalida basata su codice  
 La convalida basata su codice è supportata dalle attività che derivano dagli oggetti <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> e <xref:System.Activities.NativeActivity>.Il codice di convalida può essere inserito nell'override <xref:System.Activities.CodeActivity.CacheMetadata%2A> e gli errori o gli avvisi di convalida possono essere aggiunti all'argomento dei metadati.Nell'esempio riportato di seguito, estratto dall'esempio [Convalida di base](../../../docs/framework/windows-workflow-foundation/samples/basic-validation.md), se `Cost` è maggiore di `Price`, viene aggiunto un errore di convalida ai metadati.  
  
> [!NOTE]
>  Si noti che `Cost` e `Price` non sono argomenti dell'attività, ma proprietà impostate in fase di progettazione.Per questo motivo i valori possono essere convalidati nell'override <xref:System.Activities.CodeActivity.CacheMetadata%2A>.Il valore dei dati passati mediante un argomento non può essere convalidato in fase di progettazione perché i dati non si propagano fino alla fase di esecuzione, ma gli argomenti dell'attività possono essere convalidati per assicurarsi che siano associati utilizzano i gruppi di overload e di attributo `RequiredArgument`.Questo codice di esempio rileva l'attributo `RequiredArgument` per l'argomento `Description` e, se non è associato, viene generato un errore di convalida.Gli argomenti obbligatori vengono analizzati in [Argomenti obbligatori e gruppi di overload](../../../docs/framework/windows-workflow-foundation//required-arguments-and-overload-groups.md).  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error   
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
  
```  
  
 Per impostazione predefinita, un errore di convalida viene aggiunto ai metadati quando viene chiamato il metodo <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A>.Per aggiungere un avviso di convalida, utilizzare l'overload <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A> che accetta un oggetto <xref:System.Activities.Validation.ValidationError> e specificare che l'oggetto <xref:System.Activities.Validation.ValidationError> rappresenta un avviso impostando la proprietà <xref:System.Activities.Validation.ValidationError.IsWarning%2A>.  
  
 Viene eseguita quando un flusso di lavoro viene modificato nell'utilità di progettazione del flusso di lavoro e gli eventuali errori o avvisi di convalida vengono visualizzati in tale utilità.La convalida si verifica anche in fase di runtime quando un flusso di lavoro viene richiamato e, se si verificano errori di convalida, viene generata un'eccezione <xref:System.Activities.InvalidWorkflowException> dalla logica di convalida predefinita.[!INCLUDE[crabout](../../../includes/crabout-md.md)]lla convalida di chiamata e l'accesso agli avvisi o gli errori di convalida, vedere [Richiamo della convalida di attività](../../../docs/framework/windows-workflow-foundation//invoking-activity-validation.md).  
  
 Qualsiasi eccezione generata dal metodo <xref:System.Activities.CodeActivity.CacheMetadata%2A> non viene considerata come errore di convalida.Queste eccezioni utilizzeranno caratteri di escape dalla chiamata al metodo <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> e devono essere gestite dal chiamante.  
  
 La convalida basata su codice è utile per convalidare l'attività che contiene il codice, tuttavia non è visibile nelle altre attività del flusso di lavoro.La convalida di vincoli dichiarativi consente di convalidare le relazioni tra un'attività specifica e le altre attività del flusso di lavoro ed è descritta nell'argomento [Vincoli dichiarativi](../../../docs/framework/windows-workflow-foundation//declarative-constraints.md).