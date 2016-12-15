---
title: "Confronto di uguaglianze (Guida per programmatori C#) | Microsoft Docs"
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
  - "uguaglianza oggetti [C#]"
ms.assetid: 10b865ea-4e7b-4127-9242-c9b8f57d9f04
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Confronto di uguaglianze (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È talvolta necessario confrontare l'uguaglianza di due valori.  In alcuni casi, si testa l'*uguaglianza di valori*, detta anche *equivalenza*, ovvero si verifica che i valori contenuti dalle due variabili siano uguali.  In altri casi, è necessario determinare se due variabili si riferiscono allo stesso oggetto sottostante in memoria.  Questo tipo di uguaglianza è detto *uguaglianza di riferimenti* o *identità*.  In questo argomento vengono descritti questi due tipi di uguaglianza e vengono forniti i collegamenti ad altri argomenti per ulteriori informazioni.  
  
## Uguaglianza di riferimenti  
 Per uguaglianza dei riferimenti si intende che due riferimenti all'oggetto fanno riferimento allo stesso oggetto sottostante.  Questa situazione può verificarsi tramite una semplice assegnazione, come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideStatements#18](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/equality-comparisons_1.cs)]  
  
 In questo codice, vengono creati due oggetti, ma dopo l'istruzione di assegnazione, entrambi riferimenti puntano allo stesso oggetto.  Presentano pertanto l'uguaglianza dei riferimenti.  Utilizzare il metodo <xref:System.Object.ReferenceEquals%2A> per stabilire se due riferimenti puntano allo stesso oggetto.  
  
 Il concetto di uguaglianza dei riferimenti si applica solo ai tipi di riferimento.  Gli oggetti tipo di valore non possono presentare uguaglianza dei riferimenti perché quando un'istanza di un tipo di valore è assegnata a una variabile, viene creata una copia del valore.  Pertanto non è mai possibile disporre di due struct sottoposti a conversione unboxing che fanno riferimento allo stesso percorso in memoria.  Inoltre, se si utilizza <xref:System.Object.ReferenceEquals%2A> per confrontare due tipi di valore, il risultato sarà sempre `false`, anche se i valori contenuti negli oggetti sono tutti identici.  Ogni variabile è infatti sottoposta a conversione boxing in un'istanza dell'oggetto separata.  Per ulteriori informazioni, vedere [Procedura: testare l'uguaglianza dei riferimenti \(identità\)](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md).  
  
## Uguaglianza di valori  
 Uguaglianza di valori significa che due oggetti contengono uno o più valori identici.  Per i tipi di valore primitivi quale [int](../../../csharp/language-reference/keywords/int.md) o [bool](../../../csharp/language-reference/keywords/bool.md), i test dell'uguaglianza di valori sono semplici.  È possibile utilizzare l'operatore [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md), come illustrato nell'esempio seguente.  
  
```c#  
int a = GetOriginalValue();  
int b = GetCurrentValue();  
  
// Test for value equality.   
if( b == a)   
{  
    // The two integers are equal.  
}  
```  
  
 Per la maggior parte degli altri tipi, il test dell'uguaglianza di valori è più complesso perché è necessario comprendere come venga definita dal tipo.  Per le classi e gli struct che dispongono di più campi o proprietà, l'uguaglianza di valori indica spesso che tutti i campi o le proprietà presentano lo stesso valore.  Due oggetti `Point`, ad esempio, possono essere definiti come equivalenti se pointA.X è uguale a pointB.X e pointA.Y è uguale a pointB.Y.  
  
 Non è tuttavia indispensabile che l'equivalenza sia basata su tutti i campi in un tipo.  Può essere basata su un sottoinsieme.  Quando si confrontano tipi di cui non è proprietari, è consigliabile verificare di avere compreso in modo specifico come l'equivalenza sia definita per tale tipo.  Per ulteriori informazioni sulla definizione dell'uguaglianza di valori nelle classi e negli struct, vedere [Procedura: definire l'uguaglianza di valori per un tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md).  
  
### Uguaglianza di valori per i valori a virgola mobile  
 I confronti di uguaglianza dei valori a virgola mobile \([double](../../../csharp/language-reference/keywords/double.md) e [float](../../../csharp/language-reference/keywords/float.md)\) sono problematici a causa dell'imprecisione dell'aritmetica a virgola mobile nei computer binari.  Per ulteriori informazioni, vedere le note nell'argomento <xref:System.Double?displayProperty=fullName>.  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Procedura: testare l'uguaglianza dei riferimenti \(identità\)](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md)|Viene descritto come determinare se due variabili presentano l'uguaglianza dei riferimenti.|  
|[Procedura: definire l'uguaglianza di valori per un tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md)|Viene descritto come fornire una definizione personalizzata dell'uguaglianza di valori per un tipo.|  
|[Guida per programmatori C\#](../../../csharp/programming-guide/index.md)|Vengono forniti collegamenti a informazioni su importanti funzionalità del linguaggio C\# e sulle funzionalità disponibili per C\# tramite .NET Framework.|  
|[Tipi](../../../csharp/programming-guide/types/index.md)|Vengono fornite informazioni sul sistema dei tipi di C\# e collegamenti a ulteriori informazioni.|  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)