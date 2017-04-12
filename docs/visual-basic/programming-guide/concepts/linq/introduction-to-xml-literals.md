---
title: Introduzione ai valori letterali XML in Visual Basic2 | Documenti di Microsoft
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
ms.assetid: 94fc0e03-978e-4c08-ab6c-0dc3c1e64f10
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 391dd14f971f91d4d128841a7ebd24981266846a
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-xml-literals-in-visual-basic"></a>Introduzione ai valori letterali XML in Visual Basic
Contenuto della sezione vengono fornite informazioni sulla creazione di alberi XML in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 Per informazioni sull'utilizzo dei risultati delle query LINQ come contenuto di una struttura ad albero XML, vedere [costruzione funzionale (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-construction-linq-to-xml.md).  
  
 Per ulteriori informazioni sui valori letterali XML in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], vedere [Panoramica di LINQ to XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md).  
  
## <a name="creating-xml-trees"></a>Creazione di alberi XML  
 Nell'esempio seguente viene illustrato come creare un <xref:System.Xml.Linq.XElement>in questo caso, `contacts`:</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim contacts As XElement = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone>206-555-0144</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
### <a name="creating-an-xelement-with-simple-content"></a>Creazione di un XElement con contenuto semplice  
 È possibile creare un <xref:System.Xml.Linq.XElement>con contenuto semplice, come indicato di seguito:</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim n as XElement = <Customer>Adventure Works</Customer>  
Console.WriteLine(n)   
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
### <a name="creating-an-empty-element"></a>Creazione di un elemento vuoto  
 È possibile creare un oggetto vuoto <xref:System.Xml.Linq.XElement>, come segue:</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim n As XElement = <Customer/>  
Console.WriteLine(n)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Customer />  
```  
  
### <a name="using-embedded-expressions"></a>Uso di espressioni incorporate  
 Un'importante funzionalità dei valori letterali XML è che consentono di usare espressioni incorporate. Con le espressioni incorporate è possibile valutare un'espressione e inserirne i risultati nell'albero XML. Se l'espressione restituisce un tipo di <xref:System.Xml.Linq.XElement>, viene inserito un elemento nell'albero.</xref:System.Xml.Linq.XElement> Se l'espressione restituisce un tipo di <xref:System.Xml.Linq.XAttribute>, nell'albero viene inserito un attributo.</xref:System.Xml.Linq.XAttribute> È possibile inserire elementi e attributi nell'albero solo nei casi in cui sono validi.  
  
 È importante notare che un'espressione incorporata può includere una sola espressione. Non è possibile incorporare più istruzioni. Se un'espressione si estende oltre una singola riga, è necessario usare il carattere di continuazione di riga.  
  
 Se si usa un'espressione incorporata per aggiungere nodi (inclusi elementi) e attributi esistenti a un nuovo albero XML e se per i nodi esistenti è già presente un elemento padre, i nodi vengono duplicati. I nuovi nodi duplicati vengono collegati al nuovo albero XML. Se per i nodi esistenti non è presente un elemento padre, i nodi vengono semplicemente collegati al nuovo albero XML. Tale comportamento è illustrato nell'ultimo esempio di questo argomento.  
  
 Nell'esempio seguente viene usata un'espressione incorporata per inserire un elemento nella struttura ad albero.  
  
```vb  
xmlTree1 As XElement = _  
    <Root>  
        <Child>Contents</Child>  
    </Root>  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child> %>  
    </Root>  
Console.WriteLine(xmlTree2)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <Child>Contents</Child>  
</Root>  
```  
  
### <a name="using-embedded-expressions-for-content"></a>Uso di espressioni incorporate per il contenuto  
 È possibile usare un'espressione incorporata per fornire il contenuto di un elemento:  
  
```vb  
Dim str As String  
str = "Some content"  
Dim root As XElement = <Root><%= str %></Root>  
Console.WriteLine(root)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>Some content</Root>  
```  
  
### <a name="using-a-linq-query-in-an-embedded-expression"></a>Uso di una query LINQ in un'espressione incorporata  
 È possibile usare i risultati di una query LINQ per il contenuto di un elemento:  
  
```vb  
Dim arr As Integer() = {1, 2, 3}  
  
Dim n As XElement = _  
    <Root>  
        <%= From i In arr Select <Child><%= i %></Child> %>  
    </Root>  
  
Console.WriteLine(n)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Child>3</Child>  
</Root>  
```  
  
### <a name="using-embedded-expressions-for-node-names"></a>Uso di espressioni incorporate per i nomi di nodo  
 È inoltre possibile usare espressioni incorporate per calcolare nomi e valori di attributi ed elementi:  
  
```vb  
Dim eleName As String = "ele"  
Dim attName As String = "att"  
Dim attValue As String = "aValue"  
Dim eleValue As String = "eValue"  
Dim n As XElement = _  
    <Root <%= attName %>=<%= attValue %>>  
        <<%= eleName %>>  
            <%= eleValue %>  
        </>  
    </Root>  
Console.WriteLine(n)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root att="aValue">  
  <ele>eValue</ele>  
</Root>  
```  
  
### <a name="cloning-vs-attaching"></a>Duplicazione e collegamento  
 Come accennato in precedenza, se si usa un'espressione incorporata per aggiungere nodi (inclusi elementi) e attributi esistenti a un nuovo albero XML e se per i nodi esistenti è già presente un elemento padre, i nodi vengono duplicati. I nodi appena duplicati vengono quindi collegati al nuovo albero. Se per i nodi esistenti non è presente un elemento padre, i nodi vengono semplicemente collegati al nuovo albero XML.  
  
```vb  
' Create a tree with a child element.  
Dim xmlTree1 As XElement = _  
    <Root>  
        <Child1>1</Child1>  
    </Root>  
  
' Create an element that is not parented.  
Dim child2 As XElement = <Child2>2</Child2>  
  
' Create a tree and add Child1 and Child2 to it.  
Dim xmlTree2 As XElement = _  
    <Root>  
        <%= xmlTree1.<Child1>(0) %>  
        <%= child2 %>  
    </Root>  
  
' Compare Child1 identity.  
Console.WriteLine("Child1 was {0}", _  
    IIf(xmlTree1.Element("Child1") Is xmlTree2.Element("Child1"), _  
    "attached", "cloned"))  
  
' Compare Child2 identity.  
Console.WriteLine("Child2 was {0}", _  
    IIf(child2 Is xmlTree2.Element("Child2"), _  
    "attached", "cloned"))  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
