---
title: "Attivit&#224; ExternalizedPolicy in .NET Framework 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92fd6f92-23a1-4adf-b96a-2754ea93ad3e
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Attivit&#224; ExternalizedPolicy in .NET Framework 4.5
In questo esempio viene illustrato il modo in cui l'attività ExternalizedPolicy4 consente di eseguire gli oggetti <xref:System.Workflow.Activities.Rules.RuleSet> esistenti di [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] [!INCLUDE[wf2](../../../../includes/wf2-md.md)] \(WF 3.5\) in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] [!INCLUDE[wf2](../../../../includes/wf2-md.md)] \(WF 4.5\) direttamente tramite il motore per le regole fornito in WF 3.5.Utilizzando questa attività, è possibile aprire ed eseguire un oggetto <xref:System.Workflow.Activities.Rules.RuleSet> esistente di WF 3.5.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]l motore per le regole di WF 3.5, incluso in Windows Workflow Foundation, vedere [Introduzione al motore per le regole di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=166079).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] le regole di migrazione a [!INCLUDE[wf1](../../../../includes/wf1-md.md)] in [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)], leggere le istruzioni di migrazione in [Istruzioni di migrazione](../../../../docs/framework/windows-workflow-foundation//migration-guidance.md).  
  
## Progetti di questo esempio  
  
||||  
|-|-|-|  
|Nome progetto|Descrizione|File principali|  
|ExternalizedPolicy4|Contiene l'attività ExternalizedPolicy4 e la relativa finestra di progettazione di WF 4.5.|**ExternalizedPolicy4.cs**: definizione dell'attività.<br /><br /> **ExternalizedPolicy4Designer.xaml**: finestra di progettazione personalizzata per l'attività ExternalizedPolicy4.Utilizza l'editor delle regole \(<xref:System.Workflow.Activities.Rules.Design.RuleSetDialog>\) dal motore per le regole di WF 3.5.|  
|ImperativeCodeClientSample|Applicazione client di esempio che configura ed esegue un flusso di lavoro tramite un'applicazione ExternalizedPolicy4 e il codice C\# imperativo \(non viene utilizzata alcuna finestra di progettazione\).|**ApplyDiscount.rules**: file con definizioni delle regole di [!INCLUDE[wf1](../../../../includes/wf1-md.md)].<br /><br /> **Order.cs**: tipo che rappresenta un ordine del cliente.Le regole vengono applicate agli oggetti di questo tipo.<br /><br /> **Program.cs**: configura ed esegue un flusso di lavoro che dispone di un'attività Policy4 per applicare le regole definite in ApplyDiscount.rules alle istanze di oggetti Order.<br /><br /> App.config: file di configurazione con il percorso del file delle regole.|  
|DesignerClientSample|Applicazione client di esempio che configura ed esegue un flusso di lavoro tramite un'applicazione ExternalPolicy4 nella finestra di progettazione di [!INCLUDE[wf1](../../../../includes/wf1-md.md)].|**Sequence1.xaml**: flusso di lavoro sequenziale che utilizza un'attività Policy4 per eseguire valutazioni delle regole.<br /><br /> **Program.cs**: esegue un'istanza del flusso di lavoro definito in Sequence1.xaml.|  
  
## Attività ExternalizedPolicy4  
 L'attività ExternalizedPolicy4 è un oggetto <xref:System.Activities.NativeActivity> che consente l'esecuzione degli oggetti <xref:System.Workflow.Activities.Rules.RuleSet> di WF 3.5 all'interno dei flussi di lavoro di WF 4.5.L'esempio seguente è una definizione semplificata del modello a oggetti pubblico dell'attività.  
  
```  
public class ExternalizedPolicy4Activity<TResult>: CodeActivity  
{  
    public string RulesFilePath   
  
    public string RuleSetName           
  
    [RequiredArgument]  
    public InArgument<T> TargetObject   
  
    [RequiredArgument]  
    public OutArgument<T> ResultObject   
  
    public OutArgument<ValidationErrorCollection> ValidationErrors   
}  
```  
  
|||  
|-|-|  
|Proprietà|Descrizione|  
|RuleSetFilePath|Percorso del file <xref:System.Workflow.Activities.Rules.RuleSet> di .NET Framework 3.5 da valutare quando viene eseguita l'attività.|  
|RuleSetName|Nome dell'oggetto <xref:System.Workflow.Activities.Rules.RuleSet> da utilizzare all'interno del file con estensione rules.|  
|TargetObject|Oggetto nel quale gli oggetti <xref:System.Workflow.Activities.Rules.Rule> vengono valutati rispetto all'oggetto <xref:System.Workflow.Activities.Rules.RuleSet>.|  
|ResultObject|Oggetto risultante dopo aver applicato le regole \(ad esempio le regole vengono applicate rispetto all'argomento di input e il risultato viene archiviato nell'argomento Result\).|  
|ValidationError|Elenco di errori di convalida restituiti dal motore per le regole di WF 3.5 quando si convalida l'oggetto <xref:System.Workflow.Activities.Rules.RuleSet> rispetto all'oggetto di destinazione prima dell'esecuzione.|  
  
## ActivityDesigner di ExternalizedPolicy4  
 La finestra di progettazione ExternalizedPolicy4 consente di configurare un'attività per utilizzare un oggetto RuleSet esistente senza scrivere codice.È sufficiente impostare il percorso in cui si trova il file con estensione rules e specificare il nome dell'oggetto <xref:System.Workflow.Activities.Rules.RuleSet> che si desidera utilizzare.Consente inoltre di modificare l'oggetto <xref:System.Workflow.Activities.Rules.RuleSet>.Dopo aver compilato la soluzione, è disponibile nella casella degli strumenti nella sezione Microsoft.Samples.Activities.Rules.La finestra di progettazione consente di selezionare un file con estensione rules e un oggetto <xref:System.Workflow.Activities.Rules.RuleSet>.Quando si fa clic sul pulsante **Modifica RuleSet**, viene visualizzato l'oggetto <xref:System.Workflow.Activities.Rules.Design.RuleSetDialog> di WF 3.5.Questa finestra di dialogo è l'editor delle regole di WF 3.5 rieseguito nell'host e viene utilizzata per visualizzare e modificare le regole eseguite dall'attività ExternalizedPolicy4.  
  
## Policy4 e ExternalPolicy4  
 L'attività [Attività Policy in .NET Framework 4.5](../../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md) consente di creare ed eseguire un oggetto RuleSet di .NET Framework 3.5 in un flusso di lavoro di WF 4.5.L'oggetto <xref:System.Workflow.Activities.Rules.RuleSet> è serializzato inline nella definizione XML dell'attività Policy4.Nell'esempio ExternalizedPolicy4 viene illustrato come utilizzare un oggetto <xref:System.Workflow.Activities.Rules.RuleSet> esterno esistente \(contenuto in un file con estensione rules\).  
  
## Utilizzo dell'esempio  
 Per eseguire questo esempio non è necessaria alcuna configurazione particolare.Aprire la soluzione in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] e premere F5 per eseguire l'applicazione.  
  
 In questo esempio sono contenute due applicazioni client: ImperativeCodeClientSample e DesignerClientSample.Nel client ImperativeCodeClientSample viene illustrato come configurare ed eseguire l'attività ExternalizedPolicy4 tramite il codice imperativo C\#.In DesignerClientSample viene illustrato come configurare ed eseguire l'attività ExternalizedPolicy4 tramite la finestra di progettazione.  
  
#### Per eseguire l'applicazione ImperativeCodeClientSample  
  
1.  In [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] aprire il file della soluzione Policy4sample.sln.  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **ImperativeCodeClientSample**, quindi selezionare **Imposta come progetto di avvio**.  
  
3.  Per eseguire il progetto, premere CTRL\+F5.  
  
#### Per eseguire l'applicazione DesignerClientSample  
  
1.  In [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] aprire il file della soluzione Policy4sample.sln.  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **DesignerClientSample**, quindi selezionare **Imposta come progetto di avvio**.  
  
3.  Premere CTRL\+MAIUSC\+B per compilare il progetto.  
  
4.  Per eseguire il progetto, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Rules-ExternalizedPolicy4`