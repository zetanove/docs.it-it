---
title: "Procedura: creare testo di dimensioni variabili in un controllo ComboBox | Microsoft Docs"
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
  - "caselle combinate, creazione di testo"
  - "ComboBox (controllo) [Windows Form], creazione di testo personalizzato"
  - "ComboBox (controllo) [Windows Form], esempi [C#]"
  - "esempi [Windows Form], ComboBox (controllo)"
  - "testo, creazione in caselle combinate"
ms.assetid: ce39b9ea-e626-49fe-bd5a-f567f6d157df
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare testo di dimensioni variabili in un controllo ComboBox
In questo esempio viene illustrato il disegno personalizzato di testo in un controllo <xref:System.Windows.Forms.ComboBox>.  Quando una voce soddisfa un determinato criterio, viene disegnata con tipi di carattere più grandi e visualizzata in rosso.  
  
## Esempio  
  
```vb  
Private Sub ComboBox1_MeasureItem(ByVal sender As Object, ByVal e As _  
System.Windows.Forms.MeasureItemEventArgs) Handles ComboBox1.MeasureItem  
    Dim bFont As New Font("Arial", 8, FontStyle.Bold)  
    Dim lFont As New Font("Arial", 12, FontStyle.Bold)  
    Dim siText As SizeF  
  
    If ComboBox1.Items().Item(e.Index) = "Two" Then  
        siText = e.Graphics.MeasureString(ComboBox1.Items().Item(e.Index), _  
lFont)  
    Else  
        siText = e.Graphics.MeasureString(ComboBox1.Items().Item(e.Index), bFont)  
    End If  
  
    e.ItemHeight = siText.Height  
    e.ItemWidth = siText.Width  
End Sub  
  
Private Sub ComboBox1_DrawItem(ByVal sender As Object, ByVal e As _  
System.Windows.Forms.DrawItemEventArgs) Handles ComboBox1.DrawItem  
    Dim g As Graphics = e.Graphics  
    Dim bFont As New Font("Arial", 8, FontStyle.Bold)  
    Dim lFont As New Font("Arial", 12, FontStyle.Bold)  
  
    If ComboBox1.Items().Item(e.Index) = "Two" Then  
        g.DrawString(ComboBox1.Items.Item(e.Index), lfont, Brushes.Red, _  
e.Bounds.X, e.Bounds.Y)  
    Else  
        g.DrawString(ComboBox1.Items.Item(e.Index), bFont, Brushes.Black, e.Bounds.X, e.Bounds.Y)  
    End If  
End Sub  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un Windows Form.  
  
-   Un controllo <xref:System.Windows.Forms.ComboBox> denominato  `ListBox1` con tre voci nella proprietà <xref:System.Windows.Forms.ComboBox.Items%2A>.  In questo esempio le tre voci vengono denominate  `"One", Two", and Three"`.  La proprietà <xref:System.Windows.Forms.ComboBox.DrawMode%2A> di  `ComboBox1` deve essere impostata su <xref:System.Windows.Forms.DrawMode>.  
  
    > [!NOTE]
    >  Questa tecnica è inoltre applicabile al controllo <xref:System.Windows.Forms.ListBox>. È possibile sostituire una classe <xref:System.Windows.Forms.ListBox> con <xref:System.Windows.Forms.ComboBox>.  
  
-   Riferimenti agli spazi dei nomi <xref:System.Windows.Forms?displayProperty=fullName> e <xref:System.Drawing?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ComboBox.DrawItem>   
 <xref:System.Windows.Forms.DrawItemEventArgs>   
 <xref:System.Windows.Forms.ComboBox.MeasureItem>   
 [Controlli con supporto incorporato per la creazione da parte del proprietario](../../../../docs/framework/winforms/controls/controls-with-built-in-owner-drawing-support.md)   
 [Controllo ListBox](../../../../docs/framework/winforms/controls/listbox-control-windows-forms.md)   
 [Controllo ComboBox](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md)