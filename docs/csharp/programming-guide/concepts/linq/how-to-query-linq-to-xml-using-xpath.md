---
title: 'Procedura: Eseguire una query in LINQ to XML tramite XPath (C#) | Microsoft Docs'
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
ms.assetid: ee5af263-4ab1-45e5-b792-33a3221b426d
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 86d02a119423fe33731f0049ca232dde7509936d
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-query-linq-to-xml-using-xpath-c"></a>Procedura: Eseguire una query in LINQ to XML tramite XPath (C#)
In questo argomento vengono presentati i metodi di estensione che consentono di eseguire una query su un albero XML usando XPath. Per informazioni dettagliate sull'uso di questi metodi di estensione, vedere <xref:System.Xml.XPath.Extensions?displayProperty=fullName>.  
  
 A meno che non esista un motivo molto specifico per eseguire query tramite XPATH, ad esempio l'uso esteso di codice legacy, è preferibile non usare XPATH con LINQ to XML. Le query XPath non vengono eseguite con le stesse prestazioni delle query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
## <a name="example"></a>Esempio  
 L'esempio seguente crea un piccolo albero XML e usa <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A> per selezionare un set di elementi.  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child1", 1),  
    new XElement("Child1", 2),  
    new XElement("Child1", 3),  
    new XElement("Child2", 4),  
    new XElement("Child2", 5),  
    new XElement("Child2", 6)  
);  
IEnumerable<XElement> list = root.XPathSelectElements("./Child2");  
foreach (XElement el in list)  
    Console.WriteLine(el);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<Child2>4</Child2>  
<Child2>5</Child2>  
<Child2>6</Child2>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tecniche di query avanzate (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
