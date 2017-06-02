---
title: "Gestore di annullamento nell&#39;attivit&#224; compensabile | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: afd98bee-eccf-47e9-99c9-27cea84ce5ce
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Gestore di annullamento nell&#39;attivit&#224; compensabile
In questo esempio viene illustrato l'utilizzo di un gestore di annullamento in un oggetto <xref:System.Activities.Statements.CompensableActivity>.  
  
 Nell'esempio sono disponibili due scenari in cui viene illustrato l'utilizzo dell'annullamento dell'oggetto <xref:System.Activities.Statements.CompensableActivity>. Nel primo scenario è inclusa un'attività compensabile radice che contiene tre attività compensabili figlio.Le due attività figlio completano correttamente l'esecuzione dei relativi corpi delle attività.Quando viene eseguito il corpo della terza attività figlio, viene rilevata un'eccezione gestita annullando l'elaborazione della terza attività, dopo che viene attivato l'annullamento dell'attività radice.La logica nell'attività radice in questo esempio consiste nel compensare le altre due attività figlio che vengono completate precedentemente.  
  
```  
Try  
{  
    CA   
    {  
        CA1   
        {  
        }  
        CA2  
        {  
        }  
        CA3  
        {  
            //Exception here  
            // Then this will get cancelled  
        }  
  
       // Cancellation for the root activity automatically gets called, which, in turn, adds some logic to revert what was done (Or can decide to actually confirm CA1 & CA2 if the user so desires).  
    }  
}  
Catches {  
// Can do more stuff...  
}  
  
```  
  
 Nel secondo scenario viene illustrata l'esecuzione di un oggetto <xref:System.Activities.Statements.TryCatch> in parallelo con un oggetto <xref:System.Activities.Statements.Delay> che termina prima del ramo <xref:System.Activities.Statements.TryCatch>.La condizione di completamento viene impostata su `true` una volta terminato il primo ramo, determinando l'annullamento dell'altro ramo.  
  
```  
Parallel   
{  
    Branch1   
    {  
        // Small Delay that times out (timeout1) before branch2.  
    }  
    Branch2   
    {  
        CA   
        {  
            CA1   
            {  
            }  
            CA2   
            {  
            }  
            CA3   
            {  
            }  
            If (timeout1)    
            {  
                call Cancel CA  
            }  
        }  
    }  
}  
  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire CompensationCancellation.sln.  
  
2.  Compilare l'esempio premendo CTRL\+MAIUSC\+B o selezionare "Compila soluzione" dal menu Compila.  
  
3.  Eseguire l'esempio premendo F5 o selezionare "Avvia debug" dal menu Debug.In alternativa, è possibile premere Ctrl\+F5 o selezionare "Avvia senza eseguire debug" dal menu Debug.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Compensation\CompensationCancellation`  
  
## Vedere anche