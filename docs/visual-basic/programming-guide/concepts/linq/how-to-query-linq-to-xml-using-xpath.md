---
title: 'Procedura: eseguire una Query LINQ to XML tramite XPath (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: e1f69a20-1efa-452d-9089-c472fa84b3d5
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0356a7210fbc1b1e0c15adc9d37b6099877fa655
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-query-linq-to-xml-using-xpath-visual-basic"></a>Procedura: eseguire una Query LINQ to XML tramite XPath (Visual Basic)
In questo argomento vengono presentati i metodi di estensione che consentono di eseguire una query su un albero XML usando XPath. Per informazioni dettagliate sull'utilizzo di questi metodi di estensione, vedere <xref:System.Xml.XPath.Extensions?displayProperty=fullName>.</xref:System.Xml.XPath.Extensions?displayProperty=fullName>  
  
 A meno che non esista un motivo molto specifico per eseguire query tramite XPATH, ad esempio l'uso esteso di codice legacy, è preferibile non usare XPATH con LINQ to XML. Le query XPath non eseguirà nonché [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] query.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creata un piccolo albero XML e viene utilizzato <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A>per selezionare un set di elementi.</xref:System.Xml.XPath.Extensions.XPathSelectElements%2A>  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <Child1>1</Child1>  
        <Child1>2</Child1>  
        <Child1>3</Child1>  
        <Child2>4</Child2>  
        <Child2>5</Child2>  
        <Child2>6</Child2>  
    </Root>  
  
Dim list As IEnumerable(Of XElement) = root.XPathSelectElements("./Child2")  
For Each el As XElement In list  
    Console.WriteLine(el)  
Next  
  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<Child2>4</Child2>  
<Child2>5</Child2>  
<Child2>6</Child2>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tecniche di Query (LINQ to XML) avanzate (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
