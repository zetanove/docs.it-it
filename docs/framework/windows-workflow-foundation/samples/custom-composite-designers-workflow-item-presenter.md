---
title: "Finestre di progettazione composte personalizzate - relatore dell&#39;elemento del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f85224cf-9e30-44a5-9a81-3bc438a34364
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Finestre di progettazione composte personalizzate - relatore dell&#39;elemento del flusso di lavoro
L'oggetto <xref:System.Activities.Presentation.WorkflowItemPresenter> è un tipo di chiave nel modello di programmazione della finestra di progettazione WF che consente la creazione di un'"area di rilascio" in cui è possibile posizionare un'attività arbitraria.In questo esempio viene illustrato come compilare un ActivityDesigner che espone tale "area di rilascio".  
  
 In questo esempio viene illustrato quanto segue:  
  
## Dimostrazione  
  
-   Creazione di un ActivityDesigner personalizzato con un oggetto <xref:System.Activities.Presentation.WorkflowItemPresenter>.  
  
-   Registrazione della finestra di progettazione personalizzata utilizzando l'archivio di metadati.  
  
-   Programmazione della casella degli strumenti riallocata in modo dichiarativo e imperativo.  
  
## Dettagli dell'esempio  
 Il codice per questo esempio illustra:  
  
-   L'ActivityDesigner personalizzato compilato per la classe `SimpleNativeActivity`.  
  
-   La creazione di un ActivityDesigner personalizzato con un oggetto <xref:System.Activities.Presentation.WorkflowItemPresenter>.  
  
```xaml  
<sap:ActivityDesigner x:Class="Microsoft.Samples.UsingWorkflowItemPresenter.SimpleNativeDesigner"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"  
    xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">  
    <sap:ActivityDesigner.Resources>  
        <DataTemplate x:Key="Collapsed">  
            <StackPanel>  
                <TextBlock>This is the collapsed view</TextBlock>  
            </StackPanel>  
        </DataTemplate>  
        <DataTemplate x:Key="Expanded">  
            <StackPanel>  
                <TextBlock>Custom Text</TextBlock>  
                <sap:WorkflowItemPresenter Item="{Binding Path=ModelItem.Body, Mode=TwoWay}"  
                                        HintText="Please drop an activity here" />  
            </StackPanel>  
        </DataTemplate>  
        <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">  
            <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>  
            <Style.Triggers>  
                <DataTrigger Binding="{Binding Path=ShowExpanded}" Value="true">  
                    <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>  
                </DataTrigger>  
            </Style.Triggers>  
        </Style>  
    </sap:ActivityDesigner.Resources>  
    <Grid>  
        <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}" />  
    </Grid>  
</sap:ActivityDesigner>  
```  
  
 Notare l'utilizzo dell'associazione dati WPF per eseguire l'associazione a `ModelItem.Body`.`ModelItem` è la proprietà su <xref:System.Activities.Presentation.WorkflowElementDesigner> che fa riferimento all'oggetto sottostante la finestra di progettazione per il quale è utilizzata, in questo caso, **SimpleNativeActivity**.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\WorkflowItemPresenter`  
  
## Vedere anche  
 <xref:System.Activities.Presentation.WorkflowItemPresenter>   
 [Sviluppo di applicazioni con Progettazione flussi di lavoro](../Topic/Developing%20Applications%20with%20the%20Workflow%20Designer.md)