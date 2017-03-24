---
title: 'Procedura: proiettare un nuovo tipo (LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 8cfb24f5-89b2-4cfb-b85d-e7963f8f1845
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a7cbbce130aa78a7e14ffd61a1dcd76b969e1b35
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-project-a-new-type-linq-to-xml-visual-basic"></a>Procedura: proiettare un nuovo tipo (LINQ to XML) (Visual Basic)
Altri esempi in questa sezione sono state illustrate query che restituiscono risultati come <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>, <xref:System.Collections.Generic.IEnumerable%601>di `string`, e <xref:System.Collections.Generic.IEnumerable%601>di `int`.</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> Si tratta di tipi di risultati comuni, ma non sono appropriati per tutti gli scenari. In molti casi è consigliabile le query dovranno restituire un <xref:System.Collections.Generic.IEnumerable%601>di un altro tipo.</xref:System.Collections.Generic.IEnumerable%601>  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrato come creare istanze di oggetti nella clausola `Select`. Nel codice viene innanzitutto definita una nuova classe con un costruttore, quindi viene modificata l'istruzione `Select` in modo che l'espressione sia una nuova istanza della nuova classe.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: tipico ordine di acquisto (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml.md).  
  
```vb  
Public Class NameQty  
    Public name As String  
    Public qty As Integer  
    Public Sub New(ByVal n As String, ByVal q As Integer)  
        name = n  
        qty = q  
    End Sub  
End Class  
  
Public Class Program  
    Shared Sub Main()  
        Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
  
        Dim nqList As IEnumerable(Of NameQty) = _  
            From n In po...<Item> _  
            Select New NameQty( _  
                n.<ProductName>.Value, CInt(n.<Quantity>.Value))  
  
        For Each n As NameQty In nqList  
            Console.WriteLine(n.name & ":" & n.qty)  
        Next  
    End Sub  
End Class  
```  
  
 Questo esempio viene utilizzato il `M:System.Xml.Linq.XElement.Element` metodo che è stato introdotto nell'argomento [procedura: recuperare un singolo elemento figlio (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md). Vengono inoltre usati i cast per recuperare i valori degli elementi restituiti dal metodo `M:System.Xml.Linq.XElement.Element`.  
  
 Questo esempio produce il seguente output:  
  
```  
Lawnmower:1  
Baby Monitor:2  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proiezioni e trasformazioni (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
