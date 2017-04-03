---
title: 'Procedura: recuperare una raccolta di elementi (LINQ to XML) (C#) | Documentazione Microsoft'
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
ms.assetid: b849668c-7976-4974-b8e1-1cd587d34258
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d8cb7df493696aac23d223785d6c0f38f1285c8f
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-a-collection-of-elements-linq-to-xml-c"></a>Procedura: recuperare una raccolta di elementi (LINQ to XML) (C#)
Questo argomento illustra il metodo <xref:System.Xml.Linq.XContainer.Elements%2A>. che consente di recuperare una raccolta degli elementi figlio di un elemento.  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono scorsi gli elementi figlio dell'elemento `purchaseOrder`.  
  
 Questo esempio usa il documento XML seguente: [File XML di esempio: ordine di acquisto tipico (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml-1.md).  
  
```csharp  
XElement po = XElement.Load("PurchaseOrder.xml");  
IEnumerable<XElement> childElements =  
    from el in po.Elements()  
    select el;  
foreach (XElement el in childElements)  
    Console.WriteLine("Name: " + el.Name);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Name: Address  
Name: Address  
Name: DeliveryNotes  
Name: Items  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Assi LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)
