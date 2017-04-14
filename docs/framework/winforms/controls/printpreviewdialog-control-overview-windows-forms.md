---
title: "Cenni preliminari sul controllo PrintPreviewDialog (Windows Form) | Microsoft Docs"
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
  - "PrintPreviewDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "PrintPreviewDialog (controllo) (mediante la finestra di progettazione), informazioni"
ms.assetid: efd4ee8d-6edd-47ec-88e4-4a4759bd2384
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Cenni preliminari sul controllo PrintPreviewDialog (Windows Form)
Il controllo <xref:System.Windows.Forms.PrintPreviewDialog> di Windows Form è una finestra di dialogo preconfigurata che consente di visualizzare un [PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md) così come verrà stampato  e costituisce una semplice soluzione, utilizzabile nell'applicazione Windows creata, per evitare di configurare una propria finestra di dialogo.  Il controllo contiene pulsanti per la stampa, l'ingrandimento, la visualizzazione di una o più pagine e la chiusura della finestra di dialogo.  
  
## Proprietà e metodi principali  
 La proprietà principale del controllo corrisponde a <xref:System.Windows.Forms.PrintPreviewDialog.Document%2A>, con cui viene impostato il documento di cui deve essere visualizzata l'anteprima.   Il documento deve essere un oggetto <xref:System.Drawing.Printing.PrintDocument>.  Per visualizzare la finestra di dialogo, è necessario chiamare il relativo metodo <xref:System.Windows.Forms.Form.ShowDialog%2A>.  L'utilizzo di funzionalità di anti\-alias può migliorare l'aspetto del testo, rallentandone tuttavia la visualizzazione. Per utilizzare l'anti\-alias, impostare la proprietà <xref:System.Windows.Forms.PrintPreviewDialog.UseAntiAlias%2A> su `true`.  
  
 Alcune proprietà sono disponibili mediante il controllo <xref:System.Windows.Forms.PrintPreviewControl> incluso in <xref:System.Windows.Forms.PrintPreviewDialog>.  Non è necessario aggiungere <xref:System.Windows.Forms.PrintPreviewControl> al form, poiché viene automaticamente incluso nel controllo <xref:System.Windows.Forms.PrintPreviewDialog> quando la finestra di dialogo viene aggiunta al form. Il controllo <xref:System.Windows.Forms.PrintPreviewControl> rende disponibili proprietà quali <xref:System.Windows.Forms.PrintPreviewControl.Columns%2A> e <xref:System.Windows.Forms.PrintPreviewControl.Rows%2A>, che determinano il numero di pagine visualizzate orizzontalmente e verticalmente nel controllo.  È possibile accedere alla proprietà <xref:System.Windows.Forms.PrintPreviewControl.Columns%2A> come `PrintPreviewDialog1.PrintPreviewControl.Columns` in [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], `printPreviewDialog1.PrintPreviewControl.Columns` in [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] o `printPreviewDialog1->PrintPreviewControl->Columns` in [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)].  
  
## Vedere anche  
 <xref:System.Windows.Forms.PrintPreviewDialog>   
 [Cenni preliminari sul controllo PrintPreviewControl](../../../../docs/framework/winforms/controls/printpreviewcontrol-control-overview-windows-forms.md)   
 [Controllo PrintPreviewDialog](../../../../docs/framework/winforms/controls/printpreviewdialog-control-windows-forms.md)   
 [Controlli e componenti della finestra di dialogo](../../../../docs/framework/winforms/controls/dialog-box-controls-and-components-windows-forms.md)