---
title: "How to: Resize Windows Forms | Microsoft Docs"
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
  - "resizing Windows Forms"
  - "Windows Forms, resizing"
ms.assetid: 5d9dd47e-e68c-48c9-a0a3-a9ff34ba009d
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# How to: Resize Windows Forms
È possibile specificare le dimensioni del Windows Form in diversi modi.  È possibile modificare sia l'altezza che la larghezza del form a livello di codice impostando un nuovo valore per la proprietà <xref:System.Windows.Forms.Form.Size%2A> o modificare le singole proprietà <xref:System.Windows.Forms.Control.Height%2A> o <xref:System.Windows.Forms.Control.Width%2A>.  Se si usa [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], le dimensioni possono essere modificate usando Progettazione Windows Form.  Vedere anche [Procedura: Ridimensionare Windows Form usando la finestra di progettazione](http://msdn.microsoft.com/library/37k2zkwx\(v=vs.110\)).  
  
### Per ridimensionare un form a livello di codice  
  
-   Definire le dimensioni di un form in fase di esecuzione impostando la proprietà <xref:System.Windows.Forms.Form.Size%2A> del form.  
  
     Nell'esempio di codice riportato di seguito le dimensioni del form sono impostate su 100 × 100 pixel.  
  
    ```vb  
    Form1.Size = New System.Drawing.Size(100, 100)  
  
    ```  
  
    ```csharp  
    Form1.Size = new System.Drawing.Size(100, 100);  
  
    ```  
  
    ```cpp  
    Form1->Size = System::Drawing::Size(100, 100);  
    ```  
  
### Per modificare larghezza e altezza di un form a livello di codice  
  
-   Una volta definita la proprietà <xref:System.Windows.Forms.Form.Size%2A>, è possibile modificare l'altezza o la larghezza del form usando la proprietà <xref:System.Windows.Forms.Control.Width%2A> o <xref:System.Windows.Forms.Control.Height%2A>.  
  
     Nell'esempio di codice riportato di seguito viene illustrato come impostare la larghezza del form su 300 pixel dal bordo sinistro del form, mentre l'altezza rimane costante.  
  
    ```vb  
    Form1.Width = 300  
  
    ```  
  
    ```csharp  
    Form1.Width = 300;  
  
    ```  
  
    ```cpp  
    Form1->Width = 300;  
    ```  
  
     \-oppure\-  
  
     Modificare la proprietà <xref:System.Drawing.Size.Width%2A> o la proprietà <xref:System.Drawing.Size.Height%2A> impostando la proprietà <xref:System.Windows.Forms.Form.Size%2A>.  
  
     Tuttavia, come illustrato nell'esempio di codice riportato di seguito, questo approccio risulta più complesso rispetto alla semplice impostazione delle proprietà <xref:System.Windows.Forms.Control.Width%2A> o <xref:System.Windows.Forms.Control.Height%2A>.  
  
    ```vb  
    Form1.Size = New Size(300, Form1.Size.Height)  
  
    ```  
  
    ```csharp  
    Form1.Size = new Size(300, Form1.Size.Height);  
  
    ```  
  
    ```cpp  
    Form1->Size = System::Drawing::Size(300, Form1->Size.Height);  
    ```  
  
### Per modificare le dimensioni del form in modo incrementale a livello di codice  
  
-   Per incrementare le dimensioni del form, impostare le proprietà <xref:System.Drawing.Size.Width%2A> o <xref:System.Drawing.Size.Height%2A>.  
  
     Nell'esempio di codice riportato di seguito la larghezza del form viene aumentata di 200 pixel rispetto all'impostazione corrente.  
  
    ```vb  
    Form1.Width += 200  
  
    ```  
  
    ```csharp  
    Form1.Width += 200;  
  
    ```  
  
    ```cpp  
    Form1->Width += 200;  
    ```  
  
    > [!CAUTION]
    >  Usare sempre la proprietà <xref:System.Drawing.Size.Height%2A> o la proprietà <xref:System.Drawing.Size.Width%2A> per modificare le dimensioni di un form, a meno che le dimensioni di altezza e larghezza non vengano impostate contemporaneamente mediante la proprietà <xref:System.Windows.Forms.Form.Size%2A> in una nuova struttura <xref:System.Drawing.Size>.  La proprietà <xref:System.Windows.Forms.Form.Size%2A> restituisce una struttura <xref:System.Drawing.Size>, che è un tipo di valore.  Non è possibile assegnare un nuovo valore alla proprietà di un tipo di valore.  Di conseguenza, l'esempio di codice riportato di seguito non verrà compilato.  
  
    ```vb  
    ' NOTE: CODE WILL NOT COMPILE  
    Dim f As New Form()  
    f.Size.Width += 100  
  
    ```  
  
    ```csharp  
    // NOTE: CODE WILL NOT COMPILE  
    Form f = new Form();  
    f.Size.Width += 100;  
  
    ```  
  
    ```cpp  
    // NOTE: CODE WILL NOT COMPILE  
    Form^ f = gcnew Form();  
    f->Size->X += 100;  
    ```  
  
## Vedere anche  
 [Getting Started with Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)   
 [Enhancing Windows Forms Applications](../../../docs/framework/winforms/advanced/index.md)