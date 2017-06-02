---
title: "Procedura: aggiungere un MenuStrip a una finestra padre MDI (Windows Form) | Microsoft Docs"
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
  - "MDI, unione di voci di menu"
  - "MenuStrip (controllo) [Windows Form], aggiunta"
  - "MenuStrip (controllo) [Windows Form], unione"
ms.assetid: ab70c936-b452-4653-b417-17be57bb795b
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: aggiungere un MenuStrip a una finestra padre MDI (Windows Form)
In alcune applicazioni, il tipo di una finestra figlio di interfaccia a documenti multipli \(MDI, Multiple Document Interface\) può essere diverso dalla finestra padre MDI.  Ad esempio, il padre MDI potrebbe essere un foglio di calcolo, mentre il figlio MDI potrebbe essere un grafico.  In tal caso, è consigliabile aggiornare il contenuto del menu del padre MDI con il contenuto del menu del figlio MDI in quanto vengono attivate finestre figlio MDI di tipi diversi.  
  
 La procedura seguente usa la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A>, <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>, <xref:System.Windows.Forms.MergeAction>, e <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> per aggiungere il menu del figlio MDI al menu del padre MDI.  Chiudere la finestra figlio MDI rimuove il menu aggiunto dall'elemento padre MDI.  
  
 Vedere anche [Applicazioni MDI \(Interfaccia a documenti multipli, Multiple\-Document Interface\)](http://msdn.microsoft.com/library/xyhh2e7e\(v=vs.110\)).  
  
### Per aggiungere una voce di menu a un padre MDI  
  
1.  Creare un form e impostarne la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A> su `true`.  
  
2.  Aggiungere <xref:System.Windows.Forms.MenuStrip> a `Form1` e impostare la proprietà <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> di <xref:System.Windows.Forms.MenuStrip> su `true`.  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Visible%2A> di `Form1`<xref:System.Windows.Forms.MenuStrip> su `false`.  
  
4.  Aggiungere una voce di menu di primo livello a `Form1`<xref:System.Windows.Forms.MenuStrip> e impostare la relativa proprietà <xref:System.Windows.Forms.Control.Text%2A> su `&File`.  
  
5.  Aggiungere una voce del sottomenu alla voce di menu `&File` e impostare la relativa proprietà <xref:System.Windows.Forms.Form.Text%2A> su `&Open`.  
  
6.  Aggiungere un form al progetto, aggiungere <xref:System.Windows.Forms.MenuStrip> al form e impostare la proprietà <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> del `Form2`<xref:System.Windows.Forms.MenuStrip> su `true`.  
  
7.  Aggiungere una voce di menu di primo livello a `Form2`<xref:System.Windows.Forms.MenuStrip> e impostare la relativa proprietà <xref:System.Windows.Forms.Form.Text%2A> su `&Special`.  
  
8.  Aggiungere due voci di sottomenu alla voce di menu `&Special` e impostare le relative proprietà <xref:System.Windows.Forms.Form.Text%2A> su `Command&1` e `Command&2`, rispettivamente.  
  
9. Impostare la proprietà <xref:System.Windows.Forms.MergeAction> delle voci di menu `&Special`, `Command&1` e `Command&2` su <xref:System.Windows.Forms.MergeAction>.  
  
10. Creare un gestore eventi per l'evento <xref:System.Windows.Forms.Control.Click> di `&New`<xref:System.Windows.Forms.ToolStripMenuItem>.  
  
11. Nel gestore eventi inserire codice simile all'esempio di codice riportato di seguito per creare e visualizzare nuove istanze di `Form2` come finestre figlio MDI di `Form1`.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
  
    ```  
  
     \[C\#\]  
  
    ```  
    private void openToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
  
    ```  
  
12. Inserire codice analogo al seguente esempio di codice nel `&Open`<xref:System.Windows.Forms.ToolStripMenuItem> per registrare il gestore eventi.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles openToolStripMenuItem.Click  
  
    ```  
  
    ```csharp  
    this.openToolStripMenuItem.Click += new System.EventHandler(this.openToolStripMenuItem_Click);  
  
    ```  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Due controlli <xref:System.Windows.Forms.Form> denominati `Form1` e `Form2`.  
  
-   Un controllo <xref:System.Windows.Forms.MenuStrip> su `Form1` denominato `menuStrip1` e un controllo <xref:System.Windows.Forms.MenuStrip> su `Form2` denominato `menuStrip2`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.