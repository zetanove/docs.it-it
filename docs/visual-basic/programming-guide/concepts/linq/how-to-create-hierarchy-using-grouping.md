---
title: 'Procedura: creare una gerarchia tramite raggruppamento (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 4eb3ca6b-1aed-43de-b8b9-41c769c993f8
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 09f75d439eeba1a4b991587053e77021d1928d4c
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-create-hierarchy-using-grouping-visual-basic"></a>Procedura: creare una gerarchia tramite raggruppamento (Visual Basic)
In questo esempio viene illustrato come raggruppare dati e quindi generare codice XML basato sul raggruppamento.  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono prima raggruppati i dati in base a una categoria, quindi viene generato un nuovo file XML in cui la gerarchia XML riflette il raggruppamento.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: dati numerici (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-numerical-data-linq-to-xml.md).  
  
```vb  
Dim doc As XElement = XElement.Load("Data.xml")  
Dim newData As XElement = _  
    <Root>  
        <%= _  
            From data In doc.<Data> _  
            Group By category = data.<Category>(0).Value _  
            Into groupedData = Group _  
            Select <Group ID=<%= category %>>  
                       <%= _  
                           From g In groupedData _  
                           Select _  
                           <Data>  
                               <%= g.<Quantity>(0) %>  
                               <%= g.<Price>(0) %>  
                           </Data> _  
                       %>  
                   </Group> _  
        %>  
    </Root>  
Console.WriteLine(newData)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <Group ID="A">  
    <Data>  
      <Quantity>3</Quantity>  
      <Price>24.50</Price>  
    </Data>  
    <Data>  
      <Quantity>5</Quantity>  
      <Price>4.95</Price>  
    </Data>  
    <Data>  
      <Quantity>3</Quantity>  
      <Price>66.00</Price>  
    </Data>  
    <Data>  
      <Quantity>15</Quantity>  
      <Price>29.00</Price>  
    </Data>  
  </Group>  
  <Group ID="B">  
    <Data>  
      <Quantity>1</Quantity>  
      <Price>89.99</Price>  
    </Data>  
    <Data>  
      <Quantity>10</Quantity>  
      <Price>.99</Price>  
    </Data>  
    <Data>  
      <Quantity>8</Quantity>  
      <Price>6.99</Price>  
    </Data>  
  </Group>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tecniche di Query (LINQ to XML) avanzate (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
