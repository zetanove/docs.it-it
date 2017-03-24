---
title: 'Procedura: utilizzare dizionari in LINQ to XML (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 6cb3f969-1986-414a-b850-87418712edea
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3441e513012ba24419a3c5330cdb2f75f5ca394f
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-work-with-dictionaries-using-linq-to-xml-visual-basic"></a>Procedura: utilizzare dizionari in LINQ to XML (Visual Basic)
Spesso risulta utile eseguire la conversione in XML di varie strutture dati e la riconversione di altre strutture dati in XML. In questo argomento viene illustrata un'implementazione specifica di questo approccio generale convertendo un <xref:System.Collections.Generic.Dictionary%602>in XML e viceversa.</xref:System.Collections.Generic.Dictionary%602>  
  
## <a name="example"></a>Esempio  
 In questo esempio utilizza i valori letterali XML e una query in un'espressione incorporata. La query proietta nuovi <xref:System.Xml.Linq.XElement>oggetti, che diventano quindi il nuovo contenuto per il `Root` <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement>  
  
```vb  
Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)()  
dict.Add("Child1", "Value1")  
dict.Add("Child2", "Value2")  
dict.Add("Child3", "Value3")  
dict.Add("Child4", "Value4")  
Dim root As XElement = _  
    <Root>  
        <%= From keyValue In dict _  
            Select New XElement(keyValue.Key, keyValue.Value) %>  
    </Root>  
Console.WriteLine(root)  
```  
  
 L'output del codice è il seguente:  
  
```xml  
  
          <Root>  
  <Child1>Value1</Child1>  
  <Child2>Value2</Child2>  
  <Child3>Value3</Child3>  
  <Child4>Value4</Child4>  
</Root>  
```  
  
## <a name="example"></a>Esempio  
 Nel codice seguente viene creato un dizionario da XML.  
  
```vb  
Dim root As XElement = _  
        <Root>  
            <Child1>Value1</Child1>  
            <Child2>Value2</Child2>  
            <Child3>Value3</Child3>  
            <Child4>Value4</Child4>  
        </Root>  
  
Dim dict As Dictionary(Of String, String) = New Dictionary(Of String, String)  
For Each el As XElement In root.Elements  
    dict.Add(el.Name.LocalName, el.Value)  
Next  
For Each str As String In dict.Keys  
    Console.WriteLine("{0}:{1}", str, dict(str))  
Next  
```  
  
 L'output del codice è il seguente:  
  
```  
Child1:Value1  
Child2:Value2  
Child3:Value3  
Child4:Value4  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proiezioni e trasformazioni (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
