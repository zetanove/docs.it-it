---
title: "Attivit&#224; ParallelForEach non generica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: de17e7a2-257b-48b3-91a1-860e2e9bf6e6
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Attivit&#224; ParallelForEach non generica
Nella casella degli strumenti di [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] è disponibile un set di attività del flusso di controllo, inclusa <xref:System.Activities.Statements.ParallelForEach%601> che consente di scorrere le raccolte <xref:System.Collections.IEnumerable%601>.  
  
 L'oggetto <xref:System.Activities.Statements.ParallelForEach%601> richiede che la relativa proprietà <xref:System.Activities.Statements.ParallelForEach%601.Values%2A> sia di tipo <xref:System.Collections.IEnumerable%601>.  In questo modo, gli utenti non possono scorrere le strutture di dati che implementano l'interfaccia <xref:System.Collections.IEnumerable%601> \(ad esempio l'oggetto <xref:System.Collections.ArrayList>\).  La versione non generica dell'oggetto <xref:System.Activities.Statements.ParallelForEach%601> supera questo requisito, a discapito di una maggiore complessità della fase di esecuzione per assicurare la compatibilità dei tipi dei valori nella raccolta.  
  
 In questo esempio viene illustrato come implementare un'attività <xref:System.Activities.Statements.ParallelForEach%601> non generica e la relativa finestra di progettazione.  Questa attività può essere usata per scorrere l'oggetto <xref:System.Collections.ArrayList>.  
  
## Attività ParallelForEach  
 L'istruzione `foreach` di C\#\/VB enumera gli elementi di una raccolta eseguendo un'istruzione incorporata per ogni elemento della raccolta.  Le attività equivalenti di [!INCLUDE[wf1](../../../../includes/wf1-md.md)] sono <xref:System.Activities.Statements.ForEach%601> e <xref:System.Activities.Statements.ParallelForEach%601>.  L'attività <xref:System.Activities.Statements.ForEach%601> contiene un elenco di valori e un corpo.  In fase di esecuzione, viene scorso l'elenco e il corpo viene eseguito per ogni valore dell'elenco.  
  
 L'oggetto <xref:System.Activities.Statements.ParallelForEach%601> dispone di una proprietà <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> in modo che l'attività <xref:System.Activities.Statements.ParallelForEach%601> possa essere completata in fretta se la valutazione della proprietà <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> restituisce `true`.  La proprietà <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> viene valutata al termine di ogni iterazione.  
  
 Nella maggior parte dei casi, la versione generica dell'attività deve essere la soluzione preferita, poiché concerne la maggioranza degli scenari in cui viene usata e fornisce il controllo dei tipi in fase di compilazione.  La versione non generica può essere usata per scorrere i tipi che implementano l'interfaccia <xref:System.Collections.IEnumerable> non generica.  
  
## Definizione della classe  
 Nell'esempio di codice seguente viene illustrata la definizione di un'attività `ParallelForEach` non generica.  
  
```  
[ContentProperty("Body")]  
public class ParallelForEach : NativeActivity  
{  
    [RequiredArgument]  
    [DefaultValue(null)]  
    InArgument<IEnumerable> Values { get; set; }  
  
    [DefaultValue(null)]  
    [DependsOn("Values")]  
    public Activity<bool> CompletionCondition  
    [DefaultValue(null)]  
    [DependsOn("CompletionCondition")]  
    ActivityAction<object> Body { get; set; }   
}  
```  
  
 Body \(facoltativo\)  
 Oggetto <xref:System.Activities.ActivityAction> di tipo <xref:System.Object> eseguito per ogni elemento della raccolta.  Ogni singolo elemento viene passato al corpo tramite la proprietà Argument.  
  
 Values \(facoltativo\)  
 Raccolta di elementi che vengono scorsi.  In fase di esecuzione si verifica che tutti gli elementi della raccolta siano di tipi compatibili.  
  
 CompletionCondition \(facoltativo\)  
 La proprietà <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> viene valutata al termine di qualsiasi iterazione.  Se restituisce `true`, le iterazioni in sospeso pianificate vengono annullate.  Se questa proprietà non è impostata, tutte le attività nella raccolta di rami vengono eseguite fino al completamento.  
  
## Esempio di utilizzo di ParallelForEach  
 Nel codice seguente viene illustrato come usare l'attività ParallelForEach in un'applicazione.  
  
```  
string[] names = { "bill", "steve", "ray" };  
  
DelegateInArgument<object> iterationVariable = new DelegateInArgument<object>() { Name = "iterationVariable" };  
  
Activity sampleUsage =  
    new ParallelForEach  
    {  
       Values = new InArgument<IEnumerable>(c=> names),  
       Body = new ActivityAction<object>   
       {                          
           Argument = iterationVariable,  
           Handler = new WriteLine  
           {  
               Text = new InArgument<string>(env => string.Format("Hello {0}",                                                               iterationVariable.Get(env)))  
           }  
       }  
   };  
```  
  
## Finestra di progettazione ParallelForEachT  
 L'aspetto dell'ActivityDesigner per l'esempio è simile a quello della finestra di progettazione fornita per l'attività <xref:System.Activities.Statements.ParallelForEach%601> incorporata.  La finestra di progettazione viene visualizzata nella categoria **Esempi**, **Attività non generiche** della casella degli strumenti.  La finestra di progettazione viene denominata **ParallelForEachWithBodyFactory** nella casella degli strumenti, poiché l'attività espone un oggetto <xref:System.Activities.Presentation.IActivityTemplateFactory> nella casella degli strumenti che crea l'attività con un oggetto <xref:System.Activities.ActivityAction> correttamente configurato.  
  
```  
public sealed class ParallelForEachWithBodyFactory : IActivityTemplateFactory  
{  
    public Activity Create(DependencyObject target)  
    {  
        return new Microsoft.Samples.Activities.Statements.ParallelForEach()  
        {  
            Body = new ActivityAction<object>()  
            {  
                Argument = new DelegateInArgument<object>()  
                {  
                    Name = "item"  
                }  
            }  
        };  
    }  
}  
```  
  
#### Per eseguire l'esempio  
  
1.  Impostare il progetto scelto come progetto di avvio della soluzione.  
  
    1.  In **CodeTestClient** viene illustrato come usare l'attività tramite codice.  
  
    2.  In **DesignerTestClient** viene illustrato come usare l'attività all'interno della finestra di progettazione.  
  
2.  Compilare ed eseguire il progetto.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NonGenericParallelForEach`