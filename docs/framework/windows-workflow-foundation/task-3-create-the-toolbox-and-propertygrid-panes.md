---
title: "Attivit&#224; 3: creare i riquadri Casella degli strumenti e PropertyGrid | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 72c1546a-eed5-4f0f-a616-719a163414f4
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Attivit&#224; 3: creare i riquadri Casella degli strumenti e PropertyGrid
In questa attività verranno creati i riquadri **Casella degli strumenti** e **PropertyGrid** e verranno aggiunti a [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] riallocato.  
  
 Per riferimento, alla fine di questo argomento viene fornito il codice che dovrebbe essere presente nel file MainWindow.xaml.cs dopo il completamente delle tre attività nella serie di argomenti [Riallocazione dell'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md).  
  
### Per creare la casella degli strumenti e aggiungerla alla griglia  
  
1.  Aprire il progetto HostingApplication  ottenuto seguendo la procedura descritta in [Attività 2: ospitare l'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md).  
  
2.  Nel riquadro **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file MainWindow.xaml e selezionare **Visualizza codice**.  
  
3.  Aggiungere un metodo `GetToolboxControl` alla classe `MainWindow` che crea un oggetto <xref:System.Activities.Presentation.Toolbox.ToolboxControl>, aggiunge una nuova categoria **Casella degli strumenti** alla **Casella degli strumenti** e assegna i tipi di attività<xref:System.Activities.Statements.Assign> e <xref:System.Activities.Statements.Sequence> alla categoria.  
  
    ```csharp  
  
    private ToolboxControl GetToolboxControl()  
    {  
        // Create the ToolBoxControl.  
        ToolboxControl ctrl = new ToolboxControl();  
  
        // Create a category.  
        ToolboxCategory category = new ToolboxCategory("category1");  
  
        // Create Toolbox items.  
        ToolboxItemWrapper tool1 =   
            new ToolboxItemWrapper("System.Activities.Statements.Assign",   
            typeof(Assign).Assembly.FullName, null, "Assign");  
  
        ToolboxItemWrapper tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",   
            typeof(Sequence).Assembly.FullName, null, "Sequence");  
  
        // Add the Toolbox items to the category.  
        category.Add(tool1);  
        category.Add(tool2);  
  
        // Add the category to the ToolBox control.  
        ctrl.Categories.Add(category);  
        return ctrl;  
    }  
  
    ```  
  
4.  Aggiungere un metodo privato `AddToolbox` alla classe `MainWindow` per posizionare la **Casella degli strumenti** nella colonna a sinistra nella griglia.  
  
    ```csharp  
  
    private void AddToolBox()  
    {  
        ToolboxControl tc = GetToolboxControl();  
        Grid.SetColumn(tc, 0);  
        grid1.Children.Add(tc);  
    }  
  
    ```  
  
5.  Aggiungere una chiamata al metodo `AddToolBox` nel costruttore della classe `MainWindow()` come illustrato nel codice seguente.  
  
    ```csharp  
  
    public MainWindow()  
    {  
        InitializeComponent();  
        this.RegisterMetadata();  
        this.AddDesigner();  
  
        this.AddToolBox();  
    }  
  
    ```  
  
6.  Premere F5 per compilare ed eseguire la soluzione.La **Casella degli strumenti** che contiene le attività <xref:System.Activities.Statements.Assign> e <xref:System.Activities.Statements.Sequence> deve essere visualizzata.  
  
### Per creare il riquadro PropertyGrid  
  
1.  Nel riquadro **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file MainWindow.xaml e selezionare **Visualizza codice**.  
  
2.  Aggiungere il metodo `AddPropertyInspector` alla classe `MainWindow` per posizionare il riquadro **PropertyGrid** nella colonna più a destra nella griglia.  
  
    ```csharp  
  
    private void AddPropertyInspector()  
    {  
        Grid.SetColumn(wd.PropertyInspectorView, 2);  
        grid1.Children.Add(wd.PropertyInspectorView);              
    }  
  
    ```  
  
3.  Aggiungere una chiamata al metodo `AddPropertyInspector` nel costruttore della classe `MainWindow()` come illustrato nel codice seguente.  
  
    ```csharp  
  
    public MainWindow()  
    {  
        InitializeComponent();  
        this.RegisterMetadata();  
        this.AddDesigner();  
        this.AddToolBox();  
  
        this.AddPropertyInspector();   
    }  
  
    ```  
  
4.  Premere F5 per compilare ed eseguire la soluzione.I riquadri **Casella degli strumenti**, l'area di disegno del flusso di lavoro e **PropertyGrid** devono essere visualizzati e quando si trascina un'attività <xref:System.Activities.Statements.Assign> o un'attività <xref:System.Activities.Statements.Sequence> sull'area di disegno, la griglia delle proprietà deve essere aggiornata a seconda dell'attività evidenziata.  
  
## Esempio  
 Il file MainWindow.xaml.cs ora deve contenere il codice seguente.  
  
```  
  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
//dlls added  
using System.Activities;  
using System.Activities.Core.Presentation;  
using System.Activities.Presentation;  
using System.Activities.Presentation.Metadata;  
using System.Activities.Presentation.Toolbox;  
using System.Activities.Statements;  
using System.ComponentModel;  
  
namespace HostingApplication  
{  
    /// <summary>  
    /// Interaction logic for MainWindow.xaml  
    /// </summary>  
    public partial class MainWindow : Window  
    {  
        private WorkflowDesigner wd;  
  
        public MainWindow()  
        {  
            InitializeComponent();  
            RegisterMetadata();  
            AddDesigner();  
            this.AddToolBox();  
            this.AddPropertyInspector();  
        }  
  
        private void AddDesigner()  
        {  
            //Create an instance of WorkflowDesigner class.  
            this.wd = new WorkflowDesigner();  
  
            //Place the designer canvas in the middle column of the grid.  
            Grid.SetColumn(this.wd.View, 1);  
  
            //Load a new Sequence as default.  
            this.wd.Load(new Sequence());  
  
            //Add the designer canvas to the grid.  
            grid1.Children.Add(this.wd.View);  
        }  
  
        private void RegisterMetadata()  
        {  
            DesignerMetadata dm = new DesignerMetadata();  
            dm.Register();  
        }  
  
        private ToolboxControl GetToolboxControl()  
        {  
            // Create the ToolBoxControl.  
            ToolboxControl ctrl = new ToolboxControl();  
  
            // Create a category.  
            ToolboxCategory category = new ToolboxCategory("category1");  
  
            // Create Toolbox items.  
            ToolboxItemWrapper tool1 =  
                new ToolboxItemWrapper("System.Activities.Statements.Assign",  
                typeof(Assign).Assembly.FullName, null, "Assign");  
  
            ToolboxItemWrapper tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",  
                typeof(Sequence).Assembly.FullName, null, "Sequence");  
  
            // Add the Toolbox items to the category.  
            category.Add(tool1);  
            category.Add(tool2);  
  
            // Add the category to the ToolBox control.  
            ctrl.Categories.Add(category);  
            return ctrl;  
        }  
  
        private void AddToolBox()  
        {  
            ToolboxControl tc = GetToolboxControl();  
            Grid.SetColumn(tc, 0);  
            grid1.Children.Add(tc);  
        }  
  
        private void AddPropertyInspector()  
        {  
            Grid.SetColumn(wd.PropertyInspectorView, 2);  
            grid1.Children.Add(wd.PropertyInspectorView);  
        }  
  
    }  
}  
  
```  
  
## Vedere anche  
 [Riallocazione dell'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)   
 [Attività 1: creare una nuova applicazione Windows Presentation Foundation](../../../docs/framework/windows-workflow-foundation//task-1-create-a-new-wpf-app.md)   
 [Attività 2: ospitare l'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md)