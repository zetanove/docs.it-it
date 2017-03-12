---
title: "short (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "short"
  - "short_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "short (parola chiave) [C#]"
ms.assetid: 04c10688-e51a-4a87-bfec-83f7fb42ff11
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# short (Riferimenti per C#)
La parola chiave `short` denota un tipo di dati integrale che memorizza valori in base alla dimensione e all'intervallo indicati nella seguente tabella.  
  
|Type|Intervallo|Dimensione|Tipo .NET Framework|  
|----------|----------------|----------------|-------------------------|  
|`short`|Da \-32.768 a 32.767|Numero intero con segno a 16 bit|<xref:System.Int16?displayProperty=fullName>|  
  
## Valori letterali  
 È possibile dichiarare e inizializzare una variabile `short` come nell'esempio riportato di seguito.  
  
```  
  
short x = 32767;  
```  
  
 Nella precedente dichiarazione il valore letterale integer `32767` è convertito in modo implicito da [int](../../../csharp/language-reference/keywords/int.md) a `short`.  Se il valore letterale integer ha dimensioni troppo grandi per uno spazio di memoria `short`, verrà generato un errore di compilazione.  
  
 È necessario utilizzare un cast quando si chiamano metodi di overload.  Si considerino, ad esempio, i seguenti metodi di overload che utilizzano parametri `short` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(short s) {}  
```  
  
 L'utilizzo del cast di `short` garantisce che venga chiamato il tipo corretto, ad esempio:  
  
```  
SampleMethod(5);         // Calling the method with the int parameter  
SampleMethod((short)5);  // Calling the method with the short parameter  
```  
  
## Conversioni  
 Si verifica una conversione implicita predefinita da `short` in [int](../../../csharp/language-reference/keywords/int.md), [long](../../../csharp/language-reference/keywords/long.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  
  
 Non è possibile convertire in modo implicito in `short` tipi numerici non letterali che necessitano di maggiore spazio in memoria. Per informazioni sullo spazio necessario per l'archiviazione dei tipi integrali, vedere [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md).  Si considerino, ad esempio, le due variabili `short` seguenti `x` e `y`:  
  
```  
  
short x = 5, y = 12;  
```  
  
 L'istruzione di assegnazione riportata di seguito provocherà un errore di compilazione, poiché, per impostazione predefinita, l'espressione aritmetica a destra dell'operatore di assegnazione restituisce [int](../../../csharp/language-reference/keywords/int.md).  
  
 `short`   `z = x + y;   // Error: no conversion from int to short`  
  
 Per correggere l'errore, utilizzare un cast:  
  
 `short`   `z = (`  `short`  `)(x + y);   // OK: explicit conversion`  
  
 È tuttavia possibile utilizzare le seguenti istruzioni, in cui la variabile di destinazione ha dimensioni di archiviazione uguali o superiori:  
  
```  
int m = x + y;  
long n = x + y;  
```  
  
 Non esiste alcuna conversione implicita dai tipi a virgola mobile a `short`.  L'istruzione seguente, ad esempio, genera un errore di compilazione, a meno che non venga utilizzato un cast esplicito:  
  
```  
  
        short x = 3.0;          // Error: no implicit conversion from double  
short y = (short)3.0;   // OK: explicit conversion  
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per ulteriori informazioni sulle regole di conversione numerica implicita, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.Int16>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)