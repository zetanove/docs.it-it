---
title: "ForEach non generica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 576cd07a-d58d-4536-b514-77bad60bff38
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# ForEach non generica
Nella casella degli strumenti di [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] è disponibile un set di attività del flusso di controllo, inclusa <xref:System.Activities.Statements.ForEach%601> che consente di scorrere le raccolte <xref:System.Collections.IEnumerable%601>.  
  
 L'oggetto <xref:System.Activities.Statements.ForEach%601> richiede che la relativa proprietà <xref:System.Activities.Statements.ForEach%601.Values%2A> sia di tipo <xref:System.Collections.IEnumerable%601>.  In questo modo, gli utenti non possono scorrere le strutture di dati che implementano l'interfaccia <xref:System.Collections.IEnumerable%601> \(ad esempio l'oggetto <xref:System.Collections.ArrayList>\).  La versione non generica dell'oggetto <xref:System.Activities.Statements.ForEach%601> supera questo requisito, a discapito di una maggiore complessità della fase di esecuzione per assicurare la compatibilità dei tipi dei valori nella raccolta.  
  
 In questo esempio viene illustrato come implementare un'attività <xref:System.Activities.Statements.ForEach%601> non generica e la relativa finestra di progettazione.  Questa attività può essere usata per scorrere l'oggetto <xref:System.Collections.ArrayList>.  
  
## Attività ForEach  
 L'istruzione `foreach` di C\#\/VB enumera gli elementi di una raccolta eseguendo un'istruzione incorporata per ogni elemento della raccolta.  Le attività [!INCLUDE[wf1](../../../../includes/wf1-md.md)] equivalenti di `foreach` sono <xref:System.Activities.Statements.ForEach%601> e <xref:System.Activities.Statements.ParallelForEach%601>.  L'attività <xref:System.Activities.Statements.ForEach%601> contiene un elenco di valori e un corpo.  In fase di esecuzione, viene scorso l'elenco e il corpo viene eseguito per ogni valore dell'elenco.  
  
 Nella maggior parte dei casi, la versione generica dell'attività deve essere la soluzione preferita, poiché concerne la maggioranza degli scenari in cui verrà usata e fornisce il controllo dei tipi in fase di compilazione.  La versione non generica può essere usata per scorrere i tipi che implementano l'interfaccia <xref:System.Collections.IEnumerable> non generica.  
  
## Definizione della classe  
 Nell'esempio di codice seguente viene illustrata la definizione di un'attività `ForEach` non generica.  
  
```  
[ContentProperty("Body")]  
public class ForEach : NativeActivity  
{  
    [RequiredArgument]  
    [DefaultValue(null)]  
    InArgument<IEnumerable> Values { get; set; }  
  
    [DefaultValue(null)]  
    [DependsOn("Values")]  
    ActivityAction<object> Body { get; set; }   
}  
```  
  
 Body \(facoltativo\)  
 Oggetto <xref:System.Activities.ActivityAction> di tipo <xref:System.Object> eseguito per ogni elemento della raccolta.  Ogni singolo elemento viene passato al corpo tramite la proprietà `Argument`.  
  
 Values \(facoltativo\)  
 Raccolta di elementi che vengono scorsi.  In fase di esecuzione si verifica che tutti gli elementi della raccolta siano di tipi compatibili.  
  
## Esempio di utilizzo di ForEach  
 Nel codice seguente viene illustrato come usare l'attività ForEach in un'applicazione.  
  
```  
string[] names = { "bill", "steve", "ray" };  
  
DelegateInArgument<object> iterationVariable = new DelegateInArgument<object>() { Name = "iterationVariable" };  
  
Activity sampleUsage =  
    new ForEach  
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
  
|Condizione|Messaggio|Gravità|Tipo di eccezione|  
|----------------|---------------|-------------|-----------------------|  
|I valori sono `null`|Valore non specificato per un argomento di attività 'Values' obbligatorio.|Errore|<xref:System.InvalidOperationException>|  
  
## Finestra di progettazione ForEach  
 L'aspetto dell'ActivityDesigner per l'esempio è simile a quello della finestra di progettazione fornita per l'attività <xref:System.Activities.Statements.ForEach%601> incorporata.  La finestra di progettazione viene visualizzata nella categoria **Esempi**, **Attività non generiche** della casella degli strumenti.  La finestra di progettazione viene denominata **ForEachWithBodyFactory** nella casella degli strumenti, poiché l'attività espone un oggetto <xref:System.Activities.Presentation.IActivityTemplateFactory> nella casella degli strumenti che crea l'attività con un oggetto <xref:System.Activities.ActivityAction> correttamente configurato.  
  
```  
public sealed class ForEachWithBodyFactory : IActivityTemplateFactory  
{  
    public Activity Create(DependencyObject target)  
    {  
        return new Microsoft.Samples.Activities.Statements.ForEach()  
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
  
1.  Impostare il progetto scelto come progetto di avvio della soluzione:  
  
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
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NonGenericForEach`