---
title: "Utilizzo delle attivit&#224; di raccolta | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e1977cf8-1695-4071-b946-7046fe39601e
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Utilizzo delle attivit&#224; di raccolta
In questo esempio viene illustrato come utilizzare le attività della raccolta \(<xref:System.Activities.Statements.AddToCollection%601>, <xref:System.Activities.Statements.ClearCollection%601>, <xref:System.Activities.Statements.ExistsInCollection%601> e <xref:System.Activities.Statements.RemoveFromCollection%601>\) con una classe che implementa l'interfaccia <xref:System.Collections.ICollection> e come creare un'attività personalizzata che scorre una raccolta per stampare il contenuto di ogni elemento nella raccolta.L'attività personalizzata, denominata `PrintCollection`, stampa nella console i membri degli elementi di una raccolta denominata `Numbers`.  
  
 Nella tabella seguente vengono descritte le quattro attività che consentono di modificare la raccolta per i flussi di lavoro.  
  
|Nome attività|Descrizione|  
|-------------------|-----------------|  
|<xref:System.Activities.Statements.AddToCollection%601>|Aggiunge un elemento a una raccolta.|  
|<xref:System.Activities.Statements.ClearCollection%601>|Cancella tutti gli elementi in una raccolta|  
|<xref:System.Activities.Statements.ExistsInCollection%601>|Restituisce `true` se l'elemento specificato è presente in una raccolta.|  
|<xref:System.Activities.Statements.RemoveFromCollection%601>|Rimuove un elemento da una raccolta.|  
  
 L'esempio è costituito da due soluzioni, una sotto la directory CodedWorkflow e l'altra sotto la directory DesignerWorkflow.Vengono illustrati due modi diversi di utilizzo delle attività per gli stessi scopi.  
  
||||  
|-|-|-|  
|Soluzione|Descrizione|File principali|  
|CodedWorkflow|Applicazione client di esempio in cui viene illustrato come richiamare a livello di codice le attività della raccolta.|**PrintCollection.cs**: attività di supporto per stampare tutti gli elementi di una raccolta nella console.<br /><br /> **Program.cs**: compila a livello di codice un'attività Sequence che contiene una serie di attività della raccolta e la esegue.|  
|DesignerWorkflow|Applicazione client di esempio in cui viene illustrato come utilizzare le attività della raccolta in modo dichiarativo nella progettazione flussi di lavoro.|**CollectionWorkflow.xaml**: flusso di lavoro creato in modo dichiarativo con la finestra di progettazione che utilizza le attività della raccolta.<br /><br /> **PrintCollection.cs**: attività di supporto per stampare tutti gli elementi di una raccolta nella console.<br /><br /> **Program.cs**: richiama il flusso di lavoro descritto in CollectionWorkflow.xaml.|  
  
 Nella dimostrazione, i membri degli elementi della raccolta `Numbers` vengono stampati nella console utilizzando un'attività personalizzata denominata `PrintCollection`.  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione Collection.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Built-InActivities\Collection`  
  
## Vedere anche