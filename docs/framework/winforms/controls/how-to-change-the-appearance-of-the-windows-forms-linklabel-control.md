---
title: "Procedura: modificare l&#39;aspetto del controllo LinkLabel di Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], LinkLabel (controllo)"
  - "LinkLabel (controllo) [Windows Form], modifica dell'aspetto di collegamenti"
  - "LinkLabel (controllo) [Windows Form], esempi"
  - "LinkLabel (proprietà)"
  - "collegamenti, modifica dell'aspetto"
ms.assetid: fdc5854f-5162-4457-8cbe-1042feb2d132
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: modificare l&#39;aspetto del controllo LinkLabel di Windows Form
È possibile modificare il testo visualizzato dal controllo <xref:System.Windows.Forms.LinkLabel> per soddisfare diverse esigenze.  In genere si segnala la possibilità di fare clic sul testo impostandolo in modo che al passaggio del mouse appaia sottolineato e di un determinato colore.  Una volta che si è fatto clic sul testo, il colore cambia.  Per controllare questo comportamento, è possibile impostare cinque proprietà diverse: <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>, <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>, <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>, <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> e <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>.  
  
### Per modificare l'aspetto di un controllo LinkLabel  
  
1.  Impostare le proprietà <xref:System.Windows.Forms.LinkLabel.LinkColor%2A> e <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> sui colori desiderati.  
  
     È possibile eseguire tale operazione a livello di codice o in fase di progettazione nella finestra **Proprietà**.  
  
    ```vb  
    ' You can set the color using decimal values for red, green, and blue  
    LinkLabel1.LinkColor = Color.FromArgb(0, 0, 255)  
    ' Or you can set the color using defined constants  
    LinkLabel1.VisitedLinkColor = Color.Purple  
  
    ```  
  
    ```csharp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1.LinkColor = Color.FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1.VisitedLinkColor = Color.Purple;  
  
    ```  
  
    ```cpp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1->LinkColor = Color::FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1->VisitedLinkColor = Color::Purple;  
    ```  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.LinkLabel.Text%2A> su una didascalia appropriata.  
  
     È possibile eseguire tale operazione a livello di codice o in fase di progettazione nella finestra **Proprietà**.  
  
    ```vb  
    LinkLabel1.Text = "Click here to see more."  
  
    ```  
  
    ```csharp  
    linkLabel1.Text = "Click here to see more.";  
  
    ```  
  
    ```cpp  
    linkLabel1->Text = "Click here to see more.";  
    ```  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> per stabilire quale parte della didascalia verrà indicata come collegamento.  
  
     Il valore <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> viene rappresentato con una struttura <xref:System.Windows.Forms.LinkArea> contenente due numeri, la posizione del carattere iniziale e il numero di caratteri.  È possibile eseguire tale operazione a livello di codice o in fase di progettazione nella finestra **Proprietà**.  
  
    ```vb  
    LinkLabel1.LinkArea = new LinkArea(6,4)  
  
    ```  
  
    ```csharp  
    linkLabel1.LinkArea = new LinkArea(6,4);  
  
    ```  
  
    ```cpp  
    linkLabel1->LinkArea = LinkArea(6,4);  
    ```  
  
4.  Impostare la proprietà <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A> su <xref:System.Windows.Forms.LinkBehavior>, <xref:System.Windows.Forms.LinkBehavior> o <xref:System.Windows.Forms.LinkBehavior>.  
  
     Se la proprietà è impostata su <xref:System.Windows.Forms.LinkBehavior>, la parte di didascalia determinata da <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> viene sottolineata solo se il puntatore del mouse rimane fermo su di essa.  
  
5.  Nel gestore dell'evento <xref:System.Windows.Forms.LinkLabel.LinkClicked> impostare la proprietà <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> su `true`.  
  
     È consuetudine modificare l'aspetto di un collegamento una volta che è stato visitato, in genere cambiandone il colore.  Il testo assumerà il colore indicato dalla proprietà <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>.  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked (ByVal sender As Object, _  
       ByVal e As EventArgs) Handles LinkLabel1.LinkClicked  
       ' Change the color of the link text  
       ' by setting LinkVisited to True.  
       LinkLabel1.LinkVisited = True  
       ' Then do whatever other action is appropriate  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void LinkLabel1_LinkClicked(object sender, System.EventArgs e)  
    {  
       // Change the color of the link text by setting LinkVisited   
       // to True.  
       linkLabel1.LinkVisited = true;  
       // Then do whatever other action is appropriate  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Change the color of the link text by setting LinkVisited   
          // to True.  
          linkLabel1->LinkVisited = true;  
          // Then do whatever other action is appropriate  
       }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>   
 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>   
 <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>   
 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>   
 [Cenni preliminari sul controllo LinkLabel](../../../../docs/framework/winforms/controls/linklabel-control-overview-windows-forms.md)   
 [Procedura: eseguire il collegamento a un oggetto o a una pagina Web con il controllo LinkLabel di Windows Form](../../../../docs/framework/winforms/controls/link-to-an-object-or-web-page-with-wf-linklabel-control.md)   
 [Controllo LinkLabel](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)