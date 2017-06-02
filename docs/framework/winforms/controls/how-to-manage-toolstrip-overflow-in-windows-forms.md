---
title: "Procedura: gestire l&#39;overflow di ToolStrip in Windows Form | Microsoft Docs"
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
  - "CanOverflow (proprietà)"
  - "esempi [Windows Form], barre degli strumenti"
  - "Overflow (proprietà)"
  - "barre degli strumenti [Windows Form], gestione degli overflow"
  - "ToolStrip (controllo) [Windows Form], gestione degli overflow"
ms.assetid: fa10e0ad-4cbf-4c0d-9082-359c2f855d4e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: gestire l&#39;overflow di ToolStrip in Windows Form
Quando non tutti gli elementi di un controllo <xref:System.Windows.Forms.ToolStrip> rientrano nello spazio disponibile, è possibile attivare la funzionalità di overflow nel controllo <xref:System.Windows.Forms.ToolStrip> e determinare il comportamento di overflow di specifici oggetti <xref:System.Windows.Forms.ToolStripItem>.  
  
 Quando si aggiungono oggetti <xref:System.Windows.Forms.ToolStripItem> che richiedono più spazio di quello reso disponibile nel controllo <xref:System.Windows.Forms.ToolStrip> in funzione delle dimensioni correnti del form, viene visualizzato automaticamente un oggetto <xref:System.Windows.Forms.ToolStripOverflowButton> sul controllo <xref:System.Windows.Forms.ToolStrip>.  Alla visualizzazione dell'oggetto <xref:System.Windows.Forms.ToolStripOverflowButton> gli elementi per cui è attivato l'overflow vengono spostati nel menu di espansione.  Ciò consente di personalizzare gli elementi <xref:System.Windows.Forms.ToolStrip> e di definire una priorità per il modo in cui si adattano alle varie dimensioni dei form.  È inoltre possibile modificare l'aspetto degli elementi quando incorrono nell'overflow utilizzando le proprietà <xref:System.Windows.Forms.ToolStripItem.Placement%2A> e <xref:System.Windows.Forms.ToolStripOverflow.DisplayedItems%2A?displayProperty=fullName> e l'evento <xref:System.Windows.Forms.ToolStrip.LayoutCompleted>.  Se si ingrandisce il form in fase di progettazione o di esecuzione, più oggetti <xref:System.Windows.Forms.ToolStripItem> possono essere visualizzati sul controllo <xref:System.Windows.Forms.ToolStrip> principale e l'oggetto <xref:System.Windows.Forms.ToolStripOverflowButton> potrebbe addirittura risultare visibile solo quando le dimensioni del form vengono ridotte.  
  
### Per attivare l'overflow in un controllo ToolStrip  
  
-   Verificare che la proprietà <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> non sia impostata su `false` per il controllo <xref:System.Windows.Forms.ToolStrip>.  Il valore predefinito è `True`.  
  
     Quando la proprietà <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A> è impostata su `True` \(il valore predefinito\), viene inviata una classe <xref:System.Windows.Forms.ToolStripItem> al menu di espansione nel caso in cui il contenuto dell'oggetto <xref:System.Windows.Forms.ToolStripItem> superi la larghezza di un controllo <xref:System.Windows.Forms.ToolStrip> orizzontale o l'altezza di un controllo <xref:System.Windows.Forms.ToolStrip> verticale.  
  
### Per specificare il comportamento di overflow di una classe ToolStripItem specifica  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> della classe <xref:System.Windows.Forms.ToolStripItem> sul valore desiderato.  I valori possibili sono `Always`, `Never` e `AsNeeded`.  l'impostazione predefinitaviene  `AsNeeded`.  
  
    ```vb  
    toolStripTextBox1.Overflow = _  
    System.Windows.Forms.ToolStripItemOverflow.Never  
  
    ```  
  
    ```csharp  
    toolStripTextBox1.Overflow = _  
    System.Windows.Forms.ToolStripItemOverflow.Never;  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripOverflowButton>   
 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A>   
 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [Architettura del controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [Riepilogo della tecnologia ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)