---
title: "Procedura: visualizzare le barre di scorrimento nel controllo RichTextBox Windows Form | Microsoft Docs"
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
  - "RichTextBox (controllo) [Windows Form], visualizzazione di barre di scorrimento"
  - "barre di scorrimento, visualizzazione nei controlli"
  - "caselle di testo, visualizzazione di barre di scorrimento"
ms.assetid: cdeb42e1-86e8-410c-ba46-18aec264ef5f
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: visualizzare le barre di scorrimento nel controllo RichTextBox Windows Form
Per impostazione predefinita, nel controllo <xref:System.Windows.Forms.RichTextBox> Windows Form sono visualizzate delle barre di scorrimento orizzontali e verticali in base alle necessità.  È possibile impostare la proprietà <xref:System.Windows.Forms.RichTextBox.ScrollBars%2A> del controllo <xref:System.Windows.Forms.RichTextBox> sui sette valori possibili descritti nella tabella qui di seguito.  
  
### Per visualizzare le barre di scorrimento in un controllo RichTextBox  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.Multiline%2A> su `true`.  Se la proprietà <xref:System.Windows.Forms.RichTextBox.Multiline%2A> è impostata su `false`, non verrà visualizzata alcuna barra di scorrimento, inclusa la barra orizzontale.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.ScrollBars%2A> su un valore appropriato dell'enumerazione <xref:System.Windows.Forms.RichTextBoxScrollBars>.  
  
    |Valore|Descrizione|  
    |------------|-----------------|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars> \(impostazione predefinita\)|Consente di visualizzare la barra di scorrimento orizzontale o verticale, oppure entrambe, solo quando il testo supera la larghezza o la lunghezza del controllo.|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|Non consente di visualizzare mai alcun tipo di barra di scorrimento.|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|Consente di visualizzare una barra di scorrimento orizzontale solo quando il testo supera la larghezza del controllo.  Affinché ciò si verifichi, è necessario impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> su `false`.|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|Consente di visualizzare una barra di scorrimento verticale solo quando il testo supera l'altezza del controllo.|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|Consente di visualizzare una barra di scorrimento orizzontale quando la proprietà <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> è impostata su `false`.  La barra di scorrimento non è disponibile quando il testo non supera la larghezza del controllo.|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|Consente di visualizzare sempre una barra di scorrimento verticale.  La barra di scorrimento non è disponibile quando il testo non supera la lunghezza del controllo.|  
    |<xref:System.Windows.Forms.RichTextBoxScrollBars>|Consente di visualizzare sempre una barra di scorrimento verticale.  Consente di visualizzare una barra di scorrimento orizzontale quando la proprietà <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> è impostata su `false`.  Le barre di scorrimento non sono disponibili quando il testo non supera la larghezza o la lunghezza del controllo.|  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> su un valore appropriato.  
  
    |Valore|Descrizione|  
    |------------|-----------------|  
    |`false`|Il testo nel controllo non viene adattato automaticamente alla larghezza del controllo e si estenderà verso destra fino a raggiungere l'interruzione di riga.  Utilizzare questo valore se è stata impostata la visualizzazione della barra di scorrimento orizzontale o di entrambe le barre.|  
    |`true` \(impostazione predefinita\)|Il testo nel controllo viene adattato automaticamente alla larghezza del controllo.  La barra di scorrimento orizzontale non viene visualizzata.  Utilizzare questo valore se sono state selezionate le barre di scorrimento verticali per visualizzare uno o più paragrafi.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBoxScrollBars>   
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)