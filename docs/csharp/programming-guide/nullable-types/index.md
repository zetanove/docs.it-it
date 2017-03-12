---
title: "Tipi nullable (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, tipi nullable"
  - "nullable (tipi) [C#]"
  - "tipi [C#], nullable"
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
caps.latest.revision: 44
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 44
---
# Tipi nullable (Guida per programmatori C#)
I tipi nullable sono istanze della struttura <xref:System.Nullable%601?displayProperty=fullName>.  Un tipo nullable può rappresentare l'intervallo corretto di valori per il relativo tipo di valore sottostante, più un valore `null` aggiuntivo.  Ad esempio, a un oggetto `Nullable<Int32>`, che si legge "Nullable di Int32", può essere assegnato un qualsiasi valore compreso tra \-2147483648 e 2147483647 oppure il valore `null`.  A un oggetto `Nullable<bool>` è possibile assegnare i valori [true](../../../csharp/language-reference/keywords/true.md), [false](../../../csharp/language-reference/keywords/false.md) o [null](../../../csharp/language-reference/keywords/null.md).  La possibilità di assegnare `null` a tipi numerici e booleani è particolarmente utile quanto si utilizzano database e altri tipi di dati contenenti elementi a cui non sarebbe possibile assegnare un valore.  Ad esempio, in un campo Boolean di un database è possibile archiviare il valore `true` o `false` oppure è possibile lasciarlo indefinito.  
  
 [!code-cs[csProgGuideTypes#3](../../../csharp/programming-guide/nullable-types/codesnippet/csharp/index_1.cs)]  
  
 Nell'esempio viene visualizzato l'output:  
  
 `num = Null`  
  
 `Nullable object must have a value.`  
  
 Per ulteriori esempi, vedere [Utilizzo dei tipi nullable](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
  
## Informazioni preliminari sui tipi nullable  
 Di seguito sono riportate le caratteristiche dei tipi nullable:  
  
-   I tipi nullable rappresentano variabili di tipo di valore a cui è possibile assegnare il valore di `null`.  Non è possibile creare un tipo nullable basato su un tipo di riferimento.  \(I tipi di riferimento supportano già il valore `null`.\)  
  
-   La sintassi `T?` è una forma abbreviata dell'oggetto <xref:System.Nullable%601>, in cui l'oggetto `T` è un tipo di valore.  Le due forme sono intercambiabili.  
  
-   Assegnare un valore a un tipo nullable come se fosse un tipo di valore ordinario, ad esempio `int? x = 10;` o `double? d = 4.108`.  È possibile inoltre assegnare un valore `null`: `int? x = null.` al tipo nullable.  
  
-   Utilizzare il metodo <xref:System.Nullable%601.GetValueOrDefault%2A?displayProperty=fullName> per restituire il valore assegnato o il valore predefinito per il tipo sottostante se il valore è `null`, ad esempio  `int j = x.GetValueOrDefault();`  
  
-   Utilizzare le proprietà di sola lettura <xref:System.Nullable%601.HasValue%2A> e <xref:System.Nullable%601.Value%2A> per controllare i valori Null e recuperare il valore, come illustrato nell'esempio seguente: `if(x.HasValue) j = x.Value;`  
  
    -   La proprietà `HasValue` restituisce `true` se la variabile contiene un valore o `false` se è `null`.  
  
    -   La proprietà `Value` restituisce un valore se ne è stato assegnato uno.  In caso contrario, verrà generata un'eccezione <xref:System.InvalidOperationException?displayProperty=fullName>.  
  
    -   Il valore predefinito di `HasValue` è `false`.  La proprietà `Value` non ha valori predefiniti.  
  
    -   È anche possibile utilizzare gli operatori `==` e `!=` con un tipo nullable, come illustrato nel seguente esempio: `if (x != null) y = x;`  
  
-   Utilizzare l'operatore `??` per assegnare un valore predefinito che verrà applicato quando un tipo nullable, il cui valore corrente è `null`, viene assegnato a un tipo non nullable, ad esempio `int? x = null; int y = x ?? -1;`  
  
-   I tipi nullable annidati non sono consentiti.  La riga seguente non eseguirà la compilazione: `Nullable<Nullable<int>> n;`  
  
## Sezioni correlate  
 Per ulteriori informazioni:  
  
-   [Utilizzo dei tipi nullable](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
  
-   [Conversione boxing dei tipi nullable](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)  
  
-   [?? Operatore](../../../csharp/language-reference/operators/null-conditional-operator.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.Nullable>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [C\#](../../../csharp/csharp.md)   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Cosa fare esattamente media “sollevata„?](http://go.microsoft.com/fwlink/?LinkId=112382)