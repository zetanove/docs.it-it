---
title: "Accesso ai membri non esposti del Document Object Model HTML gestito | Microsoft Docs"
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
  - "DOM HTML gestiti, accesso a membri non esposti"
  - "membri non esposti"
ms.assetid: 762295bd-2355-4aa7-b43c-5bff997a33e6
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Accesso ai membri non esposti del Document Object Model HTML gestito
Il Document Object Model \(DOM\) HTML gestito contiene una classe denominata <xref:System.Windows.Forms.HtmlElement> che espone le proprietà, i metodi e gli eventi che tutti gli elementi HTML hanno in comune.  Talvolta, tuttavia, è necessario accedere a membri non esposti direttamente dall'interfaccia gestita.  In questo argomento vengono analizzati due tipi di accesso a membri non esposti, tra cui funzioni [!INCLUDE[jsprjscript](../../../../includes/jsprjscript-md.md)] e VBScript definite all'interno di una pagina Web.  
  
## Accesso a membri non esposti attraverso interfacce gestite  
 Le classi <xref:System.Windows.Forms.HtmlDocument> e <xref:System.Windows.Forms.HtmlElement> forniscono quattro metodi per l'accesso a membri non esposti.  Nella tabella seguente sono illustrati i tipi e i metodi corrispondenti.  
  
|Tipo di membro|Metodo\/metodi|  
|--------------------|--------------------|  
|Proprietà \(<xref:System.Windows.Forms.HtmlElement>\)|<xref:System.Windows.Forms.HtmlElement.GetAttribute%2A><br /><br /> <xref:System.Windows.Forms.HtmlElement.SetAttribute%2A>|  
|Metodi|<xref:System.Windows.Forms.HtmlElement.InvokeMember%2A>|  
|Eventi \(<xref:System.Windows.Forms.HtmlDocument>\)|<xref:System.Windows.Forms.HtmlDocument.AttachEventHandler%2A><br /><br /> <xref:System.Windows.Forms.HtmlDocument.DetachEventHandler%2A>|  
|Eventi \(<xref:System.Windows.Forms.HtmlElement>\)|<xref:System.Windows.Forms.HtmlElement.AttachEventHandler%2A><br /><br /> <xref:System.Windows.Forms.HtmlElement.DetachEventHandler%2A>|  
|Eventi \(<xref:System.Windows.Forms.HtmlWindow>\)|<xref:System.Windows.Forms.HtmlWindow.AttachEventHandler%2A><br /><br /> <xref:System.Windows.Forms.HtmlWindow.DetachEventHandler%2A>|  
  
 Quando si utilizzano tali metodi, si presume la presenza di un elemento del tipo sottostante corretto.  Si supponga di essere in attesa dell'evento `Submit` di un elemento `FORM` in una pagina HTML allo scopo di sottoporre i valori del `FORM` a pre\-elaborazione prima che l'utente li inoltri al server.  In una situazione ideale, se si esercita il controllo sull'HTML, si definirebbe per il `FORM` un attributo `ID` univoco.  
  
```  
<HTML>  
  
    <HEAD>  
        <TITLE>Form Page</TITLE>  
    </HEAD>  
  
    <BODY>  
        <FORM ID="form1">  
             ... form fields defined here ...  
        </FORM>  
    </BODY>  
  
</HTML>  
```  
  
 Dopo il caricamento della pagina nel controllo <xref:System.Windows.Forms.WebBrowser>, è possibile utilizzare il metodo <xref:System.Windows.Forms.HtmlDocument.GetElementById%2A> per recuperare il `FORM` in fase di esecuzione utilizzando `form1` come argomento.  
  
 [!code-csharp[System.Windows.Forms.HtmlElement#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.HtmlElement/CS/Form1.cs#10)]
 [!code-vb[System.Windows.Forms.HtmlElement#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.HtmlElement/VB/Form1.vb#10)]  
  
## Accesso a interfacce non gestite  
 Per accedere a membri non esposti nel DOM HTML gestito, è inoltre possibile utilizzare le interfacce Component Object Model \(COM\) non gestite esposte da ogni classe DOM.  Tale operazione è consigliabile se è necessario eseguire varie chiamate a membri non esposti o se i membri non esposti restituiscono altre interfacce non gestite di cui non è stato eseguito il wrapping nel DOM HTML gestito.  
  
 Nella tabella seguente sono illustrate tutte le interfacce non gestite esposte attraverso il DOM HTML gestito.  Fare clic sui collegamenti per visualizzare una spiegazione dell'utilizzo e il codice di esempio.  
  
|Type|Interfaccia non gestita|  
|----------|-----------------------------|  
|<xref:System.Windows.Forms.HtmlDocument>|<xref:System.Windows.Forms.HtmlDocument.DomDocument%2A>|  
|<xref:System.Windows.Forms.HtmlElement>|<xref:System.Windows.Forms.HtmlElement.DomElement%2A>|  
|<xref:System.Windows.Forms.HtmlWindow>|<xref:System.Windows.Forms.HtmlWindow.DomWindow%2A>|  
|<xref:System.Windows.Forms.HtmlHistory>|<xref:System.Windows.Forms.HtmlHistory.DomHistory%2A>|  
  
 Il modo più semplice per utilizzare le interfacce COM consiste nell' aggiungere un riferimento a una libreria non gestita DOM HTML \(MSHTML.dll\) dall' applicazione, sebbene sia non supportato.  Per ulteriori informazioni, vedere [Articolo della Knowledge Base 934368](http://support.microsoft.com/kb/934368).  
  
## Accesso a funzioni di script  
 In una pagina HTML possono essere definite una o più funzioni mediante l'utilizzo di un linguaggio di script come [!INCLUDE[jsprjscript](../../../../includes/jsprjscript-md.md)] o VBScript.  Tali funzioni sono inserite all'interno di un tag `SCRIPT` nella pagina ed è possibile eseguirle su richiesta o in risposta a un evento sul DOM.  
  
 È possibile chiamare qualsiasi funzione di script definita in una pagina HTML utilizzando il metodo <xref:System.Windows.Forms.HtmlDocument.InvokeScript%2A>.  Se viene restituito un elemento HTML, è possibile utilizzare un cast per convertire il risultato in una classe <xref:System.Windows.Forms.HtmlElement>.  Per informazioni dettagliate e il codice di esempio, vedere <xref:System.Windows.Forms.HtmlDocument.InvokeScript%2A>.  
  
## Vedere anche  
 [Utilizzare il Document Object Model HTML gestito](../../../../docs/framework/winforms/controls/using-the-managed-html-document-object-model.md)