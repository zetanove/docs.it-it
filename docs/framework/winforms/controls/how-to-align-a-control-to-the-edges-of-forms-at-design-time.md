---
title: "Procedura: allineare un controllo ai bordi dei form in fase di progettazione | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], ancoraggio (finestra di progettazione)"
  - "Dock (proprietà), allineamento dei controlli (finestra di progettazione)"
ms.assetid: 51f08998-5e3b-4330-be58-a4edd0eb60f4
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: allineare un controllo ai bordi dei form in fase di progettazione
È possibile allineare un controllo al bordo dei form impostando la proprietà <xref:System.Windows.Forms.Control.Dock%2A> che designa la posizione del controllo nel form.  La proprietà <xref:System.Windows.Forms.Control.Dock%2A> può essere impostata su uno dei valori riportati di seguito:  
  
|Impostazione|Effetto sul controllo|  
|------------------|---------------------------|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato alla parte inferiore del form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo occupa tutto lo spazio rimanente nel form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato al lato sinistro del form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo non viene ancorato e viene visualizzato nella posizione specificata dalla relativa proprietà <xref:System.Windows.Forms.Control.Location%2A>.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato al lato destro del form.|  
|<xref:System.Windows.Forms.DockStyle>|Il controllo viene ancorato alla parte superiore del form.|  
  
 Questi valori possono essere impostati anche nel codice.  Per ulteriori informazioni, vedere [Procedura: allineare un controllo ai bordi dei form](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per impostare la proprietà Dock del controllo in fase di progettazione  
  
1.  In Progettazione Windows Form selezionare il controllo.  
  
2.  Nella finestra **Proprietà** fare clic sulla casella di riepilogo a discesa visualizzata accanto alla proprietà <xref:System.Windows.Forms.Control.Dock%2A>.  
  
     Viene visualizzata un'interfaccia grafica che rappresenta le sei possibili impostazioni di <xref:System.Windows.Forms.Control.Dock%2A>.  
  
3.  Scegliere l'impostazione appropriata.  
  
4.  Il controllo verrà ancorato come specificato dall'impostazione.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=fullName>   
 [Procedura: allineare un controllo ai bordi dei form](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando guide di allineamento](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [Procedura: agganciare i controlli in Windows Form](../../../../docs/framework/winforms/controls/how-to-anchor-controls-on-windows-forms.md)   
 [Procedura: agganciare e ancorare controlli figlio in un controllo TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [Procedura: ancorare e agganciare controlli figlio in un controllo FlowLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [Procedura dettagliata: disposizione dei controlli in Windows Form utilizzando FlowLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [Sviluppo di controlli Windows Form in fase di progettazione](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)