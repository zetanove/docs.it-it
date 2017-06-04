---
title: "Serializzazione di flussi di lavoro e attivit&#224; da e verso XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37685b32-24e3-4d72-88d8-45d5fcc49ec2
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Serializzazione di flussi di lavoro e attivit&#224; da e verso XAML
Oltre alla compilazione in tipi contenuti in assembly, le definizioni di flusso di lavoro possono essere serializzate anche in XAML.Queste definizioni serializzate possono essere ricaricate per la modifica o l'ispezione, passate a un sistema di compilazione per la compilazione o caricate e richiamate.In questo argomento viene fornita una panoramica della serializzazione di definizioni del flusso di lavoro e dell'utilizzo di definizioni del flusso di lavoro XAML.  
  
## Utilizzo di definizioni del flusso di lavoro XAML  
 Per creare una definizione di flusso di lavoro per la serializzazione, viene utilizzata la classe <xref:System.Activities.ActivityBuilder>.La creazione di un oggetto <xref:System.Activities.ActivityBuilder> è molto simile alla creazione di <xref:System.Activities.DynamicActivity>.Vengono specificati gli argomenti desiderati e vengono configurate le attività che costituiscono il comportamento.Nell'esempio seguente viene creata un'attività `Add` che accetta due argomenti di input, li somma e restituisce il risultato.Poiché questa attività restituisce un risultato, viene utilizzata la classe <xref:System.Activities.ActivityBuilder%601> generica.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#41](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#41)]  
  
 Ognuna delle istanze di <xref:System.Activities.DynamicActivityProperty> rappresenta uno degli argomenti di input per il flusso di lavoro e <xref:System.Activities.ActivityBuilder.Implementation%2A> contiene le attività che costituiscono la logica del flusso di lavoro.Si noti che le espressioni r\-value in questo esempio sono espressioni di Visual Basic.Le espressioni lambda non sono serializzabili nel formato XAML a meno che non si utilizzi <xref:System.Activities.Expressions.ExpressionServices.Convert%2A>.Se i flussi di lavoro serializzati sono progettati per essere aperti o modificati nella finestra di progettazione del flusso di lavoro, dovranno essere utilizzate le espressioni di Visual Basic.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Creazione di flussi di lavoro, attività ed espressioni tramite codice imperativo](../../../docs/framework/windows-workflow-foundation//authoring-workflows-activities-and-expressions-using-imperative-code.md).  
  
 Per serializzare la definizione del flusso di lavoro rappresentata dall'istanza di <xref:System.Activities.ActivityBuilder> in XAML, utilizzare <xref:System.Activities.XamlIntegration.ActivityXamlServices> per creare un oggetto <xref:System.Xaml.XamlWriter>, quindi utilizzare <xref:System.Xaml.XamlServices> per serializzare la definizione del flusso di lavoro tramite <xref:System.Xaml.XamlWriter>.<xref:System.Activities.XamlIntegration.ActivityXamlServices> contiene metodi per eseguire il mapping delle istanze di <xref:System.Activities.ActivityBuilder> in e da XAML e per caricare i flussi di lavoro XAML e restituire un oggetto <xref:System.Activities.DynamicActivity> che può essere richiamato.Nell'esempio seguente l'istanza di <xref:System.Activities.ActivityBuilder> dall'esempio precedente viene serializzata in una stringa e inoltre salvata in un file.  
  
```csharp  
// Serialize the workflow to XAML and store it in a string.  
StringBuilder sb = new StringBuilder();  
StringWriter tw = new StringWriter(sb);  
XamlWriter xw = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(tw, new XamlSchemaContext()));  
XamlServices.Save(xw , ab);  
string serializedAB = sb.ToString();  
  
// Display the XAML to the console.  
Console.WriteLine(serializedAB);  
  
// Serialize the workflow to XAML and save it to a file.  
StreamWriter sw = File.CreateText(@"C:\Workflows\add.xaml");  
XamlWriter xw2 = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(sw, new XamlSchemaContext()));  
XamlServices.Save(xw2, ab);  
sw.Close();  
  
```  
  
 L'esempio seguente rappresenta il flusso di lavoro serializzato.  
  
```xaml  
<Activity   
  x:TypeArguments="x:Int32"   
  x:Class="Add"   
  xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"   
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <x:Members>  
    <x:Property Name="Operand1" Type="InArgument(x:Int32)" />  
    <x:Property Name="Operand2" Type="InArgument(x:Int32)" />  
  </x:Members>  
  <Sequence>  
    <WriteLine Text="[Operand1.ToString() + " + " + Operand2.ToString()]" />  
    <Assign x:TypeArguments="x:Int32" Value="[Operand1 + Operand2]">  
      <Assign.To>  
        <OutArgument x:TypeArguments="x:Int32">  
          <ArgumentReference x:TypeArguments="x:Int32" ArgumentName="Result" />  
          </OutArgument>  
      </Assign.To>  
    </Assign>  
  </Sequence>  
</Activity>  
```  
  
 Per caricare un flusso di lavoro serializzato, viene utilizzato il metodo <xref:System.Activities.XamlIntegration.ActivityXamlServices><xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A>,che accetta la definizione di flusso di lavoro serializzata e restituisce un oggetto <xref:System.Activities.DynamicActivity> che rappresenta la definizione di flusso di lavoro.Notare che XAML non viene deserializzato fino a che <xref:System.Activities.Activity.CacheMetadata%2A> non viene chiamato nel corpo di <xref:System.Activities.DynamicActivity> durante il processo di convalida.Se la convalida non viene chiamata in modo esplicito, viene quindi eseguita quando viene richiamato il flusso di lavoro.Se la definizione di flusso di lavoro XAML non è valida, verrà generata un'eccezione <xref:System.Argument>.Qualsiasi eccezione generata da <xref:System.Activities.Activity.CacheMetadata%2A> utilizza caratteri di escape dalla chiamata a <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> e deve essere gestite dal chiamante.Nell'esempio seguente il flusso di lavoro serializzato dall'esempio precedente viene caricato e richiamato tramite <xref:System.Activities.WorkflowInvoker>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#43](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#43)]  
  
 Quando questo flusso di lavoro viene richiamato, l'output seguente viene visualizzato nella console.  
  
 **25 \+ 15**   
**40**    
> [!NOTE]
>  [!INCLUDE[crabout](../../../includes/crabout-md.md)] modalità per richiamare flussi di lavoro con argomenti di input e output, vedere [Utilizzo di WorkflowInvoker e WorkflowApplication](../../../docs/framework/windows-workflow-foundation//using-workflowinvoker-and-workflowapplication.md) e <xref:System.Activities.WorkflowInvoker.Invoke%2A>.  
  
 Se il flusso di lavoro serializzato contiene le espressioni di C\#, un'istanza di <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings> con la relativa proprietà <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> impostata su `true` deve essere passata come parametro a <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A?displayProperty=fullName>; in caso contrario, verrà generata un'eccezione <xref:System.NotSupportedException> con un messaggio simile al seguente: `Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`  
  
```csharp  
ActivityXamlServicesSettings settings = new ActivityXamlServicesSettings  
{  
    CompileExpressions = true  
};  
  
DynamicActivity<int> wf = ActivityXamlServices.Load(new StringReader(serializedAB), settings) as DynamicActivity<int>;  
  
```  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Espressioni C\#](../../../docs/framework/windows-workflow-foundation//csharp-expressions.md).  
  
 Una definizione di flusso di lavoro serializzata può essere caricata anche in un'istanza di <xref:System.Activities.ActivityBuilder> tramite il metodo <xref:System.Activities.XamlIntegration.ActivityXamlServices><xref:System.Activities.XamlIntegration.ActivityXamlServices.CreateBuilderReader%2A>.Una volte che un flusso di lavoro serializzato è stato caricato in un'istanza di <xref:System.Activities.ActivityBuilder>, può essere controllato e modificato.Ciò si rivela utile per gli autori di finestre di progettazione flussi di lavoro personalizzati crea e fornisce un meccanismo per salvare e ricaricare definizioni di flusso di lavoro durante il processo di progettazione.Nell'esempio seguente la definizione di flusso di lavoro serializzato dall'esempio precedente viene caricata e le relative proprietà vengono controllate.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#44](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#44)]