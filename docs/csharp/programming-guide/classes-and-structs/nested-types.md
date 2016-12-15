---
title: "Tipi annidati (Guida per programmatori C#) | Microsoft Docs"
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
  - "tipi annidati [C#]"
ms.assetid: f2e1b315-e3d1-48ce-977f-7bae0960ba99
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Tipi annidati (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per tipo annidato si intende un tipo definito all'interno di una [classe](../../../csharp/language-reference/keywords/class.md) o di uno [struct](../../../csharp/language-reference/keywords/struct.md).  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideObjects#68](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_1.cs)]  
  
 Sia che il tipo esterno sia una classe o uno struct, per impostazione predefinita i tipi annidati sono [private](../../../csharp/language-reference/keywords/private.md), ma possono essere convertiti in [public](../../../csharp/language-reference/keywords/public.md), protected internal, [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o [private](../../../csharp/language-reference/keywords/private.md).  Nell'esempio precedente `Nested` non è accessibile a tipi esterni, ma può essere reso public nel seguente modo:  
  
 [!code-cs[csProgGuideObjects#69](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_2.cs)]  
  
 Il tipo interno o annidato può accedere al tipo esterno o che lo contiene.  Per accedere al tipo che lo contiene, passarlo come costruttore al tipo annidato.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideObjects#70](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_3.cs)]  
  
 Un tipo annidato può accedere a tutti i membri accessibili al tipo contenitore.  Può accedere a membri privati e protetti del tipo che li contengono, inclusi tutti i membri protetti ereditati.  
  
 Nella dichiarazione precedente il nome completo della classe `Nested` è `Container.Nested`.  Questo nome viene utilizzato per creare una nuova istanza della classe annidata, come illustrato di seguito:  
  
 [!code-cs[csProgGuideObjects#71](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/nested-types_4.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)