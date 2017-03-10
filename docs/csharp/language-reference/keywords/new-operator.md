---
title: "Operatore new (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "new (parola chiave di operatore) [C#]"
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# Operatore new (Riferimenti per C#)
Utilizzata per creare oggetti e richiamare costruttori.  Di seguito è riportato un esempio:  
  
```  
Class1 obj  = new Class1();  
```  
  
 Viene utilizzato anche per creare istanze di tipi anonimi:  
  
```  
var query = from cust in customers  
            select new {Name = cust.Name, Address = cust.PrimaryAddress};  
```  
  
 L'operatore `new` viene inoltre utilizzato per richiamare il costruttore predefinito per i tipi di valore.  Di seguito è riportato un esempio:  
  
```  
int i = new int();  
```  
  
 Nell'istruzione precedente `i` viene inizializzato su `0`, ovvero il valore predefinito per il tipo `int`.  L'istruzione ha lo stesso effetto dell'istruzione riportata di seguito:  
  
```  
int i = 0;  
```  
  
 Per un elenco completo dei valori predefiniti, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  
  
 È utile ricordare che è errato dichiarare un costruttore predefinito per una [struttura](../../../csharp/language-reference/keywords/struct.md), in quanto ogni tipo di valore ha implicitamente un costruttore predefinito pubblico.  È possibile dichiarare costruttori con parametri su un tipo struttura per impostarne i valori iniziali, ma questa operazione è necessaria solo se sono richiesti valori diversi da quello predefinito.  
  
 I tipi di oggetto che rappresentano un valore, ad esempio strutture, vengono creati nello stack, mentre i tipi di oggetto che rappresentano un riferimento, ad esempio le classi, vengono creati nell'heap.  Entrambi i tipi di oggetti vengono eliminati automaticamente, ma gli oggetti basati su tipi di valori vengono eliminati quando escono dall'ambito di validità, mentre quelli basati su tipi di riferimento in un momento non specificato dopo che è stato rimosso l'ultimo riferimento ad essi.  Per i tipi di riferimento che utilizzano risorse fisse, quali grandi quantità di memoria, handle di file o connessioni di rete, può risultare preferibile adottare la finalizzazione deterministica per assicurarsi che l'oggetto venga distrutto prima possibile.  Per ulteriori informazioni, vedere [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md).  
  
 Non è possibile sottoporre l'operatore `new` a overload.  
  
 Se l'operatore `new` non riesce ad allocare memoria, genererà l'eccezione <xref:System.OutOfMemoryException>.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono creati e inizializzati un oggetto `struct` e un oggetto classe tramite l'operatore `new`, quindi vengono assegnati loro i valori.  Vengono visualizzati sia i valori predefiniti sia quelli assegnati.  
  
 [!code-cs[csrefKeywordsOperator#7](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsOperator/csrefKeywordsOperators.cs#7)]  
  
 Si noti che nell'esempio il valore predefinito di una stringa è `null` e, pertanto, non viene visualizzato.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [new](../../../csharp/language-reference/keywords/new.md)   
 [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)