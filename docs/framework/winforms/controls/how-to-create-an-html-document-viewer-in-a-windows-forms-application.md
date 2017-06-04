---
title: "Procedura: creare un visualizzatore di documenti HTML in un&#39;applicazione Windows Form | Microsoft Docs"
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
  - "visualizzatori di documenti"
  - "WebBrowser (controllo) [Windows Form], creazione di un visualizzatore di documenti HTML"
  - "Windows Form, creazione di visualizzatori di documenti"
ms.assetid: 6a6338fe-f7ee-4f5e-9d8f-0465c57e9039
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: creare un visualizzatore di documenti HTML in un&#39;applicazione Windows Form
È possibile utilizzare il controllo <xref:System.Windows.Forms.WebBrowser> per visualizzare e stampare documenti HTML senza disporre della funzionalità completa di un browser Internet.  Questa procedura è utile quando si desidera usufruire delle capacità di formattazione del linguaggio HTML, ma si vuole evitare che gli utenti carichino in modo arbitrario pagine Web che possano contenere controlli Web non affidabili o codice di script potenzialmente dannoso.  È possibile, ad esempio, limitare in questo modo la capacità del controllo <xref:System.Windows.Forms.WebBrowser>, per utilizzarlo come visualizzatore di posta elettronica in formato HTML o per includere una guida HTML nell'applicazione.  
  
### Per creare un visualizzatore di documenti HTML  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A> su `false` per impedire a <xref:System.Windows.Forms.WebBrowser> di aprire i file trascinati nel controllo.  
  
     [!code-csharp[WebBrowserMisc#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/WebBrowserMisc/CS/WebBrowserMisc.cs#20)]
     [!code-vb[WebBrowserMisc#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WebBrowserMisc/vb/WebBrowserMisc.vb#20)]  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.WebBrowser.Url%2A> sul percorso del file iniziale da visualizzare.  
  
     [!code-csharp[WebBrowserMisc#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/WebBrowserMisc/CS/WebBrowserMisc.cs#21)]
     [!code-vb[WebBrowserMisc#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/WebBrowserMisc/vb/WebBrowserMisc.vb#21)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.WebBrowser> denominato `webBrowser1`.  
  
-   Riferimenti agli assembly `System` e `System.Windows.Forms`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.WebBrowser>   
 <xref:System.Windows.Forms.WebBrowser.AllowWebBrowserDrop%2A>   
 <xref:System.Windows.Forms.WebBrowser.Url%2A>   
 [Cenni preliminari sul controllo WebBrowser](../../../../docs/framework/winforms/controls/webbrowser-control-overview.md)   
 [Sicurezza dei controlli WebBrowser](../../../../docs/framework/winforms/controls/webbrowser-security.md)   
 [Procedura: passare a un URL con il controllo WebBrowser](../../../../docs/framework/winforms/controls/how-to-navigate-to-a-url-with-the-webbrowser-control.md)   
 [Procedura: stampare con un controllo WebBrowser](../../../../docs/framework/winforms/controls/how-to-print-with-a-webbrowser-control.md)