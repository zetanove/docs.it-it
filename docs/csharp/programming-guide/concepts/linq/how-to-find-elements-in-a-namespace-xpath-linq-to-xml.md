---
title: 'Procedura: Trovare elementi in uno spazio dei nomi (XPath-LINQ to XML) (C#) | Microsoft Docs'
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
ms.assetid: cae1c4ac-6cd5-46cf-9b1c-bd85bc9b7ea9
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dc1b201a807b8e5c060720018195fe3639e748dc
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-find-elements-in-a-namespace-xpath-linq-to-xml-c"></a>Procedura: Trovare elementi in uno spazio dei nomi (XPath-LINQ to XML) (C#)
Le espressioni XPath consentono di trovare nodi in un determinato spazio dei nomi. Per specificare gli spazi dei nomi, nelle espressioni XPath si usano prefissi di spazio dei nomi. Per analizzare un'espressione XPath che contiene prefissi di spazio dei nomi, è necessario passare ai metodi XPath un oggetto che implementi <xref:System.Xml.IXmlNamespaceResolver>. Questo esempio usa <xref:System.Xml.XmlNamespaceManager>.  
  
 L'espressione XPath è:  
  
 `./aw:*`  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene letto un albero XML contenente due spazi dei nomi. Per leggere il documento XML viene usato <xref:System.Xml.XmlReader>. Si ottiene quindi <xref:System.Xml.XmlNameTable> da <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlNamespaceManager> da <xref:System.Xml.XmlNameTable>. Per selezionare gli elementi viene usato <xref:System.Xml.XmlNamespaceManager>.  
  
```csharp  
XmlReader reader = XmlReader.Create("ConsolidatedPurchaseOrders.xml");  
XElement root = XElement.Load(reader);  
XmlNameTable nameTable = reader.NameTable;  
XmlNamespaceManager namespaceManager = new XmlNamespaceManager(nameTable);  
namespaceManager.AddNamespace("aw", "http://www.adventure-works.com");  
IEnumerable<XElement> list1 = root.XPathSelectElements("./aw:*", namespaceManager);  
IEnumerable<XElement> list2 =  
    from el in root.Elements()  
    where el.Name.Namespace == "http://www.adventure-works.com"  
    select el;  
if (list1.Count() == list2.Count() &&  
        list1.Intersect(list2).Count() == list1.Count())  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
foreach (XElement el in list2)  
    Console.WriteLine(el);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Results are identical  
<aw:PurchaseOrder PONumber="11223" Date="2000-01-15" xmlns:aw="http://www.adventure-works.com">  
    <aw:ShippingAddress>  
      <aw:Name>Chris Preston</aw:Name>  
      <aw:Street>123 Main St.</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98113</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:ShippingAddress>  
    <aw:BillingAddress>  
      <aw:Name>Chris Preston</aw:Name>  
      <aw:Street>123 Main St.</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98113</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:BillingAddress>  
    <aw:DeliveryInstructions>Ship only complete order.</aw:DeliveryInstructions>  
    <aw:Item PartNum="LIT-01">  
      <aw:ProductID>Litware Networking Card</aw:ProductID>  
      <aw:Qty>1</aw:Qty>  
      <aw:Price>20.99</aw:Price>  
    </aw:Item>  
    <aw:Item PartNum="LIT-25">  
      <aw:ProductID>Litware 17in LCD Monitor</aw:ProductID>  
      <aw:Qty>1</aw:Qty>  
      <aw:Price>199.99</aw:Price>  
    </aw:Item>  
  </aw:PurchaseOrder>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML per gli utenti di XPath (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
