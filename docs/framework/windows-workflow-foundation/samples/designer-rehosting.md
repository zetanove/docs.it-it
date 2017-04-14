---
title: "Riallocazione della finestra di progettazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b676ad31-5f64-4d84-9a36-b4d7113a2f4d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Riallocazione della finestra di progettazione
La riallocazione della finestra di progettazione è un scenario comune che si riferisce all'hosting dell'area di progettazione flussi di lavoro all'interno di un'applicazione personalizzata.La maggior parte degli utenti dell'applicazione host utilizza Visual Studio, tuttavia esistono scenari in cui potrebbe essere utile visualizzare la progettazione flussi di lavoro in un'applicazione:  
  
-   Monitoraggio delle applicazioni: per consentire a un utente finale di visualizzare il processo e i dati di runtime sul processo, ad esempio i dati relativi allo stato attivo attualmente, quelli relativi al tempo di esecuzione dell'aggregazione o altre informazioni su un'istanza del flusso di lavoro.  
  
-   Applicazioni che consentono a un utente di personalizzare il processo con un set limitato di attività.  
  
 Per supportare questi tipi di applicazioni, la progettazione flussi di lavoro viene fornita all'interno di .NET Framework e può essere ospitata in un'applicazione WPF o in un'applicazione Windows Form con il codice host WPF appropriato.In questo esempio viene illustrato quanto segue:  
  
-   Riallocazione della progettazione flussi di lavoro.  
  
-   Utilizzo della casella degli strumenti riallocata nonché della griglia delle proprietà.  
  
## Riallocazione della progettazione  
 In questo esempio viene illustrato come creare il layout WPF per contenere la finestra di progettazione, visualizzata nel layout della griglia seguente \(codice della Casella degli strumenti omesso per motivi di spazio\).Si noti la denominazione dei bordi che contengono la finestra di progettazione e la griglia delle proprietà.  
  
```xaml  
<Grid>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition Width="2*"/>  
        <ColumnDefinition Width="7*"/>  
        <ColumnDefinition Width="3*"/>  
    </Grid.ColumnDefinitions>  
    <Border Grid.Column="0">  
        <sapt:ToolboxControl>...</sapt:ToolboxControl>  
    </Border>  
    <Border Grid.Column="1" Name="DesignerBorder"/>  
    <Border Grid.Column="2" Name="PropertyBorder"/>  
</Grid>  
  
```  
  
 Successivamente nell'esempio viene creata la finestra di progettazione e vengono associate le relative proprietà primarie <xref:System.Activities.Presentation.WorkflowDesigner.View%2A> e <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A> al contenitore appropriato nell'interfaccia utente.Esistono alcune righe aggiuntive di codice nell'esempio seguente per le quali è opportuno fornire alcune spiegazioni.La chiamata al metodo <xref:System.Activities.Core.Presentation.DesignerMetadata.Register%2A> è necessaria per associare l'ActivityDesigner predefinito per le attività fornite con [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].<xref:System.Activities.Presentation.WorkflowDesigner.Load%2A> viene chiamato per passare l'elemento WF da modificare.Infine, le proprietà <xref:System.Activities.Presentation.WorkflowDesigner.View%2A> \(area di disegno primaria\) e <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A> \(griglia delle proprietà\) vengono posizionate sull'area dell'interfaccia utente.  
  
```csharp  
protected override void OnInitialized(EventArgs e)  
{  
   base.OnInitialized(e);  
   // register metadata  
   (new DesignerMetadata()).Register();  
  
   // create the workflow designer  
   WorkflowDesigner wd = new WorkflowDesigner();  
   wd.Load(new Sequence());  
   DesignerBorder.Child = wd.View;  
   PropertyBorder.Child = wd.PropertyInspectorView;  
}  
  
```  
  
## Utilizzo della casella degli strumenti riallocata  
 In questo esempio viene utilizzato in modo dichiarativo il controllo della casella degli strumenti riallocata in XAML.Si noti che nel codice, è possibile passare un tipo al costruttore <xref:System.Activities.Presentation.Toolbox.ToolboxItemWrapper>.  
  
```xaml  
<!-- Copyright (c) Microsoft Corporation. All rights reserved-->  
<Window x:Class="Microsoft.Samples.DesignerRehosting.RehostingWfDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sapt="clr-namespace:System.Activities.Presentation.Toolbox;assembly=System.Activities.Presentation"  
        xmlns:sys="clr-namespace:System;assembly=mscorlib"  
        Title="Window1" Height="600" Width="900">  
    <Window.Resources>  
        <sys:String x:Key="AssemblyName">System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</sys:String>  
    </Window.Resources>  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="2*"/>  
            <ColumnDefinition Width="7*"/>  
            <ColumnDefinition Width="3*"/>  
        </Grid.ColumnDefinitions>  
        <Border Grid.Column="0">  
            <sapt:ToolboxControl>  
                <sapt:ToolboxCategory CategoryName="Basic">  
                    <sapt:ToolboxItemWrapper AssemblyName="{StaticResource AssemblyName}" >  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.Sequence  
                        </sapt:ToolboxItemWrapper.ToolName>  
                       </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.WriteLine  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.If  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.While  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                </sapt:ToolboxCategory>  
            </sapt:ToolboxControl>  
        </Border>  
        <Border Grid.Column="1" Name="DesignerBorder"/>  
        <Border Grid.Column="2" Name="PropertyBorder"/>  
    </Grid>  
</Window>  
  
```  
  
#### Utilizzo dell'esempio  
  
1.  Aprire la soluzione DesignerRehosting.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Premere F5 per compilare ed eseguire l'applicazione.  
  
3.  Un'applicazione WPF viene avviata con una finestra di progettazione riallocata.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\DesignerRehosting\Basic`  
  
## Vedere anche