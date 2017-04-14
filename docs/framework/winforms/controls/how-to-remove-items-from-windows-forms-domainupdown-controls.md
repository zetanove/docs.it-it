---
title: "Procedura: rimuovere elementi dai controlli DomainUpDown Windows Form | Microsoft Docs"
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
  - "DomainUpDown (controllo) [Windows Form], rimozione di elementi"
  - "controllo pulsante di selezione, rimozione di elementi"
ms.assetid: e70f5cbc-b497-41a9-975a-344c00e56ed2
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: rimuovere elementi dai controlli DomainUpDown Windows Form
È possibile rimuovere elementi dal controllo <xref:System.Windows.Forms.DomainUpDown> Windows Form chiamando il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A> o <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A> della classe <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection>.  Il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A> rimuove un elemento specifico, mentre il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A> rimuove un elemento in base alla posizione.  
  
### Per rimuovere un elemento  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A> della classe <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection> per rimuovere un elemento in base al nome.  
  
    ```vb  
    DomainUpDown1.Items.Remove("noodles")  
  
    ```  
  
    ```csharp  
    domainUpDown1.Items.Remove("noodles");  
  
    ```  
  
    ```cpp  
    domainUpDown1->Items->Remove("noodles");  
    ```  
  
     In alternativa  
  
-   Utilizzare il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A> per rimuovere un elemento in base alla posizione.  
  
    ```vb  
    ' Removes the first item in the list.  
    DomainUpDown1.Items.RemoveAt(0)  
  
    ```  
  
    ```csharp  
    // Removes the first item in the list.  
    domainUpDown1.Items.RemoveAt(0);  
  
    ```  
  
    ```cpp  
    // Removes the first item in the list.  
    domainUpDown1->Items->RemoveAt(0);  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.DomainUpDown>   
 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Remove%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.RemoveAt%2A?displayProperty=fullName>   
 [Controllo DomainUpDown](../../../../docs/framework/winforms/controls/domainupdown-control-windows-forms.md)   
 [Cenni preliminari sul controllo DomainUpDown](../../../../docs/framework/winforms/controls/domainupdown-control-overview-windows-forms.md)