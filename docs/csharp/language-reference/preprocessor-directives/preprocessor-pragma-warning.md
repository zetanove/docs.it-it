---
title: "#pragma warning (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#pragma warning"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#pragma warning [C#]"
ms.assetid: 723493d5-9753-4cec-babb-54e2b8eb36b6
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# #pragma warning (Riferimenti per C#)
`#pragma warning` consente di attivare o disabilitare alcuni avvisi.  
  
## Sintassi  
  
```  
#pragma warning disable warning-list  
#pragma warning restore warning-list  
```  
  
#### Parametri  
 `warning-list`  
 Elenco separato da virgole di numeri di avviso.  Immettere soltanto i numeri, senza prefisso "CS".  
  
 Quando non viene specificato alcun numero di avviso, con `disable` tutti gli avvisi vengono disabilitati e con `restore` vengono attivati.  
  
> [!NOTE]
>  Per trovare i numeri di avviso in Visual Studio, compilare il progetto, quindi individuare i numeri di avviso nella finestra **Output**.  
  
## Esempio  
  
```  
// pragma_warning.cs  
using System;  
  
#pragma warning disable 414, 3021  
[CLSCompliant(false)]  
public class C  
{  
    int i = 1;  
    static void Main()  
    {  
    }  
}  
#pragma warning restore 3021  
[CLSCompliant(false)]  // CS3021  
public class D  
{  
    int i = 1;  
    public static void F()  
    {  
    }  
}  
```  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)   
 [C\# Compiler Errors](../../../csharp/language-reference/compiler-messages/index.md)