---
title: "Procedura: impostare e restituire valori numerici con il controllo NumericUpDown Windows Form | Microsoft Docs"
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
  - "valori numerici, Windows Form"
  - "NumericUpDown (controllo) [Windows Form], impostazione e restituzione di valori"
  - "controlli Windows Form, NumericUpDown"
  - "Windows Form, valori numerici"
ms.assetid: 5bd8f8cd-4c12-49ea-9cc3-2a647d064689
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: impostare e restituire valori numerici con il controllo NumericUpDown Windows Form
Il valore numerico del controllo <xref:System.Windows.Forms.NumericUpDown> Windows Form è determinato dalla relativa proprietà <xref:System.Windows.Forms.NumericUpDown.Value%2A>.  È possibile creare verifiche condizionali per il valore del controllo come per qualsiasi altra proprietà.  Una volta impostata, la proprietà <xref:System.Windows.Forms.NumericUpDown.Value%2A> può essere modificata direttamente scrivendo il codice necessario per eseguire operazioni su di essa. È altrimenti possibile chiamare i metodi <xref:System.Windows.Forms.NumericUpDown.UpButton%2A> e <xref:System.Windows.Forms.NumericUpDown.DownButton%2A>.  
  
### Per impostare il valore numerico  
  
1.  Assegnare un valore alla proprietà <xref:System.Windows.Forms.NumericUpDown.Value%2A> all'interno del codice oppure nella finestra Proprietà.  
  
    ```vb  
    NumericUpDown1.Value = 55  
  
    ```  
  
    ```csharp  
    numericUpDown1.Value = 55;  
  
    ```  
  
    ```cpp  
    numericUpDown1->Value = 55;  
    ```  
  
     In alternativa  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.NumericUpDown.UpButton%2A> o <xref:System.Windows.Forms.NumericUpDown.DownButton%2A> per incrementare o ridurre il valore in base alla quantità specificata nella proprietà <xref:System.Windows.Forms.NumericUpDown.Increment%2A>.  
  
    ```vb  
    NumericUpDown1.UpButton()  
  
    ```  
  
    ```csharp  
    numericUpDown1.UpButton();  
  
    ```  
  
    ```cpp  
    numericUpDown1->UpButton();  
    ```  
  
### Per restituire il valore numerico  
  
-   Accedere alla proprietà <xref:System.Windows.Forms.NumericUpDown.Value%2A> all'interno del codice.  
  
    ```vb  
    If NumericUpDown1.Value >= 65 Then  
       MessageBox.Show("Age is: " & NumericUpDown1.Value.ToString)  
    Else  
       MessageBox.Show("The customer is ineligible for a senior citizen discount.")  
    End If  
  
    ```  
  
    ```csharp  
    if(numericUpDown1.Value >= 65)  
    {  
       MessageBox.Show("Age is: " + numericUpDown1.Value.ToString());  
    }  
    else  
    {  
       MessageBox.Show("The customer is ineligible for a senior citizen discount.");  
    }  
  
    ```  
  
    ```cpp  
    if(numericUpDown1->Value >= 65)  
    {  
       MessageBox::Show(String::Concat("Age is: ",  
          numericUpDown1->Value.ToString()));  
    }  
    else  
    {  
       MessageBox::Show  
          ("The customer is ineligible for a senior citizen discount.");  
    }  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.NumericUpDown>   
 <xref:System.Windows.Forms.NumericUpDown.Value%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.NumericUpDown.Increment%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.NumericUpDown.UpButton%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.NumericUpDown.DownButton%2A?displayProperty=fullName>   
 [Controllo NumericUpDown](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md)   
 [Cenni preliminari sul controllo NumericUpDown](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md)