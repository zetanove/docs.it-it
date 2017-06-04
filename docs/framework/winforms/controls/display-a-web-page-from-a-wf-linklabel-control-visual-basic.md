---
title: "Procedura: visualizzare una pagina Web da un controllo LinkLabel di Windows Form (Visual Basic) | Microsoft Docs"
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
  - "LinkLabel1_LinkClicked"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "esempi [Windows Form], LinkLabel (controllo)"
  - "collegamento, a pagine Web da form"
  - "LinkLabel (controllo) [Windows Form], esempi"
  - "pagine Web, visualizzazione"
  - "Windows Form, collegamento a pagine Web"
ms.assetid: 477a7398-5971-4de3-b24c-f49f32bdb28a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: visualizzare una pagina Web da un controllo LinkLabel di Windows Form (Visual Basic)
Nell'esempio riportato di seguito viene visualizzata una pagina Web nel browser predefinito quando un utente fa clic su un controllo <xref:System.Windows.Forms.LinkLabel> di un Windows Form.  
  
## Esempio  
  
```vb  
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e _  
As System.EventArgs) Handles MyBase.Load  
    LinkLabel1.Text = "Click here to get more info."  
    LinkLabel1.Links.Add(6, 4, "www.microsoft.com")  
End Sub  
Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, ByVal _  
e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) Handles _  
LinkLabel1.LinkClicked  
    System.Diagnostics.Process.Start(e.Link.LinkData.ToString())  
End Sub  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un Windows Form denominato `Form1`.  
  
-   Un controllo <xref:System.Windows.Forms.LinkLabel> denominato `LinkLabel1`.  
  
-   Una connessione Internet attiva.  
  
## Sicurezza di .NET Framework  
 Per eseguire la chiamata al metodo <xref:System.Diagnostics.Process.Start%2A> è necessaria un'attendibilità completa.  Per ulteriori informazioni, vedere <xref:System.Security.SecurityException>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.LinkLabel>   
 [Controllo LinkLabel](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)