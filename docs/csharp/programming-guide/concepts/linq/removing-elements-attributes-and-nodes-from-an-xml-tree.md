---
title: Rimozione di elementi, attributi e nodi da un albero XML (C#) | Microsoft Docs
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
ms.assetid: 07dd06d6-1117-4077-bf98-9120cf51176e
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 23091224f314582908438f29340b811498d4c90e
ms.lasthandoff: 03/13/2017


---
# <a name="removing-elements-attributes-and-nodes-from-an-xml-tree-c"></a>Rimozione di elementi, attributi e nodi da un albero XML (C#)
È possibile modificare un albero XML, rimuovendo elementi, attributi e altri tipi di nodi.  
  
 La rimozione di un singolo elemento o di un singolo attributo da un documento XML è un processo semplice. Tuttavia, quando si rimuovono raccolte di elementi o attributi, è necessario innanzitutto materializzare una raccolta in un elenco e quindi eliminare gli elementi o gli attributi dall'elenco. L'approccio più efficace è usare il metodo di estensione <xref:System.Xml.Linq.Extensions.Remove%2A>, che consente di ottenere questi risultati.  
  
 Il motivo principale per cui scegliere questo approccio è che la maggior parte delle raccolte recuperate da un albero XML viene restituita tramite esecuzione posticipata. Se le raccolte non vengono dapprima materializzate in un elenco o se non vengono usati i metodi di estensione, è possibile riscontrare una determinata categoria di bug. Per altre informazioni, vedere [Mixed Declarative Code/Imperative Code Bugs (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/mixed-declarative-code-imperative-code-bugs-linq-to-xml.md) (Bug nel codice dichiarativo/imperativo misto (LINQ to XML) (C#)).  
  
 I metodi seguenti consentono di rimuovere nodi e attributi da un albero XML.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[XAttribute.Remove](https://msdn.microsoft.com/library/system.xml.linq.xattribute.remove\(v=vs.110\).aspx)|Rimuove un elemento <xref:System.Xml.Linq.XAttribute> dal relativo elemento padre.|  
|[XContainer.RemoveNodes](https://msdn.microsoft.com/library/system.xml.linq.xcontainer.removenodes\(v=vs.110\).aspx)|Rimuove i nodi figlio da un elemento <xref:System.Xml.Linq.XContainer>.|  
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=fullName>|Rimuove il contenuto e gli attributi da un elemento <xref:System.Xml.Linq.XElement>.|  
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=fullName>|Rimuove gli attributi di un elemento <xref:System.Xml.Linq.XElement>.|  
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=fullName>|Se viene passato `null` come valore, rimuove l'attributo.|  
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=fullName>|Se viene passato `null` come valore, rimuove l'elemento figlio.|  
|<xref:System.Xml.Linq.XNode.Remove%2A?displayProperty=fullName>|Rimuove un elemento <xref:System.Xml.Linq.XNode> dal relativo elemento padre.|  
|<xref:System.Xml.Linq.Extensions.Remove%2A?displayProperty=fullName>|Rimuove ogni attributo o elemento nella raccolta di origine dal relativo elemento padre.|  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 In questo esempio sono illustrati tre approcci per la rimozione di elementi. Con il primo viene rimosso un singolo elemento. Con il secondo viene recuperata una raccolta di elementi, che viene materializzata usando l'operatore <xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName> e quindi viene rimossa. Infine, viene recuperata una raccolta di elementi che viene rimossa usando il metodo di estensione <xref:System.Xml.Linq.Extensions.Remove%2A>.  
  
 Per altre informazioni sull'operatore <xref:System.Linq.Enumerable.ToList%2A>, vedere l'articolo relativo alla [conversione dei tipi di dati (C#)](../../../../csharp/programming-guide/concepts/linq/converting-data-types.md).  
  
### <a name="code"></a>Codice  
  
```csharp  
XElement root = XElement.Parse(@"<Root>  
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
</Root>");  
root.Element("Child1").Element("GrandChild1").Remove();  
root.Element("Child2").Elements().ToList().Remove();  
root.Element("Child3").Elements().Remove();  
Console.WriteLine(root);  
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
 [Modifying XML Trees (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md) (Modifica di strutture ad albero XML (LINQ to XML) in C#)
