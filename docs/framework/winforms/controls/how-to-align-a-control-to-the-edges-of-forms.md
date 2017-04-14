---
title: "Procedura: allineare un controllo ai bordi dei form | Microsoft Docs"
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
  - "controlli [Windows Form], allineamento nei form"
  - "controlli personalizzati [Windows Form], ancoraggio mediante il codice"
  - "Dock (proprietà), allineamento di controlli (mediante il codice)"
  - "form, allineamento di controlli"
ms.assetid: 5994cb59-242b-4e75-bd0e-62879c34d702
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: allineare un controllo ai bordi dei form
È possibile allineare un controllo al bordo dei form impostando la proprietà <xref:System.Windows.Forms.Control.Dock%2A> che designa la posizione del controllo nel form.  La proprietà <xref:System.Windows.Forms.Control.Dock%2A> può essere impostata su uno dei valori riportati di seguito:  
  
|Impostazione|Effetto sul controllo|  
|------------------|---------------------------|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato alla parte inferiore del form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo occupa tutto lo spazio rimanente nel form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato al lato sinistro del form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo non viene ancorato e viene visualizzato nella posizione specificata dalla relativa proprietà <xref:System.Windows.Forms.Control.Location%2A>.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato al lato destro del form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato alla parte superiore del form.|  
  
 È disponibile supporto in fase di progettazione per questa funzionalità in Visual Studio.  
  
### Per impostare la proprietà Dock del controllo in fase di esecuzione  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Control.Dock%2A> sul valore appropriato nel codice.  
  
    ```vb  
    ' To set the Dock property internally.  
    Me.Dock = DockStyle.Top  
    ' To set the Dock property from another object.  
    UserControl1.Dock = DockStyle.Top  
    ```  
  
    ```csharp  
    // To set the Dock property internally.  
    this.Dock = DockStyle.Top;  
    // To set the Dock property from another object.  
    UserControl1.Dock = DockStyle.Top;  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=fullName>   
 [Sviluppo di controlli Windows Form personalizzati con .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [Procedura: ancorare e agganciare controlli figlio in un controllo FlowLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control.md)   
 [Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [Cenni preliminari sulla proprietà AutoSize](../../../../docs/framework/winforms/controls/autosize-property-overview.md)