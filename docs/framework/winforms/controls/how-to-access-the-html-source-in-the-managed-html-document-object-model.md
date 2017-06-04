---
title: "Procedura: accedere all&#39;origine HTML nel Document Object Model HTML gestito | Microsoft Docs"
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
  - "HTML, accesso in Windows Form"
  - "DOM HTML gestiti"
ms.assetid: 53db79fa-8a5e-448e-88c2-f54ace3860b6
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: accedere all&#39;origine HTML nel Document Object Model HTML gestito
Le proprietà <xref:System.Windows.Forms.WebBrowser.DocumentStream%2A> r <xref:System.Windows.Forms.WebBrowser.DocumentText%2A> del controllo <xref:System.Windows.Forms.WebBrowser> restituiscono l'HTML del documento corrente come si presentava al momento della visualizzazione iniziale.  Se tuttavia si modifica la pagina con chiamate a metodo e proprietà, ad esempio <xref:System.Windows.Forms.HtmlElement.AppendChild%2A> e <xref:System.Windows.Forms.HtmlElement.InnerHtml%2A>, queste modifiche non saranno visualizzate quando si chiama <xref:System.Windows.Forms.WebBrowser.DocumentStream%2A> e <xref:System.Windows.Forms.WebBrowser.DocumentText%2A>.  Per ottenere l'origine HTML più recente del DOM, è necessario chiamare la proprietà <xref:System.Windows.Forms.HtmlElement.OuterHtml%2A> sull'elemento HTML.  
  
 La procedura seguente mostra come recuperare l'origine dinamica e visualizzarla in un menu di scelta rapida separato.  
  
### Recupero dell'origine dinamica con la proprietà OuterHtml  
  
1.  Creare una nuova applicazione Windows Form.  Iniziare con una singola classe <xref:System.Windows.Forms.Form>, e denominarla `Form1`.  
  
2.  Ospitare il controllo <xref:System.Windows.Forms.WebBrowser> nell'applicazione Windows Form e denominarlo `WebBrowser1`.  Per altre informazioni, vedere [Procedura: aggiungere funzionalità del browser Web a un'applicazione Windows Form](../../../../docs/framework/winforms/controls/how-to-add-web-browser-capabilities-to-a-windows-forms-application.md).  
  
3.  Creare una seconda classe <xref:System.Windows.Forms.Form> nell'applicazione e denominarla `CodeForm`.  
  
4.  Aggiungere un controllo <xref:System.Windows.Forms.RichTextBox> a `CodeForm` e impostare la relativa proprietà <xref:System.Windows.Forms.Control.Dock%2A> su `Fill`.  
  
5.  Creare una proprietà pubblica in `CodeForm` e denominarla `Code`.  
  
     [!code-csharp[DisplayWebBrowserCode#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/DisplayWebBrowserCode/CS/CodeForm.cs#1)]
     [!code-vb[DisplayWebBrowserCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/DisplayWebBrowserCode/VB/CodeForm.vb#1)]  
  
6.  Aggiungere un controllo <xref:System.Windows.Forms.Button> denominato `Button1` alla classe <xref:System.Windows.Forms.Form> e monitorare l'evento <xref:System.Windows.Forms.Control.Click>.  Per informazioni dettagliate sul monitoraggio degli eventi, vedere [Eventi](../../../../docs/standard/events/index.md).  
  
7.  Aggiungere il codice seguente al gestore eventi <xref:System.Windows.Forms.Control.Click>.  
  
     [!code-csharp[DisplayWebBrowserCode#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/DisplayWebBrowserCode/CS/Form1.cs#2)]
     [!code-vb[DisplayWebBrowserCode#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/DisplayWebBrowserCode/VB/Form1.vb#2)]  
  
## Programmazione efficiente  
 Verificare sempre il valore di <xref:System.Windows.Forms.WebBrowser.Document%2A> prima di tentarne il recupero.  Se il caricamento della pagina corrente non viene completato, è possibile che l'inizializzazione di <xref:System.Windows.Forms.WebBrowser.Document%2A> o di uno o più dei relativi oggetti figlio non sia eseguita.  
  
## Vedere anche  
 [Utilizzare il Document Object Model HTML gestito](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)   
 [Cenni preliminari sul controllo WebBrowser](../../../../docs/framework/winforms/controls/webbrowser-control-overview.md)