---
title: Rimozione di elementi, attributi e nodi da una struttura ad albero XML (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 5cf21919-4360-4b49-b29d-58ea3164ac72
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: eef13476733f7c883080923614683a41d7cb3b3a
ms.lasthandoff: 03/13/2017


---
# <a name="removing-elements-attributes-and-nodes-from-an-xml-tree-visual-basic"></a>Rimozione di elementi, attributi e nodi da una struttura ad albero XML (Visual Basic)
È possibile modificare un albero XML, rimuovendo elementi, attributi e altri tipi di nodi.  
  
 La rimozione di un singolo elemento o di un singolo attributo da un documento XML è un processo semplice. Tuttavia, quando si rimuovono raccolte di elementi o attributi, è necessario innanzitutto materializzare una raccolta in un elenco e quindi eliminare gli elementi o gli attributi dall'elenco. L'approccio migliore consiste nell'utilizzare il <xref:System.Xml.Linq.Extensions.Remove%2A>metodo di estensione, questa operazione verrà eseguita automaticamente.</xref:System.Xml.Linq.Extensions.Remove%2A>  
  
 Il motivo principale per cui scegliere questo approccio è che la maggior parte delle raccolte recuperate da un albero XML viene restituita tramite esecuzione posticipata. Se le raccolte non vengono dapprima materializzate in un elenco o se non vengono usati i metodi di estensione, è possibile riscontrare una determinata categoria di bug. Per ulteriori informazioni, vedere [mista dichiarativa/bug nel codice imperativo (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/mixed-declarative-code-imperative-code-bugs-linq-to-xml.md).  
  
 I metodi seguenti consentono di rimuovere nodi e attributi da un albero XML.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[XAttribute.Remove](https://msdn.microsoft.com/library/system.xml.linq.xattribute.remove\(v=vs.110\).aspx)|Rimuove un <xref:System.Xml.Linq.XAttribute>dal relativo elemento padre.</xref:System.Xml.Linq.XAttribute>|  
|[XContainer.RemoveNodes](https://msdn.microsoft.com/library/system.xml.linq.xcontainer.removenodes\(v=vs.110\).aspx)|Rimuove i nodi figlio da un <xref:System.Xml.Linq.XContainer>.</xref:System.Xml.Linq.XContainer>|  
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=fullName>|Rimuove il contenuto e gli attributi da un <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>|  
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=fullName>|Rimuove gli attributi di un <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement>|  
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=fullName>|Se viene passato `null` come valore, rimuove l'attributo.|  
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=fullName>|Se viene passato `null` come valore, rimuove l'elemento figlio.|  
|<xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=fullName>|Rimuove un <xref:System.Xml.Linq.XNode>dal relativo elemento padre.</xref:System.Xml.Linq.XNode>|  
|<xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=fullName></xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=fullName>|Rimuove ogni attributo o elemento nella raccolta di origine dal relativo elemento padre.|  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 In questo esempio sono illustrati tre approcci per la rimozione di elementi. Con il primo viene rimosso un singolo elemento. In secondo luogo, viene recuperata una raccolta di elementi, materializzata tramite il <xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>operatore e rimuove la raccolta.</xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName> Infine, recupera una raccolta di elementi e di rimuoverli tramite il <xref:System.Xml.Linq.Extensions.Remove%2A>metodo di estensione.</xref:System.Xml.Linq.Extensions.Remove%2A>  
  
 Per ulteriori informazioni sui <xref:System.Linq.Enumerable.ToList%2A>operatore, vedere [la conversione di tipi di dati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md).</xref:System.Linq.Enumerable.ToList%2A>  
  
### <a name="code"></a>Codice  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <Child1>  
            <GrandChild1/>  
            <GrandChild2/>  
            <GrandChild3/>  
        </Child1>  
        <Child2>  
            <GrandChild4/>  
            <GrandChild5/>  
            <GrandChild6/>  
        </Child2>  
        <Child3>  
            <GrandChild7/>  
            <GrandChild8/>  
            <GrandChild9/>  
        </Child3>  
    </Root>  
root.<Child1>.<GrandChild1>.Remove()  
root.<Child2>.Elements().ToList().Remove()  
root.<Child3>.Elements().Remove()  
Console.WriteLine(root)  
  
```  
  
### <a name="comments"></a>Commenti  
 L'output del codice è il seguente:  
  
```xml  
<Root>  
  <Child1>  
    <GrandChild2 />  
    <GrandChild3 />  
  </Child1>  
  <Child2 />  
  <Child3 />  
</Root>  
```  
  
 Si noti che il primo elemento nipote è stato rimosso da `Child1`. Tutti gli elementi nipote sono stati rimossi da `Child2` e da `Child3`.  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica di strutture ad albero XML (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
