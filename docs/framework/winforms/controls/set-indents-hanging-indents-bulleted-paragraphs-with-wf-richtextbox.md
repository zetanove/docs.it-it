---
title: "Procedura: impostare rientri, rientri sporgenti e paragrafi puntati con il controllo RichTextBox Windows Form | Microsoft Docs"
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
  - ".rtf (file), formattazione nel controllo RichTextBox"
  - "esempi [Windows Form], caselle di testo"
  - "RichTextBox (controllo) [Windows Form], impostazione di rientri ed elenchi puntati"
  - "RTF (file), formattazione nel controllo RichTextBox"
  - "caselle di testo, elenchi puntati"
  - "caselle di testo, impostazione dei rientri"
ms.assetid: abfb40e6-5642-4691-8ec1-9d9ae91688dc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: impostare rientri, rientri sporgenti e paragrafi puntati con il controllo RichTextBox Windows Form
Nel controllo <xref:System.Windows.Forms.RichTextBox> Windows Form sono disponibili numerose opzioni per la formattazione del testo visualizzato.  Impostando la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A>, è possibile formattare i paragrafi selezionati come elenchi puntati.  È inoltre possibile utilizzare le proprietà <xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A>, <xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A> e <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> per impostare il rientro di paragrafi rispetto ai bordi sinistro e destro del controllo e al bordo sinistro di altre righe di testo.  
  
### Per formattare un paragrafo come elenco puntato  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionBullet%2A> su `true`.  
  
    ```vb  
    RichTextBox1.SelectionBullet = True  
  
    ```  
  
    ```csharp  
    richTextBox1.SelectionBullet = true;  
  
    ```  
  
    ```cpp  
    richTextBox1->SelectionBullet = true;  
    ```  
  
### Per impostare il rientro di un paragrafo  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionIndent%2A> su un intero che rappresenta la distanza in pixel tra il bordo sinistro del controllo e il bordo sinistro del testo.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> su un intero che rappresenta la distanza in pixel tra il bordo sinistro della prima riga di testo nel paragrafo e il bordo sinistro delle righe successive nello stesso paragrafo.  Il valore della proprietà <xref:System.Windows.Forms.RichTextBox.SelectionHangingIndent%2A> viene applicato solo alle righe in un paragrafo che sono state mandate a capo sotto la prima riga.  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionRightIndent%2A> su un intero che rappresenta la distanza in pixel tra il bordo destro del controllo e il bordo destro del testo.  
  
    ```vb  
    RichTextBox1.SelectionIndent = 8  
    RichTextBox1.SelectionHangingIndent = 3  
    RichTextBox1.SelectionRightIndent = 12  
  
    ```  
  
    ```csharp  
    richTextBox1.SelectionIndent = 8;  
    richTextBox1.SelectionHangingIndent = 3;  
    richTextBox1.SelectionRightIndent = 12;  
  
    ```  
  
    ```cpp  
    richTextBox1->SelectionIndent = 8;  
    richTextBox1->SelectionHangingIndent = 3;  
    richTextBox1->SelectionRightIndent = 12;  
    ```  
  
    > [!NOTE]
    >  Tutte queste proprietà vengono applicate a qualsiasi paragrafo contenente il testo selezionato e al testo che viene digitato dopo il punto di inserimento corrente.  Quando, ad esempio, un utente seleziona una parola all'interno di un paragrafo e ne regola il rientro, le nuove impostazioni verranno applicate all'intero paragrafo che contiene tale parola nonché agli eventuali paragrafi immessi successivamente dopo il paragrafo selezionato.  Per informazioni sulla selezione di testo a livello di codice, vedere [Metodo TextBoxBase.Select](frlrfSystemWindowsFormsTextBoxBaseClassSelectTopic).  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)