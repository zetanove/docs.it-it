---
title: "extern alias (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "alias_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "alias [C#], extern (parola chiave)"
  - "alias, extern (parola chiave)"
  - "extern alias (parola chiave) [C#]"
ms.assetid: f487bf4f-c943-4fca-851b-e540c83d9027
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# extern alias (Riferimenti per C#)
È necessario far riferimento a due versioni di assembly che dispongono degli stessi nomi di tipo completi.  Ad esempio, è necessario utilizzare due o più versioni di un assembly nella stessa applicazione.  Utilizzando un alias di assembly esterno, può essere eseguito il wrapping degli spazi dei nomi di ciascun assembly all'interno degli spazi dei nomi a livello radice denominati dall'alias, consentendone l'utilizzo nello stesso file.  
  
> [!NOTE]
>  La parola chiave [extern](../../../csharp/language-reference/keywords/extern.md) viene anche utilizzata come modificatore di metodo, che dichiara un metodo scritto in codice non gestito.  
  
 Per far riferimento a due assembly con gli stessi nomi di tipo completi, è necessario specificare un alias al prompt dei comandi, come illustrato di seguito:  
  
 `/r:GridV1=grid.dll`  
  
 `/r:GridV2=grid20.dll`  
  
 In questo modo vengono creati gli alias extern `GridV1` e `GridV2`.  Per utilizzare questi alias all'interno di un programma, far riferimento a essi tramite la parola chiave `extern`.  Di seguito è riportato un esempio:  
  
 `extern alias GridV1;`  
  
 `extern alias GridV2;`  
  
 Ogni dichiarazione di alias extern introduce uno spazio dei nomi aggiuntivo a livello radice che affianca lo spazio dei nomi globale, ma non si trova al suo interno.  In questo modo, è possibile far riferimento ai tipi di ciascun assembly senza ambiguità, utilizzando il nome completo che dispone di una radice nell'alias dello spazio dei nomi appropriato.  
  
 Nell'esempio precedente, l'oggetto `GridV1::Grid` rappresenta il controllo griglia dell'oggetto `grid.dll` e l'oggetto `GridV2::Grid` rappresenta il controllo griglia dell'oggetto `grid20.dll`.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per spazi dei nomi](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [Operatore ::](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)   
 [\/reference \(Import Metadata\)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)