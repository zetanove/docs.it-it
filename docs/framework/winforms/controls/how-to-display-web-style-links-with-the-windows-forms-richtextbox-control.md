---
title: "Procedura: visualizzare collegamenti ipertestuali con il controllo RichTextBox Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], caselle di testo"
  - "RichTextBox (controllo) [Windows Form], collegamento a pagine Web"
  - "caselle di testo, visualizzazione di collegamenti Web"
ms.assetid: 95089a37-a202-4f7a-94ee-6ee312908851
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: visualizzare collegamenti ipertestuali con il controllo RichTextBox Windows Form
Il controllo <xref:System.Windows.Forms.RichTextBox> Windows Form consente di visualizzare collegamenti Web colorati e sottolineati.  È possibile scrivere il codice che apre una finestra del browser nella quale viene visualizzato il sito Web specificato nel testo del collegamento quando si fa clic sul collegamento.  
  
### Per definire un collegamento a una pagina Web con il controllo RichTextBox  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.RichTextBox.Text%2A> su una stringa che include un URL valido, ad esempio "http:\/\/www.microsoft.com\/italy\/".  
  
2.  Assicurarsi che la proprietà <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A> sia impostata su `true` \(impostazione predefinita\).  
  
3.  Creare una nuova istanza globale dell'oggetto <xref:System.Diagnostics.Process>.  
  
4.  Scrivere un gestore eventi per l'evento <xref:System.Windows.Forms.RichTextBox.LinkClicked> che invia al browser il testo desiderato.  
  
     Nell'esempio qui di seguito, l'evento <xref:System.Windows.Forms.RichTextBox.LinkClicked> consente di aprire un'istanza di Internet Explorer con l'URL specificato nella proprietà <xref:System.Windows.Forms.RichTextBox.Text%2A> del controllo <xref:System.Windows.Forms.RichTextBox>.  Nell'esempio si presuppone l'esistenza di un form contenente un controllo <xref:System.Windows.Forms.RichTextBox>.  
  
    > [!IMPORTANT]
    >  Durante la chiamata al metodo <xref:System.Diagnostics.Process.Start%2A?displayProperty=fullName> verrà generata un'eccezione <xref:System.Security.SecurityException> se si esegue il codice in un contesto parzialmente attendibile, poiché non si dispone di privilegi sufficienti.  Per ulteriori informazioni, vedere [Code Access Security Basics](../../../../docs/framework/misc/code-access-security-basics.md).  
  
    ```vb  
    Public p As New System.Diagnostics.Process  
    Private Sub RichTextBox1_LinkClicked _  
       (ByVal sender As Object, ByVal e As _  
       System.Windows.Forms.LinkClickedEventArgs) _  
       Handles RichTextBox1.LinkClicked  
          ' Call Process.Start method to open a browser  
          ' with link text as URL.  
          p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText)  
    End Sub  
  
    ```  
  
    ```csharp  
    public System.Diagnostics.Process p = new System.Diagnostics.Process();  
  
    private void richTextBox1_LinkClicked(object sender,   
    System.Windows.Forms.LinkClickedEventArgs e)  
    {  
       // Call Process.Start method to open a browser  
       // with link text as URL.  
       p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       System::Diagnostics::Process ^ p;  
  
    private:  
       void richTextBox1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkClickedEventArgs ^  e)  
       {  
          // Call Process.Start method to open a browser  
          // with link text as URL.  
          p = System::Diagnostics::Process::Start("IExplore.exe",  
             e->LinkText);  
       }  
    ```  
  
     \([!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) È necessario inizializzare il processo `p`. Per effettuare questa operazione, includere la seguente istruzione nel costruttore del form:  
  
    ```cpp  
    p = gcnew System::Diagnostics::Process();  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.richTextBox1.LinkClicked += new   
       System.Windows.Forms.LinkClickedEventHandler  
       (this.richTextBox1_LinkClicked);  
  
    ```  
  
    ```cpp  
    this->richTextBox1->LinkClicked += gcnew  
       System::Windows::Forms::LinkClickedEventHandler  
       (this, &Form1::richTextBox1_LinkClicked);  
    ```  
  
     È importante arrestare immediatamente il processo creato una volta completate le operazioni desiderate.  Con riferimento al codice sopra riportato, il codice per arrestare il processo sarà simile al seguente:  
  
    ```vb  
    Public Sub StopWebProcess()  
       p.Kill()  
    End Sub  
  
    ```  
  
    ```csharp  
    public void StopWebProcess()  
    {  
       p.Kill();  
    }  
  
    ```  
  
    ```cpp  
    public: void StopWebProcess()  
    {  
       p->Kill();  
    }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>   
 <xref:System.Windows.Forms.RichTextBox.LinkClicked>   
 <xref:System.Windows.Forms.RichTextBox>   
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)