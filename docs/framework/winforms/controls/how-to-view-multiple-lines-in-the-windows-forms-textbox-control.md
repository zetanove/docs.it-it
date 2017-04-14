---
title: "Procedura: visualizzare pi&#249; righe nel controllo TextBox Windows Form | Microsoft Docs"
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
  - "ritorno a capo"
  - "CRLF"
  - "fine riga"
  - "avanzamento riga"
  - "MultiLine (proprietà del controllo TextBox)"
  - "nuova riga"
  - "ScrollBars (proprietà), controllo TextBox"
  - "TextBox (controllo) [Windows Form], visualizzazione di più righe"
  - "WordWrap (proprietà)"
ms.assetid: 43173201-0b74-4067-a472-605029ca5f35
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: visualizzare pi&#249; righe nel controllo TextBox Windows Form
In base all'impostazione predefinita, il controllo <xref:System.Windows.Forms.TextBox> Windows Form visualizza una sola riga di testo e non visualizza barre di scorrimento.  Se il testo è più lungo dello spazio disponibile, risulterà visibile solo parte di esso.  È possibile modificare tale comportamento predefinito impostando le proprietà <xref:System.Windows.Forms.TextBox.Multiline%2A>, <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> e <xref:System.Windows.Forms.TextBox.ScrollBars%2A> sui valori appropriati.  
  
### Per visualizzare un ritorno a capo nel controllo TextBox  
  
-   Per visualizzare un ritorno a capo in un controllo <xref:System.Windows.Forms.TextBox> multilinea, utilizzare la proprietà <xref:System.Environment.NewLine%2A>.  
  
     I caratteri escape \(\\\) vengono interpretati in modo diverso in base al linguaggio.  In Visual Basic viene utilizzato `Chr$(13) & Chr$(10)` per la combinazione di ritorno a capo e avanzamento riga.  
  
### Per visualizzare più righe nel controllo TextBox  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.TextBox.Multiline%2A> su `true`.  Se <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> è `true` \(impostazione predefinita\), il testo all'interno del controllo risulterà organizzato in uno o più paragrafi. In caso contrario il testo verrà visualizzato come elenco le cui righe potrebbero apparire tagliate in corrispondenza del bordo del controllo.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.TextBox.ScrollBars%2A> su un valore appropriato.  
  
    |Valore|Descrizione|  
    |------------|-----------------|  
    |<xref:System.Windows.Forms.ScrollBars>|Utilizzare questo valore se il testo è costituito da un paragrafo quasi completamente adatto alle dimensioni del controllo.  L'utente può utilizzare il puntatore del mouse per spostarsi all'interno del controllo se il testo è troppo lungo e non può essere visualizzato completamente.|  
    |<xref:System.Windows.Forms.ScrollBars>|Utilizzare questo valore se si desidera visualizzare un elenco di righe, alcune delle quali potrebbero superare in lunghezza il controllo <xref:System.Windows.Forms.TextBox>.|  
    |<xref:System.Windows.Forms.ScrollBars>|Utilizzare questo valore se l'elenco può risultare più lungo rispetto all'altezza del controllo.|  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> su un valore appropriato.  
  
    |Valore|Descrizione|  
    |------------|-----------------|  
    |`false`|Il testo nel controllo non viene mandato a capo automaticamente e proseguirà verso destra fino a raggiungere l'interruzione della riga.  Utilizzare questo valore se è stata impostata la visualizzazione della barra di scorrimento <xref:System.Windows.Forms.ScrollBars> o <xref:System.Windows.Forms.ScrollBars>.|  
    |`true` \(impostazione predefinita\)|La barra di scorrimento orizzontale non viene visualizzata.  Utilizzare questo valore se sono state selezionate le barre di scorrimento <xref:System.Windows.Forms.ScrollBars> o <xref:System.Windows.Forms.ScrollBars> per visualizzare uno o più paragrafi.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 [Cenni preliminari sul controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-overview-windows-forms.md)   
 [Procedura: controllare il punto di inserimento in un controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo Password con il controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)   
 [Procedura: creare una casella di testo in sola lettura](../../../../docs/framework/winforms/controls/how-to-create-a-read-only-text-box-windows-forms.md)   
 [Procedura: inserire virgolette in una stringa](../../../../docs/framework/winforms/controls/how-to-put-quotation-marks-in-a-string-windows-forms.md)   
 [Procedura: selezionare testo nel controllo TextBox Windows Form](../../../../docs/framework/winforms/controls/how-to-select-text-in-the-windows-forms-textbox-control.md)   
 [Controllo TextBox](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)