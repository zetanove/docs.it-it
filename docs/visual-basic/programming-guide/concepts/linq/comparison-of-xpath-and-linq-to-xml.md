---
title: Confronto tra XPath e LINQ to XML1 | Documenti di Microsoft
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
ms.assetid: c3fd07c1-6761-4e4b-8eb1-ddd780ed8d44
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e9601c51468fdf5adab8e521f8f89ee7f2e12869
ms.lasthandoff: 03/13/2017


---
# <a name="comparison-of-xpath-and-linq-to-xml"></a>Confronto tra XPath e LINQ to XML
XPath e [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] offrono alcune funzionalità analoghe. Entrambi possono essere usati per eseguire query su un albero XML, restituendo risultati quali una raccolta di elementi, una raccolta di attributi, una raccolta di nodi o il valore di un elemento o di un attributo. Esistono tuttavia alcune differenze.  
  
## <a name="differences-between-xpath-and-linq-to-xml"></a>Differenze tra XPath e LINQ to XML  
 XPath non consente la proiezione di nuovi tipi. È in grado di restituire solo raccolte di nodi dall'albero, mentre tramite [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile eseguire una query e proiettare un oggetto grafico o un albero XML in una nuova forma. Le query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] includono molte più funzionalità e sono molto più potenti delle espressioni XPath.  
  
 Le espressioni XPath esistono in isolamento all'interno di una stringa. Il compilatore Visual Basic non consente di analizzare l'espressione XPath in fase di compilazione. Al contrario, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] le query vengono analizzate e compilate dal compilatore base theVisual. Il compilatore è in grado di intercettare molti errori di query.  
  
 I risultati di XPath non sono fortemente tipizzati. In diverse circostanze il risultato della valutazione di un'espressione XPath è un oggetto e spetta allo sviluppatore determinare il tipo appropriato ed eseguire il cast del risultato secondo necessità. Al contrario, le proiezioni di una query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] sono fortemente tipizzate.  
  
## <a name="result-ordering"></a>Ordinazione di risultati  
 Nella raccomandazione XPath 1.0 si afferma che una raccolta corrispondente al risultato della valutazione di un'espressione XPath non è ordinata.  
  
 Tuttavia, quando si scorre una raccolta restituita da un metodo dell'asse XPath [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], i nodi della raccolta vengono restituiti nell'ordine del documento. Ciò è vero anche quando si accede a assi XPath in cui i predicati sono espressi in termini di ordine inverso del documento, ad esempio `preceding` e `preceding-sibling`.  
  
 Al contrario, la maggior parte del [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] restituiscono raccolte nell'ordine del documento, ma due di essi, <xref:System.Xml.Linq.XNode.Ancestors%2A>e <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A>, restituiscono le raccolte nell'ordine inverso del documento.</xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A> </xref:System.Xml.Linq.XNode.Ancestors%2A> Nella tabella seguente sono enumerati gli assi e viene indicato l'ordine delle raccolte per ognuno di essi:  
  
|Asse LINQ to XML|Ordinazioni|  
|----------------------|--------------|  
|XContainer.DescendantNodes|Ordine del documento|  
|XContainer.Descendants|Ordine del documento|  
|XContainer.Elements|Ordine del documento|  
|XContainer.Nodes|Ordine del documento|  
|XContainer.NodesAfterSelf|Ordine del documento|  
|XContainer.NodesBeforeSelf|Ordine del documento|  
|XElement.AncestorsAndSelf|Ordine inverso del documento|  
|XElement.Attributes|Ordine del documento|  
|XElement.DescendantNodesAndSelf|Ordine del documento|  
|XElement.DescendantsAndSelf|Ordine del documento|  
|XNode.Ancestors|Ordine inverso del documento|  
|XNode.ElementsAfterSelf|Ordine del documento|  
|XNode.ElementsBeforeSelf|Ordine del documento|  
|XNode.NodesAfterSelf|Ordine del documento|  
|XNode.NodesBeforeSelf|Ordine del documento|  
  
## <a name="positional-predicates"></a>Predicati di posizione  
 All'interno di un'espressione XPath, i predicati di posizione vengono espressi in termini di ordine del documento per molti assi, mentre sono espressi in ordine inverso del documento per gli assi inversi, che sono `preceding`, `preceding-sibling`, `ancestor` e `ancestor-or-self`. Ad esempio, l'espressione XPath `preceding-sibling::*[1]` restituisce l'elemento di pari livello immediatamente precedente. Ciò è vero anche se il set di risultati finale è presentato nell'ordine del documento.  
  
 Al contrario, tutti i predicati di posizione di LINQ to XML sono sempre espressi in termini di ordine dell'asse. Ad esempio, `anElement.ElementsBeforeSelf().ToList()[0]` restituisce il primo elemento figlio del padre dell'elemento sottoposto a query, non l'elemento di pari livello immediatamente precedente. Un altro esempio: `anElement.Ancestors().ToList()[0]` restituisce l'elemento padre.  
  
 Si noti che con l'approccio precedente viene materializzata l'intera raccolta. Non si tratta della modalità più efficiente per scrivere la query. È stata scritta in questo modo per illustrare il comportamento dei predicati di posizione. Un modo più appropriato per scrivere la stessa query consiste nell'utilizzare il <xref:System.Linq.Enumerable.First%2A>(metodo), come indicato di seguito: `anElement.ElementsBeforeSelf().First()`.</xref:System.Linq.Enumerable.First%2A>  
  
 Se si desidera trovare l'elemento immediatamente precedente in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], scrivere la seguente espressione:  
  
 `ElementsBeforeSelf().Last()`  
  
## <a name="performance-differences"></a>Differenze di prestazioni  
 Query XPath che utilizzano la funzionalità XPath in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] non eseguirà nonché [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] query.  
  
## <a name="comparison-of-composition"></a>Confronto di composizione  
 La composizione di una query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è parallela a quella di un'espressione XPath, anche se molto diversa nella sintassi.  
  
 Se ad esempio una variabile denominata `customers` contiene un elemento e si desidera trovare un elemento nipote denominato `CompanyName` sotto tutti gli elementi figlio denominati `Customer`, è necessario scrivere la seguente espressione XPath:  
  
```vb  
customers.XPathSelectElements("./Customer/CompanyName")  
```  
  
 La query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] equivalente è:  
  
```vb  
customers.Element("Customer").Elements("CompanyName")  
```  
  
 Esistono paralleli analoghi per ogni asse XPath.  
  
|Asse XPath|Asse LINQ to XML|  
|----------------|----------------------|  
|child (asse predefinito)|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>|  
|Parent (..)|<xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName></xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=fullName>|  
|attribute (@)|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName><br /><br /> o<br /><br /> <xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=fullName>|  
|asse ancestor|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=fullName>|  
|asse ancestor-or-self|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=fullName>|  
|asse descendant (//)|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName><br /><br /> o<br /><br /> <xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName></xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=fullName>|  
|descendant-or-self|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=fullName><br /><br /> o<br /><br /> <xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=fullName>|  
|following-sibling|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=fullName><br /><br /> o<br /><br /> <xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=fullName>|  
|preceding-sibling|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=fullName><br /><br /> o<br /><br /> <xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=fullName>|  
|following|Nessun equivalente diretto.|  
|preceding|Nessun equivalente diretto.|  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML per gli utenti di XPath (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
