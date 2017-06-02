---
title: "Cenni preliminari sul controllo FlowLayoutPanel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "FlowLayoutPanel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "FlowLayoutPanel (controllo) [Windows Form], informazioni sul controllo FlowLayoutPanel"
  - "form, layout dinamico"
  - "layout [Windows Form], dinamico"
  - "Windows Form, layout dinamico"
ms.assetid: 3883e024-f5a0-456d-9c27-b4dfa1cc9045
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sul controllo FlowLayoutPanel
Il controllo <xref:System.Windows.Forms.FlowLayoutPanel> dispone i contenuti in una direzione di flusso orizzontale o verticale.  È possibile eseguire il wrapping dei contenuti del controllo da una riga a quella successiva o da una colonna a quella successiva.  In alternativa, è possibile troncare i contenuti.  
  
 È possibile specificare la direzione del flusso impostando il valore della proprietà <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>.  Il controllo <xref:System.Windows.Forms.FlowLayoutPanel> inverte correttamente la direzione del flusso nei layout da destra a sinistra \(RTL, Right\-To\-Left\).  È anche possibile specificare se i contenuti del controllo <xref:System.Windows.Forms.FlowLayoutPanel> vengono sottoposti a wrapping o troncati impostando il valore della proprietà <xref:System.Windows.Forms.FlowLayoutPanel.WrapContents%2A>.  
  
 Il controllo <xref:System.Windows.Forms.FlowLayoutPanel> viene automaticamente ridimensionato in base ai contenuti quando si imposta la proprietà <xref:System.Windows.Forms.Control.AutoSize%2A> su `true`.  Fornisce anche una proprietà **FlowBreak** ai controlli figlio.  Impostando il valore della proprietà FlowBreak su `true`, il controllo <xref:System.Windows.Forms.FlowLayoutPanel> interrompe il layout dei controlli nella direzione di flusso corrente ed esegue il wrapping alla riga o colonna successiva.  
  
 Qualsiasi controllo Windows Form può essere figlio del controllo <xref:System.Windows.Forms.FlowLayoutPanel>, tra cui altre istanze di <xref:System.Windows.Forms.FlowLayoutPanel>.  Con questa funzionalità, è possibile costruire layout sofisticati in grado di adattarsi alle dimensioni del form in fase di esecuzione.  
  
 Vedere anche [Procedura dettagliata: Disposizione dei controlli in Windows Form usando FlowLayoutPanel](http://msdn.microsoft.com/library/z9w7ek2f\(v=vs.110\)).  
  
## Vedere anche  
 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>   
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [Controllo FlowLayoutPanel](../../../../docs/framework/winforms/controls/flowlayoutpanel-control-windows-forms.md)