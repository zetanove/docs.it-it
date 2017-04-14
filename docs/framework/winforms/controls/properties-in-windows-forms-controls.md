---
title: "Propriet&#224; dei controlli Windows Form | Microsoft Docs"
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
  - "controlli [Windows Form], proprietà"
  - "controlli personalizzati [Windows Form], cenni preliminari delle proprietà (mediante il codice)"
  - "proprietà [Windows Form]"
ms.assetid: 2785279b-fb57-4937-8f6b-2050e475db6f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Propriet&#224; dei controlli Windows Form
Un controllo Windows Form eredita molte proprietà dalla classe base <xref:System.Windows.Forms.Control?displayProperty=fullName>.  Sono incluse proprietà come <xref:System.Windows.Forms.Control.Font%2A>, <xref:System.Windows.Forms.Control.ForeColor%2A>, <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.Bounds%2A>, <xref:System.Windows.Forms.Control.ClientRectangle%2A>, <xref:System.Windows.Forms.Control.DisplayRectangle%2A>, <xref:System.Windows.Forms.Control.Enabled%2A>, <xref:System.Windows.Forms.Control.Focused%2A>, <xref:System.Windows.Forms.Control.Height%2A>, <xref:System.Windows.Forms.Control.Width%2A>, <xref:System.Windows.Forms.Control.Visible%2A>, <xref:System.Windows.Forms.Control.AutoSize%2A> e molte altre.  Per ulteriori informazioni sulle proprietà ereditate, vedere <xref:System.Windows.Forms.Control?displayProperty=fullName>.  
  
 È possibile eseguire l'override delle proprietà ereditate dal controllo nonché definirne di nuove.  
  
## In questa sezione  
 [Definizione di una proprietà](../../../../docs/framework/winforms/controls/defining-a-property-in-windows-forms-controls.md)  
 Viene illustrato come implementare una proprietà per un controllo o un componente personalizzato e come integrare la proprietà nell'ambiente di progettazione.  
  
 [Definizione dei valori predefiniti utilizzando i metodi ShouldSerialize e Reset](../../../../docs/framework/winforms/controls/defining-default-values-with-the-shouldserialize-and-reset-methods.md)  
 Viene illustrato come definire valori di proprietà predefiniti per un controllo o un componente personalizzato.  
  
 [Eventi per proprietà modificate](../../../../docs/framework/winforms/controls/property-changed-events.md)  
 Viene descritto come attivare le notifiche di modifiche alle proprietà quando un valore di una proprietà viene modificato.  
  
 [Procedura: esporre le proprietà dei controlli costitutivi](../../../../docs/framework/winforms/controls/how-to-expose-properties-of-constituent-controls.md)  
 Viene illustrato come esporre le proprietà dei controlli che fanno parte di un controllo composito personalizzato.  
  
 [Implementazione dei metodi nei controlli personalizzati](../../../../docs/framework/winforms/controls/method-implementation-in-custom-controls.md)  
 Viene descritto come implementare metodi nei controlli e nei componenti personalizzati.  
  
## Riferimenti  
 <xref:System.Windows.Forms.UserControl>  
 Viene descritta la classe base per l'implementazione dei controlli compositi.  
  
 <xref:System.ComponentModel.TypeConverterAttribute>  
 Viene descritto l'attributo che specifica la classe <xref:System.ComponentModel.TypeConverter> da utilizzare per un tipo di proprietà personalizzato.  
  
 <xref:System.ComponentModel.EditorAttribute>  
 Viene descritto l'attributo che specifica la classe <xref:System.Drawing.Design.UITypeEditor> da utilizzare per una proprietà personalizzata.  
  
## Sezioni correlate  
 [Attributi nei controlli Windows Form](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)  
 Vengono descritti gli attributi applicabili alle proprietà o ad altri membri dei controlli e dei componenti personalizzati.  
  
 [Design\-Time Attributes for Components](../Topic/Design-Time%20Attributes%20for%20Components.md)  
 Vengono elencati attributi di metadati da applicare a componenti e controlli in modo che vengano visualizzati correttamente in fase di progettazione nelle finestre di progettazione visive.  
  
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)  
 Viene descritto come implementare classi, quali editor e finestre di progettazione, che forniscono supporto in fase di progettazione.