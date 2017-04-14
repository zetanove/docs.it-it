---
title: "Programmazione dell&#39;albero degli elementi del modello | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0229efde-19ac-4bdc-a187-c6227a7bd1a5
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Programmazione dell&#39;albero degli elementi del modello
In questo esempio viene descritto come spostarsi all'interno della struttura ad albero <xref:System.Activities.Presentation.Model.ModelItem> utilizzando l'associazione dati dichiarativa dalla visualizzazione struttura ad albero di [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)].  
  
## Dettagli dell'esempio  
 L'albero di <xref:System.Activities.Presentation.Model.ModelItem> è l'astrazione utilizzata dall'infrastruttura [!INCLUDE[wfd1](../../../../includes/wfd1-md.md)] per esporre i dati sull'istanza sottostante in fase di modifica.Nell'illustrazione seguente viene fornita una descrizione dei vari livelli dell'infrastruttura all'interno di [!INCLUDE[wfd2](../../../../includes/wfd2-md.md)].  
  
 ![Architettura della progettazione flussi di lavoro](../../../../docs/framework/windows-workflow-foundation/samples/media/workflowdesignerarch.JPG "WorkflowDesignerArch")  
  
 Un oggetto <xref:System.Activities.Presentation.Model.ModelItem> è costituito da un puntatore al valore sottostante e da una raccolta di oggetti <xref:System.Activities.Presentation.Model.ModelProperty>.Un oggetto <xref:System.Activities.Presentation.Model.ModelProperty> è costituito, a sua volta, da dati quali il nome e il tipo della proprietà e quindi da un puntatore al valore che, a sua volta, è un altro <xref:System.Activities.Presentation.Model.ModelItem>.Un convertitore di valori viene utilizzato per modificare alcuni oggetti <xref:System.Activities.Presentation.Model.ModelItem>restituiti da <xref:System.Activities.Presentation.Model.ModelProperty> in modo che siano riportati correttamente nella visualizzazione struttura ad albero.Nell'esempio viene dimostrato quindi come programmare in modo imperativo rispetto alla struttura ad albero <xref:System.Activities.Presentation.Model.ModelItem> utilizzando la sintassi imperativa, come nell'esempio seguente.  
  
```csharp  
ModelItem mi = wd.Context.Services.GetService<ModelService>().Root;  
ModelProperty mp = mi.Properties["Activities"];  
mp.Collection.Add(new Persist());  
ModelItem justAdded = mp.Collection.Last();  
justAdded.Properties["DisplayName"].SetValue("new name");  
  
```  
  
#### Per utilizzare questo esempio  
  
1.  Aprire la soluzione ProgrammingModelItemTree.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare la soluzione scegliendo **Compila soluzione** dal menu **Compila**.  
  
3.  Premere F5 per eseguire l'applicazione.Viene quindi visualizzato il form [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)].  
  
4.  Fare clic sul pulsante **Carica WF** per caricare <xref:System.Activities.Presentation.Model.ModelItem> e associarlo alla visualizzazione struttura ad albero.  
  
5.  Facendo clic sul pulsante **Modifica struttura ad albero degli elementi del modello** viene eseguito il codice precedente per aggiungere un elemento nella struttura ad albero e impostare una proprietà.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Designer\ProgrammingModelItemTree`  
  
## Vedere anche  
 <xref:System.Windows.Data.IValueConverter>