---
title: "Procedura: modificare la spaziatura e l&#39;allineamento degli elementi ToolStrip in Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], barre degli strumenti"
  - "barre degli strumenti [Windows Form], allineamento di elementi"
  - "ToolStrip (controllo) [Windows Form], allineamento di elementi"
ms.assetid: cd483466-0f49-43df-addf-e2b5fcd64027
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: modificare la spaziatura e l&#39;allineamento degli elementi ToolStrip in Windows Form
Il controllo <xref:System.Windows.Forms.ToolStrip> supporta pienamente le funzionalità di layout come il ridimensionamento, la spaziatura di controlli <xref:System.Windows.Forms.ToolStripItem> relativi uno all'altro, la disposizione di controlli nel controllo <xref:System.Windows.Forms.ToolStrip> e la spaziatura di controlli rispetto a <xref:System.Windows.Forms.ToolStrip>.  
  
 Poiché il valore predefinito della proprietà <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> è `true`, i controlli vengono ridimensionati automaticamente, a meno che non si imposti la proprietà <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> su `false`.  
  
### Per ridimensionare manualmente un ToolStripItem  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> su `false` per il controllo associato.  
  
    ```vb  
    ToolStripButton1.AutoSize = False  
  
    ```  
  
    ```csharp  
    toolStripButton1.AutoSize = false;  
  
    ```  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Size%2A> nel modo desiderato per il controllo <xref:System.Windows.Forms.ToolStripItem> associato.  
  
### Per impostare la spaziatura di un ToolStripItem  
  
1.  Inserire i valori desiderati, in pixel, nella proprietà <xref:System.Windows.Forms.ToolStripItem.Margin%2A> del controllo associato.  
  
     I valori della proprietà <xref:System.Windows.Forms.ToolStripItem.Margin%2A> specificano la spaziatura tra l'elemento e quelli adiacenti nel seguente ordine: sinistra, alto, destra, basso.  
  
    ```vb  
    ToolStripTextBox1.Margin = New System.Windows.Forms.Padding _  
        (3, 0, 3, 0)  
  
    ```  
  
    ```csharp  
    toolStripTextBox1.Margin = new System.Windows.Forms.Padding   
        (3, 0, 3, 0);  
  
    ```  
  
### Per allineare un ToolStripItem al lato destro del ToolStrip  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> su <xref:System.Windows.Forms.ToolStripItemAlignment> per il controllo associato.  Poiché per impostazione predefinita la proprietà <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> è impostata su <xref:System.Windows.Forms.ToolStripItemAlignment>, i controlli sono allineati a sinistra del controllo <xref:System.Windows.Forms.ToolStrip>.  
  
    ```vb  
    ToolStripSplitButton1.Alignment = _  
        System.Windows.Forms.ToolStripItemAlignment.Right  
  
    ```  
  
    ```csharp  
    toolStripSplitButton1.Alignment =   
        System.Windows.Forms.ToolStripItemAlignment.Right;  
  
    ```  
  
### Per disporre elementi ToolStrip sul ToolStrip  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A> sul valore di <xref:System.Windows.Forms.ToolStripLayoutStyle> desiderato.  
  
    ```vb  
    ToolStripDropDown1.LayoutStyle = _  
        System.Windows.Forms.ToolStripLayoutStyle.Flow  
  
    ```  
  
    ```csharp  
    toolStripDropDown1.LayoutStyle =   
        System.Windows.Forms.ToolStripLayoutStyle.Flow;  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.Control.Layout>   
 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted>   
 <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A>   
 <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A>   
 <xref:System.Windows.Forms.ToolStripItem.Placement%2A>   
 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [Architettura del controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [Riepilogo della tecnologia ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)