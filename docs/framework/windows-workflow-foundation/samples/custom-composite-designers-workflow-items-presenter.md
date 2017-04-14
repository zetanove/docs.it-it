---
title: "Finestre di progettazione composite personalizzate - Relatore di elementi del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 70055c4b-1173-47a3-be80-b5bce6f59e9a
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Finestre di progettazione composite personalizzate - Relatore di elementi del flusso di lavoro
<xref:System.Activities.Design.WorkflowItemsPresenter> è un tipo chiave nel modello di programmazione della finestra di progettazione di WF che consente la modifica di una raccolta di elementi contenuti.In questo esempio viene illustrato come compilare un ActivityDesigner che espone una raccolta modificabile.  
  
 In questo esempio viene illustrato quanto segue:  
  
-   Creazione di un ActivityDesigner personalizzato con un oggetto <xref:System.Activities.Design.WorkflowItemsPresenter>.  
  
-   Creazione di un ActivityDesigner con una visualizzazione "compressa" ed "espansa."  
  
-   Esecuzione dell'override di una finestra di progettazione predefinita in un'applicazione riallocata.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio **UsingWorkflowItemsPresenter.sln** per C\# o per VB in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.Dovrebbe essere visualizzata un'applicazione della finestra di progettazione flussi di lavoro riallocata in cui è possibile trascinare attività nell'area di disegno.  
  
## Evidenziazioni di esempio  
 Nel codice di questo esempio viene illustrato quanto segue:  
  
-   Compilazione di una finestra di progettazione dell'attività per: `Parallel`  
  
-   Creazione di un ActivityDesigner personalizzato con un oggetto <xref:System.Activities.Design.WorkflowItemsPresenter>.Alcune considerazioni:  
  
    -   Notare l'utilizzo dell'associazione dati WPF per eseguire l'associazione a `ModelItem.Branches`.`ModelItem` è la proprietà su <xref:System.Activities.Design.WorkflowElementDesigner> che fa riferimento all'oggetto sottostante la finestra di progettazione per il quale è utilizzata, in questo caso, `Parallel`.  
  
    -   <xref:System.Activities.Design.WorkflowItemsPresenter.SpacerTemplate%2A> può essere utilizzato per inserire un elemento visivo per visualizzare i singoli elementi nella raccolta.  
  
    -   <xref:System.Activities.Design.WorkflowItemsPresenter.ItemsPanel%2A> è un modello che può essere fornito per determinare il layout degli elementi nella raccolta.In questo caso, viene utilizzato un pannello Stack orizzontale.  
  
 Nel codice dell'esempio seguente viene illustrata questa operazione.  
  
```xaml  
<sad:WorkflowItemsPresenter HintText="Drop Activities Here"  
                              Items="{Binding Path=ModelItem.Branches}">  
    <sad:WorkflowItemsPresenter.SpacerTemplate>  
      <DataTemplate>  
        <Ellipse Width="10" Height="10" Fill="Black"/>  
      </DataTemplate>  
    </sad:WorkflowItemsPresenter.SpacerTemplate>  
    <sad:WorkflowItemsPresenter.ItemsPanel>  
      <ItemsPanelTemplate>  
        <StackPanel Orientation="Horizontal"/>  
      </ItemsPanelTemplate>  
    </sad:WorkflowItemsPresenter.ItemsPanel>  
  </sad:WorkflowItemsPresenter>  
  
```  
  
-   Eseguire un'associazione di `DesignerAttribute` al tipo `Parallel`, quindi restituire gli attributi indicati.  
  
    -   Registrare innanzitutto tutte le finestre di progettazione predefinite.  
  
 Di seguito è riportato l'esempio di codice.  
  
```csharp  
// register metadata  
(new DesignerMetadata()).Register();  
RegisterCustomMetadata();  
  
```  
  
```vb  
' register metadata  
Dim metadata = New DesignerMetadata()  
metadata.Register()  
' register custom metadata  
RegisterCustomMetadata()  
  
```  
  
-   -   Eseguire quindi l'override dell'elemento parallelo nel metodo `RegisterCustomMetadata`.  
  
 Nel codice seguente viene illustrato questa operazione in C\# e Visual Basic.  
  
 C\#  
  
```csharp  
void RegisterCustomMetadata()  
{  
      AttributeTableBuilder builder = new AttributeTableBuilder();  
      builder.AddCustomAttributes(typeof(Parallel), new DesignerAttribute(typeof(CustomParallelDesigner)));  
      MetadataStore.AddAttributeTable(builder.CreateTable());  
}  
  
```  
  
```vb  
Sub RegisterCustomMetadata()  
   Dim builder As New AttributeTableBuilder()  
   builder.AddCustomAttributes(GetType(Parallel), New DesignerAttribute(GetType(CustomParallelDesigner)))  
   MetadataStore.AddAttributeTable(builder.CreateTable())  
End Sub  
  
```  
  
-   Osservare infine notare l'utilizzo di diversi modelli di dati e trigger per selezionare il modello appropriato in base alla proprietà `IsRootDesigner`.  
  
 Di seguito è riportato l'esempio di codice.  
  
```xaml  
<sad:ActivityDesigner x:Class="Microsoft.Samples.CustomParallelDesigner"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:sad="clr-namespace:System.Activities.Design;assembly=System.Activities.Design"  
    xmlns:sadv="clr-namespace:System.Activities.Design.View;assembly=System.Activities.Design">  
  <sad:ActivityDesigner.Resources>  
    <DataTemplate x:Key="Expanded">  
      <StackPanel>  
        <TextBlock>This is the Expanded View</TextBlock>  
        <sad:WorkflowItemsPresenter HintText="Drop Activities Here"  
                                    Items="{Binding Path=ModelItem.Branches}">  
          <sad:WorkflowItemsPresenter.SpacerTemplate>  
            <DataTemplate>  
              <Ellipse Width="10" Height="10" Fill="Black"/>  
            </DataTemplate>  
          </sad:WorkflowItemsPresenter.SpacerTemplate>  
          <sad:WorkflowItemsPresenter.ItemsPanel>  
            <ItemsPanelTemplate>  
              <StackPanel Orientation="Horizontal"/>  
            </ItemsPanelTemplate>  
          </sad:WorkflowItemsPresenter.ItemsPanel>  
        </sad:WorkflowItemsPresenter>  
      </StackPanel>  
    </DataTemplate>  
    <DataTemplate x:Key="Collapsed">  
      <TextBlock>This is the Collapsed View</TextBlock>  
    </DataTemplate>  
    <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">  
      <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>  
      <Style.Triggers>  
        <DataTrigger Binding="{Binding Path=IsRootDesigner}" Value="true">  
          <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>  
        </DataTrigger>  
      </Style.Triggers>  
    </Style>  
  </sad: ActivityDesigner.Resources>  
  <Grid>  
    <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}"/>  
  </Grid>  
</sad: ActivityDesigner>  
  
```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\WorkflowItemsPresenter`  
  
## Vedere anche  
 <xref:System.Activities.Presentation.WorkflowItemsPresenter>   
 [Sviluppo di applicazioni con Progettazione flussi di lavoro](../Topic/Developing%20Applications%20with%20the%20Workflow%20Designer.md)