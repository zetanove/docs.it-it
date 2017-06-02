---
title: "Esposizione dei dati con CacheMetadata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34832f23-e93b-40e6-a80b-606a855a00d9
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Esposizione dei dati con CacheMetadata
Prima di eseguire un'attività, il runtime del flusso di lavoro ottiene tutte le informazioni sull'attività necessarie per la gestione dell'esecuzione.Tali informazioni vengono ottenute durante l'esecuzione del metodo <xref:System.Activities.Activity.CacheMetadata%2A>.L'implementazione predefinita di questo metodo fornisce al runtime tutti gli argomenti pubblici, le variabili e le attività figlio esposti dall'attività al momento dell'esecuzione; se l'attività deve dare ulteriori informazioni al runtime, ad esempio membri privati o attività che devono essere pianificate dall'attività, è possibile eseguire l'override di questo metodo.  
  
## Comportamento predefinito di CacheMetadata  
 L'implementazione predefinita di <xref:System.Activities.NativeActivity.CacheMetadata%2A> per le attività che derivano da <xref:System.Activities.NativeActivity> elabora i tipi di metodo seguenti nelle modalità riportate di seguito:  
  
-   <xref:System.Activities.InArgument%601>, <xref:System.Activities.OutArgument%601> o <xref:System.Activities.InOutArgument%601> \(argomenti generici\): questi argomenti vengono esposti al runtime come argomenti con nome e tipo uguali al nome e al tipo di proprietà esposti, la direzione di argomento appropriata e alcuni dati di convalida.  
  
-   <xref:System.Activities.Variable> o qualsiasi sottoclasse relativa: questi membri vengono esposti al runtime come variabili pubbliche.  
  
-   <xref:System.Activities.Activity> o qualsiasi sottoclasse relativa: questi membri vengono esposti al runtime come attività figlio pubbliche.Il comportamento predefinito può essere implementato in modo esplicito chiamando <xref:System.Activities.ActivityMetadata.AddImportedChild%2A>, passando nell'attività figlio.  
  
-   <xref:System.Activities.ActivityDelegate> o qualsiasi sottoclasse relativa: questi membri vengono esposti al runtime come delegati pubblici.  
  
-   <xref:System.Collections.ICollection> di tipo <xref:System.Activities.Variable>: tutti gli elementi della raccolta vengono esposti al runtime come variabili pubbliche.  
  
-   <xref:System.Collections.ICollection> di tipo <xref:System.Activities.Activity>: tutti gli elementi della raccolta vengono esposti al runtime come elementi figlio pubblici.  
  
-   <xref:System.Collections.ICollection> di tipo <xref:System.Activities.ActivityDelegate>: tutti gli elementi nella raccolta vengono esposti al runtime come delegati pubblici.  
  
 Anche l'oggetto <xref:System.Activities.Activity.CacheMetadata%2A> per le attività che derivano da <xref:System.Activities.Activity>, <xref:System.Workflow.Activities.CodeActivity> e <xref:System.Activities.AsyncCodeActivity> funziona nel modo descritto sopra, tranne che per le differenze seguenti:  
  
-   Le classi che derivano da <xref:System.Activities.Activity> non possono pianificare attività figlio o delegati, pertanto tali membri vengono esposti come elementi figlio e delegati importati.  
  
-   Le classi che derivano da <xref:System.Activities.CodeActivity> e <xref:System.Activities.AsyncCodeActivity> non supportano variabili, elementi figli o delegati, pertanto vengono esposti solo gli argomenti.  
  
## Override di CacheMetadata per fornire informazioni al runtime  
 Nel frammento di codice seguente viene illustrato come aggiungere informazioni sui membri ai metadati di un'attività durante l'esecuzione del metodo <xref:System.Activities.Activity.CacheMetadata%2A>.Notare che la base del metodo è chiamata per memorizzare nella cache tutti i dati pubblici sull'attività.  
  
```  
protected override void CacheMetadata(NativeActivityMetadata metadata)  
{      
    base.CacheMetadata(metadata);  
    metadata.AddImplementationChild(this._writeLine);  
    metadata.AddVariable(this._myVariable);  
    metadata.AddImplementationVariable(this._myImplementationVariable);  
  
    RuntimeArgument argument = new RuntimeArgument("MyArgument", ArgumentDirection.In, typeof(SomeType));  
    metadata.Bind(argument, this.SomeName);  
    metadata.AddArgument(argument);  
}  
  
```  
  
## Utilizzo di CacheMetadata per esporre elementi figlio di implementazione  
 Per passare dati ad attività figlio che devono essere pianificate da un'attività utilizzando variabili, è necessario aggiungere le variabili come variabili di implementazione; i valori delle variabili pubbliche non possono essere impostati in questo modo.Il motivo di ciò è che le attività devono essere eseguite più come implementazioni di funzioni \(che dispongono di parametri\) che come classi incapsulate \(che dispongono di proprietà\).Tuttavia, ci sono situazioni nelle quali gli argomenti devono essere impostati in modo esplicito, ad esempio nel caso dell'utilizzo di <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>, dal momento che l'attività pianificata non dispone dell'accesso agli argomenti dell'attività padre come un'attività figlio.  
  
 Nel frammento di codice seguente viene illustrato come passare un argomento da un'attività nativa in un'attività pianificata utilizzando <xref:System.Activities.Activity.CacheMetadata%2A>.  
  
```  
public sealed class ChildActivity : NativeActivity  
{  
    public WriteLine _writeLine;  
    public InArgument<string> Message { get; set; }  
    private Variable<string> MessageVariable { get; set; }  
    public ChildActivity()  
    {  
        MessageVariable = new Variable<string>();  
        _writeLine = new WriteLine  
        {  
            Text = new InArgument<string>(MessageVariable),  
        };  
    }  
    protected override void CacheMetadata(NativeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        metadata.AddImplementationVariable(this.MessageVariable);  
        metadata.AddImplementationChild(this._writeLine);  
    }  
    protected override void Execute(NativeActivityContext context)  
    {  
        string configuredMessage = context.GetValue(Message);  
        context.SetValue(MessageVariable, configuredMessage);  
        context.ScheduleActivity(this._writeLine);  
    }  
}  
  
```