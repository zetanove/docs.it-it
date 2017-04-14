---
title: "Procedura: creare un&#39;interfaccia utente a pi&#249; riquadri con Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ListView (controllo) [Windows Form], esempi"
  - "Panel (controllo) [Windows Form], esempi"
  - "RichTextBox (controllo) [Windows Form], esempi"
  - "SplitContainer (controllo) [Windows Form], esempi"
  - "Splitter (controllo) [Windows Form], esempi"
  - "TreeView (controllo) [Windows Form], esempi"
ms.assetid: e79f6bcc-3740-4d1e-b46a-c5594d9b7327
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Procedura: creare un&#39;interfaccia utente a pi&#249; riquadri con Windows Form
La procedura descritta di seguito consente di creare un'interfaccia utente a più riquadri simile all'interfaccia di Microsoft Outlook, che include l'elenco cartelle, un riquadro per i messaggi e il riquadro di anteprima.  Questa disposizione viene ottenuta principalmente tramite l'ancoraggio dei controlli al form.  
  
 Per ancorare un controllo, è necessario determinare a quale bordo del contenitore padre deve essere fissato.  Se pertanto si imposta la proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A> su <xref:System.Windows.Forms.DockStyle>, il bordo destro del controllo verrà ancorato al bordo destro del controllo padre.  Il bordo ancorato del controllo viene inoltre ridimensionato in modo da combaciare con il bordo del controllo contenitore.  Per ulteriori informazioni sul funzionamento della proprietà <xref:System.Windows.Forms.SplitContainer.Dock%2A>, vedere [Procedura: ancorare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md).  
  
 Questa procedura illustra la disposizione del controllo <xref:System.Windows.Forms.SplitContainer> e degli altri controlli sul form, ma non spiega come aggiungere le funzionalità necessarie affinché l'applicazione si comporti in modo analogo a Microsoft Outlook.  
  
 Per creare questa interfaccia utente, inserire i controlli all'interno del controllo <xref:System.Windows.Forms.SplitContainer>, che contiene il controllo <xref:System.Windows.Forms.TreeView> nel pannello sinistro.  Il pannello destro del controllo <xref:System.Windows.Forms.SplitContainer> contiene un secondo controllo <xref:System.Windows.Forms.SplitContainer> con un controllo <xref:System.Windows.Forms.ListView> sopra un controllo <xref:System.Windows.Forms.RichTextBox>.  Tali controlli <xref:System.Windows.Forms.SplitContainer> consentono di ridimensionare in modo indipendente gli altri controlli del form.  Le tecniche illustrate in questa procedura possono essere adattate in modo da realizzare interfacce utente personalizzate.  
  
### Per creare un'interfaccia utente nello stile di Outlook a livello di codice  
  
1.  All'interno di un form dichiarare i singoli controlli che compongono l'interfaccia utente.  Per questo esempio, utilizzare i controlli <xref:System.Windows.Forms.TreeView>, <xref:System.Windows.Forms.ListView>, <xref:System.Windows.Forms.SplitContainer> e <xref:System.Windows.Forms.RichTextBox> per riprodurre l'interfaccia utente di Microsoft Outlook.  
  
    ```vb  
    Private WithEvents treeView1 As System.Windows.Forms.TreeView  
    Private WithEvents listView1 As System.Windows.Forms.ListView  
    Private WithEvents richTextBox1 As System.Windows.Forms.RichTextBox  
    Private WithEvents splitContainer1 As _  
        System.Windows.Forms.SplitContainer  
    Private WithEvents splitContainer2 As _  
        System.Windows.Forms.SplitContainer  
  
    ```  
  
    ```csharp  
    private System.Windows.Forms.TreeView treeView1;  
    private System.Windows.Forms.ListView listView1;  
    private System.Windows.Forms.RichTextBox richTextBox1;  
    private System.Windows.Forms. SplitContainer splitContainer2;  
    private System.Windows.Forms. SplitContainer splitContainer1;  
  
    ```  
  
2.  Creare una routine che definisca l'interfaccia utente.  Con il codice riportato di seguito, le diverse proprietà vengono impostate in modo che il form risulti simile all'interfaccia utente di Microsoft Outlook.  Utilizzando altri controlli o un diverso ancoraggio, è tuttavia possibile creare in modo altrettanto semplice interfacce utente ugualmente flessibili.  
  
    ```vb  
    Public Sub CreateOutlookUI()  
        ' Create an instance of each control being used.  
        Me.components = New System.ComponentModel.Container()  
        Me.treeView1 = New System.Windows.Forms.TreeView()  
        Me.listView1 = New System.Windows.Forms.ListView()  
        Me.richTextBox1 = New System.Windows.Forms.RichTextBox()  
        Me.splitContainer1 = New System.Windows.Forms.SplitContainer()  
        Me.splitContainer2= New System.Windows.Forms. SplitContainer()  
  
        ' Should you develop this into a working application,  
        ' use the AddHandler method to hook up event procedures here.  
  
        ' Set properties of TreeView control.  
        ' Use the With statement to avoid repetitive code.  
        With Me.treeView1  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 0  
            .Nodes.Add("treeView")  
        End With  
  
    ' Set properties of ListView control.  
       With Me.listView1  
          .Dock = System.Windows.Forms.DockStyle.Top  
          .TabIndex = 2  
          .Items.Add("listView")  
       End With  
  
    ' Set properties of RichTextBox control.  
       With Me.richTextBox1  
          .Dock = System.Windows.Forms.DockStyle.Fill  
          .TabIndex = 3  
          .Text = "richTextBox1"  
       End With  
  
        ' Set properties of the first SplitContainer control.  
        With Me.splitContainer1  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 1  
            .SplitterWidth = 4  
            .SplitterDistance = 150  
            .Orientation = Orientation.Horizontal  
            .Panel1.Controls.Add(Me.listView1)  
            .Panel2.Controls.Add(Me.richTextBox1)  
    End With  
  
        ' Set properties of the second SplitContainer control.  
        With Me.splitContainer2  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 4  
            .SplitterWidth = 4  
            .SplitterDistance = 100  
            .Panel1.Controls.Add(Me.treeView1)  
            .Panel2.Controls.Add(Me.SplitContainer1)  
    End With  
  
    ' Add the main SplitContainer control to the form.  
        Me.Controls.Add(Me.splitContainer2)  
        Me.Text = "Intricate UI Example"  
    End Sub  
  
    ```  
  
    ```csharp  
    public void createOutlookUI()  
    {  
        // Create an instance of each control being used.  
        treeView1 = new System.Windows.Forms.TreeView();  
        listView1 = new System.Windows.Forms.ListView();  
        richTextBox1 = new System.Windows.Forms.RichTextBox();  
        splitContainer2 = new System.Windows.Forms.SplitContainer();  
        splitContainer1 = new System.Windows.Forms.SplitContainer();  
  
        // Insert code here to hook up event methods.  
  
        // Set properties of TreeView control.  
        treeView1.Dock = System.Windows.Forms.DockStyle.Fill;  
        treeView1.TabIndex = 0;  
        treeView1.Nodes.Add("treeView");  
  
        // Set properties of ListView control.  
        listView1.Dock = System.Windows.Forms.DockStyle.Top;  
        listView1.TabIndex = 2;  
        listView1.Items.Add("listView");  
  
        // Set properties of RichTextBox control.  
        richTextBox1.Dock = System.Windows.Forms.DockStyle.Fill;  
        richTextBox1.TabIndex = 3;  
        richTextBox1.Text = "richTextBox1";  
  
        // Set properties of first SplitContainer control.  
        splitContainer1.Dock = System.Windows.Forms.DockStyle.Fill;  
        splitContainer2.TabIndex = 1;  
        splitContainer2.SplitterWidth = 4;  
        splitContainer2.SplitterDistance = 150;  
        splitContainer2.Orientation = Orientation.Horizontal;  
        splitContainer2.Panel1.Controls.Add(this.listView1);  
        splitContainer2.Panel1.Controls.Add(this.richTextBox1);  
  
        // Set properties of second SplitContainer control.  
        splitContainer2.Dock = System.Windows.Forms.DockStyle.Fill;  
        splitContainer2.TabIndex = 4;  
        splitContainer2.SplitterWidth = 4;  
        splitContainer2.SplitterDistance = 100;  
        splitContainer2.Panel1.Controls.Add(this.treeView1);  
        splitContainer2.Panel1.Controls.Add(this.splitContainer1);  
  
        // Add the main SplitContainer control to the form.  
        this.Controls.Add(this.splitContainer2);  
        this.Text = "Intricate UI Example";  
    }  
  
    ```  
  
3.  In [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] aggiungere una chiamata alla procedura appena creata nella procedura `New()`.  In [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] aggiungere questa riga di codice al costruttore per la classe del form.  
  
    ```vb  
    ' Add this to the New procedure.  
    CreateOutlookUI()  
  
    ```  
  
    ```csharp  
    // Add this to the form class's constructor.  
    createOutlookUI();  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.SplitContainer>   
 [Controllo SplitContainer](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)   
 [Procedura: creare un'interfaccia utente a più riquadri con Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/create-a-multipane-user-interface-with-wf-using-the-designer.md)