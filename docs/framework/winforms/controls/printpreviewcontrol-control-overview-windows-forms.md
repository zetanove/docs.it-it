---
title: "Cenni preliminari sul controllo PrintPreviewControl (Windows Form) | Microsoft Docs"
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
  - "PrintPreviewControl"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "anteprima di stampa"
  - "PrintPreviewControl (controllo)"
ms.assetid: 4513c6c7-5e9b-4f4c-82ca-00f993a26955
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Cenni preliminari sul controllo PrintPreviewControl (Windows Form)
Il controllo  <xref:System.Windows.Forms.PrintPreviewControl> di Windows Form viene utilizzato per visualizzare un [PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-windows-forms.md) così come verrà stampato.  Poiché non dispone di pulsanti né di altri elementi di interfaccia utente, il controllo <xref:System.Windows.Forms.PrintPreviewControl> viene in genere utilizzato solo se si desidera creare un'interfaccia utente personalizzata per l'anteprima di stampa.  Per visualizzare l'interfaccia utente standard, utilizzare un controllo <xref:System.Windows.Forms.PrintPreviewDialog>. Per informazioni generali, vedere [Cenni preliminari sul controllo PrintPreviewDialog](../../../../docs/framework/winforms/controls/printpreviewdialog-control-overview-windows-forms.md).  
  
## Proprietà principali  
 La proprietà principale del controllo corrisponde a <xref:System.Windows.Forms.PrintPreviewControl.Document%2A>, con cui viene impostato il documento di cui deve essere visualizzata l'anteprima.  Il documento deve essere un oggetto <xref:System.Drawing.Printing.PrintDocument>.  Per informazioni generali sulla creazione di documenti per la stampa, vedere [Cenni preliminari sul componente PrintDocument](../../../../docs/framework/winforms/controls/printdocument-component-overview-windows-forms.md) e [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md).  Le proprietà <xref:System.Windows.Forms.PrintPreviewControl.Columns%2A> e <xref:System.Windows.Forms.PrintPreviewControl.Rows%2A> determinano il numero di pagine visualizzate orizzontalmente e verticalmente nel controllo.  Sebbene la funzione di antialiasing consenta di migliorare l'aspetto del testo, potrebbe rallentarne la visualizzazione. Per utilizzarla, impostare la proprietà <xref:System.Windows.Forms.PrintPreviewControl.UseAntiAlias%2A> su `true`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.PrintPreviewControl>   
 [Cenni preliminari sul controllo PrintPreviewDialog](../../../../docs/framework/winforms/controls/printpreviewdialog-control-overview-windows-forms.md)   
 [Controllo PrintPreviewControl](../../../../docs/framework/winforms/controls/printpreviewcontrol-control-windows-forms.md)   
 [Controlli e componenti della finestra di dialogo](../../../../docs/framework/winforms/controls/dialog-box-controls-and-components-windows-forms.md)