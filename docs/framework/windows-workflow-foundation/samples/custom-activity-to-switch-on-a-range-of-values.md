---
title: "Attivit&#224; personalizzata per il passaggio in base a un intervallo di valori | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 441e0a17-421f-430c-ba97-59e4cc6c88e3
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Attivit&#224; personalizzata per il passaggio in base a un intervallo di valori
In questo esempio viene illustrato come creare un'attività personalizzata che estende l'utilizzo di <xref:System.Activities.Statements.Switch%601>.Un'istruzione <xref:System.Activities.Statements.Switch%601> convenzionale consente il passaggio in base a un singolo valore.Esistono tuttavia scenari aziendali in cui il passaggio di un'attività deve basarsi su un intervallo di valori.Ad esempio, un'attività potrebbe eseguire un'azione quando il valore su cui si basa il passaggio è compreso tra 1 e 5, un'altra azione quando il valore è compreso tra 6 e 10 e un'azione predefinita per tutti gli altri valori.Questa attività personalizzata abilita esattamente tale scenario.  
  
## Attività SwitchRange  
 Tramite l'attività `SwitchRange` viene pianificata un'attività figlio quando il valore restituito dall'espressione è incluso nell'intervallo di uno dei relativi `Cases`.  
  
 L'esempio di codice seguente è un'attività personalizzata il cui passaggio si basa su un intervallo di valori.  
  
```csharp  
  
public sealed class SwitchRange<T> : NativeActivity where T : IComparable  
{  
   [RequiredArgument]  
   [DefaultValue(null)]  
   public InArgument<T> Expression { get; set; }  
  
   public IList<CaseRange<T>> Cases  
  
   [DefaultValue(null)]  
   public Activity Default { get; set; }}  
}  
```  
  
|||  
|-|-|  
|Proprietà|Descrizione|  
|Espressione|Si tratta dell'espressione da valutare e confrontare rispetto agli intervalli nell'elenco Cases.Il risultato dell'espressione è di tipo T.|  
|Cases|Ogni caso è costituito da un intervallo \(Da e A\) e da un'attività \(Body\).L'espressione viene valutata e confrontata rispetto agli intervalli.Se il risultato dell'espressione è compreso nell'intervallo di uno dei casi, viene eseguita l'attività corrispondente.|  
|Default|L'attività che viene eseguita quando nessun caso corrisponde.Quando è impostata su `null`, non viene eseguita alcuna azione.|  
  
## Classe CaseRange  
 La classe `CaseRange` rappresenta un intervallo all'interno di un'attività `SwitchRange`.Ogni istanza di `CaseRange` contiene un intervallo \(costituito da un oggetto `From` e un oggetto `To`\) e un'attività `Body` che viene pianificata se l'espressione in `SwitchRange` viene valutata all'interno dell'intervallo.  
  
 L'esempio di codice riportato di seguito è la definizione per la classe `CaseRange`.  
  
```  
  
public class CaseRange<T> where T : IComparable  
{  
    public T From { get; set; }  
  
    public T To { get; set; }  
  
    public Activity Action { get; set; }  
}  
```  
  
> [!NOTE]
>  Entrambe le classi `SwitchRange` e `CaseRange`, definite nell'esempio, sono classi generiche che possono essere utilizzate con qualsiasi tipo che implementa `IComparable`, come la classe <xref:System.Activities.Statements.Switch%601>.  
  
## Utilizzo dell'esempio  
 Nell'esempio di codice seguente viene illustrato come utilizzare l'attività `SwitchRange`.  
  
```csharp  
  
Activity SwitchRange = new SwitchRange<int>  
{  
    Expression = new InArgument<int>(value),  
    Cases =   
    {  
        new CaseRange<int>                      
        {  
            From = 1,  
            To = 5,  
            Action = new WriteLine  
            {  
                Text = "Case 1-5 selected",  
            }  
        },  
        new CaseRange<int>  
        {  
            From = 6,  
            To = 10,  
            Action = new WriteLine  
            {  
                Text = "Case 6-10 selected",  
            }  
        }  
    },  
    Default = new WriteLine { Text = "Default Case selected" }  
};  
```  
  
#### Per utilizzare questo esempio  
  
1.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione SwitchRange.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SwitchRange`  
  
## Vedere anche