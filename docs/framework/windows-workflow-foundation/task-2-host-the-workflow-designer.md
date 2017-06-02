---
title: "Attivit&#224; 2: ospitare l&#39;utilit&#224; di progettazione del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a29b138-270d-4846-b78e-2b875e34e501
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Attivit&#224; 2: ospitare l&#39;utilit&#224; di progettazione del flusso di lavoro
In questo argomento viene descritta la procedura per ospitare un'istanza di [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] in un'applicazione [!INCLUDE[avalon1](../../../includes/avalon1-md.md)].  
  
 Nella procedura viene configurato il controllo **Griglia** che contiene la finestra di progettazione, viene creata a livello di codice un'istanza di <xref:System.Activities.Presentation.WorkflowDesigner> che contiene un'attività <xref:System.Activities.Statements.Sequence> predefinita, vengono registrati i metadati della finestra di progettazione per fornire supporto della finestra di progettazione per tutte le attività predefinite e viene ospitato [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] nell'applicazione [!INCLUDE[avalon2](../../../includes/avalon2-md.md)].  
  
### Per ospitare la finestra di progettazione del flusso di lavoro  
  
1.  Aprire il progetto HostingApplication creato in [Attività 1: creare una nuova applicazione Windows Presentation Foundation](../../../docs/framework/windows-workflow-foundation//task-1-create-a-new-wpf-app.md).  
  
2.  Regolare le dimensioni della finestra per semplificare l'utilizzo di [!INCLUDE[wfd2](../../../includes/wfd2-md.md)].A tal fine, selezionare **MainWindow** nella finestra di progettazione, premere F4 per visualizzare la finestra **Proprietà**, quindi nella sezione **Layout** impostare su 600 il valore di **Larghezza** e su 350 il valore di **Altezza**.  
  
3.  Impostare il nome della griglia selezionando il pannello **Griglia** nella finestra di progettazione \(fare clic sulla casella all'interno di **MainWindow**\) e impostando su "grid1" la proprietà **Name** nella parte superiore della finestra **Proprietà**.  
  
4.  Nella finestra **Proprietà** fare clic sui puntini di sospensione \(**…**\) accanto alla proprietà `ColumnDefinitions` per aprire la finestra di dialogo **Editor della raccolta**.  
  
5.  Nella finestra di dialogo **Editor della raccolta** fare clic tre volte sul pulsante **Aggiungi** per inserire tre colonne nel layout.La prima colonna conterrà la **Casella degli strumenti**, la seconda ospiterà [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] e la terza colonna sarà utilizzata per il controllo proprietà.  
  
6.  Impostare la proprietà `Width` della colonna centrale sul valore "4\*".  
  
7.  Scegliere **OK** per salvare le modifiche.Il seguente codice XAML viene aggiunto al file MainWindow.xaml:  
  
    ```  
  
    <Grid Name="grid1">  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition />  
            <ColumnDefinition Width="4*" />  
            <ColumnDefinition />  
        </Grid.ColumnDefinitions>  
    </Grid>  
  
    ```  
  
8.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su MainWindow.xaml e selezionare **Visualizza codice**.Modificare il codice attenendosi ai passaggi seguenti:  
  
    1.  Aggiungere gli spazi dei nomi seguenti:  
  
        ```csharp  
  
        using System.Activities;  
        using System.Activities.Core.Presentation;  
        using System.Activities.Presentation;  
        using System.Activities.Presentation.Metadata;  
        using System.Activities.Presentation.Toolbox;  
        using System.Activities.Statements;  
        using System.ComponentModel;  
  
        ```  
  
    2.  Per dichiarare un campo membro privato per contenere un'istanza di <xref:System.Activities.Presentation.WorkflowDesigner>, aggiungere il codice seguente alla classe `MainWindow`.  
  
        ```csharp  
  
        public partial class MainWindow : Window  
        {  
            private WorkflowDesigner wd;  
  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
        }  
  
        ```  
  
    3.  Aggiungere il metodo `AddDesigner` seguente alla classe `MainWindow`.Tramite l'implementazione viene creata un'istanza dell'oggetto <xref:System.Activities.Presentation.WorkflowDesigner>, viene aggiunta un'attività <xref:System.Activities.Statements.Sequence> che viene inserita nella colonna centrale della **Griglia** grid1.  
  
        ```csharp  
  
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
  
        ```  
  
    4.  Registrare i metadati della finestra di progettazione per aggiungere il supporto della finestra di progettazione per tutte le attività incorporate.In questo modo sarà possibile spostare le attività dalla casella degli strumenti all'attività <xref:System.Activities.Statements.Sequence> originale in [!INCLUDE[wfd2](../../../includes/wfd2-md.md)].A tal fine, aggiungere il metodo `RegisterMetadata` alla classe `MainWindow`.  
  
        ```csharp  
  
        private void RegisterMetadata()  
        {               
            DesignerMetadata dm = new DesignerMetadata();  
            dm.Register();  
        }  
  
        ```  
  
         [!INCLUDE[crabout](../../../includes/crabout-md.md)] registrazione di ActivityDesigner, vedere [Procedura: Creare un ActivityDesigner personalizzato](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-activity-designer.md).  
  
    5.  Nel costruttore della classe `MainWindow`, aggiungere chiamate ai metodi dichiarati precedentemente per registrare i metadati per il supporto della finestra di progettazione e per creare l'oggetto <xref:System.Activities.Presentation.WorkflowDesigner>.  
  
        ```csharp  
        public MainWindow()  
        {  
            InitializeComponent();  
  
            // Register the metadata  
            RegisterMetadata();  
  
            // Add the WFF Designer  
            AddDesigner();  
        }  
  
        ```  
  
        > [!NOTE]
        >  Il metodo `RegisterMetadata` registra i metadati della finestra di progettazione di attività incorporate, inclusa l'attività <xref:System.Activities.Statements.Sequence>.Poiché il metodo `AddDesigner` utilizza l'attività <xref:System.Activities.Statements.Sequence>, è necessario chiamare innanzitutto il metodo `RegisterMetadata`.  
  
9. Premere F5 per compilare ed eseguire la soluzione.  
  
10. Per informazioni su come aggiungere il supporto della **Casella degli strumenti** e di **PropertyGrid** alla finestra di progettazione del flusso di lavoro riallocata, vedere [Attività 3: creare i riquadri Casella degli strumenti e PropertyGrid](../../../docs/framework/windows-workflow-foundation//task-3-create-the-toolbox-and-propertygrid-panes.md).  
  
## Vedere anche  
 [Riallocazione dell'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)   
 [Attività 1: creare una nuova applicazione Windows Presentation Foundation](../../../docs/framework/windows-workflow-foundation//task-1-create-a-new-wpf-app.md)   
 [Attività 3: creare i riquadri Casella degli strumenti e PropertyGrid](../../../docs/framework/windows-workflow-foundation//task-3-create-the-toolbox-and-propertygrid-panes.md)