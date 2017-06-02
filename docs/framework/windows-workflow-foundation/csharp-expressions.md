---
title: "Espressioni C# | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 29110be7-f4e3-407e-8dbe-78102eb21115
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Espressioni C# #
A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], le espressioni C\# sono supportate in [!INCLUDE[wf](../../../includes/wf-md.md)].I nuovi progetti di flusso di lavoro C\# creati in [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] e destinati a [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] utilizzano le espressioni C\# mentre i progetti di flusso di lavoro di Visual Basic utilizzano le espressioni Visual Basic.I progetti di flusso di lavoro [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] esistenti che utilizzano espressioni Visual Basic possono essere migrati a [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], indipendentemente dal linguaggio del progetto, e sono supportati.In questo argomento viene fornita una panoramica sulle espressioni C\# in [!INCLUDE[wf1](../../../includes/wf1-md.md)].  
  
## Utilizzo delle espressioni C\# nei flussi di lavoro  
  
-   [Utilizzo delle espressioni C# in Progettazione flussi di lavoro](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#WFDesigner)  
  
    -   [Compatibilità con le versioni precedenti](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#BackwardCompat)  
  
-   [Utilizzo delle espressioni C# nei flussi di lavoro di codice](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CodeWorkflows)  
  
-   [Utilizzo delle espressioni C# nei flussi di lavoro XAML](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#XamlWorkflows)  
  
    -   [XAML compilato](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CompiledXaml)  
  
    -   [XAML separato](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#LooseXaml)  
  
-   [Utilizzo delle espressioni C# nei servizi flusso di lavoro XAMLX](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#WFServices)  
  
###  <a name="WFDesigner"></a> Utilizzo delle espressioni C\# in Progettazione flussi di lavoro  
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], le espressioni C\# sono supportate in [!INCLUDE[wf](../../../includes/wf-md.md)].I progetti di flusso di lavoro C\# creati in [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] e destinati a [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] utilizzano le espressioni C\# mentre i progetti di flusso di lavoro di Visual Basic utilizzano le espressioni Visual Basic.Per specificare l'espressione C\# desiderata, digitarla nella casella con l'etichetta **Immetti un'espressione C\#**.Questa etichetta viene visualizzata nella finestra delle proprietà quando l'attività viene selezionata nella finestra di progettazione o sull'attività in Progettazione flussi di lavoro.Nell'esempio seguente, due attività `WriteLine` sono contenute in `Sequence` all'interno di `NoPersistScope`.  
  
 ![Attività Sequence creata automaticamente](../../../docs/framework/windows-workflow-foundation//media/autosurround2.png "AutoSurround2")  
  
> [!NOTE]
>  Le espressioni C\# sono supportate solo in [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] e non sono supportate nella finestra di progettazione del flusso di lavoro ospitata nuovamente.[!INCLUDE[crabout](../../../includes/crabout-md.md)]lle nuove funzionalità WF45 supportate nella finestra di progettazione ospitata nuovamente, vedere [Supporto per nuovo funzionalità di Workflow Foundation 4.5 nella finestra di progettazione del flusso di lavoro ospitata nuovamente](../../../docs/framework/windows-workflow-foundation//wf-features-in-the-rehosted-workflow-designer.md).  
  
####  <a name="BackwardCompat"></a> Compatibilità con le versioni precedenti  
 Sono supportate le espressioni Visual Basic dei progetti di flusso di lavoro C\# di [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] esistenti che sono stati migrati a [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)].Quando le espressioni Visual Basic vengono visualizzate nella finestra di progettazione del flusso di lavoro, il testo dell'espressione Visual Basic esistente viene sostituito con **Valore impostato in XAML**, a meno che l'espressione Visual Basic costituisca una sintassi C\# valida.Se l'espressione Visual Basic è una sintassi C\# valida, l'espressione viene visualizzata.Per aggiornare le espressioni Visual Basic a C\#, è possibile modificarle nella finestra di progettazione del flusso di lavoro e specificare l'espressione C\# equivalente.Non è obbligatorio aggiornare le espressioni Visual Basic a C\#, ma una volta che le espressioni vengono aggiornate nella finestra di progettazione del flusso di lavoro, vengono convertite in C\# e non possono essere ripristinate in Visual Basic.  
  
###  <a name="CodeWorkflows"></a> Utilizzo delle espressioni C\# nei flussi di lavoro di codice  
 Le espressioni C\# sono supportate nei flussi di lavoro basati sul codice di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], ma prima di poter richiamare il flusso di lavoro, le espressioni C\# devono essere compilate utilizzando <xref:System.Activities.XamlIntegration.TextExpressionCompiler.Compile%2A?displayProperty=fullName>.Gli autori di flusso di lavoro possono utilizzare `CSharpValue` per rappresentare l'elemento r\-value di un'espressione e `CSharpReference` per rappresentare l'elemento l\-value di un'espressione.Nell'esempio seguente viene creato un flusso di lavoro costituito da un'attività `Assign` e da un'attività `WriteLine` contenuta in un'attività `Sequence`.`CSharpReference` viene specificato per l'argomento di `To` di `Assign` e rappresenta l'elemento l\-value dell'espressione.`CSharpValue` viene specificato per l'argomento `Value` di `Assign` e per l'argomento `Text` di `WriteLine` e rappresenta l'elemento r\-value delle due espressioni.  
  
```csharp  
Variable<int> n = new Variable<int>  
{  
    Name = "n"  
};  
  
Activity wf = new Sequence  
{  
    Variables = { n },  
    Activities =  
    {  
        new Assign<int>  
        {  
            To = new CSharpReference<int>("n"),  
            Value = new CSharpValue<int>("new Random().Next(1, 101)")  
        },  
        new WriteLine  
        {  
            Text = new CSharpValue<string>("\"The number is \" + n")  
        }  
    }  
};  
  
CompileExpressions(wf);  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 Dopo aver costruito il flusso di lavoro, le espressioni C\# vengono compilate chiamando il metodo di supporto `CompileExpressions`, quindi viene richiamato il flusso di lavoro.Nell'esempio seguente viene indicato il metodo `CompileExpressions`:  
  
```csharp  
static void CompileExpressions(Activity activity)  
{  
    // activityName is the Namespace.Type of the activity that contains the  
    // C# expressions.  
    string activityName = activity.GetType().ToString();  
  
    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name  
    // to represent the new type that represents the compiled expressions.  
    // Take everything after the last . for the type name.  
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";  
    // Take everything before the last . for the namespace.  
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());  
  
    // Create a TextExpressionCompilerSettings.  
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings  
    {  
        Activity = activity,  
        Language = "C#",  
        ActivityName = activityType,  
        ActivityNamespace = activityNamespace,  
        RootNamespace = null,  
        GenerateAsPartialClass = false,  
        AlwaysGenerateSource = true,  
        ForImplementation = false  
    };  
  
    // Compile the C# expression.  
    TextExpressionCompilerResults results =  
        new TextExpressionCompiler(settings).Compile();  
  
    // Any compilation errors are contained in the CompilerMessages.  
    if (results.HasErrors)  
    {  
        throw new Exception("Compilation failed.");  
    }  
  
    // Create an instance of the new compiled expression type.  
    ICompiledExpressionRoot compiledExpressionRoot =  
        Activator.CreateInstance(results.ResultType,  
            new object[] { activity }) as ICompiledExpressionRoot;  
  
    // Attach it to the activity.  
    CompiledExpressionInvoker.SetCompiledExpressionRoot(  
        activity, compiledExpressionRoot);  
}  
```  
  
> [!NOTE]
>  Se le espressioni C\# non vengono compilate, <xref:System.NotSupportedException> viene generato quando il flusso di lavoro viene richiamato con un messaggio simile al seguente: `Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`  
  
 Se il flusso di lavoro basato sul codice personalizzato utilizza `DynamicActivity`, sono richieste alcune modifiche al metodo `CompileExpressions`, come illustrato nell'esempio di codice riportato di seguito.  
  
```csharp  
static void CompileExpressions(DynamicActivity dynamicActivity)  
{  
    // activityName is the Namespace.Type of the activity that contains the  
    // C# expressions. For Dynamic Activities this can be retrieved using the  
    // name property , which must be in the form Namespace.Type.  
    string activityName = dynamicActivity.Name;  
  
    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name  
    // to represent the new type that represents the compiled expressions.  
    // Take everything after the last . for the type name.  
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";  
    // Take everything before the last . for the namespace.  
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());  
  
    // Create a TextExpressionCompilerSettings.  
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings  
    {  
        Activity = dynamicActivity,  
        Language = "C#",  
        ActivityName = activityType,  
        ActivityNamespace = activityNamespace,  
        RootNamespace = null,  
        GenerateAsPartialClass = false,  
        AlwaysGenerateSource = true,  
        ForImplementation = true  
    };  
  
    // Compile the C# expression.  
    TextExpressionCompilerResults results =  
        new TextExpressionCompiler(settings).Compile();  
  
    // Any compilation errors are contained in the CompilerMessages.  
    if (results.HasErrors)  
    {  
        throw new Exception("Compilation failed.");  
    }  
  
    // Create an instance of the new compiled expression type.  
    ICompiledExpressionRoot compiledExpressionRoot =  
        Activator.CreateInstance(results.ResultType,  
            new object[] { dynamicActivity }) as ICompiledExpressionRoot;  
  
    // Attach it to the activity.  
    CompiledExpressionInvoker.SetCompiledExpressionRootForImplementation(  
        dynamicActivity, compiledExpressionRoot);  
}  
```  
  
 Esistono numerose differenze nell'overload di `CompileExpressions` che compila le espressioni C\# in un'attività dinamica.  
  
-   Il parametro per `CompileExpressions` è `DynamicActivity`.  
  
-   Il nome del tipo e lo spazio dei nomi vengono recuperati utilizzando la proprietà `DynamicActivity.Name`.  
  
-   `TextExpressionCompilerSettings.ForImplementation` è impostato su `true`.  
  
-   `CompiledExpressionInvoker.SetCompiledExpressionRootForImplementation` viene chiamato al posto di `CompiledExpressionInvoker.SetCompiledExpressionRoot`.  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]ll'utilizzo di espressioni nel codice, vedere [Creazione di flussi di lavoro, attività ed espressioni tramite codice imperativo](../../../docs/framework/windows-workflow-foundation//authoring-workflows-activities-and-expressions-using-imperative-code.md).  
  
###  <a name="XamlWorkflows"></a> Utilizzo delle espressioni C\# nei flussi di lavoro XAML  
 Le espressioni C\# sono supportate nei flussi di lavoro XAML.I flussi di lavoro XAML compilato vengono compilati in un tipo e i flussi di lavoro XAML separato vengono caricati dal runtime e compilati in un albero di attività quando il flusso di lavoro viene eseguito.  
  
-   [XAML compilato](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CompiledXaml)  
  
-   [XAML separato](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#LooseXaml)  
  
####  <a name="CompiledXaml"></a> XAML compilato  
 Le espressioni C\# sono supportate nei flussi di lavoro XAML compilato che vengono compilati in un tipo come parte di un progetto di flusso di lavoro C\# destinato a [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)].XAML compilato è il tipo di creazione predefinito dei flussi di lavoro in [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] e i progetti di flusso di lavoro C\# creati in [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] destinati a [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] utilizzano espressioni C\#.  
  
####  <a name="LooseXaml"></a> XAML separato  
 Le espressioni C\# sono supportate nei flussi di lavoro XAML separato.Il programma host del flusso di lavoro che carica e richiama il flusso di lavoro XAML separato deve essere destinato a [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] e <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> deve essere impostato su `true` \(l'impostazione predefinita è `false`\).Per impostare <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> su `true`, creare un'istanza di <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings> con la relativa proprietà <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> impostata su `true` e passarla come parametro a <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A?displayProperty=fullName>.Se `CompileExpressions` non è impostato su `true`, <xref:System.NotSupportedException> verrà generato con un messaggio simile al seguente: `Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`  
  
```csharp  
ActivityXamlServicesSettings settings = new ActivityXamlServicesSettings  
{  
    CompileExpressions = true  
};  
  
DynamicActivity<int> wf = ActivityXamlServices.Load(new StringReader(serializedAB), settings) as DynamicActivity<int>;  
```  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]ll'utilizzo dei flussi di lavoro XAML, vedere [Serializzazione di flussi di lavoro e attività da e verso XAML](../../../docs/framework/windows-workflow-foundation//serializing-workflows-and-activities-to-and-from-xaml.md).  
  
###  <a name="WFServices"></a> Utilizzo delle espressioni C\# nei servizi flusso di lavoro XAMLX  
 Le espressioni C\# sono supporte nei servizi flusso di lavoro XAMLX.Quando un servizio flusso di lavoro è ospitato in IIS o WAS non sono necessarie ulteriori attività, ma se il servizio flusso di lavoro XAML è indipendente, è necessario compilare le espressioni C\#.Per compilare le espressioni C\# in un servizio flusso di lavoro XAMLX indipendente, innanzitutto caricare il file XAMLX in `WorkflowService` e passare l'elemento `Body` di `WorkflowService` al metodo `CompileExpressions` descritto nella sezione precedente [Utilizzo delle espressioni C# nei flussi di lavoro di codice](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CodeWorkflows).Nell'esempio seguente, viene caricato un servizio flusso di lavoro XAMLX, vengono compilate espressioni C\# e quindi viene aperto il servizio flusso di lavoro in attesa di richieste.  
  
```csharp  
// Load the XAMLX workflow service.  
WorkflowService workflow1 =  
    (WorkflowService)XamlServices.Load(xamlxPath);  
  
// Compile the C# expressions in the workflow by passing the Body to CompileExpressions.  
CompileExpressions(workflow1.Body);  
  
// Initialize the WorkflowServiceHost.  
var host = new WorkflowServiceHost(workflow1, new Uri("http://localhost:8293/Service1.xamlx"));  
  
// Enable Metadata publishing/  
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
smb.HttpGetEnabled = true;  
smb.MetadataExporter.PolicyVersion = PolicyVersion.Policy15;  
host.Description.Behaviors.Add(smb);  
  
// Open the WorkflowServiceHost and wait for requests.  
host.Open();  
Console.WriteLine("Press enter to quit");  
Console.ReadLine();  
```  
  
 Se le espressioni C\# non sono compilate, l'operazione `Open` viene eseguita, ma il flusso di lavoro non verrà richiamato.Il metodo `CompileExpressions` riportato di seguito corrisponde al metodo della sezione precedente [Utilizzo delle espressioni C# nei flussi di lavoro di codice](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md#CodeWorkflows).  
  
```csharp  
static void CompileExpressions(Activity activity)  
{  
    // activityName is the Namespace.Type of the activity that contains the  
    // C# expressions.  
    string activityName = activity.GetType().ToString();  
  
    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name  
    // to represent the new type that represents the compiled expressions.  
    // Take everything after the last . for the type name.  
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";  
    // Take everything before the last . for the namespace.  
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());  
  
    // Create a TextExpressionCompilerSettings.  
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings  
    {  
        Activity = activity,  
        Language = "C#",  
        ActivityName = activityType,  
        ActivityNamespace = activityNamespace,  
        RootNamespace = null,  
        GenerateAsPartialClass = false,  
        AlwaysGenerateSource = true,  
        ForImplementation = false  
    };  
  
    // Compile the C# expression.  
    TextExpressionCompilerResults results =  
        new TextExpressionCompiler(settings).Compile();  
  
    // Any compilation errors are contained in the CompilerMessages.  
    if (results.HasErrors)  
    {  
        throw new Exception("Compilation failed.");  
    }  
  
    // Create an instance of the new compiled expression type.  
    ICompiledExpressionRoot compiledExpressionRoot =  
        Activator.CreateInstance(results.ResultType,  
            new object[] { activity }) as ICompiledExpressionRoot;  
  
    // Attach it to the activity.  
    CompiledExpressionInvoker.SetCompiledExpressionRoot(  
        activity, compiledExpressionRoot);  
}  
```