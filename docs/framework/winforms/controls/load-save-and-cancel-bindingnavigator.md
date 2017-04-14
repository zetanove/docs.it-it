---
title: "Procedura: aggiungere i pulsanti Carica, Salva e Annulla al controllo BindingNavigator di Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], modifica"
  - "Controllo BindingNavigator [Windows Form], aggiunta di pulsanti"
ms.assetid: faa33042-186e-4bb2-8798-17ceb987ec62
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: aggiungere i pulsanti Carica, Salva e Annulla al controllo BindingNavigator di Windows Form
<xref:System.Windows.Forms.BindingNavigator> è un controllo <xref:System.Windows.Forms.ToolStrip> specifico per lo spostamento e la modifica dei controlli nel form associati ai dati.  
  
 Dal momento che si tratta di un controllo <xref:System.Windows.Forms.ToolStrip>, il componente <xref:System.Windows.Forms.BindingNavigator> può facilmente essere modificato in modo da includere comandi aggiuntivi o alternativi per l'utente.  
  
 Nella procedura indicata di seguito, un controllo <xref:System.Windows.Forms.TextBox> viene associato ai dati e il controllo <xref:System.Windows.Forms.ToolStrip> aggiunto al form viene modificato in modo da includere i pulsanti di caricamento, salvataggio e annullamento.  
  
### Per aggiungere i pulsante di caricamento, salvataggio e annullamento al componente BindingNavigator  
  
1.  Aggiungere un controllo <xref:System.Windows.Forms.TextBox> al form.  
  
2.  Associarlo a <xref:System.Windows.Forms.BindingSource>, il quale è associato a un'origine dati.  In questo esempio, <xref:System.Windows.Forms.BindingSource> è associato a un database.  
  
3.  Una volta generato il dataset e il TableAdapter, trascinare un controllo <xref:System.Windows.Forms.BindingNavigator> nel form.  
  
4.  Impostare la proprietà <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> del controllo <xref:System.Windows.Forms.BindingNavigator> su <xref:System.Windows.Forms.BindingSource> nel form associato ai controlli.  
  
5.  Fare clic sul controllo <xref:System.Windows.Forms.BindingNavigator>.  
  
6.  Fare clic sull'icona dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) per visualizzare la finestra di dialogo **Attività BindingNavigator** e selezionare **Modifica elementi**.  
  
     Viene visualizzato l'**editor della raccolta Items**.  
  
7.  Nell'**editor della raccolta Items**, effettuare quando indicato di seguito.  
  
    1.  Aggiungere un <xref:System.Windows.Forms.ToolStripSeparator> e tre elementi <xref:System.Windows.Forms.ToolStripButton> selezionando il tipo appropriato di <xref:System.Windows.Forms.ToolStripItem> e facendo clic sul pulsante **Aggiungi**.  
  
    2.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Name%2A> dei pulsanti su `` LoadButton, `` SaveButton e `` CancelButton, rispettivamente.  
  
    3.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Text%2A> dei pulsanti su `` Load`,` Save e `` Cancel.  
  
    4.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> per ognuno dei pulsanti su `` Text.  In alternativa, è possibile impostare questa proprietà su `` Image `` o `` ImageAndText ``  e impostare l'immagine da visualizzare nella proprietà <xref:System.Windows.Forms.ToolStripItem.Image%2A>.  
  
    5.  Scegliere **OK** per chiudere la finestra di dialogo. I pulsanti vengono aggiunti a <xref:System.Windows.Forms.ToolStrip>.  
  
8.  Fare clic con il pulsante destro del mouse sul form, quindi scegliere **Visualizza codice**.  
  
9. Nell'editor di codice, trovare la riga di codice che carica i dati nel TableAdapter.  Il codice è stato generato quando è stata impostata l'associazione dati al passaggio 2.  Il codice dovrebbe risultare simile al seguente: `TableAdapterName.Fill(DataSetName.TableName)`.  Probabilmente sarà nell'evento <xref:System.Windows.Forms.Form.Load> del form.  
  
10. Creare un gestore per l'evento <xref:System.Windows.Forms.ToolStripItem.Click> di  `` **Load** `` <xref:System.Windows.Forms.ToolStripButton> creato in precedenza e spostarvi il codice di caricamento dati.  
  
     Il codice dovrebbe ora risultare simile al seguente:  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub LoadButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles LoadButton.Click  
        TableAdapterName.Fill(DataSetName.TableName)  
    End Sub  
    ```  
  
     \[C\#\]  
  
    ```  
    private void LoadButton_Click(System.Object sender,   
        System.EventArgs e)  
    {  
        TableAdapterName.Fill(DataSetName.TableName);  
    }  
    ```  
  
11. Creare un gestore per l'evento <xref:System.Windows.Forms.ToolStripItem.Click> di **Save** `` <xref:System.Windows.Forms.ToolStripButton> creato in precedenza e scrivere il codice per aggiornare i dati nella tabella a cui è associato il controllo.  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub SaveButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SaveButton.Click  
        TableAdapterName.Update(DataSetName.TableName)  
    End Sub  
    ```  
  
     \[C\#\]  
  
    ```  
    private void SaveButton_Click(System.Object sender,   
        System.EventArgs e)  
    {  
        TableAdapterName.Update(DataSetName.TableName);  
    }  
    ```  
  
    > [!NOTE]
    >  In alcuni casi, il componente <xref:System.Windows.Forms.BindingNavigator> disporrà già di un pulsante `` **Salva**, ma non è stato generato alcun codice da Progettazione Windows Form.  In tal caso, inserire il codice precedente nel gestore dell'evento <xref:System.Windows.Forms.ToolStripItem.Click> per tale pulsante invece di creare un pulsante completamente nuovo in <xref:System.Windows.Forms.ToolStrip>.  Tuttavia, il pulsante è disabilitato per impostazione predefinita e quindi è necessario impostare la proprietà <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> del pulsante su `true` affinché funzioni correttamente.  
  
12. Creare un gestore per l'evento <xref:System.Windows.Forms.ToolStripItem.Click> di  `` **Cancel** `` <xref:System.Windows.Forms.ToolStripButton> creato in precedenza e scrivere il codice per annullare le modifiche al record di dati visualizzato.  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub CancelButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CancelButton.Click  
        BindingSourceName.CancelEdit()  
    End Sub  
    ```  
  
     \[C\#\]  
  
    ```  
    private void CancelButton_Click(System.Object sender, System.EventArgs e)  
    {  
        BindingSourceName.CancelEdit();  
    }  
    ```  
  
    > [!NOTE]
    >  L'ambito del metodo <xref:System.Windows.Forms.BindingSource.CancelEdit%2A> è la riga di dati.  Salvare le modifiche apportate durante la visualizzazione del singolo record prima di procedere al successivo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.BindingNavigator>   
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.ToolStrip>   
 [Controllo BindingNavigator](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)   
 [Cenni preliminari sul componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component-overview.md)