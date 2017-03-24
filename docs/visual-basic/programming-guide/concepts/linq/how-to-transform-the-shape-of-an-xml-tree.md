---
title: 'Procedura: trasformare la forma di una struttura ad albero XML (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 84b60854-48b2-452c-87f2-77d53e1d653a
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9c71f4af829a395204bc17161547aa5fdd06cbb1
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-transform-the-shape-of-an-xml-tree-visual-basic"></a>Procedura: trasformare la forma di una struttura ad albero XML (Visual Basic)
Il *forma* di un file XML documento si intende i relativi nomi di elemento, i nomi degli attributi e le caratteristiche della relativa gerarchia.  
  
 In alcuni casi è necessario modificare la forma di un documento XML. Ad esempio, può essere necessario inviare un documento XML esistente a un altro sistema che richiede nomi di elemento e di attributo diversi. In tal caso, è possibile scorrere il documento, eliminando e rinominando gli elementi a seconda dei casi, tuttavia l'uso della costruzione funzionale consente di ottenere codice più leggibile e conservabile. Per ulteriori informazioni sulla costruzione funzionale, vedere [costruzione funzionale (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-construction-linq-to-xml.md).  
  
 Nel primo esempio viene modificata l'organizzazione del documento XML. Gli elementi complessi vengono spostati da un punto all'altro dell'albero.  
  
 Nel secondo esempio di questo argomento viene creato un documento XML con una forma diversa rispetto al documento di origine. Viene modificato l'uso di maiuscole e minuscole nei nomi di elemento, alcuni elementi vengono rinominati e alcuni elementi dell'albero di origine vengono esclusi dall'albero trasformato.  
  
## <a name="example"></a>Esempio  
 Il codice seguente consente di modificare la forma di un file XML usando espressioni di query incorporate.  
  
 Il documento XML di origine di questo esempio include un elemento `Customers` sotto l'elemento `Root` che contiene tutti i clienti. Include inoltre un elemento `Orders` sotto l'elemento `Root` che contiene tutti gli ordini. In questo esempio viene creata un nuovo albero XML in cui gli ordini relativi a ciascun cliente sono contenuti in un elemento `Orders` all'interno dell'elemento `Customer`. Il documento originale include inoltre nell'elemento `CustomerID` un elemento `Order` che verrà rimosso dal documento modificato.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: Customers e Orders (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md).  
  
```vb  
Dim co As XElement = XElement.Load("CustomersOrders.xml")  
Dim newCustOrd = _  
    <Root>  
        <%= From cust In co.<Customers>.<Customer> _  
            Select _  
            <Customer>  
                <%= cust.Attributes() %>  
                <%= cust.Elements() %>  
                <Orders>  
                    <%= From ord In co.<Orders>.<Order> _  
                        Where ord.<CustomerID>.Value = cust.@CustomerID _  
                        Select _  
                        <Order>  
                            <%= ord.Attributes() %>  
                            <%= ord.<EmployeeID> %>  
                            <%= ord.<OrderDate> %>  
                            <%= ord.<RequiredDate> %>  
                            <%= ord.<ShipInfo> %>  
                        </Order> _  
                    %>  
                </Orders>  
            </Customer> _  
        %>  
    </Root>  
Console.WriteLine(newCustOrd)  
```  
  
 L'output del codice è il seguente:  
  
```xml  
  
        <Root>  
<Customer CustomerID="GREAL">  
  <CompanyName>Great Lakes Food Market</CompanyName>  
  <ContactName>Howard Snyder</ContactName>  
  <ContactTitle>Marketing Manager</ContactTitle>  
  <Phone>(503) 555-7555</Phone>  
  <FullAddress>  
    <Address>2732 Baker Blvd.</Address>  
    <City>Eugene</City>  
    <Region>OR</Region>  
    <PostalCode>97403</PostalCode>  
    <Country>USA</Country>  
  </FullAddress>  
  <Orders />  
</Customer>  
<Customer CustomerID="HUNGC">  
  <CompanyName>Hungry Coyote Import Store</CompanyName>  
  <ContactName>Yoshi Latimer</ContactName>  
  <ContactTitle>Sales Representative</ContactTitle>  
  <Phone>(503) 555-6874</Phone>  
  <Fax>(503) 555-2376</Fax>  
  <FullAddress>  
    <Address>City Center Plaza 516 Main St.</Address>  
    <City>Elgin</City>  
    <Region>OR</Region>  
    <PostalCode>97827</PostalCode>  
    <Country>USA</Country>  
  </FullAddress>  
  <Orders />  
</Customer>  
. . .  
```  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono rinominati alcuni elementi e convertiti alcuni attributi in elementi.  
  
 Il codice chiama `ConvertAddress`, che restituisce un elenco di <xref:System.Xml.Linq.XElement>oggetti.</xref:System.Xml.Linq.XElement> L'argomento del metodo è una query che determina l'elemento complesso `Address` in cui il valore dell'attributo `Type` è `"Shipping"`.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: tipico ordine di acquisto (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml.md).  
  
```vb  
Function ConvertAddress(ByVal add As XElement) As IEnumerable(Of XElement)  
    Dim fragment = New List(Of XElement)  
    fragment.Add(<NAME><%= add.<Name>.Value %></NAME>)  
    fragment.Add(<STREET><%= add.<Street>.Value %></STREET>)  
    fragment.Add(<CITY><%= add.<City>.Value %></CITY>)  
    fragment.Add(<ST><%= add.<State>.Value %></ST>)  
    fragment.Add(<POSTALCODE><%= add.<Zip>.Value %></POSTALCODE>)  
    fragment.Add(<COUNTRY><%= add.<Country>.Value %></COUNTRY>)  
    Return fragment  
End Function  
  
Sub Main()  
    Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
    Dim newPo As XElement = _  
        <PO>  
            <ID><%= po.@PurchaseOrderNumber %></ID>  
            <DATE><%= CDate(po.@OrderDate) %></DATE>  
            <%= _  
                ConvertAddress( _  
                (From el In po.<Address> _  
                Where el.@Type = "Shipping" _  
                Select el) _  
                .First() _  
                ) _  
            %>  
        </PO>  
    Console.WriteLine(newPo)  
End Sub  
  
```  
  
 L'output del codice è il seguente:  
  
```xml  
<PO>  
  <ID>99503</ID>  
  <DATE>1999-10-20T00:00:00</DATE>  
  <NAME>Ellen Adams</NAME>  
  <STREET>123 Maple Street</STREET>  
  <CITY>Mill Valley</CITY>  
  <ST>CA</ST>  
  <POSTALCODE>10999</POSTALCODE>  
  <COUNTRY>USA</COUNTRY>  
</PO>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Proiezioni e trasformazioni (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
