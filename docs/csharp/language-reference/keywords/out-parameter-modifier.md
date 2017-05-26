---
title: Modificatore del parametro out (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], out
- out parameters [C#]
ms.assetid: 3fce0dc5-03f4-4faa-bd61-36c41bc6baf1
caps.latest.revision: 9
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: a2f2e9b9239836b051820bda66523822e95cdf52
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="out-parameter-modifier-c-reference"></a>Modificatore del parametro out (Riferimenti per C#)
La parola chiave `out` fa sì che gli argomenti vengono passati per riferimento. È come la parola chiave [ref](../../../csharp/language-reference/keywords/ref.md), con la differenza che `ref` richiede l'inizializzazione della variabile prima di essere passato. Per usare un parametro `out`, la definizione del metodo e il metodo chiamante devono usare in modo esplicito la parola chiave `out`. Ad esempio:  
  
 [!code-cs[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/out/out-1.cs)]  

> [!NOTE] 
> La parola chiave `out` può essere usata anche con un parametro di tipo generico per specificare che il parametro tipo è covariante. Per altre informazioni sull'uso della parola chiave `out` in questo contesto, vedere [out (Modificatore generico)](../../../csharp/language-reference/keywords/out-generic-modifier.md).
  
 Le variabili passate come argomenti `out` non devono essere inizializzate prima di essere passate in una chiamata al metodo. È necessario tuttavia che il metodo chiamato assegni un valore prima della restituzione del metodo.  
  
 Nonostante le parole chiave `ref` e `out` determinino un comportamento differente in fase di esecuzione, non sono considerate parte della firma del metodo in fase di compilazione. Non è quindi possibile eseguirne l'overload se l'unica differenza è che un metodo accetta un argomento `ref` e l'altro un argomento `out`. Il codice seguente, ad esempio, non verrà compilato:  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
L'overload può essere eseguito, tuttavia, se un metodo accetta un argomento `ref` o `out` e l'altro non ne usa, come illustrato di seguito:  
  
 [!code-cs[csrefKeywordsMethodParams#3](../../../../samples/snippets/csharp/language-reference/keywords/out/out-3.cs)]  
  
 Le proprietà non sono variabili e quindi non possono essere passate come parametri `out`.  
  
 Per informazioni sul passaggio di matrici, vedere [Passaggio di matrici mediante ref e out](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md).  
  
 Non è possibile usare le parole chiave `ref` e `out` per i seguenti tipi di metodi:  
  
-   Metodi asincroni definiti usando il modificatore [async](../../../csharp/language-reference/keywords/async.md).  
  
-   Metodi iteratori che includono un'istruzione [yield return](../../../csharp/language-reference/keywords/yield.md) o `yield break`.  

## <a name="declaring-out-arguments"></a>Dichiarazione di argomenti `out`   

 La dichiarazione di un metodo con argomenti `out` è utile quando si vuole che un metodo restituisca più valori. Nell'esempio seguente viene usato `out` per restituire tre variabili con una sola chiamata al metodo. Notare che il terzo argomento è assegnato a null. In questo modo i metodi restituiscono i valori facoltativamente.  
  
 [!code-cs[csrefKeywordsMethodParams#4](../../../../samples/snippets/csharp/language-reference/keywords/out/out-4.cs)]  

 Il [modello Try](https://docs.microsoft.com/visualstudio/code-quality/ca1021-avoid-out-parameters#try-pattern-methods.md) prevede la restituzione di `bool` per indicare se l'operazione è riuscita e la restituzione del valore prodotto dall'operazione in un argomento `out`. Numerosi metodi di analisi, ad esempio il metodo @System.DateTime.TryParse(System.String,@System.DateTime), usano questo modello.
   
## <a name="calling-a-method-with-an-out-argument"></a>Chiamata a un metodo con un argomento `out`

In C# 6 e nelle versioni precedenti è necessario dichiarare una variabile in un'istruzione separata prima di passarla come argomento `out`. L'esempio seguente dichiara una variabile denominata `number` prima che venga passata al metodo [Int32.TryParse](xref:System.Int32.TryParse(System.String,@System.Int32) che tenta di convertire una stringa in numero.

 [!code-cs[csrefKeywordsMethodParams#5](../../../../samples/snippets/csharp/language-reference/keywords/out/out-5.cs)]  

A partire da C# 7, è possibile dichiarare la variabile `out` nell'elenco degli argomenti della chiamata al metodo anziché in una dichiarazione di variabile separata. Il codice prodotto risulta più compatto e leggibile e viene impedita l'assegnazione accidentale di un valore alla variabile prima della chiamata al metodo. L'esempio seguente è uguale all'esempio precedente, ad eccezione del fatto che definisce la variabile `number` nella chiamata al metodo [Int32.TryParse](xref:System.Int32.TryParse(System.String,@System.Int32).

 [!code-cs[csrefKeywordsMethodParams#6](../../../../samples/snippets/csharp/language-reference/keywords/out/out-6.cs)]  
   
Nell'esempio precedente la variabile `number` è fortemente tipizzata come `int`. È anche possibile dichiarare una variabile locale tipizzata in modo implicito, come avviene nell'esempio seguente.

 [!code-cs[csrefKeywordsMethodParams#7](../../../../samples/snippets/csharp/language-reference/keywords/out/out-7.cs)]  
   
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Parametri dei metodi](../../../csharp/language-reference/keywords/method-parameters.md)
