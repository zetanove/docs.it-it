---
title: "Procedura: accedere al Document Object Model HTML gestito | Microsoft Docs"
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
  - "DOM HTML, l'accesso"
  - "DOM HTML gestito l'accesso"
ms.assetid: 40fa5cd5-1ed8-42f6-a93f-9ac01608bbeb
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: accedere al Document Object Model HTML gestito
È possibile accedere a Document Object Model (DOM) HTML gestito da due tipi di applicazione:  
  
-   Un'applicazione Windows Form (.exe) ospitata gestita <xref:System.Windows.Forms.WebBrowser> controllo. Queste due tecnologie sono complementari, con la <xref:System.Windows.Forms.WebBrowser> controllo Visualizza la pagina all'utente e DOM HTML rappresenta la struttura del documento logico.  
  
-   Un Windows Form <xref:System.Windows.Forms.UserControl> ospitata in Internet Explorer. È possibile accedere a DOM HTML rappresenta la pagina in cui il <xref:System.Windows.Forms.UserControl> ospitato per modificare la struttura del documento o aprire finestre di dialogo modali, tra le molte altre possibilità.  
  
### <a name="to-access-dom-from-a-windows-forms-application"></a>Per accedere a DOM da un'applicazione Windows Forms  
  
1.  Host un <xref:System.Windows.Forms.WebBrowser> controllo all'interno dell'applicazione Windows Form e verificare la presenza di <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> evento. Per informazioni dettagliate sull'hosting di controlli e monitoraggio degli eventi, vedere [eventi](../../../../docs/standard/events/index.md).  
  
2.  Recuperare il <xref:System.Windows.Forms.HtmlDocument> per la pagina corrente accedendo il <xref:System.Windows.Forms.WebBrowser.Document%2A> proprietà del <xref:System.Windows.Forms.WebBrowser> controllo.  
  
<!-- TODO: review snippet reference  [!CODE [AccessHTMLDOMApp#1](AccessHTMLDOMApp#1)]  -->  
  
### <a name="to-access-dom-from-a-usercontrol-hosted-in-internet-explorer"></a>Per accedere a DOM da una classe UserControl ospitata in Internet Explorer  
  
1.  Creare una propria classe personalizzata derivata la <xref:System.Windows.Forms.UserControl> (classe). Per ulteriori informazioni, vedere [procedura: creare controlli compositi](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md).  
  
2.  Inserire il codice seguente nel gestore eventi Load per la <xref:System.Windows.Forms.UserControl>:  
  
 [!code-csharp[AccessHTMLDOMControl#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/AccessHTMLDOMControl/cs/UserControl1.cs#1)]
 [!code-vb[AccessHTMLDOMControl#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/AccessHTMLDOMControl/vb/UserControl1.vb#1)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
  
1.  Quando si usa DOM tramite il <xref:System.Windows.Forms.WebBrowser> controllo, è consigliabile attendere sempre finché il <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> evento si verifica prima di tentare di accedere il <xref:System.Windows.Forms.WebBrowser.Document%2A> proprietà del <xref:System.Windows.Forms.WebBrowser> controllo. Il <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> evento viene generato dopo che l'intero documento è caricato, se si usa DOM prima di allora, si rischia di causare un'eccezione in fase di esecuzione dell'applicazione.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
  
1.  L'applicazione o <xref:System.Windows.Forms.UserControl> richiederà l'attendibilità totale per poter accedere a DOM. HTML gestito Se si distribuisce un'applicazione Windows Form utilizzando [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)], è possibile richiedere l'attendibilità totale mediante elevazione delle autorizzazioni o distribuzione di applicazioni attendibili, vedere [protezione di applicazioni ClickOnce](../Topic/Securing%20ClickOnce%20Applications.md) per informazioni dettagliate.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzando il modello a oggetti documento HTML gestito](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)