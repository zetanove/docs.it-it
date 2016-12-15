---
title: "Procedura: eseguire il cast sicuro da bool? a bool (Guida per programmatori C#) | Microsoft Docs"
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
  - "cast [C#], tipi nullable"
  - "nullable (tipi) [C#], cast da bool? a bool"
ms.assetid: e06e4274-a443-422d-8ef1-9dbf9df55237
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: eseguire il cast sicuro da bool? a bool (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il tipo `bool?` nullable può contenere tre valori diversi: `true`, `false` e `null`.  Non è pertanto possibile utilizzare il tipo `bool?` in istruzioni condizionali, ad esempio con `if`, `for` o `while`.  Il codice seguente, ad esempio, causa un errore del compilatore:  
  
```  
bool? b = null;  
if (b) // Error CS0266.  
{  
}  
```  
  
 Questa operazione non è consentita, in quanto il significato di `null` non è chiaro nel contesto di un'istruzione condizionale.  Per utilizzare un valore `bool?` in un'istruzione condizionale, controllare innanzitutto la proprietà <xref:System.Nullable%601.HasValue%2A> per garantire che il valore non sia `null`, quindi eseguire il cast a `bool`.  Per ulteriori informazioni, vedere [bool](../../../csharp/language-reference/keywords/bool.md).  Se si esegue il cast su un valore `bool?` con valore `null`, verrà generata un'eccezione <xref:System.InvalidOperationException> nel test condizionale.  Nell'esempio seguente viene illustrato un modo per eseguire il cast in modo sicuro da `bool?` a `bool`:  
  
## Esempio  
  
```c#  
bool? test = null;  
// Other code that may or may not  
// give a value to test.  
if(!test.HasValue) //check for a value  
{  
    // Assume that IsInitialized  
    // returns either true or false.  
    test = IsInitialized();  
}  
if((bool)test) //now this cast is safe  
{  
   // Do something.  
}  
```  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave letterali](../../../csharp/language-reference/keywords/literal-keywords.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [?? Operatore](../../../csharp/language-reference/operators/null-conditional-operator.md)