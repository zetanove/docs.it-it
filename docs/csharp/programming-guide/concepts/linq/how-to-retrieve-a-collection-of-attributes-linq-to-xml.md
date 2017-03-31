---
title: 'Procedura: Recuperare una raccolta di attributi (LINQ to XML) (C#) | Microsoft Docs'
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
ms.assetid: a49ee7a3-b2c2-4d49-9b5c-b7c6c41f4f13
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 646e012392c3c49de1f89b170416fc00f24e5dae
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-a-collection-of-attributes-linq-to-xml-c"></a>Procedura: Recuperare una raccolta di attributi (LINQ to XML) (C#)
Questo argomento presenta il metodo <xref:System.Xml.Linq.XElement.Attributes%2A> che consente di recuperare gli attributi di un elemento.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come scorrere la raccolta di attributi di un elemento.  
  
```csharp  
XElement val = new XElement("Value",  
    new XAttribute("ID", "1243"),  
    new XAttribute("Type", "int"),  
    new XAttribute("ConvertableTo", "double"),  
    "100");  
IEnumerable<XAttribute> listOfAttributes =  
    from att in val.Attributes()  
    select att;  
foreach (XAttribute a in listOfAttributes)  
    Console.WriteLine(a);  
```  
  
 L'output del codice è il seguente:  
  
```  
ID="1243"  
Type="int"  
ConvertableTo="double"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Assi LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)
