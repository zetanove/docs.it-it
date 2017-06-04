---
title: "Aggiornamento dinamico | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b6ef19b-9691-4b4b-824c-3c651a9db96e
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Aggiornamento dinamico
L'aggiornamento dinamico fornisce agli sviluppatori di applicazioni del flusso di lavoro un meccanismo per aggiornare la definizione del flusso di lavoro di un'istanza persistente del flusso di lavoro.  Può servire a implementare una correzione di bug, nuovi requisiti o per implementare modifiche impreviste.  In questo argomento viene fornita una panoramica sulla funzionalità di aggiornamento dinamico introdotta in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  
  
## Aggiornamento dinamico  
 Per applicare gli aggiornamenti dinamici a un'istanza persistente del flusso di lavoro, viene creato un oggetto <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> contenente le istruzioni per il runtime che spiegano come modificare tale istanza in modo da riflettere le modifiche desiderate.  Una volta creata, la mappa di aggiornamento viene applicata alle istanze persistenti del flusso di lavoro desiderate.  Dopo che è stato applicato l'aggiornamento dinamico, le istanze di flusso di lavoro possono essere riprese usando la nuova definizione aggiornata del flusso di lavoro.  Per la creazione e l'applicazione di una mappa di aggiornamento sono richiesti quattro passaggi.  
  
1.  [Preparare la definizione del flusso di lavoro per l'aggiornamento dinamico.](../../../docs/framework/windows-workflow-foundation//dynamic-update.md#Prepare)  
  
2.  [Aggiornare la definizione del flusso di lavoro in modo da riflettere le modifiche desiderate.](../../../docs/framework/windows-workflow-foundation//dynamic-update.md#Update)  
  
3.  [Creare la mappa di aggiornamento.](../../../docs/framework/windows-workflow-foundation//dynamic-update.md#Create)  
  
4.  [Applicare la mappa di aggiornamento alle istanze persistenti del flusso di lavoro desiderate.](../../../docs/framework/windows-workflow-foundation//dynamic-update.md#Apply)  
  
> [!NOTE]
>  Si noti che i passaggi da 1 a 3, relativi alla creazione della mappa di aggiornamento, possono essere eseguiti indipendentemente dal fatto che l'aggiornamento venga poi applicato o meno.  In uno scenario comune, lo sviluppatore del flusso di lavoro crea la mappa di aggiornamento offline e un amministratore applica l'aggiornamento in un secondo momento.  
  
 In questo argomento viene fornita una panoramica sul processo di aggiornamento dinamico per l'aggiunta di una nuova attività a un'istanza persistente di un flusso di lavoro XAML compilato.  
  
###  <a name="Prepare"></a> Preparare la definizione del flusso di lavoro per l'aggiornamento dinamico.  
 Il primo passaggio nel processo di aggiornamento dinamico consiste nel preparare all'aggiornamento la definizione del flusso di lavoro desiderata.  Questa operazione viene eseguita chiamando il metodo <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=fullName> e passando la definizione del flusso di lavoro per la modifica.  Questo metodo convalida e successivamente analizza l'albero del flusso di lavoro per identificare tutti gli oggetti, quali le variabili e le attività pubbliche che devono essere contrassegnate in modo da poter essere confrontate in un secondo momento con la definizione del flusso di lavoro modificata.  Al termine, l'albero del flusso di lavoro viene duplicato e collegato alla definizione del flusso di lavoro originale.  Quando viene creata la mappa di aggiornamento, la versione aggiornata della definizione del flusso di lavoro viene confrontata con la definizione del flusso di lavoro originale. Sulla base delle differenze viene generata la mappa di aggiornamento.  
  
 Ai fini della preparazione per l'aggiornamento dinamico, un flusso di lavoro XAML può essere caricato in un oggetto <xref:System.Activities.ActivityBuilder>. L'oggetto <xref:System.Activities.ActivityBuilder> verrà quindi passato a <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=fullName>.  
  
> [!NOTE]
>  Per altre informazioni sull'utilizzo di flussi di lavoro serializzati e di <xref:System.Activities.ActivityBuilder>, vedere [Serializzazione di flussi di lavoro e attività da e verso XAML](../../../docs/framework/windows-workflow-foundation//serializing-workflows-and-activities-to-and-from-xaml.md).  
  
 Nell'esempio riportato di seguito, una definizione di `MortgageWorkflow` \(costituita da un oggetto <xref:System.Activities.Statements.Sequence> con varie attività figlio\) viene caricata in un oggetto <xref:System.Activities.ActivityBuilder> e successivamente preparata per l'aggiornamento dinamico.  Una volta completato il metodo, <xref:System.Activities.ActivityBuilder> contiene la definizione del flusso di lavoro originale nonché una copia.  
  
```csharp  
// Load the MortgageWorkflow definition from Xaml into  
// an ActivityBuilder.  
XamlXmlReaderSettings readerSettings = new XamlXmlReaderSettings()  
{  
    LocalAssembly = Assembly.GetExecutingAssembly()  
};  
  
XamlXmlReader xamlReader = new XamlXmlReader(@"C:\WorkflowDefitinions\MortgageWorkflow.xaml",   
    readerSettings);  
  
ActivityBuilder ab = XamlServices.Load(  
    ActivityXamlServices.CreateBuilderReader(xamlReader)) as ActivityBuilder;  
  
// Prepare the workflow definition for dynamic update.  
DynamicUpdateServices.PrepareForUpdate(ab);  
```  
  
> [!NOTE]
>  Per scaricare il codice di esempio che accompagna questo argomento, vedere [Codice di esempio di aggiornamento dinamico \(le informazioni potrebbero essere in inglese\)](http://go.microsoft.com/fwlink/?LinkId=227905).  
  
###  <a name="Update"></a> Aggiornare la definizione del flusso di lavoro in modo da riflettere le modifiche desiderate.  
 Una volta che la definizione del flusso di lavoro è stata preparata per l'aggiornamento, è possibile apportare le modifiche desiderate.  È possibile aggiungere o rimuovere attività, aggiungere, spostare o eliminare variabili pubbliche, aggiungere o rimuovere argomenti e apportare modifiche alla firma dei delegati dell'attività.  Non è possibile rimuovere un'attività in esecuzione o modificare la firma di un delegato in esecuzione.  Tali modifiche possono essere eseguite usando il codice o in una finestra di progettazione del flusso di lavoro rieseguita nell'host.  Nell'esempio riportato di seguito viene aggiunta un'attività `VerifyAppraisal` personalizzata alla sequenza che costituisce il corpo dell'oggetto `MortgageWorkflow` usato nell'esempio precedente.  
  
```csharp  
// Make desired changes to the definition. In this example, we are  
// inserting a new VerifyAppraisal activity as the 3rd child of the root Sequence.  
VerifyAppraisal va = new VerifyAppraisal  
{  
    Result = new VisualBasicReference<bool>("LoanCriteria")  
};  
  
// Get the Sequence that makes up the body of the workflow.  
Sequence s = ab.Implementation as Sequence;  
  
// Insert the new activity into the Sequence.  
s.Activities.Insert(2, va);  
```  
  
###  <a name="Create"></a> Creare la mappa di aggiornamento.  
 Una volta che la definizione del flusso di lavoro preparata per l'aggiornamento è stata modificata, è possibile creare la mappa di aggiornamento.  Per creare una mappa di aggiornamento dinamico, viene richiamato il metodo <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=fullName>.  Il metodo restituisce un oggetto <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> contenente le informazioni necessarie al runtime per modificare un'istanza persistente del flusso di lavoro in modo che possa essere caricata e ripresa con la nuova definizione del flusso di lavoro.  Nell'esempio riportato di seguito, viene creata una mappa di aggiornamento per la definizione di `MortgageWorkflow` modificata usata nell'esempio precedente.  
  
```csharp  
// Create the update map.  
DynamicUpdateMap map = DynamicUpdateServices.CreateUpdateMap(ab);  
```  
  
 Questa mappa di aggiornamento può essere immediatamente usata per modificare le istanze persistenti del flusso di lavoro o, come accade più spesso, può essere salvata e gli aggiornamenti possono essere applicati in un secondo momento.  Un modo per salvare la mappa di aggiornamento consiste nel serializzarla in un file, come illustrato nell'esempio seguente.  
  
```csharp  
// Serialize the update map to a file.  
DataContractSerializer serializer = new DataContractSerializer(typeof(DynamicUpdateMap));  
using (FileStream fs = System.IO.File.Open(@"C:\WorkflowDefitinions\MortgageWorkflow.map", FileMode.Create))  
{  
    serializer.WriteObject(fs, map);  
}  
```  
  
 Al termine del metodo <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=fullName>, la definizione duplicata del flusso di lavoro e altre informazioni relative all'aggiornamento dinamico aggiunte nella chiamata al metodo <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=fullName> vengono rimosse e la definizione modificata del flusso di lavoro è pronta per essere salvata per poter essere usata in un secondo momento quando le istanze aggiornate del flusso di lavoro vengono riprese.  Nell'esempio riportato di seguito la definizione modificata del flusso di lavoro viene salvata in `MortgageWorkflow_v2.xaml`.  
  
```csharp  
// Save the modified workflow definition.  
StreamWriter sw = File.CreateText(@"C:\WorkflowDefitinions\MortgageWorkflow_v1.1.xaml");  
XamlWriter xw = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(sw, new XamlSchemaContext()));  
XamlServices.Save(xw, ab);  
sw.Close();  
```  
  
###  <a name="Apply"></a> Applicare la mappa di aggiornamento alle istanze persistenti del flusso di lavoro desiderate.  
 Una volta creata, la mappa di aggiornamento può essere applicata in qualsiasi momento.  Può essere applicata subito usando l'istanza <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> restituita dal metodo <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=fullName> oppure in secondo momento usando una copia salvata.  Per aggiornare un'istanza del flusso di lavoro, caricarla in <xref:System.Activities.WorkflowApplicationInstance> usando <xref:System.Activities.WorkflowApplication.GetInstance%2A?displayProperty=fullName>.  Creare quindi un elemento <xref:System.Activities.WorkflowApplication> usando la definizione aggiornata del flusso di lavoro, quindi l'elemento <xref:System.Activities.WorkflowIdentity> desiderato.  Questo oggetto <xref:System.Activities.WorkflowIdentity> può essere diverso da quello usato per rendere persistente il flusso di lavoro originale e in genere è diverso in modo da indicare che l'istanza persistente è stata modificata.  Una volta creato l'oggetto <xref:System.Activities.WorkflowApplication>, viene caricato usando l'overload di <xref:System.Activities.WorkflowApplication.Load%2A?displayProperty=fullName> che accetta un oggetto <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> quindi viene scaricato tramite una chiamata a <xref:System.Activities.WorkflowApplication.Unload%2A?displayProperty=fullName>.  In questo modo viene applicato l'aggiornamento dinamico e resa persistente l'istanza aggiornata del flusso di lavoro.  
  
```csharp  
// Load the serialized update map.  
DynamicUpdateMap map;  
using (FileStream fs = File.Open(@"C:\WorkflowDefitinions\MortgageWorkflow.map", FileMode.Open))  
{  
    DataContractSerializer serializer = new DataContractSerializer(typeof(DynamicUpdateMap));  
    object updateMap = serializer.ReadObject(fs);  
    if (updateMap == null)  
    {  
        throw new ApplicationException("DynamicUpdateMap is null.");  
    }  
  
    map = (DynamicUpdateMap)updateMap;  
}  
  
// Retrieve a list of workflow instance ids that corresponds to the  
// workflow instances to update. This step is the responsibility of  
// the application developer.  
List<Guid> ids = GetPersistedWorkflowIds();  
foreach (Guid id in ids)  
{  
    // Get a proxy to the persisted workflow instance.  
    SqlWorkflowInstanceStore store = new SqlWorkflowInstanceStore(connectionString);  
    WorkflowApplicationInstance instance = WorkflowApplication.GetInstance(id, store);  
  
    // If desired, you can inspect the WorkflowIdentity of the instance  
    // using the DefinitionIdentity property to determine whether to apply  
    // the update.  
    Console.WriteLine(instance.DefinitionIdentity);  
  
    // Create a workflow application. You must specify the updated workflow definition, and  
    // you may provide an updated WorkflowIdentity if desired to reflect the update.  
    WorkflowIdentity identity = new WorkflowIdentity  
    {  
        Name = "MortgageWorkflow v1.1",  
        Version = new Version(1, 1, 0, 0)  
    };  
  
    // Load the persisted workflow instance using the updated workflow definition  
    // and with an updated WorkflowIdentity. In this example the MortgageWorkflow class  
    // contains the updated definition.  
    WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);  
  
    // Apply the dynamic update on the loaded instance.                
    wfApp.Load(instance, map);  
  
    // Unload the updated instance.  
    wfApp.Unload();  
}  
```  
  
### Ripresa di un'istanza aggiornata del flusso di lavoro  
 Una volta applicato l'aggiornamento dinamico, è possibile riprendere l'istanza del flusso di lavoro.  Si noti che è necessario usare la nuova definizione aggiornata e l'oggetto <xref:System.Activities.WorkflowIdentity>.  
  
> [!NOTE]
>  Per altre informazioni sull'utilizzo di <xref:System.Activities.WorkflowApplication> e <xref:System.Activities.WorkflowIdentity>, vedere [Utilizzo di WorkflowIdentity e controllo delle versioni](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md).  
  
 Nell'esempio riportato di seguito, il flusso di lavoro `MortgageWorkflow_v1.1.xaml` dell'esempio precedente è stato compilato e viene caricato e ripreso usando la definizione aggiornata del flusso di lavoro.  
  
```csharp  
// Load the persisted workflow instance using the updated workflow definition  
// and updated WorkflowIdentity.  
WorkflowIdentity identity = new WorkflowIdentity  
{  
    Name = "MortgageWorkflow v1.1",  
    Version = new Version(1, 1, 0, 0)  
};  
  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);  
  
// Configure persistence and desired workflow event handlers.  
// (Omitted for brevity.)  
ConfigureWorkflowApplication(wfApp);  
  
// Load the persisted workflow instance.  
wfApp.Load(InstanceId);  
  
// Resume the workflow.  
// wfApp.ResumeBookmark(...);  
```  
  
> [!NOTE]
>  Per scaricare il codice di esempio che accompagna questo argomento, vedere [Codice di esempio di aggiornamento dinamico \(le informazioni potrebbero essere in inglese\)](http://go.microsoft.com/fwlink/?LinkId=227905).