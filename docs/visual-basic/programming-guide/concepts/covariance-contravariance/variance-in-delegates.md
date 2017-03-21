---
title: Varianza nei delegati (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 38e9353f-74f8-4211-a8f0-7a495414df4a
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
ms.openlocfilehash: cbab7da8c97ca202f8a4d0a1a65b8fa240cca32d
ms.lasthandoff: 03/13/2017

---
# <a name="variance-in-delegates-visual-basic"></a>Varianza nei delegati (Visual Basic)
.NET framework 3.5 è stato introdotto il supporto della varianza per la corrispondenza delle firme di metodo con i tipi delegati in tutti i delegati in c# e Visual Basic. Ciò significa che è possibile assegnare ai delegati non solo i metodi con firme corrispondenti, ma anche i metodi che restituiscono più derivati (covarianza) i tipi o che accettano parametri con tipi meno derivati (controvarianza) rispetto a quello specificato dal tipo di delegato. Ciò include delegati sia generici e non generica.  
  
 Ad esempio, si consideri il codice seguente, che dispone di due classi e due delegati: generico e non generici.  
  
```vb  
Public Class First  
End Class  
  
Public Class Second  
    Inherits First  
End Class  
  
Public Delegate Function SampleDelegate(ByVal a As Second) As First  
Public Delegate Function SampleGenericDelegate(Of A, R)(ByVal a As A) As R  
```  
  
 Quando si creano delegati del `SampleDelegate` o `SampleDelegate(Of A, R)` tipi, è possibile assegnare uno dei metodi seguenti per i delegati.  
  
```vb  
' Matching signature.  
Public Shared Function ASecondRFirst(  
    ByVal second As Second) As First  
    Return New First()  
End Function  
  
' The return type is more derived.  
Public Shared Function ASecondRSecond(  
    ByVal second As Second) As Second  
    Return New Second()  
End Function  
  
' The argument type is less derived.  
Public Shared Function AFirstRFirst(  
    ByVal first As First) As First  
    Return New First()  
End Function  
  
' The return type is more derived   
' and the argument type is less derived.  
Public Shared Function AFirstRSecond(  
    ByVal first As First) As Second  
    Return New Second()  
End Function  
```  
  
 Esempio di codice seguente viene illustrata la conversione implicita tra la firma del metodo e il tipo delegato.  
  
```vb  
' Assigning a method with a matching signature   
' to a non-generic delegate. No conversion is necessary.  
Dim dNonGeneric As SampleDelegate = AddressOf ASecondRFirst  
' Assigning a method with a more derived return type   
' and less derived argument type to a non-generic delegate.  
' The implicit conversion is used.  
Dim dNonGenericConversion As SampleDelegate = AddressOf AFirstRSecond  
  
' Assigning a method with a matching signature to a generic delegate.  
' No conversion is necessary.  
Dim dGeneric As SampleGenericDelegate(Of Second, First) = AddressOf ASecondRFirst  
' Assigning a method with a more derived return type   
' and less derived argument type to a generic delegate.  
' The implicit conversion is used.  
Dim dGenericConversion As SampleGenericDelegate(Of Second, First) = AddressOf AFirstRSecond  
```  
  
 Per ulteriori esempi, vedere [utilizzando varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md) e [utilizzando la varianza per i delegati generici azione (Visual Basic) e Func](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).  
  
## <a name="variance-in-generic-type-parameters"></a>Varianza nei parametri di tipo generico  
 In .NET Framework 4 e versioni successive è possibile abilitare la conversione implicita tra delegati, in modo che i delegati generici con tipi diversi specificati dai parametri di tipo generico possono essere assegnati tra loro, se i tipi vengono ereditati da altra come richiesto dalla varianza.  
  
 Per abilitare la conversione implicita, è necessario dichiarare in modo esplicito i parametri generici di un delegato come covarianti o controvarianti utilizzando il `in` o `out` (parola chiave).  
  
 Esempio di codice seguente viene illustrato come creare un delegato con un parametro di tipo generico covariante.  
  
```vb  
' Type T is declared covariant by using the out keyword.  
Public Delegate Function SampleGenericDelegate(Of Out T)() As T  
Sub Test()  
    Dim dString As SampleGenericDelegate(Of String) = Function() " "  
    ' You can assign delegates to each other,  
    ' because the type T is declared covariant.  
    Dim dObject As SampleGenericDelegate(Of Object) = dString  
End Sub  
```  
  
 Se si utilizza solo il supporto della varianza per la corrispondenza delle firme di metodo con tipi delegati e non utilizzare il `in` e `out` le parole chiave, è possibile che in alcuni casi è possibile creare istanze di delegati con metodi o espressioni lambda identiche, ma non è possibile assegnare un delegato a un altro.  
  
 Nell'esempio di codice seguente, `SampleGenericDelegate(Of String)` non può essere convertito in modo esplicito in `SampleGenericDelegate(Of Object)`, sebbene `String` eredita `Object`. È possibile risolvere questo problema contrassegnando il parametro generico `T` con il `out` (parola chiave).  
  
```vb  
Public Delegate Function SampleGenericDelegate(Of T)() As T  
Sub Test()  
    Dim dString As SampleGenericDelegate(Of String) = Function() " "  
  
    ' You can assign the dObject delegate  
    ' to the same lambda expression as dString delegate  
    ' because of the variance support for   
    ' matching method signatures with delegate types.  
    Dim dObject As SampleGenericDelegate(Of Object) = Function() " "  
  
    ' The following statement generates a compiler error  
    ' because the generic type T is not marked as covariant.  
    ' Dim dObject As SampleGenericDelegate(Of Object) = dString  
  
End Sub  
```  
  
### <a name="generic-delegates-that-have-variant-type-parameters-in-the-net-framework"></a>Delegati generici con variante di parametri di tipo in .NET Framework  
 .NET framework 4 è stato introdotto il supporto della varianza per i parametri di tipo generico in diversi delegati generici esistenti:  
  
-   `Action`delega dal <xref:System>spazio dei nomi, ad esempio, <xref:System.Action%601>e <xref:System.Action%602></xref:System.Action%602> </xref:System.Action%601> </xref:System>  
  
-   `Func`delega dal <xref:System>spazio dei nomi, ad esempio, <xref:System.Func%601>e <xref:System.Func%602></xref:System.Func%602> </xref:System.Func%601> </xref:System>  
  
-   Il <xref:System.Predicate%601>delegato</xref:System.Predicate%601>  
  
-   Il <xref:System.Comparison%601>delegato</xref:System.Comparison%601>  
  
-   Il <xref:System.Converter%602>delegato</xref:System.Converter%602>  
  
 Per ulteriori informazioni ed esempi, vedere [utilizzando la varianza per i delegati generici azione (Visual Basic) e Func](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).  
  
### <a name="declaring-variant-type-parameters-in-generic-delegates"></a>Dichiarazione dei parametri di tipo Variant in delegati generici  
 Se un delegato generico è covariante o parametri di tipo generico controvariante, può essere indicato come un *delegati generici varianti*.  
  
 È possibile dichiarare un parametro di tipo generico covarianti in un delegato generico utilizzando il `out` (parola chiave). Di tipo covariante può essere utilizzato solo come un tipo restituito del metodo e non come un tipo di argomenti del metodo. Esempio di codice seguente viene illustrato come dichiarare un delegato generico covariante.  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
 È possibile dichiarare una controvariante del parametro di tipo generico in un delegato generico utilizzando il `in` (parola chiave). Il tipo controvariante può essere utilizzato solo come un tipo di argomenti del metodo e non come un tipo restituito del metodo. Esempio di codice seguente viene illustrato come dichiarare un delegato generico controvariante.  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
> [!IMPORTANT]
>  `ByRef`i parametri in Visual Basic non possono essere contrassegnati come variant.  
  
 È inoltre possibile supportare sia la varianza e covarianza nello stesso delegato, ma per i parametri di tipo diverso. come illustrato nell'esempio riportato di seguito.  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
### <a name="instantiating-and-invoking-variant-generic-delegates"></a>Creare un'istanza e richiamare delegati generici varianti  
 È possibile creare un'istanza e richiamare delegati varianti esattamente come si crea un'istanza e richiamare delegati invarianti. Nell'esempio seguente viene creata un'istanza di delegato da un'espressione lambda.  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
### <a name="combining-variant-generic-delegates"></a>La combinazione dei delegati generici varianti  
 È consigliabile non combinare delegati varianti. Il <xref:System.Delegate.Combine%2A>metodo non supporta la conversione di delegati varianti e prevede che i delegati per essere dello stesso tipo.</xref:System.Delegate.Combine%2A> Questo può causare un'eccezione in fase di esecuzione quando si combinano delegati utilizzando il <xref:System.Delegate.Combine%2A>(metodo) (in c# e Visual Basic) o tramite il `+` (operatore) (in c#), come illustrato nell'esempio di codice seguente.</xref:System.Delegate.Combine%2A>  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
## <a name="variance-in-generic-type-parameters-for-value-and-reference-types"></a>Varianza nei parametri di tipo generico per valore e tipi di riferimento  
 La varianza per i parametri di tipo generico è supportata per i tipi di riferimento solo. Ad esempio, `DVariant(Of Int)`non può essere convertita implicitamente in `DVariant(Of Object)` o `DVariant(Of Long)`, poiché integer è un tipo di valore.  
  
 Nell'esempio seguente viene illustrato che la varianza in tipo generico con parametri non è supportata per i tipi di valore.  
  
```vb  
' The type T is covariant.  
Public Delegate Function DVariant(Of Out T)() As T  
' The type T is invariant.  
Public Delegate Function DInvariant(Of T)() As T  
Sub Test()  
    Dim i As Integer = 0  
    Dim dInt As DInvariant(Of Integer) = Function() i  
    Dim dVaraintInt As DVariant(Of Integer) = Function() i  
  
    ' All of the following statements generate a compiler error  
    ' because type variance in generic parameters is not supported  
    ' for value types, even if generic type parameters are declared variant.  
    ' Dim dObject As DInvariant(Of Object) = dInt  
    ' Dim dLong As DInvariant(Of Long) = dInt  
    ' Dim dVaraintObject As DInvariant(Of Object) = dInt  
    ' Dim dVaraintLong As DInvariant(Of Long) = dInt  
End Sub  
```  
  
## <a name="relaxed-delegate-conversion-in-visual-basic"></a>Conversione di tipo relaxed del delegato in Visual Basic  
 Conversione di tipo relaxed del delegato consente una maggiore flessibilità in corrispondenza delle firme di metodo con i tipi delegati. Ad esempio, consente di omettere le specifiche dei parametri e omettere i valori restituiti dalla funzione quando si assegna un metodo a un delegato. Per ulteriori informazioni, vedere [conversione di tipo Relaxed del delegato](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Generics](https://msdn.microsoft.com/library/ms172192)   
 [Utilizzo della varianza per Func e azione delegati generici (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
