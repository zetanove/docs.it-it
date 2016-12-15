---
title: "Procedura: utilizzare espressioni lambda al di fuori di LINQ (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "espressioni lambda [C#], fuori da LINQ"
ms.assetid: 2b519274-6ee4-4455-ab2e-aed67dbfd07c
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: utilizzare espressioni lambda al di fuori di LINQ (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le espressioni lambda non sono limitate alle query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].  È possibile utilizzarle dove è previsto un valore del delegato, ovvero dove può essere utilizzato un metodo anonimo.  Nell'esempio seguente viene illustrato come utilizzare un'espressione lambda in un gestore eventi Windows Form.  I tipi degli input \(<xref:System.Object> e <xref:System.Windows.Forms.MouseEventArgs>\) vengono dedotti dal compilatore e non dovevano essere forniti in modo esplicito nei parametri di input delle espressioni lambda.  
  
## Esempio  
  
```  
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
        // Use a lambda expression to define an event handler.  
       this.Click += (s, e) => { MessageBox.Show(((MouseEventArgs)e).Location.ToString());};  
    }  
}  
```  
  
## Vedere anche  
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)