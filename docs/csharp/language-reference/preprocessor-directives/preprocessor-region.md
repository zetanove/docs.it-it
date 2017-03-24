---
title: "#region (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#region"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#region (direttiva) [C#]"
ms.assetid: 672c87d1-9771-4f64-ab3f-0ad3d4ffb2b4
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# #region (Riferimenti per C#)
`#region` consente di specificare un blocco di codice che è possibile espandere o comprimere tramite la funzionalità [Struttura](/visual-studio/ide/outlining) dell'editor di codice di Visual Studio.  Nei file di codice più lunghi, può essere comodo comprimere o nascondere una o più aree in modo da potersi concentrare sulla parte del file su cui si sta lavorando.  Nell'esempio seguente viene illustrato come definire un'area.  
  
```  
  
      #region MyClass definition  
public class MyClass   
{  
    static void Main()   
    {  
    }  
}  
#endregion  
```  
  
## Note  
 Un blocco `#region` deve terminare con la direttiva [\#endregion](../../../csharp/language-reference/preprocessor-directives/preprocessor-endregion.md).  
  
 Non è possibile sovrapporre un blocco `#region` con un blocco [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md).  È tuttavia possibile annidare un blocco `#region` in un blocco `#if` e un blocco `#if` in un blocco `#region`.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)