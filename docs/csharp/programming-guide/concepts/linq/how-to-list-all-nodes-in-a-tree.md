---
title: 'Procedura: Elencare tutti i nodi in un albero (C#) | Microsoft Docs'
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
ms.assetid: 3e934371-f4c6-458b-9f6b-f9061b596f5b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0d91ec6807a533a504c643bc1303d1a42953f942
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-list-all-nodes-in-a-tree-c"></a>Procedura: Elencare tutti i nodi in un albero (C#)
A volte risulta utile elencare tutti i nodi di un albero, ad esempio quando si desidera identificare gli effetti esatti di una proprietà o metodo sull'albero. Uno degli approcci disponibili per elencare tutti i nodi in formato testuale consiste nel generare un'espressione XPath che identifica in modo esatto e specifico qualsiasi nodo nell'albero.  
  
 Non risulta particolarmente utile eseguire espressioni XPath tramite [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]. Le espressioni XPath hanno prestazioni inferiori rispetto alle query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] e le query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] sono molto più potenti. Tuttavia, XPath è efficace per identificare i nodi nell'albero XML.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrata una funzione denominata `GetXPath` che genera un'espressione XPath specifica per qualsiasi nodo nell'albero XML. Genera espressioni XPath appropriate anche quando i nodi sono inclusi in uno spazio dei nomi. Le espressioni XPath vengono generate usando prefissi di spazio dei nomi.  
  
 Nell'esempio viene quindi creata un piccolo albero XML che contiene un esempio di diversi tipi di nodi. Vengono quindi scorsi i nodi discendenti e viene stampata l'espressione XPath per ogni nodo.  
  
 Si noterà che la dichiarazione di XML non è un nodo dell'albero.  
  
 Il file XML seguente contiene diversi tipi di nodi:  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<?target data?>  
<Root AttName="An Attribute" xmlns:aw="http://www.adventure-works.com">  
  <!--This is a comment-->  
  <Child>Text</Child>  
  <Child>Other Text</Child>  
  <ChildWithMixedContent>text<b>BoldText</b>otherText</ChildWithMixedContent>  
  <aw:ElementInNamespace>  
    <aw:ChildInNamespace />  
  </aw:ElementInNamespace>  
</Root>  
```  
  
 Di seguito è riportato l'elenco dei nodi dell'albero XML precedente, espressi come espressioni XPath:  
  
```  
/processing-instruction()  
/Root  
/Root/@AttName  
/Root/@xmlns:aw  
/Root/comment()  
/Root/Child[1]  
/Root/Child[1]/text()  
/Root/Child[2]  
/Root/Child[2]/text()  
/Root/ChildWithMixedContent  
/Root/ChildWithMixedContent/text()[1]  
/Root/ChildWithMixedContent/b  
/Root/ChildWithMixedContent/b/text()  
/Root/ChildWithMixedContent/text()[2]  
/Root/aw:ElementInNamespace  
/Root/aw:ElementInNamespace/aw:ChildInNamespace  
```  
  
```csharp  
public static class MyExtensions  
{  
    private static string GetQName(XElement xe)  
    {  
        string prefix = xe.GetPrefixOfNamespace(xe.Name.Namespace);  
        if (xe.Name.Namespace == XNamespace.None || prefix == null)  
            return xe.Name.LocalName.ToString();  
        else  
            return prefix + ":" + xe.Name.LocalName.ToString();  
    }  
  
    private static string GetQName(XAttribute xa)  
    {  
        string prefix =  
            xa.Parent.GetPrefixOfNamespace(xa.Name.Namespace);  
        if (xa.Name.Namespace == XNamespace.None || prefix == null)  
            return xa.Name.ToString();  
        else  
            return prefix + ":" + xa.Name.LocalName;  
    }  
  
    private static string NameWithPredicate(XElement el)  
    {  
        if (el.Parent != null && el.Parent.Elements(el.Name).Count() != 1)  
            return GetQName(el) + "[" +  
                (el.ElementsBeforeSelf(el.Name).Count() + 1) + "]";  
        else  
            return GetQName(el);  
    }  
  
    public static string StrCat<T>(this IEnumerable<T> source,  
        string separator)  
    {  
        return source.Aggregate(new StringBuilder(),  
                   (sb, i) => sb  
                       .Append(i.ToString())  
                       .Append(separator),  
                   s => s.ToString());  
    }  
  
    public static string GetXPath(this XObject xobj)  
    {  
        if (xobj.Parent == null)  
        {  
            XDocument doc = xobj as XDocument;  
            if (doc != null)  
                return ".";  
            XElement el = xobj as XElement;  
            if (el != null)  
                return "/" + NameWithPredicate(el);  
            // the XPath data model does not include white space text nodes  
            // that are children of a document, so this method returns null.  
            XText xt = xobj as XText;  
            if (xt != null)  
                return null;  
            XComment com = xobj as XComment;  
            if (com != null)  
                return  
                    "/" +  
                    (  
                        com  
                        .Document  
                        .Nodes()  
                        .OfType<XComment>()  
                        .Count() != 1 ?  
                        "comment()[" +  
                        (com  
                        .NodesBeforeSelf()  
                        .OfType<XComment>()  
                        .Count() + 1) +  
                        "]" :  
                        "comment()"  
                    );  
            XProcessingInstruction pi = xobj as XProcessingInstruction;  
            if (pi != null)  
                return  
                    "/" +  
                    (  
                        pi.Document.Nodes()  
                        .OfType<XProcessingInstruction>()  
                        .Count() != 1 ?  
                        "processing-instruction()[" +  
                        (pi  
                        .NodesBeforeSelf()  
                        .OfType<XProcessingInstruction>()  
                        .Count() + 1) +  
                        "]" :  
                        "processing-instruction()"  
                    );  
            return null;  
        }  
        else  
        {  
            XElement el = xobj as XElement;  
            if (el != null)  
            {  
                return  
                    "/" +  
                    el  
                    .Ancestors()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    NameWithPredicate(el);  
            }  
            XAttribute at = xobj as XAttribute;  
            if (at != null)  
                return  
                    "/" +  
                    at  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    "@" + GetQName(at);  
            XComment com = xobj as XComment;  
            if (com != null)  
                return  
                    "/" +  
                    com  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        com  
                        .Parent  
                        .Nodes()  
                        .OfType<XComment>()  
                        .Count() != 1 ?  
                        "comment()[" +  
                        (com  
                        .NodesBeforeSelf()  
                        .OfType<XComment>()  
                        .Count() + 1) + "]" :  
                        "comment()"  
                    );  
            XCData cd = xobj as XCData;  
            if (cd != null)  
                return  
                    "/" +  
                    cd  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        cd  
                        .Parent  
                        .Nodes()  
                        .OfType<XText>()  
                        .Count() != 1 ?  
                        "text()[" +  
                        (cd  
                        .NodesBeforeSelf()  
                        .OfType<XText>()  
                        .Count() + 1) + "]" :  
                        "text()"  
                    );  
            XText tx = xobj as XText;  
            if (tx != null)  
                return  
                    "/" +  
                    tx  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        tx  
                        .Parent  
                        .Nodes()  
                        .OfType<XText>()  
                        .Count() != 1 ?  
                        "text()[" +  
                        (tx  
                        .NodesBeforeSelf()  
                        .OfType<XText>()  
                        .Count() + 1) + "]" :  
                        "text()"  
                    );  
            XProcessingInstruction pi = xobj as XProcessingInstruction;  
            if (pi != null)  
                return  
                    "/" +  
                    pi  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        pi  
                        .Parent  
                        .Nodes()  
                        .OfType<XProcessingInstruction>()  
                        .Count() != 1 ?  
                        "processing-instruction()[" +  
                        (pi  
                        .NodesBeforeSelf()  
                        .OfType<XProcessingInstruction>()  
                        .Count() + 1) + "]" :  
                        "processing-instruction()"  
                    );  
            return null;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        XNamespace aw = "http://www.adventure-works.com";  
        XDocument doc = new XDocument(  
            new XDeclaration("1.0", "utf-8", "yes"),  
            new XProcessingInstruction("target", "data"),  
            new XElement("Root",  
                new XAttribute("AttName", "An Attribute"),  
                new XAttribute(XNamespace.Xmlns + "aw", aw.ToString()),  
                new XComment("This is a comment"),  
                new XElement("Child",  
                    new XText("Text")  
                ),  
                new XElement("Child",  
                    new XText("Other Text")  
                ),  
                new XElement("ChildWithMixedContent",  
                    new XText("text"),  
                    new XElement("b", "BoldText"),  
                    new XText("otherText")  
                ),  
                new XElement(aw + "ElementInNamespace",  
                    new XElement(aw + "ChildInNamespace")  
                )  
            )  
        );  
        doc.Save("Test.xml");  
        Console.WriteLine(File.ReadAllText("Test.xml"));  
        Console.WriteLine("------");  
        foreach (XObject obj in doc.DescendantNodes())  
        {  
            Console.WriteLine(obj.GetXPath());  
            XElement el = obj as XElement;  
            if (el != null)  
                foreach (XAttribute at in el.Attributes())  
                    Console.WriteLine(at.GetXPath());  
        }  
    }  
}  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<?target data?>  
<Root AttName="An Attribute" xmlns:aw="http://www.adventure-works.com">  
  <!--This is a comment-->  
  <Child>Text</Child>  
  <Child>Other Text</Child>  
  <ChildWithMixedContent>text<b>BoldText</b>otherText</ChildWithMixedContent>  
  <aw:ElementInNamespace>  
    <aw:ChildInNamespace />  
  </aw:ElementInNamespace>  
</Root>  
------  
/processing-instruction()  
/Root  
/Root/@AttName  
/Root/@xmlns:aw  
/Root/comment()  
/Root/Child[1]  
/Root/Child[1]/text()  
/Root/Child[2]  
/Root/Child[2]/text()  
/Root/ChildWithMixedContent  
/Root/ChildWithMixedContent/text()[1]  
/Root/ChildWithMixedContent/b  
/Root/ChildWithMixedContent/b/text()  
/Root/ChildWithMixedContent/text()[2]  
/Root/aw:ElementInNamespace  
/Root/aw:ElementInNamespace/aw:ChildInNamespace  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tecniche di query avanzate (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
