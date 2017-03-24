---
title: Aggiunta di elementi, attributi e nodi a una struttura ad albero XML (Visual Basic) | Documenti di Microsoft
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
ms.assetid: e243e694-c987-43aa-8b22-1e33dace582c
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b8a1644757fb4ce9f1498e79b16d1077e412346b
ms.lasthandoff: 03/13/2017


---
# <a name="adding-elements-attributes-and-nodes-to-an-xml-tree-visual-basic"></a>Aggiunta di elementi, attributi e nodi a una struttura ad albero XML (Visual Basic)
È possibile aggiungere contenuto (elementi, attributi, commenti, istruzioni di elaborazione, testo e CDATA) a un albero XML esistente.  
  
## <a name="methods-for-adding-content"></a>Metodi per l'aggiunta di contenuto  
 I metodi seguenti aggiungono contenuto figlio a un <xref:System.Xml.Linq.XElement>o un <xref:System.Xml.Linq.XDocument>:</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Add%2A></xref:System.Xml.Linq.XContainer.Add%2A>|Consente di aggiungere contenuto alla fine del contenuto figlio dell'elemento <xref:System.Xml.Linq.XContainer>.</xref:System.Xml.Linq.XContainer>|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A></xref:System.Xml.Linq.XContainer.AddFirst%2A>|Aggiunge contenuto all'inizio del contenuto figlio dell'elemento <xref:System.Xml.Linq.XContainer>.</xref:System.Xml.Linq.XContainer>|  
  
 I seguenti metodi di aggiungere contenuto come nodi di pari livello di un <xref:System.Xml.Linq.XNode>.</xref:System.Xml.Linq.XNode> Il nodo più comune a cui aggiungere contenuto di pari livello è <xref:System.Xml.Linq.XElement>, anche se è possibile aggiungere contenuto di pari livello valido ad altri tipi di nodi, ad esempio <xref:System.Xml.Linq.XText>o <xref:System.Xml.Linq.XComment>.</xref:System.Xml.Linq.XComment> </xref:System.Xml.Linq.XText> </xref:System.Xml.Linq.XElement>  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A></xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|Aggiunge contenuto dopo la <xref:System.Xml.Linq.XNode>.</xref:System.Xml.Linq.XNode>|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A></xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|Aggiunge contenuto prima di <xref:System.Xml.Linq.XNode>.</xref:System.Xml.Linq.XNode>|  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente vengono create due strutture ad albero XML e quindi ne viene modificata una.  
  
### <a name="code"></a>Codice  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element1>1</Element1>  
        <Element2>2</Element2>  
        <Element3>3</Element3>  
        <Element4>4</Element4>  
        <Element5>5</Element5>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child1>1</Child1>  
        <Child2>2</Child2>  
        <Child3>3</Child3>  
        <Child4>4</Child4>  
        <Child5>5</Child5>  
    </Root>  
  
xmlTree.Add(<NewChild>new content</NewChild>)  
xmlTree.Add( _  
    From el In srcTree.Elements() _  
    Where CInt(el) > 3 _  
    Select el)  
  
' Even though Child9 does not exist in srcTree, the following statement  
' will not throw an exception, and nothing will be added to xmlTree.  
xmlTree.Add(srcTree.Element("Child9"))  
Console.WriteLine(xmlTree)  
  
```  
  
### <a name="comments"></a>Commenti  
 L'output del codice è il seguente:  
  
```xml  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
  <Child4>4</Child4>  
  <Child5>5</Child5>  
  <NewChild>new content</NewChild>  
  <Element4>4</Element4>  
  <Element5>5</Element5>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica di strutture ad albero XML (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
