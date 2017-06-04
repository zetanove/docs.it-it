---
title: "Utilizzo di estensioni di attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 500eb96a-c009-4247-b6b5-b36faffdf715
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Utilizzo di estensioni di attivit&#224;
Le attività possono interagire con estensioni dell'applicazione flusso di lavoro che consentono all'host di fornire funzionalità aggiuntive non modellate in modo esplicito nel flusso di lavoro.In questo argomento viene descritto come creare e utilizzare un'estensione per contare il numero di volte in cui un'attività viene eseguita.  
  
### Per utilizzare un'estensione di attività per contare le esecuzioni  
  
1.  Aprire [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].Selezionare **Nuovo**, **Progetto**.Nel nodo **Visual C\#** selezionare **Flusso di lavoro**.Selezionare **Applicazione console flusso di lavoro** nell'elenco di modelli.Assegnare il nome `Extensions` al progetto.Fare clic su **OK** per creare il progetto.  
  
2.  Aggiungere un'istruzione `using` nel file Program.cs per lo spazio dei nomi **System.Collections.Generic**.  
  
    ```  
    using System.Collections.Generic;  
  
    ```  
  
3.  Nel file Program.cs creare una nuova classe denominata **ExecutionCountExtension**.Nel codice seguente viene creata un'estensione del flusso di lavoro che tiene traccia degli ID istanza quando viene chiamato il metodo **Register**.  
  
    ```  
    // This extension collects a list of workflow Ids  
    public class ExecutionCountExtension  
    {  
        IList<Guid> instances = new List<Guid>();  
  
        public int ExecutionCount  
        {  
            get  
            {  
                return this.instances.Count;  
            }  
        }  
  
        public IEnumerable<Guid> InstanceIds  
        {  
            get  
            {  
                return this.instances;  
            }  
        }  
  
        public void Register(Guid activityInstanceId)  
        {  
            if (!this.instances.Contains<Guid>(activityInstanceId))  
            {  
                instances.Add(activityInstanceId);  
            }  
        }  
    }  
  
    ```  
  
4.  Creare un'attività che utilizza **ExecutionCountExtension**.Nel codice seguente viene definita un'attività che recupera l'oggetto **ExecutionCountExtension** dal runtime e chiama il metodo **Register** quando l'attività viene eseguita.  
  
    ```  
    // Activity that consumes an extension provided by the host. If the extension is available  
    // in the context, it will invoke (in this case, registers the Id of the executing workflow)  
    public class MyActivity: CodeActivity  
    {  
        protected override void Execute(CodeActivityContext context)  
        {  
            ExecutionCountExtension ext = context.GetExtension<ExecutionCountExtension>();  
            if (ext != null)  
            {  
                ext.Register(context.WorkflowInstanceId);                         
            }  
  
        }  
    }  
  
    ```  
  
5.  Implementare l'attività nel metodo **Main** del file program.cs.Nel codice seguente sono contenuti metodi per generare due flussi di lavoro diversi, eseguire ogni flusso di lavoro più volte e visualizzare i dati risultanti contenuti nell'estensione.  
  
    ```  
    class Program  
    {  
        // Creates a workflow that uses the activity that consumes the extension  
        static Activity CreateWorkflow1()  
        {  
            return new Sequence  
            {  
                Activities =  
                {  
                    new MyActivity()  
                }  
            };  
        }  
  
        // Creates a workflow that uses two instances of the activity that consumes the extension  
        static Activity CreateWorkflow2()  
        {  
            return new Sequence  
            {  
                Activities =  
                {  
                    new MyActivity(),  
                    new MyActivity()  
                }  
            };  
        }  
  
        static void Main(string[] args)  
        {  
            // create the extension   
            ExecutionCountExtension executionCountExt = new ExecutionCountExtension();  
  
            // configure the first invoker and execute 3 times  
            WorkflowInvoker invoker = new WorkflowInvoker(CreateWorkflow1());  
            invoker.Extensions.Add(executionCountExt);                          
            invoker.Invoke();  
            invoker.Invoke();  
            invoker.Invoke();  
  
            // configure the second invoker and execute 2 times  
            WorkflowInvoker invoker2 = new WorkflowInvoker(CreateWorkflow2());  
            invoker2.Extensions.Add(executionCountExt);  
            invoker2.Invoke();  
            invoker2.Invoke();  
  
            // show the data in the extension  
            Console.WriteLine("Executed {0} times", executionCountExt.ExecutionCount);  
            executionCountExt.InstanceIds.ToList().ForEach(i => Console.WriteLine("...{0}", i));  
        }  
    }  
    ```