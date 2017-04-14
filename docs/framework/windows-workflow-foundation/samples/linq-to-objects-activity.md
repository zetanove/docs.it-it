---
title: "Attivit&#224; LINQ to Objects | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 403c82e8-7f2b-42f6-93cd-95c35bc76ead
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Attivit&#224; LINQ to Objects
In questo esempio viene illustrato come creare un'attività per utilizzare LINQ to Objects per eseguire query su elementi di una raccolta.  
  
## Dettagli dell'attività per FindInCollection  
 Questa attività consente agli utenti di eseguire query su elementi di raccolte in memoria utilizzando LINQ to Objects.È necessario fornire un predicato LINQ nel formato di un'espressione lambda per filtrare i risultati.Questa attività può essere utilizzata unitamente ad attività <xref:System.Activities.Statements.AddToCollection%601>.  
  
 Nella tabella seguente viene descritta la proprietà e i valori restituiti per l'attività.  
  
|Proprietà o valore restituito|Descrizione|  
|-----------------------------------|-----------------|  
|Proprietà `Collection`|Proprietà obbligatoria che specifica la raccolta di origine.|  
|Proprietà `Predicate`|Proprietà obbligatoria che specifica il filtro per la raccolta nel formato di un'espressione lambda.|  
|Valore restituito|La raccolta filtrata.|  
  
## Esempio di codice che utilizza l'attività personalizzata  
 Nell'esempio di codice seguente viene utilizzata l'attività personalizzata `FindInCollection` per trovare tutte le righe in una raccolta di dipendenti la cui proprietà `Role` è impostata su `Manager` e la proprietà `Location` è impostata su `Redmond`.  
  
```csharp  
// Find all program managers in Redmond in the employees collection.  
  
Activity wf = new FindInCollection<Employee>  
{  
    Collections = new LambdaValue<IEnumerable<Employee>>(c => employees),                
    Predicate = new LambdaValue<Func<Employee, bool>>(c => new Func<Employee, bool>(e => e.Role.Equals("Manager") && e.Location.Equals("Redmond")))  
};  
  
```  
  
 Nel codice seguente viene illustrato come creare un programma flusso di lavoro che utilizza l'attività FindInCollection personalizzata e le attività <xref:System.Activities.Statements.AddToCollection%601> e <xref:System.Activities.Statements.ForEach%601> per popolare una raccolta con dipendenti, trovare tutti i dipendenti con il ruolo di sviluppatore e che si trovano a Redmond, quindi scorrere l'elenco risultante.  
  
```csharp  
// Create the Linq predicate for the find expression  
  
Func<Employee, bool> predicate = e => e.Role == "DEV" && e.Location.Equals("Redmond");  
  
// Create workflow program  
Activity sampleWorkflow = new Sequence  
{  
    Variables = { employees, devsFromRedmond },  
    Activities =  
    {  
        new Assign<IList<Employee>>  
        {  
            To = employees,  
            Value = new LambdaValue<IList<Employee>>(c => new List<Employee>())  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(1, "Employee 1", "DEV", "Redmond"))  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(2, "Employee 2", "DEV", "Redmond"))  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(3, "Employee 3", "PM", "Redmond"))  
        },  
        new AddToCollection<Employee>  
        {  
            Collection = new InArgument<ICollection<Employee>>(employees),  
            Item =  new LambdaValue<Employee>(c => new Employee(4, "Employee 4", "PM", "China"))  
        },  
        new FindInCollection<Employee>  
        {  
            Collections = new InArgument<IEnumerable<Employee>>(employees),  
            Predicate = new LambdaValue<Func<Employee, bool>>(c => predicate),  
            Result = new OutArgument<IList<Employee>>(devsFromRedmond)  
        },  
        new ForEach<Employee>  
        {  
            Values = new InArgument<IEnumerable<Employee>>(devsFromRedmond),  
            Body = new ActivityAction<Employee>  
            {  
                Argument = iterationVariable,  
                Handler = new WriteLine  
                {  
                    Text = new InArgument<string>(env => iterationVariable.Get(env).ToString())  
                }  
            }  
        }  
    }  
};  
```  
  
#### Per utilizzare questo esempio  
  
1.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione LinqToObjects.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\LinqToObjects`  
  
## Vedere anche  
 [Espressioni lambda \(Guida per programmatori C\#\)](http://go.microsoft.com/fwlink/?LinkId=150381)   
 [LINQ to Objects](http://go.microsoft.com/fwlink/?LinkID=150380)