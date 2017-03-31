---
title: 'Procedura: Trovare un elemento figlio (XPath-LINQ to XML) (C#) | Microsoft Docs'
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
ms.assetid: 4fa6182d-6196-4ed1-9c9e-82949ff89c71
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b788d6dbd44f8ed01fe65a18fb25d8e3a0592220
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-find-a-child-element-xpath-linq-to-xml-c"></a>Procedura: Trovare un elemento figlio (XPath-LINQ to XML) (C#)
Questo argomento confronta l'asse degli elementi figlio XPath e il metodo <xref:System.Xml.Linq.XContainer.Element%2A> di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 L'espressione XPath è `DeliveryNotes`.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene trovato l'elemento figlio `DeliveryNotes`.  
  
 Nell'esempio viene usato il documento XML seguente: [File XML di esempio: più ordini di acquisto (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-linq-to-xml.md).  
  
```csharp  
XDocument cpo = XDocument.Load("PurchaseOrders.xml");  
XElement po = cpo.Root.Element("PurchaseOrder");  
  
// LINQ to XML query  
XElement el1 = po.Element("DeliveryNotes");  
  
// XPath expression  
XElement el2 = po.XPathSelectElement("DeliveryNotes");  
// same as "child::DeliveryNotes"  
// same as "./DeliveryNotes"  
  
if (el1 == el2)  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
Console.WriteLine(el1);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Results are identical  
<DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML per gli utenti di XPath (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
