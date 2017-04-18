---
title: Covarianza e controvarianza (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 59224c46-9931-466b-8c6e-3648c3e609c6
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b785e298c5ba38a8e3d8cc549b2dcf2df1ef6bd8
ms.lasthandoff: 03/13/2017

---
# <a name="covariance-and-contravariance-visual-basic"></a>Covarianza e controvarianza (Visual Basic)
In Visual Basic, covarianza e controvarianza abilitare la conversione implicita del riferimento per i tipi di matrice, tipi delegati e gli argomenti di tipo generico. La covarianza conserva la compatibilità di assegnazione e la controvarianza inverte.  
  
 Il codice seguente viene illustrata la differenza tra la compatibilità di assegnazione, covarianza e controvarianza.  
  
```vb  
' Assignment compatibility.   
Dim str As String = "test"  
' An object of a more derived type is assigned to an object of a less derived type.   
Dim obj As Object = str  
  
' Covariance.   
Dim strings As IEnumerable(Of String) = New List(Of String)()  
' An object that is instantiated with a more derived type argument   
' is assigned to an object instantiated with a less derived type argument.   
' Assignment compatibility is preserved.   
Dim objects As IEnumerable(Of Object) = strings  
  
' Contravariance.             
' Assume that there is the following method in the class:   
' Shared Sub SetObject(ByVal o As Object)  
' End Sub  
Dim actObject As Action(Of Object) = AddressOf SetObject  
  
' An object that is instantiated with a less derived type argument   
' is assigned to an object instantiated with a more derived type argument.   
' Assignment compatibility is reversed.   
Dim actString As Action(Of String) = actObject  
```  
  
 La covarianza per le matrici permette la conversione implicita di una matrice di un tipo più derivato in una matrice di un tipo meno derivato. Ma questa operazione non è indipendente dai tipi, come illustrato nell'esempio di codice seguente.  
  
```vb  
Dim array() As Object = New String(10) {}  
' The following statement produces a run-time exception.  
' array(0) = 10  
```  
  
 Supporto di covarianza e controvarianza per i gruppi di metodi consente di corrispondenza delle firme di metodo con i tipi delegati. In questo modo è possibile assegnare ai delegati non solo i metodi con firme corrispondenti, ma anche metodi che restituiscono che più derivati (covarianza) i tipi o che accettano parametri tipi meno derivati (controvarianza) rispetto a quello specificato dal tipo di delegato. Per ulteriori informazioni, vedere [varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) e [utilizzando varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md).  
  
 Esempio di codice seguente mostra la covarianza e controvarianza supporto per i gruppi di metodi.  
  
```vb  
Shared Function GetObject() As Object  
    Return Nothing  
End Function  
  
Shared Sub SetObject(ByVal obj As Object)  
End Sub  
  
Shared Function GetString() As String  
    Return ""  
End Function  
  
Shared Sub SetString(ByVal str As String)  
  
End Sub  
  
Shared Sub Test()  
    ' Covariance. A delegate specifies a return type as object,  
    ' but you can assign a method that returns a string.  
    Dim del As Func(Of Object) = AddressOf GetString  
  
    ' Contravariance. A delegate specifies a parameter type as string,  
    ' but you can assign a method that takes an object.  
    Dim del2 As Action(Of String) = AddressOf SetObject  
End Sub  
```  
  
 In .NET Framework 4 o versione successiva di Visual Basic supportano la covarianza e controvarianza in interfacce e delegati generici e consentire la conversione implicita dei parametri di tipo generico. Per ulteriori informazioni, vedere [varianza nelle interfacce generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md) e [varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md).  
  
 Esempio di codice seguente viene illustrata la conversione implicita del riferimento per le interfacce generiche.  
  
```vb  
Dim strings As IEnumerable(Of String) = New List(Of String)  
Dim objects As IEnumerable(Of Object) = strings  
```  
  
 Un'interfaccia generica o delegato viene chiamato *variante* se i parametri generici vengono dichiarati covarianti o controvarianti. Visual Basic consente di creare interfacce variant e delegati personalizzati. Per ulteriori informazioni, vedere [la creazione di interfacce generiche Variant (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md) e [varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md).  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Varianza nelle interfacce generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)|Illustra la covarianza e la controvarianza nelle interfacce generiche e fornisce un elenco di interfacce generiche variant in .NET Framework.|  
|[Creazione di interfacce generiche Variant (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/creating-variant-generic-interfaces.md)|Viene illustrato come creare interfacce variant personalizzate.|  
|[Utilizzo della varianza nelle interfacce per le raccolte generiche (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-interfaces-for-generic-collections.md)|Viene illustrato come supportare la covarianza e controvarianza nel <xref:System.Collections.Generic.IEnumerable%601>e <xref:System.IComparable%601>interfacce consentono di riutilizzare il codice.</xref:System.IComparable%601> </xref:System.Collections.Generic.IEnumerable%601>|  
|[Varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)|Illustra la covarianza e controvarianza nei delegati generici e non generica e fornisce un elenco di delegati generici in .NET Framework.|  
|[Utilizzo della varianza nei delegati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)|Di seguito viene illustrato come utilizzare il supporto di covarianza e controvarianza nei delegati non generici per la corrispondenza delle firme di metodo con i tipi delegati.|  
|[Utilizzo della varianza per i delegati generici azione (Visual Basic) e Func](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)|Viene illustrato come supportare la covarianza e controvarianza nel `Func` e `Action` delegati consente di riutilizzare il codice.|
