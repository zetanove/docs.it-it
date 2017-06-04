---
title: "Procedura: inserire un MenuStrip in un menu a discesa MDI (Windows Form) | Microsoft Docs"
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
  - "MenuStrip (controllo) [Windows Form], inserimento"
  - "MenuStrip (controllo) [Windows Form], unione"
ms.assetid: 0fad444e-26d9-49af-8860-044d9c10d608
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: inserire un MenuStrip in un menu a discesa MDI (Windows Form)
In alcune applicazioni il tipo di una finestra figlio MDI \(Multiple Document Interface, interfaccia a documenti multipli\) può essere diverso dalla finestra padre MDI.  La finestra padre MDI, ad esempio, potrebbe essere un foglio di lavoro mentre la finestra figlio MDI un grafico.  In tal caso è necessario aggiornare il contenuto del menu del padre MDI con quello del menu del figlio MDI in quanto sono attivate finestre figlio MDI di tipi diversi.  
  
 Nella procedura seguente vengono utilizzate le proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A>, <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A>, <xref:System.Windows.Forms.MergeAction> e <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> per inserire un gruppo di voci di menu dal menu del figlio MDI alla parte a discesa del menu del padre MDI.  Se la finestra figlio MDI viene chiusa, le voci di menu inserite nel padre MDI vengono eliminate.  
  
### Per inserire un MenuStrip in un menu a discesa MDI  
  
1.  Creare un form e impostarne la proprietà <xref:System.Windows.Forms.Form.IsMdiContainer%2A> su `true`.  
  
2.  Aggiungere una classe <xref:System.Windows.Forms.MenuStrip> a `Form1` e impostare la proprietà <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> di <xref:System.Windows.Forms.MenuStrip> su `true`.  
  
3.  Aggiungere una voce di menu di primo livello alla classe <xref:System.Windows.Forms.MenuStrip> di `Form1` e impostarne la proprietà <xref:System.Windows.Forms.Control.Text%2A> su `&File`.  
  
4.  Aggiungere tre voci di sottomenu alla voce di menu `&File` e impostare le relative proprietà <xref:System.Windows.Forms.ToolStripItem.Text%2A> su `&Open`, `&Import from` e `E&xit`.  
  
5.  Aggiungere due voci di sottomenu alla voce di sottomenu `&Import from` e impostare le relative proprietà <xref:System.Windows.Forms.ToolStripItem.Text%2A> su `&Word` e `&Excel`.  
  
6.  Aggiungere un form al progetto, aggiungere una classe <xref:System.Windows.Forms.MenuStrip> al form e impostare la proprietà <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> del <xref:System.Windows.Forms.MenuStrip> di `Form2` su `true`.  
  
7.  Aggiungere una voce di menu di primo livello alla classe <xref:System.Windows.Forms.MenuStrip> di `Form2` e impostare la relativa proprietà <xref:System.Windows.Forms.ToolStripItem.Text%2A> su `&File`.  
  
8.  Aggiungere voci di sottomenu al menu `&File` di `Form2` nell'ordine seguente: una classe <xref:System.Windows.Forms.ToolStripSeparator>, `&Save`, `&Close` `and Save` e un'altra classe <xref:System.Windows.Forms.ToolStripSeparator>.  
  
9. Impostare le proprietà <xref:System.Windows.Forms.MergeAction> e <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> delle voci di menu di `Form2` come indicato nella tabella seguente.  
  
    |Voce di menu di Form2|Valore di MergeAction|Valore di MergeIndex|  
    |---------------------------|---------------------------|--------------------------|  
    |File|MatchOnly|\-1|  
    |Separatore|Insert|2|  
    |Salva|Insert|3|  
    |Save and Close|Insert|4|  
    |Separatore|Insert|5|  
  
10. Creare un gestore eventi per l'evento <xref:System.Windows.Forms.Control.Click> della classe <xref:System.Windows.Forms.ToolStripMenuItem> di `&Open`.  
  
11. All'interno del gestore eventi inserire codice simile a quello dell'esempio riportato di seguito per creare e visualizzare nuove istanze di `Form2` come istanze figlio MDI di `Form1`.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(ByVal sender As System.Object, _  
    ByVal e As System.EventArgs) Handles openToolStripMenuItem.Click  
        Dim NewMDIChild As New Form2()  
        'Set the parent form of the child window.  
            NewMDIChild.MdiParent = Me  
        'Display the new form.  
            NewMDIChild.Show()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void openToolStripMenuItem_Click(object sender, EventArgs e)  
    {  
        Form2 newMDIChild = new Form2();  
        // Set the parent form of the child window.  
            newMDIChild.MdiParent = this;  
        // Display the new form.  
            newMDIChild.Show();  
    }  
  
    ```  
  
12. Inserire codice analogo a quello dell'esempio seguente nella classe <xref:System.Windows.Forms.ToolStripMenuItem> di `&Open` per registrare il gestore eventi.  
  
    ```vb  
    Private Sub openToolStripMenuItem_Click(sender As Object, e As _  
    EventArgs) Handles openToolStripMenuItem.Click  
  
    ```  
  
    ```csharp  
    this.openToolStripMenuItem.Click += new System.EventHandler(this.openToolStripMenuItem_Click);  
  
    ```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Due controlli <xref:System.Windows.Forms.Form> denominati `Form1` e `Form2`.  
  
-   Un controllo <xref:System.Windows.Forms.MenuStrip> nel controllo `Form1` denominato `menuStrip1` e un controllo <xref:System.Windows.Forms.MenuStrip> nel controllo `Form2` denominato `menuStrip2`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 [Procedura: creare form padre MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [Procedura: creare form figlio MDI](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)