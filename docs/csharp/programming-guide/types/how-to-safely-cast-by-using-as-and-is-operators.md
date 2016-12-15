---
title: "Procedura: eseguire il cast sicuro tramite gli operatori as e is (Guida per programmatori C#) | Microsoft Docs"
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
  - "as (operatore) [C#]"
  - "operatori di cast [C#], as e is (operatori)"
  - "is (operatore) [C#]"
ms.assetid: c1176cea-1426-4a44-8570-3eadafa58863
caps.latest.revision: 10
caps.handback.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: eseguire il cast sicuro tramite gli operatori as e is (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Poiché gli oggetti sono polimorfici, per una variabile di un tipo di classe di base è possibile contenere un tipo derivato.  Per accedere al metodo del tipo derivato, è necessario eseguire nuovamente il cast del valore nel tipo derivato.  Tuttavia, tentare un cast semplice in questi casi crea il rischio della generazione di <xref:System.InvalidCastException>.  Per questo motivo C\# fornisce gli operatori [is](../../../csharp/language-reference/keywords/is.md) e [as](../../../csharp/language-reference/keywords/as.md).  È possibile utilizzare questi operatori per verificare se un cast riuscirà senza provocare la generazione di un'eccezione.  In generale, l'operatore `as` è più efficiente perché, se è possibile effettuare il cast, ne restituisce il valore.  L'operatore `is` restituisce solo un valore booleano.  Si può pertanto utilizzare quando si desidera solo determinare il tipo di un oggetto ma non si deve realmente eseguirne il cast.  
  
## Esempio  
 Negli esempi seguenti viene mostrato come utilizzare gli operatori `is` e `as` per eseguire il cast da un tipo riferimento a un altro senza il rischio della generazione di un'eccezione.  Nell'esempio viene mostrato anche come utilizzare l'operatore `as` con i tipi valore nullable.  
  
 [!code-cs[csProgGuideTypes#40](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-safely-cast-by-using-as-and-is-operators_1.cs)]  
  
## Vedere anche  
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)