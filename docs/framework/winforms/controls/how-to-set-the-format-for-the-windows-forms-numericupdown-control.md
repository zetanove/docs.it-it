---
title: "Procedura: impostare il formato per il controllo NumericUpDown Windows Form | Microsoft Docs"
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
  - "NumericUpDown (controllo) [Windows Form], formattazione di valori"
  - "controlli di scorrimento, formattazione di valori numerici"
ms.assetid: fa7c5557-6bfb-45b2-975d-8887b23b0ba0
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: impostare il formato per il controllo NumericUpDown Windows Form
È possibile configurare la visualizzazione dei valori nel controllo <xref:System.Windows.Forms.NumericUpDown> Windows Form.  La proprietà <xref:System.Windows.Forms.NumericUpDown.DecimalPlaces%2A> determina il numero di cifre decimali visualizzate; l'impostazione predefinita corrisponde a 0.  La proprietà <xref:System.Windows.Forms.NumericUpDown.ThousandsSeparator%2A> determina se inserire un separatore dopo ogni tre cifre decimali; l'impostazione predefinita corrisponde a `false`.  Se la proprietà <xref:System.Windows.Forms.NumericUpDown.Hexadecimal%2A> viene impostata su `true`, il controllo potrà visualizzare i valori in formato esadecimale anziché decimale; il valore predefinito è `false`.  
  
### Per formattare il valore numerico  
  
-   Visualizzare un valore decimale impostando la proprietà <xref:System.Windows.Forms.NumericUpDown.DecimalPlaces%2A> su Integer e la proprietà <xref:System.Windows.Forms.NumericUpDown.ThousandsSeparator%2A> su `true` o `false`.  
  
    ```vb  
    NumericUpDown1.DecimalPlaces = 2  
    NumericUpDown1.ThousandsSeparator = True  
  
    ```  
  
    ```csharp  
    numericUpDown1.DecimalPlaces = 2;  
    numericUpDown1.ThousandsSeparator = true;  
  
    ```  
  
    ```cpp  
    numericUpDown1->DecimalPlaces = 2;  
    numericUpDown1->ThousandsSeparator = true;  
    ```  
  
     In alternativa  
  
-   Visualizzare un valore esadecimale impostando la proprietà <xref:System.Windows.Forms.NumericUpDown.Hexadecimal%2A> su `true`.  
  
    ```vb  
    NumericUpDown1.Hexadecimal = True  
  
    ```  
  
    ```csharp  
    numericUpDown1.Hexadecimal = true;  
  
    ```  
  
    ```cpp  
    numericUpDown1->Hexadecimal = true;  
    ```  
  
    > [!NOTE]
    >  Anche nel caso in cui il valore venga visualizzato nel form come esadecimale, qualsiasi test eseguito sulla proprietà <xref:System.Windows.Forms.NumericUpDown.Value%2A> ne controllerà il valore decimale.  
  
## Vedere anche  
 <xref:System.Windows.Forms.NumericUpDown>   
 [Controllo NumericUpDown](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md)   
 [Cenni preliminari sul controllo NumericUpDown](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md)