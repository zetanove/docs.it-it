---
title: "Accesso a frame nel Document Object Model HTML gestito | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DOM, accesso a frame in HTML gestito"
  - "frame, accesso"
  - "DOM HTML, gestito"
  - "HTML, DOM"
  - "HTML, gestito"
  - "DOM HTML gestiti"
ms.assetid: cdeeaa22-0be4-4bbf-9a75-4ddc79199f8d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Accesso a frame nel Document Object Model HTML gestito
Alcuni documenti HTML sono composti da *frame*, o finestre, che possono contenere i rispettivi documenti HTML distinti.  Con i frame è possibile creare facilmente pagine HTML in cui una o più parti della pagina sono statiche, ad esempio una barra di spostamento, mentre il contenuto degli altri frame cambia continuamente.  
  
 Gli autori di documenti HTML possono creare i frame in uno dei due modi seguenti:  
  
-   Usando i tag `FRAMESET` e `FRAME`, che creano finestre fisse.  
  
 \-oppure\-  
  
-   Usando il tag `IFRAME`, che crea una finestra mobile che può essere riposizionata in fase di esecuzione.  
  
1.  Poiché i frame contengono documenti HTML, vengono rappresentati in Document Object Model \(DOM\) sia come elementi finestra che come elementi frame.  
  
2.  Quando si accede a un tag `FRAME` o `IFRAME` usando la raccolta Frames di <xref:System.Windows.Forms.HtmlWindow>, si recupererà l'elemento finestra corrispondente al frame.  Questo rappresenta tutte le proprietà dinamiche del frame, ad esempio l'URL, il documento e le dimensioni correnti.  
  
3.  Quando si accede a un tag `FRAME` o `IFRAME` usando la proprietà <xref:System.Windows.Forms.HtmlWindow.WindowFrameElement%2A> di <xref:System.Windows.Forms.HtmlWindow>, la raccolta <xref:System.Windows.Forms.HtmlElement.Children%2A> oppure metodi come <xref:System.Windows.Forms.HtmlElementCollection.GetElementsByName%2A> o <xref:System.Windows.Forms.HtmlDocument.GetElementById%2A>, si recupererà l'elemento frame.  Questo rappresenta le proprietà statiche del frame, incluso l'URL specificato nel file HTML originale.  
  
## Frame e sicurezza  
 L'accesso ai frame non è semplice perché il modello DOM HTML gestito implementa una misura di sicurezza nota come *sicurezza di scripting di interazione tra frame*.  Se un documento contiene un `FRAMESET` con due o più `FRAME` in domini diversi, questi `FRAME` non possono interagire tra loro.  In altre parole, un `FRAME` che visualizza contenuto dal sito Web non può accedere alle informazioni di un `FRAME` che ospita un sito di terze parti, ad esempio http:\/\/www.adatum.com\/.  Questa misura di sicurezza è implementata a livello della classe <xref:System.Windows.Forms.HtmlWindow>.  È possibile ottenere informazioni generali su un `FRAME` che ospita un altro sito Web, ad esempio l'URL, ma non si potrà accedere alla proprietà <xref:System.Windows.Forms.HtmlWindow.Document%2A> o modificare le dimensioni o la posizione del `FRAME` o dell'`IFRAME` di hosting.  
  
 Questa regola si applica anche alle finestre aperte con i metodi <xref:System.Windows.Forms.HtmlWindow.Open%2A> e <xref:System.Windows.Forms.HtmlWindow.OpenNew%2A>.  Se la finestra aperta è in un dominio diverso da quello della pagina ospitata nel controllo <xref:System.Windows.Forms.WebBrowser>, non sarà possibile spostare la finestra o esaminarne i contenuti.  Queste restrizioni vengono applicate anche se si usa il controllo <xref:System.Windows.Forms.WebBrowser> per visualizzare un sito Web diverso dal sito Web usato per distribuire l'applicazione basata su Windows Form.  Se si usa la tecnologia di distribuzione [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] per installare l'applicazione dal sito Web A e si usa <xref:System.Windows.Forms.WebBrowser> per visualizzare il sito Web B, non sarà possibile accedere ai dati del sito Web B.  
  
 Per altre informazioni sullo scripting di interazione tra siti, vedere [Informazioni sullo scripting di interazione tra frame e sulla sicurezza](http://msdn.microsoft.com/library/ms533028.aspx).  
  
## Vedere anche  
 [Elemento FRAME &#124; Oggetto frame](http://msdn.microsoft.com/library/ms535250.aspx)   
 [Utilizzare il Document Object Model HTML gestito](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)