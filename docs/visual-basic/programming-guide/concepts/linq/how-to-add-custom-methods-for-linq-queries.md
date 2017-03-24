---
title: 'Procedura: aggiungere metodi personalizzati per le query LINQ (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 099b2e2a-83cd-45c6-aa4d-01b398b5faaf
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
ms.openlocfilehash: 166eb731d41e009c374ba55f929eed302793ecd0
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-add-custom-methods-for-linq-queries-visual-basic"></a>Procedura: aggiungere metodi personalizzati per le query LINQ (Visual Basic)
È possibile estendere il set di metodi che è possibile utilizzare per le query LINQ aggiungendo metodi di estensione per il <xref:System.Collections.Generic.IEnumerable%601>interfaccia.</xref:System.Collections.Generic.IEnumerable%601> Oltre alla media standard o un numero massimo di operazioni, ad esempio, è possibile creare un metodo di aggregazione personalizzato per un singolo valore da una sequenza di valori di calcolo. È inoltre possibile creare un metodo che funziona come un filtro personalizzato o una trasformazione di dati specifico per una sequenza di valori e restituisce una nuova sequenza. Esempi di tali metodi sono <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Skip%2A>e <xref:System.Linq.Enumerable.Reverse%2A>.</xref:System.Linq.Enumerable.Reverse%2A> </xref:System.Linq.Enumerable.Skip%2A> </xref:System.Linq.Enumerable.Distinct%2A>  
  
 Quando si estende il <xref:System.Collections.Generic.IEnumerable%601>interfaccia, è possibile applicare i metodi personalizzati per qualsiasi raccolta enumerabile.</xref:System.Collections.Generic.IEnumerable%601> Per ulteriori informazioni, vedere [metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md).  
  
## <a name="adding-an-aggregate-method"></a>Aggiunta di un metodo di aggregazione  
 Un metodo di aggregazione calcola un singolo valore da un set di valori. LINQ fornisce diversi metodi di aggregazione, tra cui <xref:System.Linq.Enumerable.Average%2A>, <xref:System.Linq.Enumerable.Min%2A>e <xref:System.Linq.Enumerable.Max%2A>.</xref:System.Linq.Enumerable.Max%2A> </xref:System.Linq.Enumerable.Min%2A> </xref:System.Linq.Enumerable.Average%2A> È possibile creare il proprio metodo di aggregazione mediante l'aggiunta di un metodo di estensione per il <xref:System.Collections.Generic.IEnumerable%601>interfaccia.</xref:System.Collections.Generic.IEnumerable%601>  
  
 Esempio di codice seguente viene illustrato come creare un metodo di estensione denominato `Median` per calcolare un valore medio per una sequenza di numeri di tipo `double`.  
  
```vb  
Imports System.Runtime.CompilerServices  
  
Module LINQExtension  
  
    ' Extension method for the IEnumerable(of T) interface.   
    ' The method accepts only values of the Double type.  
    <Extension()>   
    Function Median(ByVal source As IEnumerable(Of Double)) As Double  
        If source.Count = 0 Then  
            Throw New InvalidOperationException("Cannot compute median for an empty set.")  
        End If  
  
        Dim sortedSource = From number In source   
                           Order By number  
  
        Dim itemIndex = sortedSource.Count \ 2  
  
        If sortedSource.Count Mod 2 = 0 Then  
            ' Even number of items in list.  
            Return (sortedSource(itemIndex) + sortedSource(itemIndex - 1)) / 2  
        Else  
            ' Odd number of items in list.  
            Return sortedSource(itemIndex)  
        End If  
    End Function  
End Module  
```  
  
 Chiamare questo metodo di estensione per qualsiasi raccolta enumerabile nello stesso modo chiamare altri metodi di aggregazione dal <xref:System.Collections.Generic.IEnumerable%601>interfaccia.</xref:System.Collections.Generic.IEnumerable%601>  
  
> [!NOTE]
>  In Visual Basic, è possibile utilizzare una chiamata al metodo o una sintassi di query standard per il `Aggregate` o `Group By` clausola. Per ulteriori informazioni, vedere [clausola Aggregate](../../../../visual-basic/language-reference/queries/aggregate-clause.md) e [Group By Clause](../../../../visual-basic/language-reference/queries/group-by-clause.md).  
  
 Esempio di codice seguente viene illustrato come utilizzare il `Median` metodo per una matrice di tipo `double`.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
### <a name="overloading-an-aggregate-method-to-accept-various-types"></a>L'overload di un metodo di aggregazione per accettare tipi diversi  
 È possibile eseguire l'overload del metodo di aggregazione in modo che accetti le sequenze di vario tipo. L'approccio standard consiste nel creare un overload per ogni tipo. Un altro approccio consiste nel creare un overload che accettano un tipo generico e convertirlo in un tipo specifico tramite un delegato. È inoltre possibile combinare entrambi gli approcci.  
  
#### <a name="to-create-an-overload-for-each-type"></a>Per creare un overload per ogni tipo  
 È possibile creare un overload specifico per ogni tipo che si desidera supportare. Esempio di codice seguente viene illustrato un overload di `Median` metodo per la `integer` tipo.  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
 È ora possibile chiamare il `Median` overload per entrambe `integer` e `double` tipi, come illustrato nel codice seguente:  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
#### <a name="to-create-a-generic-overload"></a>Per creare un overload generico  
 È inoltre possibile creare un overload che accetta una sequenza di oggetti generici. Questo overload accetta un delegato come parametro e lo utilizza per convertire una sequenza di oggetti di un tipo generico a un tipo specifico.  
  
 Nel codice seguente viene illustrato un overload di `Median` metodo che accetta il <xref:System.Func%602>delegato come parametro.</xref:System.Func%602> Questo delegato accetta un oggetto di tipo generico T e restituisce un oggetto di tipo `double`.  
  
```vb  
' Generic overload.  
  
<Extension()>   
Function Median(Of T)(ByVal source As IEnumerable(Of T),   
                      ByVal selector As Func(Of T, Double)) As Double  
    Return Aggregate num In source Select selector(num) Into med = Median()  
End Function  
```  
  
 È ora possibile chiamare il `Median` metodo per una sequenza di oggetti di qualsiasi tipo. Se il tipo non dispone di un proprio overload del metodo, è necessario passare un parametro delegato. In Visual Basic, è possibile utilizzare un'espressione lambda a questo scopo. Inoltre, se si utilizza il `Aggregate` o `Group By` clausola anziché la chiamata al metodo, è possibile passare qualsiasi valore o espressione che si trova nell'ambito di questa clausola.  
  
 Esempio di codice seguente viene illustrato come chiamare il `Median` metodo per una matrice di integer e una matrice di stringhe. Per le stringhe, viene calcolato il valore mediano per la lunghezza delle stringhe nella matrice. Nell'esempio viene illustrato come passare il <xref:System.Func%602>parametro per delegare il `Median` metodo per ogni case.</xref:System.Func%602>  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
## <a name="adding-a-method-that-returns-a-collection"></a>Aggiunta di un metodo che restituisce una raccolta  
 È possibile estendere il <xref:System.Collections.Generic.IEnumerable%601>interfaccia con un metodo di query personalizzato che restituisce una sequenza di valori.</xref:System.Collections.Generic.IEnumerable%601> In questo caso, il metodo deve restituire una raccolta di tipo <xref:System.Collections.Generic.IEnumerable%601>.</xref:System.Collections.Generic.IEnumerable%601> Tali metodi consente di applicare filtri o trasformazioni di dati in una sequenza di valori.  
  
 Nell'esempio seguente viene illustrato come creare un metodo di estensione denominato `AlternateElements` che restituisce tutti gli altri elementi in una raccolta, a partire dal primo elemento.  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 È possibile chiamare questo metodo di estensione per qualsiasi raccolta enumerabile come chiamare altri metodi di <xref:System.Collections.Generic.IEnumerable%601>interfaccia, come illustrato nel codice seguente:</xref:System.Collections.Generic.IEnumerable%601>  
  
```vb  
Dim strings() As String = {"a", "b", "c", "d", "e"}  
  
Dim query = strings.AlternateElements()  
  
For Each element In query  
    Console.WriteLine(element)  
Next  
  
' This code produces the following output:  
'  
' a  
' c  
' e  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>   
 [Metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
