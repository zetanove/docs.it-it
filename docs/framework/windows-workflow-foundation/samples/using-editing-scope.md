---
title: "Utilizzo dell&#39;ambito di modifica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 79306f9e-318b-4687-9863-8b93d1841716
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Utilizzo dell&#39;ambito di modifica
In questo esempio viene illustrato come raggruppare un set di modifiche in modo che possano essere annullate in un'unica unità atomica.Per impostazione predefinita, le azioni intraprese da un autore dell'ActivityDesigner vengono integrate automaticamente nel sistema di annullamento\/ripristino.  
  
## Dimostrazione  
 Modifica di ambito e comandi Annulla e Ripeti.  
  
## Discussione  
 In questo esempio viene illustrato come riunire in batch un set di modifiche nella struttura ad albero <xref:System.Activities.Presentation.Model.ModelItem> all'interno di una singola unità di lavoro.Notare che in caso di associazione ai valori di <xref:System.Activities.Presentation.Model.ModelItem> direttamente da una finestra di progettazione WPF, le modifiche vengono applicate automaticamente.In questo esempio vengono illustrate le operazioni che è necessario eseguire quando, anziché una singola modifica, vengono apportate più modifiche da riunire in batch tramite codice imperativo.  
  
 In questo esempio vengono aggiunte tre attività.Quando inizia la modifica, viene chiamato <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A> su un'istanza di <xref:System.Activities.Presentation.Model.ModelItem>.le modifiche apportate alla struttura ad albero <xref:System.Activities.Presentation.Model.ModelItem> all'interno di questo ambito di modifica vengono riunite in batch.Il comando <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A> restituisce un oggetto <xref:System.Activities.Presentation.Model.EditingScope>che può essere utilizzato per controllare questa istanza.È possibile chiamare <xref:System.Activities.Presentation.Model.EditingScope.OnComplete%2A> o <xref:System.Activities.Presentation.Model.EditingScope.OnRevert%2A> per eseguire il commit o ripristinare l'ambito di modifica.  
  
 È inoltre possibile annidare oggetti <xref:System.Activities.Presentation.Model.EditingScope>, in modo da consentire il rilevamento di più set di modifiche, come parte di un ambito di modifica più esteso, e il controllo individuale.Un scenario in cui può essere utilizzata questa funzionalità si presenta, ad esempio, quando deve essere eseguito il commit di modifiche da più finestre di dialogo, o quando tali modifiche devono essere ripristinate separatamente, e tutte le modifiche vengono considerate come una singola operazione atomica.In questo esempio gli ambiti di modifica vengono organizzati in stack utilizzando un oggetto <xref:System.Collections.ObjectModel.ObservableCollection%601> di tipo <xref:System.Activities.Presentation.Model.ModelEditingScope>.<xref:System.Collections.ObjectModel.ObservableCollection%601> viene utilizzato in modo da poter osservare la profondità dell'annidamento nell'area di progettazione.  
  
## Per impostare, compilare ed eseguire l'esempio  
  
1.  Compilare ed eseguire l'esempio, quindi utilizzare i pulsanti a sinistra per modificare il flusso di lavoro.  
  
2.  Fare clic sull'opzione per l'apertura dell'ambito di modifica.  
  
    1.  Questo comando consente di chiamare <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A> che crea un ambito di modifica e lo inserisce nello stack di modifica.  
  
    2.  Vengono quindi aggiunte tre attività all'oggetto <xref:System.Activities.Presentation.Model.ModelItem> selezionato.Notare che se l'ambito di modifica non è stato aperto con <xref:System.Activities.Presentation.Model.ModelItem.BeginEdit%2A>, le tre nuove attività vengono visualizzate nell'area di disegno della finestra di progettazione.Poiché questa operazione è ancora in sospeso all'interno di <xref:System.Activities.Presentation.Model.EditingScope>, la finestra di progettazione non viene ancora aggiornata.  
  
3.  Fare clic sull'opzione per la chiusura dell'ambito di modifica per eseguirne il commit.Nella finestra di progettazione vengono visualizzate tre attività.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\UsingEditingScope`