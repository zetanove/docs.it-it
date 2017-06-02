---
title: "Procedura: creare un elenco di finestre MDI con MenuStrip (Windows Form) | Microsoft Docs"
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
  - "MDI, creazione di elenchi di finestre"
  - "MenuStrip (controllo) [Windows Form], creazione di elenchi di finestre"
ms.assetid: 04fb414b-811f-4a83-aab6-b4a24646dec5
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: creare un elenco di finestre MDI con MenuStrip (Windows Form)
Per creare applicazioni in cui è possibile aprire vari documenti contemporaneamente e copiare e incollare contenuto da un documento all'altro, utilizzare l'interfaccia a documenti multipli \(MDI, Multiple Document Interface\).  
  
 In questa procedura viene illustrato come creare un elenco di tutti i form figlio attivi nel menu Finestra del padre.  
  
### Per creare un elenco di finestre MDI con MenuStrip  
  
1.  Creare un form e impostarne la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A> su `true`.  
  
2.  Aggiungere una classe <xref:System.Windows.Forms.MenuStrip> al form.  
  
3.  Aggiungere due voci di menu di primo livello a <xref:System.Windows.Forms.MenuStrip> e impostare le relative proprietà <xref:System.Windows.Forms.Control.Text%2A> su `&File` e `&Window`.  
  
4.  Aggiungere una voce di sottomenu alla voce di menu `&File` e impostare la relativa proprietà <xref:System.Windows.Forms.ToolStripItem.Text%2A> su `&Open`.  
  
5.  impostare <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> proprietà di  <xref:System.Windows.Forms.MenuStrip> in  `&Window`<xref:System.Windows.Forms.ToolStripMenuItem>.  
  
6.  Aggiungere un form al progetto e aggiungervi il controllo desiderato, ad esempio un'altra classe <xref:System.Windows.Forms.MenuStrip>.  
  
7.  creare un gestore eventi per <xref:System.Windows.Forms.Control.Click> evento di  `&New`<xref:System.Windows.Forms.ToolStripMenuItem>.  
  
8.  All'interno del gestore eventi inserire codice simile al seguente per creare e visualizzare nuove istanze di `Form2` come finestre figlio MDI di `Form1`:  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As _  
    System.Object, ByVal e As System.EventArgs) Handles _  
    openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
  
    ```  
  
     \[C\#\]  
  
    ```  
    private void newToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
  
    ```  
  
9. Codice del posto come quanto segue in `&New`<xref:System.Windows.Forms.ToolStripMenuItem> per registrare il gestore eventi.  
  
    ```vb  
    Private Sub newToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles newToolStripMenuItem.Click  
  
    ```  
  
    ```csharp  
    this.newToolStripMenuItem.Click += new System.EventHandler(this.newToolStripMenuItem_Click);  
  
    ```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Due controlli <xref:System.Windows.Forms.Form> denominati `Form1` e `Form2`.  
  
-   Un controllo <xref:System.Windows.Forms.MenuStrip> nel controllo `Form1` denominato `menuStrip1` e un controllo <xref:System.Windows.Forms.MenuStrip> nel controllo `Form2` denominato `menuStrip2`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 [Procedura: creare form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [Procedura: creare form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [Controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)