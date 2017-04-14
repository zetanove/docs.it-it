---
title: "Disegno e rendering di controlli personalizzati | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], disegno"
  - "controlli personalizzati [Windows Form], rendering"
  - "OnPaint (metodo)"
  - "controlli utente [Windows Form], disegno"
ms.assetid: a09dbf76-0966-4cbf-a66a-2083ba98e068
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Disegno e rendering di controlli personalizzati
Il disegno personalizzato dei controlli è una delle molte attività complesse che sono state semplificate da .NET Framework.  Con la creazione di un controllo personalizzato vengono messe a disposizione numerose opzioni relative all'aspetto grafico.  Se si crea un controllo che eredita dalla classe `Control`, è necessario fornire codice che consenta al controllo di eseguire il rendering della propria rappresentazione grafica.  Se si crea un controllo utente ereditando dalla classe `UserControl` o da uno dei controlli di Windows Form, è possibile eseguire l'override della rappresentazione grafica standard e fornire codice grafico personalizzato.  Se si desidera fornire il rendering personalizzato per i controlli costitutivi di `UserControl` in fase di creazione, le opzioni sono più limitate, ma offrono comunque un'ampia gamma di possibilità grafiche per controlli e applicazioni.  
  
## In questa sezione  
 [Rendering di un controllo Windows Form](../../../../docs/framework/winforms/controls/rendering-a-windows-forms-control.md)  
 Viene spiegato come programmare la logica necessaria per la visualizzazione di un controllo.  
  
 [Controlli creati dall'utente](../../../../docs/framework/winforms/controls/user-drawn-controls.md)  
 Viene fornita una panoramica sui passaggi relativi alla scrittura e all'override del codice di rendering per il controllo.  
  
 [Controlli costitutivi](../../../../docs/framework/winforms/controls/constituent-controls.md)  
 Viene descritto come implementare il codice di rendering personalizzato per i controlli costitutivi nei controlli utente e nei form.  
  
 [Procedura: rendere invisibile il controllo in fase di esecuzione](../../../../docs/framework/winforms/controls/how-to-make-your-control-invisible-at-run-time.md)  
 Viene illustrato come utilizzare la proprietà <xref:System.Windows.Forms.Control.Visible%2A> per nascondere e mostrare un controllo.  
  
 [Procedura: assegnare uno sfondo trasparente al controllo](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)  
 Viene illustrato come utilizzare il metodo <xref:System.Windows.Forms.Control.SetStyle%2A> per creare un colore di sfondo opaco, trasparente o parzialmente trasparente.  
  
 [Rendering dei controlli con stili visivi](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)  
 Viene illustrato come eseguire il rendering dei controlli utilizzando stili visivi nei sistemi operativi che li supportano.  
  
## Riferimenti  
 <xref:System.Windows.Forms.Control>  
 Viene descritta la classe e vengono forniti collegamenti a tutti i relativi membri.  
  
 <xref:System.Windows.Forms.UserControl>  
 Viene descritta la classe e vengono forniti collegamenti a tutti i relativi membri.  
  
 <xref:System.Windows.Forms.Control.OnPaint%2A>  
 Viene illustrato questo metodo.  
  
## Sezioni correlate  
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)  
 Viene presentata la funzionalità grafica [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] dal punto di vista di Visual Studio, con collegamenti a ulteriori informazioni.  
  
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)  
 Vengono descritti i tipi di controlli personalizzati che è possibile creare.