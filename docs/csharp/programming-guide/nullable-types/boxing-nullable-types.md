---
title: "Conversione boxing di tipi nullable (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "boxing [C#], tipi nullable"
  - "nullable (tipi) [C#], boxing e unboxing"
  - "unboxing [C#], tipi nullable"
ms.assetid: bdb5b626-abc0-405d-8f64-0f0a0bf883a4
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Conversione boxing di tipi nullable (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La conversione boxing di oggetti basati su tipi nullable viene eseguita solo se l'oggetto non è null.  Se l'oggetto <xref:System.Nullable%601.HasValue%2A> è `false`, anziché eseguire la conversione boxing, il riferimento a un oggetto viene assegnato a `null`.  Di seguito è riportato un esempio:  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Se l'oggetto non è null, ovvero se l'oggetto <xref:System.Nullable%601.HasValue%2A> è `true`, la conversione boxing viene eseguita, ma viene sottoposto a boxing solo il tipo sottostante su cui è basato l'oggetto nullable.  La conversione boxing di un valore nullable non null viene eseguita sul tipo di valore stesso, non sul tipo <xref:System.Nullable%601?displayProperty=fullName> che lo incapsula.  Di seguito è riportato un esempio:  
  
```  
bool? b = false;  
int? i = 44;  
object bBoxed = b; // bBoxed contains a boxed bool.  
object iBoxed = i; // iBoxed contains a boxed int.  
```  
  
 I due oggetti boxed sono identici a quelli creati mediante il boxing di tipi non nullable.  Proprio come per i tipi boxed non nullable, è possibile eseguirne la conversione unboxing in tipi nullable, come nell'esempio riportato di seguito:  
  
```  
bool? b2 = (bool?)bBoxed;  
int? i2 = (int?)iBoxed;  
```  
  
## Note  
 Il comportamento dei tipi nullable boxed presenta due vantaggi:  
  
1.  Gli oggetti nullable e la controparte boxed possono essere testati per verificare se sono null:  
  
    ```  
    bool? b = null;  
    object boxedB = b;  
    if (b == null)  
    {  
      // True.  
    }  
    if (boxedB == null)  
    {  
      // Also true.  
    }  
    ```  
  
2.  I tipi nullable boxed supportano completamente le funzionalità del tipo sottostante:  
  
    ```  
    double? d = 44.4;  
    object iBoxed = d;  
    // Access IConvertible interface implemented by double.  
    IConvertible ic = (IConvertible)iBoxed;  
    int i = ic.ToInt32(null);  
    string str = ic.ToString();  
    ```  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [Procedura: identificare un tipo nullable](../../../csharp/programming-guide/nullable-types/how-to-identify-a-nullable-type.md)