---
title: "Procedura: abilitare il completamento automatico nei controlli ToolStrip Windows Form | Microsoft Docs"
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
  - "AutoComplete, abilitazione nelle barre degli strumenti"
  - "AutoComplete, esempi"
  - "esempi [Windows Form], barre degli strumenti"
  - "barre degli strumenti [Windows Form], AutoComplete"
  - "ToolStrip (controllo) [Windows Form], AutoComplete"
  - "ToolStripComboBox (classe), esempi"
ms.assetid: fd66d085-1af1-45d4-930a-cde944da2e16
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: abilitare il completamento automatico nei controlli ToolStrip Windows Form
Nella procedura riportata di seguito vengono combinate una classe <xref:System.Windows.Forms.ToolStripLabel> e una classe <xref:System.Windows.Forms.ToolStripComboBox> che è possibile selezionare per visualizzare un elenco a discesa di elementi, come ad esempio i siti Web visitati di recente.  Se l'utente digita un carattere che corrisponde al primo carattere di uno degli elementi in elenco, l'elemento viene visualizzato immediatamente.  
  
> [!NOTE]
>  Il completamento automatico funziona con i controlli `ToolStrip` nello stesso modo in cui funziona con controlli tradizionali quali <xref:System.Windows.Forms.ComboBox> e <xref:System.Windows.Forms.TextBox>.  
  
### Per attivare il completamento automatico in un controllo ToolStrip  
  
1.  Creare un controllo <xref:System.Windows.Forms.ToolStrip> e aggiungervi elementi.  
  
    ```vb  
    ToolStrip1 = New System.Windows.Forms.ToolStrip  
    ToolStrip1.Items.AddRange(New System.Windows.Forms.ToolStripItem()_  
        {ToolStripLabel1, ToolStripComboBox1})  
    ```  
  
    ```csharp  
    toolStrip1 = new System.Windows.Forms.ToolStrip();  
    toolStrip1.Items.AddRange(new System.Windows.Forms.ToolStripItem[]   
        {toolStripLabel1, toolStripComboBox1});  
  
    ```  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> dell'etichetta e della casella combinata su <xref:System.Windows.Forms.ToolStripItemOverflow> affinché l'elenco sia sempre disponibile indipendentemente dalle dimensioni del form.  
  
    ```vb  
    ToolStripLabel1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    ToolStripComboBox1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    ```  
  
    ```csharp  
    toolStripLabel1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    toolStripComboBox1.Overflow = System.Windows.Forms.ToolStripItemOverflow.Never  
  
    ```  
  
3.  Aggiungere termini alla raccolta Items del controllo <xref:System.Windows.Forms.ToolStripComboBox>.  
  
    ```vb  
    ToolStripComboBox1.Items.AddRange(New Object() {"First Item", _  
        "Second Item", "Third Item"})  
  
    ```  
  
    ```csharp  
    toolStripComboBox1.Items.AddRange(new object[] {"First item", "Second item", "Third item"});  
  
    ```  
  
4.  Impostare la proprietà <xref:System.Windows.Forms.ComboBox.AutoCompleteMode%2A> della casella combinata su <xref:System.Windows.Forms.AutoCompleteMode>.  
  
    ```vb  
    ToolStripComboBox1.AutoCompleteMode = _  
        System.Windows.Forms.AutoCompleteMode.Append  
    ```  
  
    ```csharp  
    toolStripComboBox1.AutoCompleteMode = System.Windows.Forms.AutoCompleteMode.Append;  
  
    ```  
  
5.  Impostare la proprietà <xref:System.Windows.Forms.ComboBox.AutoCompleteSource%2A> della casella combinata su <xref:System.Windows.Forms.AutoCompleteSource>.  
  
    ```vb  
    ToolStripComboBox1.AutoCompleteSource = _  
        System.Windows.Forms.AutoCompleteSource.ListItems  
    ```  
  
    ```csharp  
    toolStripComboBox1.AutoCompleteSource = System.Windows.Forms.AutoCompleteSource.ListItems;  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripLabel>   
 <xref:System.Windows.Forms.ToolStripComboBox>   
 <xref:System.Windows.Forms.ToolStripComboBox.AutoCompleteMode%2A>   
 <xref:System.Windows.Forms.ToolStripComboBox.AutoCompleteSource%2A>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [Architettura del controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [Riepilogo della tecnologia ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)