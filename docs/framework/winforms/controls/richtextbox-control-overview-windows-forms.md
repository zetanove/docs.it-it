---
title: "Cenni preliminari sul controllo RichTextBox (Windows Form) | Microsoft Docs"
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
  - "RichTextBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "RichTextBox (controllo) [Windows Form], informazioni sul controllo RichTextBox"
  - "caselle di testo, informazioni sulle caselle di testo"
ms.assetid: 95081194-3dd4-4b84-9545-dd373e491eca
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Cenni preliminari sul controllo RichTextBox (Windows Form)
Il controllo <xref:System.Windows.Forms.RichTextBox> di Windows Form viene utilizzato per visualizzare, immettere e modificare testo formattato.  Oltre alle funzionalità offerte dal controllo <xref:System.Windows.Forms.TextBox>, il controllo <xref:System.Windows.Forms.RichTextBox> consente di visualizzare tipi di carattere, colori e collegamenti, caricare da un file un testo e immagini incorporate e trovare caratteri specificati.  Il controllo <xref:System.Windows.Forms.RichTextBox> viene generalmente utilizzato per fornire funzionalità di visualizzazione e modifica del testo simili a quelle offerte da programmi di elaborazione testi quali Microsoft Word.  Analogamente al controllo <xref:System.Windows.Forms.TextBox>, il controllo <xref:System.Windows.Forms.RichTextBox> è in grado di visualizzare barre di scorrimento. A differenza di <xref:System.Windows.Forms.TextBox>, tuttavia, consente di visualizzare per impostazione predefinita entrambe le barre di scorrimento, orizzontale e verticale, per le quali fornisce impostazioni aggiuntive.  
  
## Utilizzo del controllo RichTextBox  
 Come per il controllo <xref:System.Windows.Forms.TextBox>, il testo visualizzato viene impostato mediante la proprietà <xref:System.Windows.Forms.RichTextBox.Text%2A>.  Il controllo <xref:System.Windows.Forms.RichTextBox> è dotato di numerose proprietà per la formattazione del testo.  Per informazioni dettagliate su queste proprietà, vedere [Procedura: impostare gli attributi dei caratteri per il controllo RichTextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-set-font-attributes-for-the-windows-forms-richtextbox-control.md) e [Procedura: impostare rientri, rientri sporgenti e paragrafi puntati con il controllo RichTextBox Windows Form](../../../../docs/framework/winforms/controls/set-indents-hanging-indents-bulleted-paragraphs-with-wf-richtextbox.md).  Per la modifica dei file, i metodi <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> e <xref:System.Windows.Forms.RichTextBox.SaveFile%2A> consentono di visualizzare e scrivere diversi formati di file, quali testo normale, testo normale Unicode e formato RTF \(Rich Text Format\).  Per un elenco dei formati di file supportati, vedere [Enumerazione RichTextBoxStreamType](frlrfSystemWindowsFormsRichTextBoxStreamTypeClassTopic).  È inoltre disponibile il metodo <xref:System.Windows.Forms.RichTextBox.Find%2A> per trovare stringhe di testo o caratteri specifici.  
  
 Il controllo <xref:System.Windows.Forms.RichTextBox> può inoltre essere utilizzato per collegamenti ipertestuali, impostando la proprietà <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A> su `true` e scrivendo del codice per gestire l'evento <xref:System.Windows.Forms.RichTextBox.LinkClicked>.  Per ulteriori informazioni, vedere [Procedura: visualizzare collegamenti ipertestuali con il controllo RichTextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-display-web-style-links-with-the-windows-forms-richtextbox-control.md).  Per impedire la modifica totale o parziale da parte dell'utente del testo incluso nel controllo, impostare la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionProtected%2A> su `true`.  
  
 In un controllo <xref:System.Windows.Forms.RichTextBox> è possibile annullare e ripristinare la maggior parte delle operazioni di modifica chiamando i metodi <xref:System.Windows.Forms.TextBoxBase.Undo%2A> e <xref:System.Windows.Forms.RichTextBox.Redo%2A>.  Il metodo <xref:System.Windows.Forms.RichTextBox.CanRedo%2A> consente di determinare se l'ultima operazione annullata dall'utente può essere riapplicata al controllo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)