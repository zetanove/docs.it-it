---
title: 'Procedura: trovare precedenti elementi di pari livello (XPath-LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 59055718-d0a7-4db3-8901-18dd33587703
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 250028f73eff7aad3926ee4916aef7d118b6fbea
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-find-preceding-siblings-xpath-linq-to-xml-visual-basic"></a>Procedura: trovare precedenti elementi di pari livello (XPath-LINQ to XML) (Visual Basic)
In questo argomento viene confrontato con il `preceding-sibling` asse il [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] figlio <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName>asse.</xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName>  
  
 L'espressione XPath è:  
  
 `preceding-sibling::*`  
  
 Si noti che i risultati di <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A>e <xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName>sono nell'ordine del documento.</xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName> </xref:System.Xml.XPath.Extensions.XPathSelectElements%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene cercato l'elemento `FullAddress` e quindi vengono recuperati gli elementi precedenti usando l'asse `preceding-sibling`.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: Customers e Orders (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md).  
  
```vb  
Dim co As XElement = XElement.Load("CustomersOrders.xml")  
Dim add As XElement = co.<Customers>.<Customer>. _  
        <FullAddress>.FirstOrDefault  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = add.ElementsBeforeSelf()  
  
' XPath expression  
Dim list2 As IEnumerable(Of XElement) = add.XPathSelectElements("preceding-sibling::*")  
  
If list1.Count() = list2.Count() And _  
        list1.Intersect(list2).Count() = list1.Count() Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
For Each el As XElement In list2  
    Console.WriteLine(el)  
Next  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Results are identical  
<CompanyName>Great Lakes Food Market</CompanyName>  
<ContactName>Howard Snyder</ContactName>  
<ContactTitle>Marketing Manager</ContactTitle>  
<Phone>(503) 555-7555</Phone>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML per gli utenti di XPath (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
