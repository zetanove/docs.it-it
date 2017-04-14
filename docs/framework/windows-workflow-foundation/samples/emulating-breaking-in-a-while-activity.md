---
title: "Emulazione di interruzione in un&#39;attivit&#224; While | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ddff715d-d623-4b54-b841-60bacbc3ca21
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Emulazione di interruzione in un&#39;attivit&#224; While
In questo esempio viene illustrato come interrompere il meccanismo di ciclo delle attività seguenti: <xref:System.Activities.Statements.DoWhile>, <xref:System.Activities.Statements.ForEach%601>, <xref:System.Activities.Statements.While> e <xref:System.Activities.Statements.ParallelForEach%601>.  
  
 Tale operazione è utile poiché in [!INCLUDE[wf](../../../../includes/wf-md.md)] non è inclusa alcuna attività per interrompere l'esecuzione di questi cicli.  
  
## Scenario  
 Nell'esempio viene rilevato il primo fornitore affidabile in un elenco di fornitori \(istanze della classe `Vendor`\).Ogni fornitore dispone di un oggetto `ID`, di un oggetto `Name` e di un valore di affidabilità numerico che determina l'affidabilità del fornitore.Nell'esempio viene creata un'attività personalizzata denominata `FindReliableVendor` che riceve due parametri di input \(un elenco di fornitori e un valore di affidabilità minimo\) e restituisce il primo fornitore dell'elenco che corrisponde ai criteri forniti.  
  
## Interruzione di un ciclo  
 In [!INCLUDE[wf](../../../../includes/wf-md.md)] non è inclusa alcuna attività per interrompere un ciclo.Nell'esempio di codice viene eseguita l'interruzione di un ciclo tramite un'attività <xref:System.Activities.Statements.If> e diverse variabili.Nell'esempio, l'attività <xref:System.Activities.Statements.While> viene interrotta dopo che alla variabile `reliableVendor` viene assegnato un valore diverso da `null`.  
  
 Nell'esempio di codice seguente viene illustrato il modo in cui l'esempio interrompe un ciclo while.  
  
```csharp  
// Iterates while the “i” variable is lower than the size of the list   
// and any reliable Vendor is found.        
new While(env => i.Get(env) < this.Vendors.Get(env).Count && reliableVendor.Get(env) == null)  
{  
    DisplayName = "Main loop. Breaks when a reliable vendor is found",  
    Body = new Sequence  
    {                              
        Activities =  
        {  
            // This is the if used for setting the value of the break value…  
            new If  
            {  
                DisplayName = "Check for a reliable vendor",  
  
                //  If a vendor satisfies the reliability level…  
                Condition = new InArgument<bool>(env =>   
                           this.Vendors.Get(env)[i.Get(env)].Reliability >   
                           this.MinimumReliability.Get(env)),  
  
                // then assign that vendor to the reliable vendor variable and   
                // the while condition becomes false (exit the loop).  
                Then = new Assign<Vendor>  
                {  
                    To = reliableVendor,  
                    Value = new InArgument<Vendor>(env =>   
                                  this.Vendors.Get(env)[i.Get(env)])  
                }  
            },  
  
            // Increment the iteration variable.   
            new Assign<int>  
            {  
                DisplayName = "Increment iteration variable",  
                To = i,  
                Value = new InArgument<int>(env => i.Get(env) + 1)  
            }   
        }  
    }  
}  
  
```  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione EmulatingBreakInWhile.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Built-InActivities\EmulatingBreakInWhile`  
  
## Vedere anche