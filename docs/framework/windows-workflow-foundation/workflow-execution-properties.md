---
title: "Propriet&#224; di esecuzione del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a50e088e-3a45-4267-bd51-1a3e6c2d246d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Propriet&#224; di esecuzione del flusso di lavoro
Tramite l'archiviazione locale di thread \(TLS\), CLR gestisce un contesto di esecuzione per ogni thread.Questo contesto di esecuzione determina le proprietà note dei thread quali l'identità del thread, la transazione di ambiente e il set di autorizzazioni corrente, in aggiunta alle proprietà del thread definite dall'utente come gli slot denominati.  
  
 A differenza dei programmi destinati direttamente a CLR, i programmi del flusso di lavoro sono strutture ad albero di attività con ambiti gerarchici che vengono eseguite in un ambiente indipendente dal thread.Pertanto i meccanismi TLS standard non possono essere utilizzati direttamente per determinare il contesto incluso nell'ambito per un elemento di lavoro specificato.Ad esempio, due rami paralleli di esecuzione potrebbero utilizzare transazioni diverse, oppure il servizio di pianificazione potrebbe eseguire l'interfoliazione dell'esecuzione sullo stesso thread CLR.  
  
 Le proprietà di esecuzione del flusso di lavoro forniscono un meccanismo per aggiungere proprietà specifiche del contesto all'ambiente di un'attività.In questo modo un'attività può dichiarare quali proprietà sono incluse nell'ambito per i relativi sottoalberi, nonché fornire hook per impostare e chiudere TLS al fine di interoperare correttamente con gli oggetti CLR.  
  
## Creazione e utilizzo di proprietà di esecuzione del flusso di lavoro  
 Le proprietà di esecuzione del flusso di lavoro in genere implementano l'interfaccia di <xref:System.Activities.IExecutionProperty>, anche se le proprietà incentrate sulla messaggistica possono implementare invece <xref:> System.ServiceModel.Activities.ISendMessageCallback?qualifyHint=False&autoUpgrade=True e <xref:> System.ServiceModel.Activities.IReceiveMessageCallback?qualifyHint=False&autoUpgrade=True.Per creare una proprietà di esecuzione del flusso di lavoro, creare una classe che implementa l'interfaccia <xref:System.Activities.IExecutionProperty> e implementare i membri <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> e <xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A>.Questi membri forniscono la proprietà di esecuzione e consentono di impostare e chiudere correttamente l'archivio locale del thread durante ogni impulso di lavoro dell'attività che contiene la proprietà, incluse eventuali attività figlio.In questo esempio viene creato un oggetto `ConsoleColorProperty` che imposta l'oggetto `Console.ForegroundColor`.  
  
> [!NOTE]
>  Il seguente codice di esempio di questo argomento si basa sull'esempio [Proprietà di esecuzione](../../../docs/framework/windows-workflow-foundation/samples/execution-properties.md).  
  
```csharp  
class ConsoleColorProperty : IExecutionProperty  
{  
    public const string Name = "ConsoleColorProperty";  
  
    ConsoleColor original;  
    ConsoleColor color;  
  
    public ConsoleColorProperty(ConsoleColor color)  
    {  
        this.color = color;  
    }  
  
    void IExecutionProperty.SetupWorkflowThread()  
    {  
        original = Console.ForegroundColor;  
        Console.ForegroundColor = color;  
    }  
  
    void IExecutionProperty.CleanupWorkflowThread()  
    {  
        Console.ForegroundColor = original;  
    }  
}  
```  
  
 Gli autori di attività possono utilizzare questa proprietà registrandola nell'override di esecuzione dell'attività.In questo esempio viene definita un'attività `ConsoleColorScope` che registra l'oggetto `ConsoleColorProperty` aggiungendolo alla raccolta <xref:System.Activities.NativeActivityContext.Properties%2A> dell'oggetto <xref:System.Activities.NativeActivityContext> corrente.  
  
```csharp  
public sealed class ConsoleColorScope : NativeActivity  
{  
    public ConsoleColorScope()  
        : base()  
    {  
    }  
  
    public ConsoleColor Color { get; set; }  
    public Activity Body { get; set; }  
  
    protected override void Execute(NativeActivityContext context)  
    {  
        context.Properties.Add(ConsoleColorProperty.Name, new ConsoleColorProperty(this.Color));  
  
        if (this.Body != null)  
        {  
            context.ScheduleActivity(this.Body);  
        }  
    }  
}  
```  
  
 Quando il corpo dell'attività avvia un impulso di lavoro, viene chiamato il metodo <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> della proprietà e quando l'impulso di lavoro viene completato, viene chiamato il metodo <xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A>.In questo esempio viene creato un flusso di lavoro che utilizza un'attività <xref:System.Activities.Statements.Parallel> con tre rami.I primi due rami, a differenza del terzo, utilizzano l'attività `ConsoleColorScope`.Tutti i tre rami contengono due attività <xref:System.Activities.Statements.WriteLine> e un'attività <xref:System.Activities.Statements.Delay>.Quando l'attività <xref:System.Activities.Statements.Parallel> viene eseguita, le attività contenute nei branch vengono eseguite in un modo caratterizzato da interfoliazione, ma quando ogni attività figlio viene eseguita, l'oggetto `ConsoleColorProperty` applica il corretto colore della console.  
  
```csharp  
Activity wf = new Parallel  
{  
    Branches =   
    {  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Blue,  
            Body = new Sequence  
            {  
                Activities =   
                {  
                    new WriteLine  
                    {  
                        Text = "Start blue text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End blue text."  
                    }  
                }  
            }  
        },  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Red,  
            Body = new Sequence  
            {  
                Activities =   
                {  
                    new WriteLine  
                    {  
                        Text = "Start red text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End red text."  
                    }  
                }  
            }  
        },  
        new Sequence  
        {  
            Activities =   
            {  
                new WriteLine  
                {  
                    Text = "Start default text."  
                },  
                new Delay  
                {  
                    Duration = TimeSpan.FromSeconds(1)  
                },  
                new WriteLine  
                {  
                    Text = "End default text."  
                }  
            }  
        }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 Quando il flusso di lavoro viene richiamato, l'output seguente viene scritto nella finestra della console.  
  
```  
Start blue text.  
Start red text.  
Start default text.  
End blue text.  
End red text.  
End default text.  
```  
  
> [!NOTE]
>  Sebbene non venga mostrata nell'output precedente, ogni riga di testo nella finestra della console viene visualizzata con il colore indicato.  
  
 Le proprietà di esecuzione del flusso di lavoro possono essere utilizzate dagli autori di attività personalizzate e consentono di gestire l'handle per attività quali <xref:System.ServiceModel.Activities.CorrelationScope> e <xref:System.Activities.Statements.TransactionScope>.  
  
## Vedere anche  
 <xref:System.Activities.IExecutionProperty>   
 <xref:System.Activities.IPropertyRegistrationCallback>   
 <xref:System.Activities.RegistrationContext>