---
title: string (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- string
- string_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], reference
- '@ string literal'
- string literals [C#]
- string keyword [C#]
ms.assetid: 3037e558-fb22-494d-bca1-a15ade11b11a
caps.latest.revision: 31
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 737a0902a0cb010a74b59560abe43f5cfb6550db
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="string-c-reference"></a>string (Riferimenti per C#)
Il tipo `string` rappresenta una sequenza di zero o più caratteri Unicode. `string` è un alias per <xref:System.String> in .NET Framework.  
  
 Sebbene `string` sia un tipo riferimento, gli operatori di uguaglianza (`==` e `!=`) vengono definiti per confrontare i valori degli oggetti `string` e non dei riferimenti. In questo modo il test di uguaglianza delle stringhe è più intuitivo. Ad esempio:  
  
```csharp  
string a = "hello";  
string b = "h";  
// Append to contents of 'b'  
b += "ello";  
Console.WriteLine(a == b);  
Console.WriteLine((object)a == (object)b);  
```  
  
 Viene visualizzato "True" e quindi "False" perché il contenuto delle stringhe è equivalente, ma `a` e `b` non fanno riferimento alla stessa istanza della stringa.  
  
 L'operatore + concatena le stringhe:  
  
```csharp  
string a = "good " + "morning";  
```  
  
 Questo crea un oggetto stringa contenente "good morning".  
  
 Le stringhe sono *immutabili*: non è possibile modificare il contenuto di un oggetto stringa dopo la creazione dell'oggetto, sebbene la sintassi sembri indicare che è possibile apportare modifiche. Ad esempio, quando si scrive il codice, il compilatore crea un nuovo oggetto stringa per archiviare la nuova sequenza di caratteri e il nuovo oggetto viene assegnato a b. La stringa "h" è quindi idonea per Garbage Collection.  
  
```csharp
string b = "h";  
b += "ello";  
```  
  
 L'operatore [] può essere usato per accedere in lettura ai singoli caratteri di un `string`:  
  
```csharp  
string str = "test";  
char x = str[2];  // x = 's';  
```  
  
 I valori letterali della stringa sono di tipo `string` e possono essere scritti in due formati, tra virgolette e @-quoted. I valori letterali della stringa tra virgolette sono racchiusi in virgolette doppie ("):  
  
```csharp  
"good morning"  // a string literal  
```  
  
 I valori letterali della stringa possono contenere qualsiasi carattere letterale. Sono incluse le sequenze di escape. L'esempio seguente usa una sequenza di escape `\\` per la barra rovesciata, `\u0066` per la lettera f e `\n` per la nuova riga.  
  
```  
string a = "\\\u0066\n";  
Console.WriteLine(a);  
```  
  
> [!NOTE]
>  Il codice di escape `\`u`dddd` (dove `dddd` è un numero a quattro cifre) rappresenta il carattere Unicode U +`dddd`. Vengono riconosciuti anche i codici di escape Unicode a otto cifre: `\Udddddddd`.  
  
 I valori letterali della stringa verbatim iniziano con @ e sono anche racchiusi tra virgolette doppie. Ad esempio:  
  
```csharp  
@"good morning"  // a string literal  
```  
  
 Il vantaggio delle stringhe verbatim è che le sequenze di escape *non* sono elaborate, e quindi rendono più semplice scrivere, ad esempio, un nome completo del file:  
  
```csharp  
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"  
```  
  
 Per includere le virgolette doppie in una stringa @-quoted, duplicarla:  
  
```csharp  
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.  
```  
  
 Un altro impiego del simbolo @ è l'uso di identificatori ([/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)) con riferimento che sono parole chiave di C#.  
  
 Per altre informazioni sulle stringhe in C#, vedere [Stringhe](../../../csharp/programming-guide/strings/index.md).  
  
## <a name="example"></a>Esempio  
 [!code-cs[csrefKeywordsTypes#17](../../../csharp/language-reference/keywords/codesnippet/CSharp/string_1.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Procedure consigliate per l'uso delle stringhe](../../../standard/base-types/best-practices-strings.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Tipi di valore](../../../csharp/language-reference/keywords/value-types.md)   
 [Operazioni di base su stringhe](../../../standard/base-types/basic-string-operations.md)   
 [Creazione di nuove stringhe](../../../standard/base-types/creating-new.md)   
 [Tabella di formattazione dei risultati numerici](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)

