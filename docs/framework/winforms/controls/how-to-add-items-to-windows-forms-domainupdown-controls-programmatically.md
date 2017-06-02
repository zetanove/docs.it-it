---
title: "Procedura: aggiungere elementi ai controlli DomainUpDown Windows Form a livello di codice | Microsoft Docs"
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
  - "DomainUpDown (controllo) [Windows Form], aggiunta di elementi"
  - "controllo pulsante di selezione, aggiunta di elementi"
ms.assetid: fd31d314-33eb-4181-90f8-d32ed0c4e072
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: aggiungere elementi ai controlli DomainUpDown Windows Form a livello di codice
È possibile aggiungere elementi al controllo <xref:System.Windows.Forms.DomainUpDown> Windows Form mediante codice.  Per aggiungere elementi alla proprietà <xref:System.Windows.Forms.DomainUpDown.Items%2A> del controllo, chiamare il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A> o <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Insert%2A> della classe <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection>.  Il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A> aggiunge un elemento alla fine di una raccolta, mentre il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Insert%2A> aggiunge un elemento in una posizione specificata.  
  
### Per aggiungere un nuovo elemento  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A> per aggiungere un elemento alla fine dell'elenco di elementi.  
  
    ```vb  
    DomainUpDown1.Items.Add("noodles")  
  
    ```  
  
    ```csharp  
    domainUpDown1.Items.Add("noodles");  
  
    ```  
  
    ```cpp  
    domainUpDown1->Items->Add("noodles");  
    ```  
  
     In alternativa  
  
2.  Utilizzare il metodo <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Insert%2A> per inserire un elemento in una posizione specificata all'interno dell'elenco.  
  
    ```vb  
    ' Inserts an item at the third position in the list  
    DomainUpDown1.Items.Insert(2, "rice")  
  
    ```  
  
    ```csharp  
    // Inserts an item at the third position in the list  
    domainUpDown1.Items.Insert(2, "rice");  
  
    ```  
  
    ```cpp  
    // Inserts an item at the third position in the list  
    domainUpDown1->Items->Insert(2, "rice");  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.DomainUpDown>   
 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A?displayProperty=fullName>   
 <xref:System.Collections.ArrayList.Insert%2A?displayProperty=fullName>   
 [Controllo DomainUpDown](../../../../docs/framework/winforms/controls/domainupdown-control-windows-forms.md)   
 [Cenni preliminari sul controllo DomainUpDown](../../../../docs/framework/winforms/controls/domainupdown-control-overview-windows-forms.md)