---
title: "Cenni preliminari sul controllo WebBrowser | Microsoft Docs"
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
  - "WebBrowser"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "pagine Web, visualizzazione in applicazioni"
  - "WebBrowser (controllo) [Windows Form], informazioni"
ms.assetid: 6e3e1cc2-9c48-4136-9659-e99e4e60b7e9
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Cenni preliminari sul controllo WebBrowser
Il controllo <xref:System.Windows.Forms.WebBrowser> fornisce un wrapper gestito per il controllo ActiveX WebBrowser.  Il wrapper gestito consente di visualizzare pagine Web nelle applicazioni client Windows Form.  È possibile utilizzare il controllo <xref:System.Windows.Forms.WebBrowser> per duplicare le funzionalità del browser Internet Explorer nell'applicazione oppure disabilitare le funzionalità predefinite di Internet Explorer e utilizzare il controllo come semplice visualizzatore di documenti HTML.  Il controllo inoltre può essere utilizzato per aggiungere elementi dell'interfaccia utente basata su DHTML al form e nascondere il fatto che siano inclusi nel controllo <xref:System.Windows.Forms.WebBrowser>.  Questo approccio consente di combinare facilmente in un'unica applicazione i controlli Web e i controlli Windows Form.  
  
## Proprietà, metodi ed eventi di uso comune  
 Il controllo <xref:System.Windows.Forms.WebBrowser> dispone di numerose proprietà, metodi ed eventi che possono essere utilizzati per implementare i controlli disponibili in Internet Explorer.  È possibile utilizzare, ad esempio, il metodo `Navigate` per implementare una barra degli indirizzi e i metodi `GoBack`, `GoForward`, `Stop` e `Refresh` per implementare i pulsanti di navigazione su una barra degli strumenti.  L'evento `Navigated` può essere gestito per aggiornare la barra degli indirizzi con il valore della proprietà `Url` e la barra del titolo con il valore della proprietà `DocumentTitle`.  
  
 Se si desidera generare contenuto personalizzato per le pagine all'interno dell'applicazione, è possibile impostare la proprietà `DocumentText`.  Se si ha dimestichezza con il modello DOM \(Document Object Model\) HTML, è anche possibile modificare il contenuto della pagina Web corrente mediante la proprietà `Document`.  Con questa proprietà, è possibile archiviare e modificare i documenti in memoria anziché spostarsi tra i vari file.  
  
 La proprietà `Document` consente inoltre di chiamare i metodi implementati nel codice di script delle pagine Web dal codice dell'applicazione client.  Per accedere al codice dell'applicazione client dal codice di script, impostare la proprietà `ObjectForScripting`.  L'oggetto specificato sarà accessibile al codice di script come oggetto `window.external`.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|Proprietà <xref:System.Windows.Forms.WebBrowser.Document%2A>|Consente di ottenere un oggetto che fornisce accesso gestito al modello DOM \(Document Object Model\) HTML della pagina Web corrente.|  
|Evento <xref:System.Windows.Forms.WebBrowser.DocumentCompleted>|Si verifica una volta completato il caricamento di una pagina Web.|  
|Proprietà <xref:System.Windows.Forms.WebBrowser.DocumentText%2A>|Consente di ottenere o impostare il contenuto HTML della pagina Web corrente.|  
|Proprietà <xref:System.Windows.Forms.WebBrowser.DocumentTitle%2A>|Consente di ottenere il titolo della pagina Web corrente.|  
|Metodo <xref:System.Windows.Forms.WebBrowser.GoBack%2A>|Consente di passare alla pagina precedente della cronologia.|  
|Metodo <xref:System.Windows.Forms.WebBrowser.GoForward%2A>|Consente di passare alla pagina successiva della cronologia.|  
|Metodo <xref:System.Windows.Forms.WebBrowser.Navigate%2A>|Consente di passare all'URL specificato.|  
|Evento <xref:System.Windows.Forms.WebBrowser.Navigating>|Viene eseguito prima dell'avvio della navigazione, consentendo l'annullamento dell'azione.|  
|Proprietà <xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A>|Consente di ottenere o impostare un oggetto che può essere utilizzato dal codice di script della pagina Web per comunicare con l'applicazione.|  
|Metodo <xref:System.Windows.Forms.WebBrowser.Print%2A>|Consente di stampare la pagina Web corrente.|  
|Metodo <xref:System.Windows.Forms.WebBrowser.Refresh%2A>|Consente di ricaricare la pagina Web corrente.|  
|Metodo <xref:System.Windows.Forms.WebBrowser.Stop%2A>|Consente di arrestare la navigazione corrente e interrompere gli elementi di pagina dinamici, come ad esempio gli effetti audio e di animazione.|  
|Proprietà <xref:System.Windows.Forms.WebBrowser.Url%2A>|Consente di ottenere o impostare l'URL della pagina Web corrente.  L'impostazione di questa proprietà consente di passare al nuovo URL con il controllo.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.WebBrowser>   
 <xref:System.Windows.Forms.WebBrowserDocumentCompletedEventArgs>   
 <xref:System.Windows.Forms.WebBrowserDocumentCompletedEventHandler>   
 <xref:System.Windows.Forms.WebBrowserEncryptionLevel>   
 <xref:System.Windows.Forms.WebBrowserNavigatedEventArgs>   
 <xref:System.Windows.Forms.WebBrowserNavigatedEventHandler>   
 <xref:System.Windows.Forms.WebBrowserNavigatingEventArgs>   
 <xref:System.Windows.Forms.WebBrowserNavigatingEventHandler>   
 <xref:System.Windows.Forms.WebBrowserProgressChangedEventArgs>   
 <xref:System.Windows.Forms.WebBrowserReadyState>   
 <xref:System.Windows.Forms.WebBrowserRefreshOption>   
 [Procedura: passare a un URL con il controllo WebBrowser](../../../../docs/framework/winforms/controls/how-to-navigate-to-a-url-with-the-webbrowser-control.md)   
 [Procedura: stampare con un controllo WebBrowser](../../../../docs/framework/winforms/controls/how-to-print-with-a-webbrowser-control.md)   
 [Procedura: aggiungere funzionalità del browser Web a un'applicazione Windows Form](../../../../docs/framework/winforms/controls/how-to-add-web-browser-capabilities-to-a-windows-forms-application.md)   
 [Procedura: creare un visualizzatore di documenti HTML in un'applicazione Windows Form](../../../../docs/framework/winforms/controls/how-to-create-an-html-document-viewer-in-a-windows-forms-application.md)   
 [Procedura: implementare comunicazioni bidirezionali tra il codice DHTML e il codice dell'applicazione client](../../../../docs/framework/winforms/controls/implement-two-way-com-between-dhtml-and-client.md)   
 [Sicurezza dei controlli WebBrowser](../../../../docs/framework/winforms/controls/webbrowser-security.md)