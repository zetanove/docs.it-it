---
title: "Procedura: modificare gli stili di un elemento nel Document Object Model HTML gestito | Microsoft Docs"
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
  - "DOM HTML gestiti, modifica dello stile degli elementi"
ms.assetid: 154e8d9f-3e2d-4e8b-a6f3-c85a070e9cc1
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: modificare gli stili di un elemento nel Document Object Model HTML gestito
È possibile utilizzare stili in HTML per controllare l'aspetto di un documento e dei relativi elementi.  <xref:System.Windows.Forms.HtmlDocument> e <xref:System.Windows.Forms.HtmlElement> supportano le proprietà <xref:System.Windows.Forms.HtmlElement.Style%2A> che accettano stringhe di stile del formato seguente:  
  
 `name1:value1;...;nameN:valueN;`  
  
 Nell'esempio seguente è riportato un `DIV` con una stringa di stile in cui il testo è impostato sul tipo di carattere Arial e sul grassetto:  
  
 `<DIV style="font-face:arial;font-weight:bold;">`  
  
 `Hello, world!`  
  
 `</DIV>`  
  
 Il problema della gestione degli stili con la proprietà <xref:System.Windows.Forms.HtmlElement.Style%2A> consiste nella difficoltà nell'aggiungere e rimuovere singole impostazioni di stile dalla stringa.  Sarebbe ad esempio difficile trasformare il testo precedente in corsivo ogni volta che il cursore viene posizionato su un elemento `DIV` e annullare l'applicazione del corsivo quando il cursore viene spostato dall'elemento `DIV`.  Se si dovessero gestire molti stili in tal modo, il fattore tempo diventerebbe un problema.  
  
 Nella procedura seguente è contenuto codice che è possibile utilizzare per gestire facilmente stili in documenti ed elementi HTML.  La procedura presuppone esperienza nell'esecuzione delle attività di base in Windows Form, quali la creazione di un nuovo progetto e l'aggiunta di un controllo a un form.  
  
### Per elaborare modifiche di stile in un'applicazione Windows Form  
  
1.  Creare un nuovo progetto Windows Form.  
  
2.  Creare un nuovo file di classe con l'estensione corretta per il linguaggio di programmazione utilizzato.  
  
3.  Copiare il codice della classe `StyleGenerator` riportato nella sezione Esempio del presente argomento nel file di classe e salvarlo.  
  
4.  Salvare il testo HTML seguente in un file denominato Test.htm.  
  
    ```  
    <HTML>  
        <BODY>  
  
            <DIV style="font-face:arial;font-weight:bold;">  
                Hello, world!  
            </DIV><P>  
  
            <DIV>  
                Hello again, world!  
            </DIV><P>  
  
        </BODY>  
    </HTML>  
    ```  
  
5.  Aggiungere un controllo <xref:System.Windows.Forms.WebBrowser> denominato `webBrowser1` al form principale del progetto.  
  
6.  Aggiungere il codice riportato di seguito al file di codice del progetto.  
  
    > [!IMPORTANT]
    >  Assicurarsi che il gestore eventi `webBrowser1_DocumentCompleted` sia configurato come listener per l'evento <xref:System.Windows.Forms.WebBrowser.DocumentCompleted>.  In [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] fare doppio clic sul controllo <xref:System.Windows.Forms.WebBrowser>. In un editor di testo configurare il listener a livello di codice.  
  
     [!code-csharp[ManagedDOMStyles#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/Form1.cs#2)]
     [!code-vb[ManagedDOMStyles#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/Form1.vb#2)]  
  
7.  Eseguire il progetto.  Spostare il cursore sul primo elemento `DIV` e osservare gli effetti del codice.  
  
## Esempio  
 Il codice completo per la classe `StyleGenerator`, illustrato nell'esempio di codice riportato di seguito, analizza un valore di stile esistente, supporta l'aggiunta, la modifica e la rimozione di stili e restituisce un valore di stile con le modifiche richieste.  
  
 [!code-csharp[ManagedDOMStyles#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/StyleGenerator.cs#1)]
 [!code-vb[ManagedDOMStyles#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/StyleGenerator.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.HtmlElement>