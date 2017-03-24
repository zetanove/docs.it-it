---
title: 'Procedura: trovare elementi in un Namespace (XPath-LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: c7cb3b77-3424-4b54-9efa-4dc715948e41
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d665ddc1e7ad7340b05c97e790195abbc53e4f95
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-find-elements-in-a-namespace-xpath-linq-to-xml-visual-basic"></a>Procedura: trovare elementi in un Namespace (XPath-LINQ to XML) (Visual Basic)
Le espressioni XPath consentono di trovare nodi in un determinato spazio dei nomi. Per specificare gli spazi dei nomi, nelle espressioni XPath si usano prefissi di spazio dei nomi. Per analizzare un'espressione XPath che contiene i prefissi dello spazio dei nomi, è necessario passare un oggetto ai metodi XPath che implementa <xref:System.Xml.IXmlNamespaceResolver>.</xref:System.Xml.IXmlNamespaceResolver> Questo esempio viene utilizzato <xref:System.Xml.XmlNamespaceManager>.</xref:System.Xml.XmlNamespaceManager>  
  
 L'espressione XPath è:  
  
 `./aw:*`  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene letto un albero XML contenente due spazi dei nomi. Viene utilizzato un <xref:System.Xml.XmlReader>per leggere il documento XML.</xref:System.Xml.XmlReader> Ottiene quindi un <xref:System.Xml.XmlNameTable>dal <xref:System.Xml.XmlReader>e un <xref:System.Xml.XmlNamespaceManager>da <xref:System.Xml.XmlNameTable>.</xref:System.Xml.XmlNameTable> </xref:System.Xml.XmlNamespaceManager> </xref:System.Xml.XmlReader> </xref:System.Xml.XmlNameTable> Usa il <xref:System.Xml.XmlNamespaceManager>quando si selezionano elementi.</xref:System.Xml.XmlNamespaceManager>  
  
```vb  
Dim reader As XmlReader = _  
        XmlReader.Create("ConsolidatedPurchaseOrders.xml")  
Dim root As XElement = XElement.Load(reader)  
Dim nameTable As XmlNameTable = reader.NameTable  
Dim namespaceManager As XmlNamespaceManager = New XmlNamespaceManager(nameTable)  
namespaceManager.AddNamespace("aw", "http://www.adventure-works.com")  
  
Dim list1 As IEnumerable(Of XElement) = _  
        root.XPathSelectElements("./aw:*", namespaceManager)  
Dim list2 As IEnumerable(Of XElement) = _  
    From el In root.Elements() _  
    Where el.Name.Namespace = "http://www.adventure-works.com" _  
    Select el  
  
If list1.Count() = list2.Count() And _  
        list1.Intersect(list2).Count() = list1.Count() Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
For Each el As XElement In list2  
    Console.WriteLine(el)  
Next  
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
 [LINQ to XML per gli utenti di XPath (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
