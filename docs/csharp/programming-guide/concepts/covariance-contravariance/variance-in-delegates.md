---
title: Varianza nei delegati (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 19de89d2-8224-4406-8964-2965b732b890
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: cd1b765faa734973bf5e184cee2ac934ebdf9241
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="variance-in-delegates-c"></a>Varianza nei delegati (C#)
In .NET framework 3.5 è stato introdotto il supporto della varianza per la corrispondenza delle firme del metodo con i tipi di delegati in tutti i delegati in C#. Ciò significa che è possibile assegnare ai delegati non solo i metodi con firme corrispondenti, ma anche i metodi che restituiscono più tipi derivati (covarianza) o accettano parametri con meno tipi derivati (controvarianza) rispetto a quelli specificati dal tipo di delegato. Sono inclusi sia i delegati generici che quelli non generici.  
  
 Ad esempio, si consideri il codice seguente, che ha due classi e due delegati: generico e non generico.  
  
```csharp  
public class First { }  
public class Second : First { }  
public delegate First SampleDelegate(Second a);  
public delegate R SampleGenericDelegate<A, R>(A a);  
```  
  
 Quando si creano i delegati dei tipi `SampleDelegate` o `SampleGenericDelegate<A, R>` è possibile assegnare uno qualsiasi dei metodi seguenti ai delegati.  
  
```csharp  
// Matching signature.  
public static First ASecondRFirst(Second first)  
{ return new First(); }  
  
// The return type is more derived.  
public static Second ASecondRSecond(Second second)  
{ return new Second(); }  
  
// The argument type is less derived.  
public static First AFirstRFirst(First first)  
{ return new First(); }  
  
// The return type is more derived   
// and the argument type is less derived.  
public static Second AFirstRSecond(First first)  
{ return new Second(); }  
```  
  
 L'esempio di codice seguente viene illustra la conversione implicita tra la firma del metodo e il tipo di delegato.  
  
```csharp  
// Assigning a method with a matching signature   
// to a non-generic delegate. No conversion is necessary.  
SampleDelegate dNonGeneric = ASecondRFirst;  
// Assigning a method with a more derived return type   
// and less derived argument type to a non-generic delegate.  
// The implicit conversion is used.  
SampleDelegate dNonGenericConversion = AFirstRSecond;  
  
// Assigning a method with a matching signature to a generic delegate.  
// No conversion is necessary.  
SampleGenericDelegate<Second, First> dGeneric = ASecondRFirst;  
// Assigning a method with a more derived return type   
// and less derived argument type to a generic delegate.  
// The implicit conversion is used.  
SampleGenericDelegate<Second, First> dGenericConversion = AFirstRSecond;  
```  
  
 Per altri esempi, vedere [Uso della varianza nei delegati (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md) e [Uso della varianza per i delegati generici Func e Action (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).  
  
## <a name="variance-in-generic-type-parameters"></a>Varianza nei parametri di tipo generico  
 In .NET Framework 4 o versioni successive è possibile abilitare la conversione implicita tra delegati, in modo che i delegati generici con tipi diversi specificati dai parametri di tipo generico possano essere assegnati l'uno all'altro, se i tipi vengono ereditati reciprocamente come richiesto dalla varianza.  
  
 Per abilitare la conversione implicita, è necessario dichiarare esplicitamente i parametri generici in un delegato come covariante o controvariante usando la parola chiave `in` o `out`.  
  
 L'esempio di codice seguente illustra come creare un delegato con un parametro di tipo generico covariante.  
  
```csharp  
// Type T is declared covariant by using the out keyword.  
public delegate T SampleGenericDelegate <out T>();  
  
public static void Test()  
{  
    SampleGenericDelegate <String> dString = () => " ";  
  
    // You can assign delegates to each other,  
    // because the type T is declared covariant.  
    SampleGenericDelegate <Object> dObject = dString;             
}  
```  
  
 Se si usa solo il supporto della varianza per la corrispondenza delle firme del metodo con i tipi delegati e non si usano le parole chiave `in` e `out`, è possibile che in alcuni casi si possano creare istanze di delegati con metodi o espressioni lambda identici, ma non è possibile assegnare un delegato a un altro.  
  
 Nell'esempio di codice seguente non è possibile convertire in modo esplicito `SampleGenericDelegate<String>` in `SampleGenericDelegate<Object>`, sebbene `String` erediti `Object`. È possibile correggere questo problema contrassegnando il parametro generico `T` con la parola chiave `out`.  
  
```csharp  
public delegate T SampleGenericDelegate<T>();  
  
public static void Test()  
{  
    SampleGenericDelegate<String> dString = () => " ";  
  
    // You can assign the dObject delegate  
    // to the same lambda expression as dString delegate  
    // because of the variance support for   
    // matching method signatures with delegate types.  
    SampleGenericDelegate<Object> dObject = () => " ";  
  
    // The following statement generates a compiler error  
    // because the generic type T is not marked as covariant.  
    // SampleGenericDelegate <Object> dObject = dString;  
  
}  
```  
  
### <a name="generic-delegates-that-have-variant-type-parameters-in-the-net-framework"></a>Delegati generici con parametri di tipo variante in .NET Framework  
 In .NET framework 4 è stato introdotto il supporto della varianza per i parametri di tipo generico in diversi delegati generici esistenti:  
  
-   Delegati `Action` dallo spazio dei nomi <xref:System>, ad esempio <xref:System.Action%601> e <xref:System.Action%602>  
  
-   Delegati `Func` dallo spazio dei nomi <xref:System>, ad esempio <xref:System.Action%601> e <xref:System.Action%602>  
  
-   Il delegato <xref:System.Predicate%601>  
  
-   Il delegato <xref:System.Comparison%601>  
  
-   Il delegato <xref:System.Converter%602>  
  
 Per altre informazioni ed esempi, vedere [Uso della varianza per i delegati generici Func e Action (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).  
  
### <a name="declaring-variant-type-parameters-in-generic-delegates"></a>Dichiarare parametri di tipo variante nei delegati generici  
 Se un delegato generico ha parametri di tipo generico covariante o controvariante, può essere indicato come un *delegato generico variante*.  
  
 È possibile dichiarare un parametro di tipo generico covariante in un delegato generico usando la parola chiave `out`. Il tipo covariante può essere usato solo come tipo restituito del metodo e non come tipo di argomenti del metodo. Nell'esempio di codice seguente viene illustrato come dichiarare un delegato generico covariante.  
  
```csharp  
public delegate R DCovariant<out R>();  
```  
  
 È possibile dichiarare un parametro di tipo generico controvariante in un delegato generico usando la parola chiave `in`. Il tipo controvariante può essere usato solo come tipo di argomenti del metodo e non come tipo restituito del metodo. Nell'esempio di codice seguente viene illustrato come dichiarare un delegato generico controvariante.  
  
```csharp  
public delegate void DContravariant<in A>(A a);  
```  
  
> [!IMPORTANT]
> I parametri  `ref`e `out` in C# non possono essere contrassegnati come varianti.  
  
 È anche possibile supportare sia la varianza che la covarianza nello stesso delegato, ma per parametri di tipo diverso. come illustrato nell'esempio riportato di seguito.  
  
```csharp  
public delegate R DVariant<in A, out R>(A a);  
```  
  
### <a name="instantiating-and-invoking-variant-generic-delegates"></a>Creare un'istanza e richiamare delegati generici varianti  
 È possibile creare un'istanza e richiamare delegati varianti con la stessa procedura con cui si crea un'istanza e si richiamano i delegati invariabili. Nell'esempio seguente viene creata un'istanza del delegato da un'espressione lambda.  
  
```csharp  
DVariant<String, String> dvariant = (String str) => str + " ";  
dvariant("test");  
```  
  
### <a name="combining-variant-generic-delegates"></a>Combinare delegati generici varianti  
 È consigliabile non combinare i delegati varianti. Il metodo <xref:System.Delegate.Combine%2A> non supporta la conversione dei delegati varianti e prevede che i delegati siano esattamente dello stesso tipo. Questo può causare un'eccezione in fase di esecuzione quando si combinano delegati usando il metodo <xref:System.Delegate.Combine%2A> o l'operatore `+`, come illustrato nell'esempio di codice seguente.  
  
```csharp  
Action<object> actObj = x => Console.WriteLine("object: {0}", x);  
Action<string> actStr = x => Console.WriteLine("string: {0}", x);  
// All of the following statements throw exceptions at run time.  
// Action<string> actCombine = actStr + actObj;  
// actStr += actObj;  
// Delegate.Combine(actStr, actObj);  
```  
  
## <a name="variance-in-generic-type-parameters-for-value-and-reference-types"></a>Varianza nei parametri di tipo generico per tipi di valore e riferimento  
 La varianza per i parametri di tipo generico è supportata solo per i tipi di riferimento. Ad esempio, `DVariant<int>` non può essere convertito implicitamente in `DVariant<Object>` o `DVariant<long>`, poiché integer è un tipo di valore.  
  
 L'esempio seguente dimostra che la varianza nei parametri di tipo generico non è supportata per i tipi di valore.  
  
```csharp  
// The type T is covariant.  
public delegate T DVariant<out T>();  
  
// The type T is invariant.  
public delegate T DInvariant<T>();  
  
public static void Test()  
{  
    int i = 0;  
    DInvariant<int> dInt = () => i;  
    DVariant<int> dVariantInt = () => i;  
  
    // All of the following statements generate a compiler error  
    // because type variance in generic parameters is not supported  
    // for value types, even if generic type parameters are declared variant.  
    // DInvariant<Object> dObject = dInt;  
    // DInvariant<long> dLong = dInt;  
    // DVariant<Object> dVariantObject = dVariantInt;  
    // DVariant<long> dVariantLong = dVariantInt;              
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Generics](https://msdn.microsoft.com/library/ms172192)   
 [Uso della varianza per i delegati generici Func e Action (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)   
 [Procedura: Combinare delegati multicast](../../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)
