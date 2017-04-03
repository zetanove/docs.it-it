---
title: Creazione di interfacce generiche varianti (C#) | Microsoft Docs
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
ms.assetid: 30330ec4-9df2-4838-a535-6c406d0ed4df
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a3dcc75151a3cff601869b4f8a3a4de698d2dc47
ms.lasthandoff: 03/13/2017

---
# <a name="creating-variant-generic-interfaces-c"></a>Creazione di interfacce generiche varianti (C#)
È possibile dichiarare parametri di tipo generico nelle interfacce come covarianti o controvarianti. La *covarianza* consente ai metodi di interfaccia di avere tipi restituiti più derivati rispetto a quelli definiti dai parametri di tipo generico. La *controvarianza* consente ai metodi di interfaccia di avere tipi di argomenti meno derivati rispetto a quelli specificati dai parametri generici. Un'interfaccia generica che ha parametri di tipo generico varianti e covarianti è definita *variante*.  
  
> [!NOTE]
>  In .NET framework 4 è stato introdotto il supporto della varianza per diverse interfacce generiche esistenti. Per l'elenco delle interfacce varianti in .NET Framework, vedere [Varianza nelle interfacce generiche (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md).  
  
## <a name="declaring-variant-generic-interfaces"></a>Dichiarazione delle interfacce generiche varianti  
 È possibile dichiarare le interfacce generiche varianti usando le parole chiave `in` e `out` per i parametri di tipo generico.  
  
> [!IMPORTANT]
> I parametri  `ref` e `out` in C# non possono essere varianti. Anche i tipi di valore non supportano la varianza.  
  
 È possibile dichiarare un parametro di tipo generico covariante usando la parola chiave `out`. Il tipo covariante deve soddisfare le condizioni seguenti:  
  
-   Il tipo viene usato solo come tipo restituito dei metodi di interfaccia e non come tipo di argomenti del metodo. Come illustrato nell'esempio seguente, il tipo `R` viene dichiarato covariante.  
  
    ```csharp  
    interface ICovariant<out R>  
    {  
        R GetSomething();  
        // The following statement generates a compiler error.  
        // void SetSometing(R sampleArg);  
  
    }  
    ```  
  
     Esiste un'eccezione a questa regola. Se si usa un delegato generico controvariante come parametro di metodo, è possibile usare il tipo come parametro di tipo generico per il delegato. Questo aspetto è illustrato nell'esempio seguente dal tipo `R`. Per altre informazioni, vedere [Uso della varianza nei delegati (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) e [Uso della varianza per i delegati generici Func e Action (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).  
  
    ```csharp  
    interface ICovariant<out R>  
    {  
        void DoSomething(Action<R> callback);  
    }  
    ```  
  
-   Il tipo non viene usato come vincolo generico per i metodi di interfaccia. Questa situazione è illustrata nel codice seguente.  
  
    ```csharp  
    interface ICovariant<out R>  
    {  
        // The following statement generates a compiler error  
        // because you can use only contravariant or invariant types  
        // in generic contstraints.  
        // void DoSomething<T>() where T : R;  
    }  
    ```  
  
 È possibile dichiarare un parametro di tipo generico controvariante usando la parola chiave `in`. Il tipo controvariante può essere usato solo come tipo di argomenti del metodo e non come tipo restituito dei metodi di interfaccia. Il tipo controvariante può essere usato anche per i vincoli generici. Il codice seguente illustra come dichiarare un'interfaccia controvariante e usare un vincolo generico per uno dei relativi metodi.  
  
```csharp  
interface IContravariant<in A>  
{  
    void SetSomething(A sampleArg);  
    void DoSomething<T>() where T : A;  
    // The following statement generates a compiler error.  
    // A GetSomething();              
}  
```  
  
 È anche possibile supportare sia la covarianza che la controvarianza nella stessa interfaccia, ma per parametri di tipo diverso, come illustrato nell'esempio di codice seguente.  
  
```csharp  
interface IVariant<out R, in A>  
{  
    R GetSomething();  
    void SetSomething(A sampleArg);  
    R GetSetSometings(A sampleArg);  
}  
```  
  
## <a name="implementing-variant-generic-interfaces"></a>Implementazione di interfacce generiche varianti  
 Implementare le interfacce generiche varianti nelle classi usando la stessa sintassi usata per le interfacce invariabili. L'esempio di codice seguente illustra come implementare un'interfaccia covariante in una classe generica.  
  
```csharp  
interface ICovariant<out R>  
{  
    R GetSomething();  
}  
class SampleImplementation<R> : ICovariant<R>  
{  
    public R GetSomething()  
    {  
        // Some code.  
        return default(R);  
    }  
}  
```  
  
 Le classi che implementano le interfacce varianti sono invariabili. Si consideri il codice di esempio seguente.  
  
```csharp  
// The interface is covariant.  
ICovariant<Button> ibutton = new SampleImplementation<Button>();  
ICovariant<Object> iobj = ibutton;  
  
// The class is invariant.  
SampleImplementation<Button> button = new SampleImplementation<Button>();  
// The following statement generates a compiler error  
// because classes are invariant.  
// SampleImplementation<Object> obj = button;  
```  
  
## <a name="extending-variant-generic-interfaces"></a>Estensione di interfacce generiche varianti  
 Quando si estende un'interfaccia generica variante è necessario usare le parole chiave `in` e `out` per specificare in modo esplicito se l'interfaccia derivata supporta la varianza. Il compilatore non deduce la varianza dall'interfaccia che viene estesa. Si considerino ad esempio le interfacce seguenti.  
  
```csharp  
nterface ICovariant<out T> { }  
interface IInvariant<T> : ICovariant<T> { }  
interface IExtCovariant<out T> : ICovariant<T> { }  
```  
  
 Nell'interfaccia `IInvariant<T>` il parametro di tipo generico `T` è invariabile, mentre in `IExtCovariant<out T>` il parametro di tipo è covariante, anche se entrambe le interfacce estendono la stessa interfaccia. La stessa regola viene applicata ai parametri di tipo generico controvarianti.  
  
 È possibile creare un'interfaccia che estende sia l'interfaccia in cui il parametro di tipo generico `T` è covariante, sia l'interfaccia in cui è controvariante se nell'interfaccia che viene estesa il parametro di tipo generico `T` è invariabile, come illustra l'esempio di codice riportato di seguito.  
  
```csharp  
interface ICovariant<out T> { }  
interface IContravariant<in T> { }  
interface IInvariant<T> : ICovariant<T>, IContravariant<T> { }  
```  
  
 Tuttavia, se un parametro di tipo generico `T` è dichiarato covariante in una sola interfaccia, non è possibile dichiararlo controvariante nell'interfaccia da estendere o viceversa, come illustra l'esempio di codice riportato di seguito.  
  
```csharp  
interface ICovariant<out T> { }  
// The following statement generates a compiler error.  
// interface ICoContraVariant<in T> : ICovariant<T> { }  
```  
  
### <a name="avoiding-ambiguity"></a>Evitare le ambiguità  
 Quando si implementano le interfacce generiche varianti, la varianza può talvolta causare ambiguità. Questa evenienza deve essere evitata.  
  
 Ad esempio, se si implementa in modo esplicito la stessa interfaccia generica variante con parametri di tipo generico diversi in una sola classe, è possibile creare ambiguità. Il compilatore non genera un errore in questo caso, ma non viene specificato quale implementazione dell'interfaccia verrà scelta in fase di esecuzione. Questo potrebbe causare bug nel codice. Si prenda in considerazione il seguente esempio di codice.  
  
```csharp  
// Simple class hierarchy.  
class Animal { }  
class Cat : Animal { }  
class Dog : Animal { }  
  
// This class introduces ambiguity  
// because IEnumerable<out T> is covariant.  
class Pets : IEnumerable<Cat>, IEnumerable<Dog>  
{  
    IEnumerator<Cat> IEnumerable<Cat>.GetEnumerator()  
    {  
        Console.WriteLine("Cat");  
        // Some code.  
        return null;  
    }  
  
    IEnumerator IEnumerable.GetEnumerator()  
    {  
        // Some code.  
        return null;  
    }  
  
    IEnumerator<Dog> IEnumerable<Dog>.GetEnumerator()  
    {  
        Console.WriteLine("Dog");  
        // Some code.  
        return null;  
    }  
}  
class Program  
{  
    public static void Test()  
    {  
        IEnumerable<Animal> pets = new Pets();  
        pets.GetEnumerator();  
    }  
}  
```  
  
 In questo esempio non viene specificato in che modo il metodo `pets.GetEnumerator` sceglie tra `Cat` e `Dog`. Ciò potrebbe causare problemi nel codice.  
  
## <a name="see-also"></a>Vedere anche  
 [Varianza nelle interfacce generiche (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)   
 [Uso della varianza per i delegati generici Func e Action (C#)](../../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
