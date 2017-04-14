---
title: "Ispezione dell&#39;albero delle attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 100d00e4-8c1d-4233-8fbb-dd443a01155d
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Ispezione dell&#39;albero delle attivit&#224;
L'ispezione della struttura ad albero delle attività viene utilizzata dagli autori dell'applicazione flusso di lavoro per controllare i flussi di lavoro ospitati dall'applicazione.Tramite l'oggetto <xref:System.Activities.WorkflowInspectionServices>, nei flussi di lavoro è possibile cercare attività figlio specifiche, enumerare attività singole e le relative proprietà, nonché memorizzare nella cache i metadati di runtime delle attività in un momento specifico.In questo argomento viene fornita una panoramica sull'oggetto <xref:System.Activities.WorkflowInspectionServices> e viene descritto come utilizzarlo per controllare una struttura ad albero delle attività.  
  
## Utilizzo dell'oggetto WorkflowInspectionServices  
 Il metodo <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> viene utilizzato per enumerare tutte le attività nell'albero delle attività specificato.<xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> restituisce un enumerabile che tocca tutte le attività all'interno dell'albero, inclusi gli elementi figlio, i gestori delegato, le impostazioni predefinite variabili e le espressioni argomento.Nell'esempio seguente viene creata una definizione di flusso di lavoro tramite gli oggetti <xref:System.Activities.Statements.Sequence>, <xref:System.Activities.Statements.While>, <xref:System.Activities.Statements.ForEach%601>, <xref:System.Activities.Statements.WriteLine> e le espressioni.Una volta creata, la definizione di flusso di lavoro viene richiamata, quindi viene chiamato il metodo `InspectActivity`.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#45](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#45)]  
  
 Per enumerare le attività, viene chiamato  <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> nell'attività radice e di nuovo in modo ricorsivo in ogni attività restituita.Nell'esempio seguente la proprietà <xref:System.Activities.Activity.DisplayName%2A> di ogni attività ed espressione della struttura ad albero delle attività viene scritta nella console.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#46](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#46)]  
  
 Questo codice di esempio fornisce l'output seguente.  
  
 **Voce elenco 1**   
**Voce elenco 2**   
**Voce elenco 3**   
**Voce elenco 4**   
**Voce elenco 5**   
**Elementi aggiunti alla raccolta.**   
**Sequenza**   
 **Literal\<List\<String\>\>**   
 **While**   
 **AddToCollection\<String\>**   
 **VariableValue\<ICollection\<String\>\>**   
 **LambdaValue\<String\>**   
 **LocationReferenceValue\<List\<String\>\>**   
 **LambdaValue\<Boolean\>**   
 **LocationReferenceValue\<List\<String\>\>**   
 **ForEach\<String\>**   
 **VariableValue\<IEnumerable\<String\>\>**   
 **WriteLine**   
 **DelegateArgumentValue\<String\>**   
 **Sequenza**   
 **WriteLine**   
 **Literal\<String\>**  Per recuperare un'attività specifica anziché enumerare tutte le attività, viene utilizzato il metodo <xref:System.Activities.WorkflowInspectionServices.Resolve%2A>.Entrambi i metodi <xref:System.Activities.WorkflowInspectionServices.Resolve%2A> e <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> eseguono la memorizzazione dei metadati nella cache se non è stato precedentemente chiamato l'oggetto `WorkflowInspectionServices.CacheMetadata`.Se il metodo <xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A> è stato chiamato, il metodo <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> si basa sui metadati esistenti.Pertanto, se sono state apportate modifiche alla struttura ad albero dall'ultima chiamata al metodo <xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A>, il metodo <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> potrebbe fornire risultati imprevisti.Se sono state apportate modifiche al flusso di lavoro dopo avere chiamato <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A>, è possibile memorizzare di nuovo i metadati nella cache chiamando il metodo <xref:System.Activities.Validation.ActivityValidationServices><xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>.La memorizzazione dei metadati nella cache è descritta nella prossima sezione.  
  
### Memorizzazione dei metadati nella cache  
 La memorizzazione dei metadati nella cache per un'attività compila e convalida una descrizione degli argomenti dell'attività, delle variabili, delle attività figlio e dei delegati di attività.Per impostazione predefinita, i metadati vengono memorizzati nella cache dal runtime quando un'attività viene preparata per l'esecuzione.Se un autore dell'host del flusso di lavoro desidera memorizzare i metadati nella cache per un'attività o una struttura ad albero delle attività prima di questa fase, ad esempio per accettare in anticipo tutto il costo, è possibile utilizzare il metodo <xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A> per memorizzare i metadati nella cache nel momento desiderato.