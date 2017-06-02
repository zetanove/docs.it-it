---
title: "Procedura: impostare gli attributi dei caratteri per il controllo RichTextBox Windows Form | Microsoft Docs"
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
  - "tipi di carattere, modifica di attributi nel controllo RichTextBox"
  - "formattazione [Windows Form]"
  - "RichTextBox (controllo) [Windows Form], impostazione di attributi dei tipi di carattere"
  - "RTF (file), formattazione nel controllo RichTextBox"
  - "testo [Windows Form]"
  - "caselle di testo, formattazione di testo"
ms.assetid: 2bc23ddb-0529-4489-a1a2-ad253cb43f9a
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: impostare gli attributi dei caratteri per il controllo RichTextBox Windows Form
Nel controllo <xref:System.Windows.Forms.RichTextBox> Windows Form sono disponibili numerose opzioni per la formattazione del testo visualizzato.  Utilizzando la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionFont%2A>, è possibile visualizzare i caratteri selezionati in grassetto, corsivo o sottolineato.  È inoltre possibile utilizzare questa proprietà per modificare la dimensione e il carattere tipografico dei caratteri selezionati.  La proprietà <xref:System.Windows.Forms.RichTextBox.SelectionColor%2A> consente di modificare il colore dei caratteri selezionati.  
  
### Per modificare l'aspetto dei caratteri  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionFont%2A> su un tipo di carattere appropriato.  
  
     Per consentire agli utenti di impostare la famiglia del tipo di carattere, la dimensione e il carattere tipografico in un'applicazione, viene in genere utilizzato il componente <xref:System.Windows.Forms.FontDialog>.  Per informazioni generali, vedere [Cenni preliminari sul componente FontDialog](../../../../docs/framework/winforms/controls/fontdialog-component-overview-windows-forms.md).  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.SelectionColor%2A> su un colore appropriato.  
  
     Per consentire agli utenti di impostare il colore in un'applicazione, viene in genere utilizzato il componente <xref:System.Windows.Forms.ColorDialog>.  Per informazioni generali, vedere [Cenni preliminari sul componente ColorDialog](../../../../docs/framework/winforms/controls/colordialog-component-overview-windows-forms.md).  
  
    ```vb  
    RichTextBox1.SelectionFont = New Font("Tahoma", 12, FontStyle.Bold)  
    RichTextBox1.SelectionColor = System.Drawing.Color.Red  
  
    ```  
  
    ```csharp  
    richTextBox1.SelectionFont = new Font("Tahoma", 12, FontStyle.Bold);  
    richTextBox1.SelectionColor = System.Drawing.Color.Red;  
  
    ```  
  
    ```cpp  
    richTextBox1->SelectionFont =  
       gcnew System::Drawing::Font("Tahoma", 12, FontStyle::Bold);  
    richTextBox1->SelectionColor = System::Drawing::Color::Red;  
    ```  
  
    > [!NOTE]
    >  Queste proprietà vengono applicate solo al testo selezionato oppure, se non è stato selezionato alcun testo, vengono applicate al testo che viene digitato nella posizione corrente del punto di inserimento.  Per informazioni sulla selezione di testo a livello di codice, vedere [Metodo TextBoxBase.Select](frlrfSystemWindowsFormsTextBoxBaseClassSelectTopic).  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)