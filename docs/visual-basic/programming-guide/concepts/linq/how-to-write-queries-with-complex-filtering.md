---
title: 'Procedura: scrivere query con filtri complessi (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: bf286ffc-7990-4b00-a4eb-ee3d70129950
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e46d07674d901aef77db04d63314080a4ca68801
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-write-queries-with-complex-filtering-visual-basic"></a>Procedura: scrivere query con filtri complessi (Visual Basic)
A volte si desidera scrivere query LINQ to XML con filtri complessi. Può ad esempio essere necessario trovare tutti gli elementi che hanno un elemento figlio con un determinato nome e valore. In questo argomento viene illustrato come scrivere una query di esempio con filtri complessi.  
  
## <a name="example"></a>Esempio  
 Nell'esempio viene illustrato come trovare tutti gli elementi `PurchaseOrder` che includono un elemento figlio `Address` con un attributo `Type` uguale a "Shipping" e un elemento figlio `State` uguale a "NY". Viene usata una query annidata nella clausola `Where` e l'operatore `Any` restituisce `True` se la raccolta contiene elementi.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: più ordini di acquisto (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-linq-to-xml.md).  
  
 Per ulteriori informazioni sui `Any` operatore, vedere [operazioni del quantificatore (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md).  
  
```vb  
Dim root As XElement = XElement.Load("PurchaseOrders.xml")  
Dim purchaseOrders As IEnumerable(Of XElement) = _  
    From el In root.<PurchaseOrder> _  
    Where _  
        (From add In el.<Address> _  
        Where _  
             add.@Type = "Shipping" And _  
             add.<State>.Value = "NY" _  
        Select add) _  
    .Any() _  
    Select el  
For Each el As XElement In purchaseOrders  
    Console.WriteLine(el.@PurchaseOrderNumber)  
Next  
```  
  
 L'output del codice è il seguente:  
  
```  
99505  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è illustrata la stessa query per XML in uno spazio dei nomi. Per ulteriori informazioni, vedere [utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: più ordini di acquisto in un Namespace](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-in-a-namespace.md).  
  
```vb  
Imports <xmlns:aw='http://www.adventure-works.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("PurchaseOrdersInNamespace.xml")  
        Dim purchaseOrders As IEnumerable(Of XElement) = _  
            From el In root.<aw:PurchaseOrder> _  
            Where _  
                (From add In el.<aw:Address> _  
                Where _  
                     add.@aw:Type = "Shipping" And _  
                     add.<aw:State>.Value = "NY" _  
                Select add) _  
            .Any() _  
            Select el  
        For Each el As XElement In purchaseOrders  
            Console.WriteLine(el.@aw:PurchaseOrderNumber)  
        Next  
    End Sub  
End Module  
```  
  
 L'output del codice è il seguente:  
  
```  
99505  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement.Attribute%2A></xref:System.Xml.Linq.XElement.Attribute%2A>   
 <xref:System.Xml.Linq.XContainer.Elements%2A></xref:System.Xml.Linq.XContainer.Elements%2A>   
 [Query di base (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)   
 [Proprietà Child Axis XML](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)   
 [Proprietà axis dell'attributo XML](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)   
 [Proprietà Value XML](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)   
 [Operazioni di proiezione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projection-operations.md)   
 [Operazioni quantificatore (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md)
