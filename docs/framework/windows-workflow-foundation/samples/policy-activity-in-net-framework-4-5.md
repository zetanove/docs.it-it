---
title: "Attivit&#224; Policy in .NET Framework 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8e375e0c-d7c1-4d69-88ab-36d52db0aa7e
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Attivit&#224; Policy in .NET Framework 4.5
L'attività Policy4 consente di utilizzare gli oggetti <xref:System.Workflow.Activities.Rules.RuleSet> di [!INCLUDE[wf2](../../../../includes/wf2-md.md)] in [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] \(WF 3.5\) direttamente in [!INCLUDE[wf2](../../../../includes/wf2-md.md)] in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] \(WF 4.5\) tramite il motore fornito in WF 3.5.Utilizzando questa attività, è possibile creare ed eseguire un oggetto <xref:System.Workflow.Activities.Rules.RuleSet> di WF 3.5.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] motore per le regole di WF 3.5, incluso in Windows Workflow Foundation, vedere Introduzione al motore per le regole di Windows Workflow Foundation.Per ulteriori informazioni sulla migrazione delle regole a WF in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)], vedere [Istruzioni di migrazione](../../../../docs/framework/windows-workflow-foundation//migration-guidance.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Rules-Policy4`  
  
## Progetti di questo esempio  
  
|Nome progetto|Descrizione|File principali|  
|-------------------|-----------------|---------------------|  
|Policy4|Contiene l'attività Policy4 e la relativa finestra di progettazione di [!INCLUDE[wf1](../../../../includes/wf1-md.md)].|**Policy4.cs**: definizione dell'attività Policy4.<br /><br /> **PolicyDesigner.xaml**: finestra di progettazione personalizzata per l'attività Policy4.Utilizza l'editor delle regole \([Classe RuleSetDialog](http://go.microsoft.com/fwlink/?LinkId=150378)\) dal motore per le regole di [!INCLUDE[wf1](../../../../includes/wf1-md.md)].|  
|ImperativeCodeClientSample|Applicazione client di esempio che configura ed esegue un flusso di lavoro tramite un'applicazione Policy4 e il codice C\# imperativo \(non viene utilizzata alcuna finestra di progettazione di [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\).|**ApplyDiscount.rules**: file con definizioni delle regole di [!INCLUDE[wf1](../../../../includes/wf1-md.md)].<br /><br /> **Order.cs**: tipo che rappresenta un ordine del cliente.Le regole vengono applicate agli oggetti di questo tipo.<br /><br /> **Program.cs**: configura ed esegue un flusso di lavoro che dispone di un'attività Policy4 per applicare le regole definite in ApplyDiscount.rules alle istanze di oggetti Order.<br /><br /> **App.config**: file di configurazione con il percorso del file delle regole.|  
|DesignerClientSample|Applicazione client di esempio che configura ed esegue un flusso di lavoro tramite un'applicazione Policy4 nella finestra di progettazione di [!INCLUDE[wf1](../../../../includes/wf1-md.md)].|**Sequence1.xaml**: flusso di lavoro sequenziale che utilizza un'attività Policy4 per eseguire valutazioni delle regole.<br /><br /> `Program.cs`: esegue un'istanza del flusso di lavoro definito in Sequence1.xaml.|  
  
## Attività Policy4  
 L'attività Policy4 è una classe che deriva dall'oggetto <xref:System.Activities.NativeActivity%601> che consente ai flussi di lavoro di eseguire oggetti RuleSet di [!INCLUDE[wf1](../../../../includes/wf1-md.md)].L'esempio di codice seguente è una definizione semplificata del modello a oggetti pubblico dell'attività.  
  
```csharp  
  
public class Policy4Activity<TResult>: NativeActivity<TResult>  
{  
    public RuleSet RuleSet  
  
    [IsRequired]  
    public InArgument Input  
  
    public OutArgument<ValidationErrorCollection> ValidationErrors  
}  
```  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|RuleSet|[Classe RuleSet](http://go.microsoft.com/fwlink/?LinkId=150379) di WF per .NET Framework 3.5 da valutare quando viene eseguita l'attività.|  
|TargetObject|Oggetto rispetto al quale vengono valutate le regole nella [Classe RuleSet](http://go.microsoft.com/fwlink/?LinkId=150379).|  
|ValidationError|Elenco di errori di convalida restituiti dal motore per le regole di [!INCLUDE[wf1](../../../../includes/wf1-md.md)] per .NET Framework 3.5 quando si convalida la [Classe RuleSet](http://go.microsoft.com/fwlink/?LinkId=150379) rispetto all'oggetto di destinazione prima dell'esecuzione.|  
  
## ActivityDesigner di Policy4  
 La finestra di progettazione di Policy4 aggiunge la funzionalità che consente di configurare un'attività Policy4 senza dover scrivere codice.Dopo aver compilato la soluzione, è disponibile nella casella degli strumenti nella sezione **Microsoft.Samples.Activities.Rules**.  
  
 La finestra di progettazione di WF consente di configurare un oggetto di destinazione e un oggetto RuleSet.Quando si fa clic sul pulsante **Modifica RuleSet**, viene visualizzata la [Classe RuleSetDialog](http://go.microsoft.com/fwlink/?LinkId=150378) di WF per [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)].Questa finestra di dialogo è l'editor delle regole di [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] rieseguito nell'host.Utilizzare l'editor per creare e modificare le regole eseguite dall'attività Policy4.  
  
## Utilizzo dell'esempio  
 Per eseguire questo esempio non è necessaria alcuna configurazione particolare.È sufficiente aprire la soluzione in Visual Studio e premere F5 per eseguire l'applicazione.  
  
 In questo esempio sono contenute due applicazioni client: ImperativeCodeClientSample e DesignerClientSample.Nel client ImperativeCodeClientSample viene illustrato come configurare ed eseguire l'attività Policy40 tramite il codice imperativo C\#.In DesignerClientSample viene illustrato come configurare ed eseguire l'attività Policy4 tramite la finestra di progettazione.  
  
#### Per eseguire l'applicazione client ImperativeCodeClientSample  
  
1.  In [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] aprire il file della soluzione Policy4Sample.sln.  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **ImperativeCodeClientSample**, quindi selezionare **Imposta come progetto di avvio**.  
  
3.  Per eseguire il progetto, premere CTRL\+F5.  
  
#### Per eseguire l'applicazione client ImperativeCodeClientSample  
  
1.  In [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] aprire il file della soluzione Policy4Sample.sln.  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **DesignerClientSample**.  
  
    -   Selezionare **Imposta come progetto di avvio**.  
  
3.  Premere CTRL\+MAIUSC\+B per compilare il progetto.  
  
4.  Per eseguire il progetto, premere CTRL\+F5.  
  
## Vedere anche