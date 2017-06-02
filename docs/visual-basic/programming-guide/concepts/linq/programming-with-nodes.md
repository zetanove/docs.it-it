---
title: Programmazione con nodi (Visual Basic) | Documenti di Microsoft
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
ms.assetid: d8422a9b-dd37-44a3-8aac-2237ed9561e0
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 52fb60b95b869a79900f84c2a1a7a6151bb5b58f
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="programming-with-nodes-visual-basic"></a>Programmazione con nodi (Visual Basic)
Gli sviluppatori di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] che hanno la necessità di scrivere programmi come un editor XML, un sistema di trasformazioni o un writer di rapporti, spesso devono scrivere programmi che funzionano a un livello di granularità maggiore rispetto a elementi e attributi. Devono spesso operare a livello di nodo, modificando i nodi di testo, elaborando istruzioni e commenti. In questo argomento vengono forniti dettagli sulla programmazione a livello di nodo.  
  
## <a name="node-details"></a>Dettagli sui nodi  
 I programmatori che operano a livello di nodo devono conoscere diversi dettagli di programmazione.  
  
### <a name="parent-property-of-children-nodes-of-xdocument-is-set-to-null"></a>La proprietà padre dei nodi figlio di XDocument è impostata su Null  
 Il <xref:System.Xml.Linq.XObject.Parent%2A>proprietà contiene l'elemento padre <xref:System.Xml.Linq.XElement>, non il nodo padre.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XObject.Parent%2A> Nodi figlio di <xref:System.Xml.Linq.XDocument>alcun elemento padre <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> L'elemento padre è il documento, in modo che il <xref:System.Xml.Linq.XObject.Parent%2A>per questi nodi è impostata su null.</xref:System.Xml.Linq.XObject.Parent%2A>  
  
 Questo concetto è illustrato nell'esempio seguente:  
  
```vb  
Dim doc As XDocument = XDocument.Parse("<!-- a comment --><Root/>")  
Console.WriteLine(doc.Nodes().OfType(Of XComment).First().Parent Is Nothing)  
Console.WriteLine(doc.Root.Parent Is Nothing)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
True  
True  
```  
  
### <a name="adjacent-text-nodes-are-possible"></a>I nodi di testo adiacenti sono possibili  
 In diversi modelli di programmazione XML i nodi di testo adiacenti vengono sempre uniti. Questa operazione è denominata normalizzazione dei nodi di testo. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] i nodi di testo non vengono normalizzati. Se si aggiungono due nodi di testo allo stesso elemento, si otterranno nodi di testo adiacenti. Tuttavia, se si aggiunge contenuto specificato come stringa anziché come un <xref:System.Xml.Linq.XText>nodo [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] potrebbe essere di tipo merge la stringa con un nodo di testo adiacente.</xref:System.Xml.Linq.XText>  
  
 Questo concetto è illustrato nell'esempio seguente:  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
' This does not add a new text node.  
xmlTree.Add("new content")  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
'// This does add a new, adjacent text node.  
xmlTree.Add(New XText("more text"))  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
```  
  
 Questo esempio produce il seguente output:  
  
```  
1  
1  
2  
```  
  
### <a name="empty-text-nodes-are-possible"></a>I nodi di testo vuoti sono possibili  
 In alcuni modelli di programmazione di XML è garantito che i nodi di testo non contengono la stringa vuota. Il concetto di base è che un nodo di testo di questo tipo non ha impatto sulla serializzazione dell'XML. Tuttavia, per lo stesso motivo per cui i nodi di testo sono possibili, la rimozione di testo da un nodo di testo impostandone il valore sulla stringa vuota non comporta l'eliminazione del nodo di testo stesso.  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Dim textNode As XText = xmlTree.Nodes().OfType(Of XText)().First()  
  
' The following line does not cause the removal of the text node.  
textNode.Value = ""  
  
Dim textNode2 As XText = xmlTree.Nodes().OfType(Of XText)().First()  
Console.WriteLine(">>{0}<<", textNode2)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
>><<  
```  
  
### <a name="an-empty-text-node-impacts-serialization"></a>Un nodo di testo vuoto ha effetto sulla serializzazione  
 Se un elemento contiene solo un nodo di testo figlio vuoto, verrà serializzato con la sintassi lunga dei tag: `<Child></Child>`. Se un elemento non contiene alcun tipo di nodo figlio, verrà serializzato con la sintassi breve dei tag: `<Child />`.  
  
```vb  
Dim child1 As XElement = New XElement("Child1", _  
    New XText("") _  
)  
Dim child2 As XElement = New XElement("Child2")  
Console.WriteLine(child1)  
Console.WriteLine(child2)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<Child1></Child1>  
<Child2 />  
```  
  
### <a name="namespaces-are-attributes-in-the-linq-to-xml-tree"></a>Gli spazi dei nomi sono attributi nell'albero LINQ to XML  
 Anche se la sintassi delle dichiarazioni di spazi dei nomi è identica a quella degli attributi, in alcune interfacce di programmazione, ad esempio XSLT e XPath, le dichiarazioni di spazi dei nomi non sono considerati attributi. Tuttavia, in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], gli spazi dei nomi vengono archiviati come <xref:System.Xml.Linq.XAttribute>oggetti nell'albero XML.</xref:System.Xml.Linq.XAttribute> Se si scorrono gli attributi per un elemento che contiene una dichiarazione di spazio dei nomi, le dichiarazioni di spazi dei nomi verranno visualizzate come uno degli elementi nella raccolta restituita.  
  
 Il <xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A>proprietà indica se un attributo è una dichiarazione dello spazio dei nomi.</xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A>  
  
```vb  
Dim root As XElement = _   
<Root  
    xmlns='http://www.adventure-works.com'  
    xmlns:fc='www.fourthcoffee.com'  
    AnAttribute='abc'/>  
For Each att As XAttribute In root.Attributes()  
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, _  
                      att.IsNamespaceDeclaration)  
Next  
```  
  
 Questo esempio produce il seguente output:  
  
```  
xmlns="http://www.adventure-works.com"  IsNamespaceDeclaration:True  
xmlns:fc="www.fourthcoffee.com"  IsNamespaceDeclaration:True  
AnAttribute="abc"  IsNamespaceDeclaration:False  
```  
  
### <a name="xpath-axis-methods-do-not-return-child-white-space-of-xdocument"></a>I metodi dell'asse di XPath non restituiscono lo spazio vuoto figlio di XDocument  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]Consente di nodi di testo figlio di un <xref:System.Xml.Linq.XDocument>, purché i nodi di testo contengano solo spazio vuoto.</xref:System.Xml.Linq.XDocument> Tuttavia, il modello a oggetti XPath non include gli spazi vuoti come nodi figlio di un documento, pertanto quando si scorrono gli elementi figlio di un <xref:System.Xml.Linq.XDocument>utilizzando il <xref:System.Xml.Linq.XContainer.Nodes%2A>asse, verranno restituiti nodi di testo di spazi vuoti.</xref:System.Xml.Linq.XContainer.Nodes%2A> </xref:System.Xml.Linq.XDocument> Tuttavia, quando si scorrono gli elementi figlio di un <xref:System.Xml.Linq.XDocument>utilizzando i metodi dell'asse di XPath, nodi testo con spazi vuoti non verranno restituiti.</xref:System.Xml.Linq.XDocument>  
  
```vb  
' Create a document with some white space child nodes of the document.  
Dim root As XDocument = XDocument.Parse( _  
"<?xml version='1.0' encoding='utf-8' standalone='yes'?>" & _  
vbNewLine & "<Root/>" & vbNewLine & "<!--a comment-->" & vbNewLine, _  
LoadOptions.PreserveWhitespace)  
  
' Count the white space child nodes using LINQ to XML.  
Console.WriteLine(root.Nodes().OfType(Of XText)().Count())  
  
' Count the white space child nodes using XPathEvaluate.  
Dim nodes As IEnumerable = CType(root.XPathEvaluate("text()"), IEnumerable)  
Console.WriteLine(nodes.OfType(Of XText)().Count())  
```  
  
 Questo esempio produce il seguente output:  
  
```  
3  
0  
```  
  
### <a name="xdeclaration-objects-are-not-nodes"></a>Gli oggetti XDeclaration non sono nodi  
 Quando si scorrono i nodi figlio di un <xref:System.Xml.Linq.XDocument>, l'oggetto dichiarazione XML non verrà.</xref:System.Xml.Linq.XDocument> Si tratta di una proprietà, non di un nodo figlio del documento.  
  
```vb  
Dim doc As XDocument = _  
<?xml version='1.0' encoding='utf-8' standalone='yes'?>  
<Root/>  
  
doc.Save("Temp.xml")  
Console.WriteLine(File.ReadAllText("Temp.xml"))  
  
' This shows that there is only one child node of the document.  
Console.WriteLine(doc.Nodes().Count())  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root />  
1  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML (Visual Basic) di programmazione avanzata](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

