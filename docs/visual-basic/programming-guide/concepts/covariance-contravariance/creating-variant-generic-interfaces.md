---
title: Creazione di interfacce generiche Variant (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: d4037dd2-dfe9-4811-9150-93d4e8b20113
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 324e2a906e84950aa9019bbf68a524458492646e
ms.lasthandoff: 03/13/2017

---
# <a name="creating-variant-generic-interfaces-visual-basic"></a>Creazione di interfacce generiche Variant (Visual Basic)
È possibile dichiarare parametri di tipo generico nelle interfacce come covariante o controvariante. *La covarianza* consente ai metodi di interfaccia di tipi restituiti sono più derivati da quello definito dai parametri di tipo generico. *La controvarianza* consente metodi di interfaccia di disporre di tipi di argomenti che sono meno derivati rispetto a quello specificato dai parametri generici. Un'interfaccia generica che è covariante o controvariante parametri di tipo generico viene chiamato *variante*.  
  
> [!NOTE]
>  .NET framework 4 è stato introdotto il supporto della varianza per diverse interfacce generiche esistenti. Per l'elenco delle interfacce variante in .NET Framework, vedere [varianza nelle interfacce generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md).  
  
## <a name="declaring-variant-generic-interfaces"></a>Dichiarazione di interfacce generiche Variant  
 È possibile dichiarare interfacce generiche variant utilizzando il `in` e `out` le parole chiave per i parametri di tipo generico.  
  
> [!IMPORTANT]
>  `ByRef`in Visual Basic non possono essere variant. Tipi di valore non supportano inoltre la varianza.  
  
 È possibile dichiarare un parametro di tipo generico covariante mediante il `out` (parola chiave). Il tipo covariante deve soddisfare le condizioni seguenti:  
  
-   Il tipo viene utilizzato solo come tipo restituito dei metodi di interfaccia e non come tipo di argomenti del metodo. Come illustrato nell'esempio seguente, in cui il tipo `R` viene dichiarato covariante.  
  
    ```vb  
    Interface ICovariant(Of Out R)  
        Function GetSomething() As R  
        ' The following statement generates a compiler error.  
        ' Sub SetSomething(ByVal sampleArg As R)  
    End Interface  
    ```  
  
     Esiste un'eccezione a questa regola. Se si dispone di un delegato generico controvariante come parametro di metodo, è possibile utilizzare il tipo come parametro di tipo generico per il delegato. Questo comportamento è illustrato il tipo `R` nell'esempio seguente. Per ulteriori informazioni, vedere [varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) e [utilizzando la varianza per i delegati generici azione (Visual Basic) e Func](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).  
  
    ```vb  
    Interface ICovariant(Of Out R)  
        Sub DoSomething(ByVal callback As Action(Of R))  
    End Interface  
    ```  
  
-   Il tipo non viene utilizzato come vincolo generico per i metodi di interfaccia. Come illustrato nel codice seguente.  
  
    ```vb  
    Interface ICovariant(Of Out R)  
        ' The following statement generates a compiler error  
        ' because you can use only contravariant or invariant types  
        ' in generic contstraints.  
        ' Sub DoSomething(Of T As R)()  
    End Interface  
    ```  
  
 È possibile dichiarare una controvariante del parametro di tipo generico utilizzando il `in` (parola chiave). Il tipo controvariante può essere utilizzato solo come un tipo di argomenti del metodo e non come un tipo restituito dei metodi di interfaccia. Il tipo di controvariante può essere utilizzato anche per i vincoli generici. Il codice seguente viene illustrato come dichiarare un'interfaccia controvariante e utilizzare un vincolo generico per uno dei relativi metodi.  
  
```vb  
Interface IContravariant(Of In A)  
    Sub SetSomething(ByVal sampleArg As A)  
    Sub DoSomething(Of T As A)()  
    ' The following statement generates a compiler error.  
    ' Function GetSomething() As A  
End Interface  
```  
  
 È anche possibile supportare sia la covarianza e controvarianza nella stessa interfaccia, ma per i parametri di tipo diverso, come illustrato nell'esempio di codice seguente.  
  
```vb  
Interface IVariant(Of Out R, In A)  
    Function GetSomething() As R  
    Sub SetSomething(ByVal sampleArg As A)  
    Function GetSetSomething(ByVal sampleArg As A) As R  
End Interface  
```  
  
 In Visual Basic, è possibile dichiarare gli eventi nelle interfacce variante senza specificare il tipo delegato. Inoltre, un'interfaccia variante non può disporre di strutture, enumerazioni o classi annidate, ma è possibile disporre di interfacce annidate. Come illustrato nel codice seguente.  
  
```vb  
Interface ICovariant(Of Out R)  
    ' The following statement generates a compiler error.  
    ' Event SampleEvent()  
    ' The following statement specifies the delegate type and   
    ' does not generate an error.  
    Event AnotherEvent As EventHandler  
  
    ' The following statements generate compiler errors,  
    ' because a variant interface cannot have  
    ' nested enums, classes, or structures.  
  
    'Enum SampleEnum : test : End Enum  
    'Class SampleClass : End Class  
    'Structure SampleStructure : Dim value As Integer : End Structure  
  
    ' Variant interfaces can have nested interfaces.  
    Interface INested : End Interface  
End Interface  
```  
  
## <a name="implementing-variant-generic-interfaces"></a>Implementazione di interfacce generiche Variant  
 Implementare le interfacce generiche variant nelle classi utilizzando la stessa sintassi utilizzata per le interfacce invarianti. Esempio di codice seguente viene illustrato come implementare un'interfaccia covariante in una classe generica.  
  
```vb  
Interface ICovariant(Of Out R)  
    Function GetSomething() As R  
End Interface  
  
Class SampleImplementation(Of R)  
    Implements ICovariant(Of R)  
    Public Function GetSomething() As R _  
    Implements ICovariant(Of R).GetSomething  
        ' Some code.  
    End Function  
End Class  
```  
  
 Le classi che implementano interfacce variant sono invariabili. Si consideri il codice di esempio seguente.  
  
```vb  
 The interface is covariant.  
Dim ibutton As ICovariant(Of Button) =  
    New SampleImplementation(Of Button)  
Dim iobj As ICovariant(Of Object) = ibutton  
  
' The class is invariant.  
Dim button As SampleImplementation(Of Button) =  
    New SampleImplementation(Of Button)  
' The following statement generates a compiler error  
' because classes are invariant.  
' Dim obj As SampleImplementation(Of Object) = button  
```  
  
## <a name="extending-variant-generic-interfaces"></a>Estensione di interfacce generiche Variant  
 Quando si estende un'interfaccia generica variant, è necessario utilizzare il `in` e `out` le parole chiave per specificare in modo esplicito se l'interfaccia derivata supporta la varianza. Il compilatore non deduce la varianza dall'interfaccia che viene esteso. Si consideri ad esempio le interfacce seguenti.  
  
```vb  
Interface ICovariant(Of Out T)  
End Interface  
  
Interface IInvariant(Of T)  
    Inherits ICovariant(Of T)  
End Interface  
  
Interface IExtCovariant(Of Out T)  
    Inherits ICovariant(Of T)  
End Interface  
```  
  
 Nel `Invariant(Of T)` interfaccia, il parametro di tipo generico `T` è invariante, mentre in `IExtCovariant (Of Out T)`il parametro di tipo è covariante, anche se entrambe le interfacce estendono la stessa interfaccia. La stessa regola viene applicata ai parametri di tipo generico controvariante.  
  
 È possibile creare un'interfaccia che estende l'interfaccia del parametro di tipo generico in cui `T` è covariante e l'interfaccia in cui è controvariante in estende il parametro di tipo generico dell'interfaccia `T` è invariante. Come illustrato nell'esempio di codice seguente.  
  
```vb  
Interface ICovariant(Of Out T)  
End Interface  
  
Interface IContravariant(Of In T)  
End Interface  
  
Interface IInvariant(Of T)  
    Inherits ICovariant(Of T), IContravariant(Of T)  
End Interface  
```  
  
 Tuttavia, se un parametro di tipo generico `T` è dichiarato covariante in un'unica interfaccia, non è possibile dichiararlo controvariante nell'interfaccia di estensione, o viceversa. Come illustrato nell'esempio di codice seguente.  
  
```vb  
Interface ICovariant(Of Out T)  
End Interface  
  
' The following statements generate a compiler error.  
' Interface ICoContraVariant(Of In T)  
'     Inherits ICovariant(Of T)  
' End Interface  
```  
  
### <a name="avoiding-ambiguity"></a>Evitare l'ambiguità  
 Quando si implementano le interfacce generiche variant, varianza può talvolta causare ambiguità. Questa evenienza deve essere evitata.  
  
 Ad esempio, se si implementa in modo esplicito la stessa interfaccia generica variante con parametri di tipo generico diversi in una classe, è possibile creare ambiguità. Il compilatore non genera un errore in questo caso, ma non viene specificato quale implementazione dell'interfaccia verrà scelto in fase di esecuzione. Questo potrebbe causare bug nel codice. Si consideri l'esempio di codice seguente.  
  
> [!NOTE]
>  Con `Option Strict Off`, Visual Basic genera un avviso del compilatore quando vi è un'implementazione dell'interfaccia ambigua. Con `Option Strict On`, Visual Basic genera un errore del compilatore.  
  
```vb  
' Simple class hierarchy.  
Class Animal  
End Class  
  
Class Cat  
    Inherits Animal  
End Class  
  
Class Dog  
    Inherits Animal  
End Class  
  
' This class introduces ambiguity  
' because IEnumerable(Of Out T) is covariant.  
Class Pets  
    Implements IEnumerable(Of Cat), IEnumerable(Of Dog)  
  
    Public Function GetEnumerator() As IEnumerator(Of Cat) _  
        Implements IEnumerable(Of Cat).GetEnumerator  
        Console.WriteLine("Cat")  
        ' Some code.  
    End Function  
  
    Public Function GetEnumerator1() As IEnumerator(Of Dog) _  
        Implements IEnumerable(Of Dog).GetEnumerator  
        Console.WriteLine("Dog")  
        ' Some code.  
    End Function  
  
    Public Function GetEnumerator2() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
        ' Some code.  
    End Function  
End Class  
  
Sub Main()  
    Dim pets As IEnumerable(Of Animal) = New Pets()  
    pets.GetEnumerator()  
End Sub  
```  
  
 In questo esempio, non viene specificato come il `pets.GetEnumerator` metodo sceglie tra `Cat` e `Dog`. Ciò potrebbe causare problemi nel codice.  
  
## <a name="see-also"></a>Vedere anche  
 [Varianza nelle interfacce generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)   
 [Utilizzo della varianza per i delegati generici azione (Visual Basic) e Func](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
