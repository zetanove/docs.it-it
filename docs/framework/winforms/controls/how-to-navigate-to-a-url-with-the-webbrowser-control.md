---
title: "Procedura: passare a un URL con il controllo WebBrowser | Microsoft Docs"
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
  - "WebBrowser.Navigate"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "esempi [Windows Form], WebBrowser (controllo)"
  - "URL, passaggio"
  - "WebBrowser (controllo) [Windows Form], esempi"
  - "WebBrowser (controllo) [Windows Form], passaggio a URL"
ms.assetid: b3ec38cb-f509-4d0b-bd79-9f3611259c62
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: passare a un URL con il controllo WebBrowser
Nell'esempio di codice riportato di seguito viene illustrato come utilizzare il controllo <xref:System.Windows.Forms.WebBrowser> per passare a uno specifico URL.  
  
 Per determinare quando il nuovo documento è stato completamente caricato, è possibile gestire l'evento <xref:System.Windows.Forms.WebBrowser.DocumentCompleted>.  Per una descrizione di questo evento, vedere [Procedura: stampare con un controllo WebBrowser](../../../../docs/framework/winforms/controls/how-to-print-with-a-webbrowser-control.md).  
  
## Esempio  
  
```vb  
Me.webBrowser1.Navigate("http://www.microsoft.com")  
```  
  
```csharp  
this.webBrowser1.Navigate("http://www.microsoft.com");  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.WebBrowser> denominato `webBrowser1`.  
  
-   Riferimenti agli assembly `System` e `System.Windows.Forms`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.WebBrowser>   
 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted?displayProperty=fullName>   
 <xref:System.Windows.Forms.WebBrowser.Navigating?displayProperty=fullName>   
 <xref:System.Windows.Forms.WebBrowser.Navigated?displayProperty=fullName>   
 [Controllo WebBrowser](../../../../docs/framework/winforms/controls/webbrowser-control-windows-forms.md)   
 [Procedura: stampare con un controllo WebBrowser](../../../../docs/framework/winforms/controls/how-to-print-with-a-webbrowser-control.md)