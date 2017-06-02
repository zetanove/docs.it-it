---
title: "Walkthrough: Performing a Drag-and-Drop Operation in Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Windows Forms, drag and drop operations"
  - "drag and drop, Windows Forms"
ms.assetid: eb66f6bf-4a7d-4c2d-b276-40fefb2d3b6c
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Walkthrough: Performing a Drag-and-Drop Operation in Windows Forms
Per eseguire operazioni di trascinamento all'interno di applicazioni per Windows è necessario gestire una serie di eventi, in particolare gli eventi <xref:System.Windows.Forms.Control.DragEnter>, <xref:System.Windows.Forms.Control.DragLeave> e <xref:System.Windows.Forms.Control.DragDrop>.  Utilizzando le informazioni disponibili negli argomenti event di questi eventi, è possibile semplificare le operazioni di trascinamento.  
  
## Trascinamento di dati  
 Tutte le operazioni di trascinamento degli elementi selezionati iniziano con il trascinamento.  La funzionalità che consente di raccogliere i dati all'inizio dell'operazione di trascinamento è implementata nel metodo <xref:System.Windows.Forms.Control.DoDragDrop%2A>.  
  
 Nell'esempio che segue viene utilizzato l'evento <xref:System.Windows.Forms.Control.MouseDown> per avviare l'operazione di trascinamento. Si tratta infatti del metodo più intuitivo, dato che la maggior parte delle operazioni di trascinamento degli elementi selezionati iniziano con la pressione del pulsante del mouse.  È necessario tuttavia ricordare che per avviare una routine di trascinamento è possibile utilizzare qualsiasi evento.  
  
> [!NOTE]
>  Alcuni controlli dispongono di eventi personalizzati per il trascinamento.  I controlli <xref:System.Windows.Forms.ListView> e <xref:System.Windows.Forms.TreeView>, ad esempio, dispongono di un evento <xref:System.Windows.Forms.TreeView.ItemDrag>.  
  
#### Per iniziare un'operazione di trascinamento  
  
1.  in <xref:System.Windows.Forms.Control.MouseDown>l'evento per il controllo in cui inizia il trascinamento, viene utilizzato  `DoDragDrop` il metodo per impostare i dati da trascinare e l'effetto consentito.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.DragEventArgs.Data%2A> e <xref:System.Windows.Forms.DragEventArgs.AllowedEffect%2A>.  
  
     Nell'esempio che segue viene illustrato come iniziare un'operazione di trascinamento.  Il controllo in cui inizia il trascinamento è un controllo <xref:System.Windows.Forms.Button>, i dati trascinati corrispondono alla stringa che rappresenta la proprietà <xref:System.Windows.Forms.Control.Text%2A> del controllo <xref:System.Windows.Forms.Button> e gli effetti consentiti sono la copia o lo spostamento.  
  
    ```vb  
    Private Sub Button1_MouseDown(ByVal sender As Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles Button1.MouseDown  
       Button1.DoDragDrop(Button1.Text, DragDropEffects.Copy Or DragDropEffects.Move)  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_MouseDown(object sender,   
    System.Windows.Forms.MouseEventArgs e)  
    {  
       button1.DoDragDrop(button1.Text, DragDropEffects.Copy |   
          DragDropEffects.Move);  
    }  
  
    ```  
  
    > [!NOTE]
    >  Come parametro per il metodo `DoDragDrop` è possibile utilizzare qualsiasi dato. Nell'esempio precedente, la proprietà <xref:System.Windows.Forms.Control.Text%2A> del controllo <xref:System.Windows.Forms.Button> è utilizzata \(al posto della specificazione a livello di codice di un valore o del recupero di dati da un set di dati\) in quanto la proprietà era correlata alla posizione di origine del trascinamento \(il controllo <xref:System.Windows.Forms.Button>\).  È importante tenere presente tali aspetti durante l'inserimento delle operazioni di trascinamento nelle applicazioni per Windows.  
  
 Durante l'esecuzione di un'operazione di trascinamento è possibile gestire l'evento <xref:System.Windows.Forms.Control.QueryContinueDrag> che richiede al sistema l'autorizzazione a proseguire l'operazione di trascinamento.  Quando si gestisce questo metodo è inoltre opportuno chiamare i metodi che avranno effetto sull'operazione di trascinamento, ad esempio ampliando un controllo <xref:System.Windows.Forms.TreeNode> in un controllo <xref:System.Windows.Forms.TreeView> quando il cursore si sposta sopra di esso.  
  
## Rilascio dei dati  
 Una volta iniziato il trascinamento dei dati da una posizione in un Windows Form o da un controllo, è possibile rilasciare i dati nel punto desiderato.  Il puntatore assume un aspetto diverso quando viene spostato su un'area di un form o su un controllo appropriatamente configurato per il rilascio dei dati.  È possibile utilizzare qualsiasi area all'interno di un Windows Form o qualsiasi controllo per il rilascio di dati impostando la proprietà <xref:System.Windows.Forms.Control.AllowDrop%2A> e gestendo gli eventi <xref:System.Windows.Forms.Control.DragEnter> e <xref:System.Windows.Forms.Control.DragDrop>.  
  
#### Per rilasciare i dati  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Control.AllowDrop%2A> su true.  
  
2.  Nell'evento `DragEnter` per il controllo in cui rilasciare i dati, assicurarsi che il tipo dei dati trascinati sia accettabile \(in questo caso, <xref:System.Windows.Forms.Control.Text%2A>\).  Nel codice, l'effetto associato al rilascio verrà quindi impostato su un valore dell'enumerazione <xref:System.Windows.Forms.DragDropEffects>.  Per ulteriori informazioni, vedere <xref:System.Windows.Forms.DragEventArgs.Effect%2A>.  
  
    ```vb  
    Private Sub TextBox1_DragEnter(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragEnter  
       If (e.Data.GetDataPresent(DataFormats.Text)) Then  
         e.Effect = DragDropEffects.Copy  
       Else  
         e.Effect = DragDropEffects.None  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_DragEnter(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       if (e.Data.GetDataPresent(DataFormats.Text))   
          e.Effect = DragDropEffects.Copy;  
       else  
          e.Effect = DragDropEffects.None;  
    }  
  
    ```  
  
    > [!NOTE]
    >  È possibile definire una classe <xref:System.Windows.Forms.DataFormats> personalizzata specificando un oggetto personalizzato come parametro <xref:System.Object> del metodo <xref:System.Windows.Forms.DataObject.SetData%2A>.  Durante questa operazione, assicurarsi sempre che l'oggetto specificato sia serializzabile.  Per ulteriori informazioni, vedere [Interfaccia ISerializable](frlrfSystemRuntimeSerializationISerializableClassTopic).  
  
3.  Nell'evento <xref:System.Windows.Forms.Control.DragDrop> per il controllo sul quale si intendono rilasciare gli elementi selezionati, utilizzare il metodo <xref:System.Windows.Forms.DataObject.GetData%2A> per recuperare i dati trascinati.  Per ulteriori informazioni, vedere: [Proprietà DtaObject.Data](frlrfSystemSecurityCryptographyXmlDataObjectClassDataTopic).  
  
     Nell'esempio che segue il controllo sul quale vengono trascinati gli elementi è <xref:System.Windows.Forms.TextBox>.  Nel codice, la proprietà <xref:System.Windows.Forms.Control.Text%2A> del controllo <xref:System.Windows.Forms.TextBox> viene impostata su un valore equivalente ai dati trascinati.  
  
    ```vb  
    Private Sub TextBox1_DragDrop(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragDrop  
       TextBox1.Text = e.Data.GetData(DataFormats.Text).ToString  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_DragDrop(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       textBox1.Text = e.Data.GetData(DataFormats.Text).ToString();  
    }  
  
    ```  
  
    > [!NOTE]
    >  È inoltre possibile utilizzare la proprietà <xref:System.Windows.Forms.DragEventArgs.KeyState%2A> in modo che, in base ai tasti premuti durante l'operazione di trascinamento, si verifichi un determinato effetto. Ad esempio, è consuetudine eseguire una copia dei dati trascinati quando viene premuto il tasto CTRL.  
  
## Vedere anche  
 [How to: Add Data to the Clipboard](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)   
 [How to: Retrieve Data from the Clipboard](../../../../docs/framework/winforms/advanced/how-to-retrieve-data-from-the-clipboard.md)   
 [Drag\-and\-Drop Operations and Clipboard Support](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)