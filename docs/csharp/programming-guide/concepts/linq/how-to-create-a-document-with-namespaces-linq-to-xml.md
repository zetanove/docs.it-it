---
title: 'Procedura: Creare un documento con spazi dei nomi (C#) (LINQ to XML) | Microsoft Docs'
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
ms.assetid: 37e63c57-f86d-47ac-88a7-2c2d107def30
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 23cc762b1dcd5e39b923c1a57b6f171c7885f0ad
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-document-with-namespaces-c-linq-to-xml"></a>Procedura: creare un documento con spazi dei nomi (C#) (LINQ to XML)
In questo argomento viene illustrato come creare documenti con spazi dei nomi.  
  
## <a name="example"></a>Esempio  
 Per creare un elemento o un attributo in uno spazio dei nomi, è prima necessario dichiarare e inizializzare un oggetto <xref:System.Xml.Linq.XNamespace>. È quindi possibile usare l'overload dell'operatore di addizione per combinare lo spazio dei nomi con il nome locale, espresso come stringa.  
  
 Nell'esempio seguente viene creato un documento con un solo spazio dei nomi. Per impostazione predefinita, in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] questo documento viene serializzato con uno spazio dei nomi predefinito.  
  
```csharp  
// Create an XML tree in a namespace.  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
    new XElement(aw + "Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child>child content</Child>  
</Root>  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un documento con un solo spazio dei nomi. nonché un attributo che dichiara lo spazio dei nomi con un prefisso. Per creare un attributo che dichiara uno spazio dei nomi con un prefisso, è possibile creare un attributo il cui nome sia il prefisso dello spazio dei nomi e si trovi nello spazio dei nomi <xref:System.Xml.Linq.XNamespace.Xmlns%2A>. Il valore di questo attributo è l'URI dello spazio dei nomi.  
  
```csharp  
// Create an XML tree in a namespace, with a specified prefix  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XElement(aw + "Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child>child content</aw:Child>  
</aw:Root>  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è illustrata la creazione di un documento che contiene due spazi dei nomi. Uno è lo spazio dei nomi predefinito, mentre l'altro è uno spazio dei nomi con prefisso.  
  
 Includendo gli attributi dello spazio dei nomi nell'elemento radice, gli spazi dei nomi vengono serializzati in modo che http://www.adventure-works.com corrisponda allo spazio dei nomi predefinito e www.fourthcoffee.com venga serializzato con il prefisso "fc". Per creare un attributo che dichiara uno spazio dei nomi predefinito, viene creato un attributo denominato "xmlns" e senza spazio dei nomi. Il valore dell'attributo è l'URI dello spazio dei nomi predefinito.  
  
```csharp  
// The http://www.adventure-works.com namespace is forced to be the default namespace.  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute("xmlns", "http://www.adventure-works.com"),  
    new XAttribute(XNamespace.Xmlns + "fc", "www.fourthcoffee.com"),  
    new XElement(fc + "Child",  
        new XElement(aw + "DifferentChild", "other content")  
    ),  
    new XElement(aw + "Child2", "c2 content"),  
    new XElement(fc + "Child3", "c3 content")  
);  
Console.WriteLine(root);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root xmlns="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <DifferentChild>other content</DifferentChild>  
  </fc:Child>  
  <Child2>c2 content</Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</Root>  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un documento contenente due spazi dei nomi, entrambi con prefisso.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", aw.NamespaceName),  
    new XAttribute(XNamespace.Xmlns + "fc", fc.NamespaceName),  
    new XElement(fc + "Child",  
        new XElement(aw + "DifferentChild", "other content")  
    ),  
    new XElement(aw + "Child2", "c2 content"),  
    new XElement(fc + "Child3", "c3 content")  
);  
Console.WriteLine(root);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="example"></a>Esempio  
 È possibile ottenere lo stesso risultato anche usando nomi espansi anziché dichiarando e creando un oggetto <xref:System.Xml.Linq.XNamespace>.  
  
 Questo approccio può tuttavia incidere sulle prestazioni. Ogni volta che si passa una stringa che contiene un nome espanso a [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] deve analizzare il nome, individuare lo spazio dei nomi atomicizzato e individuare il nome atomicizzato. Questo processo impiega il tempo della CPU. Se le prestazioni sono importanti, è necessario dichiarare e usare un oggetto <xref:System.Xml.Linq.XNamespace> in modo esplicito.  
  
 Se le prestazioni rappresentano un problema rilevante, per altre informazioni vedere [Pre-atomizzazione di oggetti XName (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/pre-atomization-of-xname-objects-linq-to-xml.md).  
  
```csharp  
// Create an XML tree in a namespace, with a specified prefix  
XElement root = new XElement("{http://www.adventure-works.com}Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XElement("{http://www.adventure-works.com}Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child>child content</aw:Child>  
</aw:Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso degli spazi dei nomi XML (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)
