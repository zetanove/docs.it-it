---
title: "Cenni preliminari sul controllo LinkLabel (Windows Form) | Microsoft Docs"
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
  - "LinkLabel"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Label (controllo) [Windows Form], informazioni sul controllo Label"
  - "LinkLabel (controllo) [Windows Form], informazioni"
  - "collegamenti, LinkLabel (controllo)"
ms.assetid: 9e248549-10ca-43a3-bb5e-60f583d369f1
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Cenni preliminari sul controllo LinkLabel (Windows Form)
Il controllo <xref:System.Windows.Forms.LinkLabel> di Windows Form consente di aggiungere collegamenti ipertestuali alle applicazioni Windows Form.  Il controllo <xref:System.Windows.Forms.LinkLabel> può essere utilizzato per gli stessi scopi per cui si utilizza il controllo <xref:System.Windows.Forms.Label> e anche per impostare parte del testo come collegamento a un file, a una cartella o a una pagina Web.  
  
## Operazioni che è possibile eseguire con il controllo LinkLabel  
 Oltre a tutte le proprietà, ai metodi e agli eventi del controllo <xref:System.Windows.Forms.Label>, il controllo <xref:System.Windows.Forms.LinkLabel> è dotato di proprietà per i collegamenti ipertestuali e i colori di tali collegamenti.  La proprietà <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> imposta l'area di testo che attiva il collegamento.  Le proprietà <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>, <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> e <xref:System.Windows.Forms.LinkLabel.ActiveLinkColor%2A> impostano i colori del collegamento.  L'evento <xref:System.Windows.Forms.LinkLabel.LinkClicked> determina ciò che accade quando il testo del collegamento viene selezionato.  
  
 L'utilizzo più semplice del controllo <xref:System.Windows.Forms.LinkLabel> consiste nella visualizzazione di un singolo collegamento mediante la proprietà <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>, ma è anche possibile visualizzare più collegamenti ipertestuali utilizzando la proprietà <xref:System.Windows.Forms.LinkLabel.Links%2A>.  La proprietà <xref:System.Windows.Forms.LinkLabel.Links%2A> consente di accedere a una raccolta di collegamenti.  È inoltre possibile specificare dei dati nella proprietà <xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A> di ogni singolo oggetto <xref:System.Windows.Forms.LinkLabel.Link>.  Il valore della proprietà <xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A> può essere utilizzato per memorizzare il percorso di un file da visualizzare o l'indirizzo di un sito Web.  
  
## Vedere anche  
 <xref:System.Windows.Forms.LinkLabel>   
 [Cenni preliminari sul controllo Label](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)   
 [Procedura: eseguire il collegamento a un oggetto o a una pagina Web con il controllo LinkLabel di Windows Form](../../../../docs/framework/winforms/controls/link-to-an-object-or-web-page-with-wf-linklabel-control.md)   
 [Procedura: modificare l'aspetto del controllo LinkLabel di Windows Form](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)