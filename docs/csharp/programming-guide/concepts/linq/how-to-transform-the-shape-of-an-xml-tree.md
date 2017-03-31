---
title: 'Procedura: trasformare la forma di una struttura ad albero XML (C#) | Documentazione Microsoft'
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
ms.assetid: 93c5d426-dea2-4709-a991-60204de42e8f
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8f11c77bc6273642bc4ffce3bf546c5a897729bc
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-transform-the-shape-of-an-xml-tree-c"></a>Procedura: trasformare la forma di una struttura ad albero XML (C#)
Per *forma* di un documento XML si intendono i relativi nomi di elemento, nomi di attributi, nonché le caratteristiche della relativa gerarchia.  
  
 In alcuni casi è necessario modificare la forma di un documento XML. Ad esempio, può essere necessario inviare un documento XML esistente a un altro sistema che richiede nomi di elemento e di attributo diversi. In tal caso, è possibile scorrere il documento, eliminando e rinominando gli elementi a seconda dei casi, tuttavia l'uso della costruzione funzionale consente di ottenere codice più leggibile e conservabile. Per altre informazioni sulla costruzione funzionale, vedere [Costruzione funzionale (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/functional-construction-linq-to-xml.md).  
  
 Nel primo esempio viene modificata l'organizzazione del documento XML. Gli elementi complessi vengono spostati da un punto all'altro dell'albero.  
  
 Nel secondo esempio di questo argomento viene creato un documento XML con una forma diversa rispetto al documento di origine. Viene modificato l'uso di maiuscole e minuscole nei nomi di elemento, alcuni elementi vengono rinominati e alcuni elementi dell'albero di origine vengono esclusi dall'albero trasformato.  
  
## <a name="example"></a>Esempio  
 Il codice seguente consente di modificare la forma di un file XML usando espressioni di query incorporate.  
  
 Il documento XML di origine di questo esempio include un elemento `Customers` sotto l'elemento `Root` che contiene tutti i clienti. Include inoltre un elemento `Orders` sotto l'elemento `Root` che contiene tutti gli ordini. In questo esempio viene creata un nuovo albero XML in cui gli ordini relativi a ciascun cliente sono contenuti in un elemento `Orders` all'interno dell'elemento `Customer`. Il documento originale include inoltre nell'elemento `CustomerID` un elemento `Order` che verrà rimosso dal documento modificato.  
  
 Questo esempio usa il documento XML seguente: [File XML di esempio: clienti e ordini (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
```csharp  
XElement co = XElement.Load("CustomersOrders.xml");  
XElement newCustOrd =  
    new XElement("Root",  
        from cust in co.Element("Customers").Elements("Customer")  
        select new XElement("Customer",  
            cust.Attributes(),  
            cust.Elements(),  
            new XElement("Orders",  
                from ord in co.Element("Orders").Elements("Order")  
                where (string)ord.Element("CustomerID") == (string)cust.Attribute("CustomerID")  
                select new XElement("Order",  
                    ord.Attributes(),  
                    ord.Element("EmployeeID"),  
                    ord.Element("OrderDate"),  
                    ord.Element("RequiredDate"),  
                    ord.Element("ShipInfo")  
                )  
            )  
        )  
    );  
Console.WriteLine(newCustOrd);  
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
  
 Il codice chiama `ConvertAddress`, che restituisce un elenco di oggetti <xref:System.Xml.Linq.XElement>. L'argomento del metodo è una query che determina l'elemento complesso `Address` in cui il valore dell'attributo `Type` è `"Shipping"`.  
  
 Questo esempio usa il documento XML seguente: [File XML di esempio: ordine di acquisto tipico (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml-1.md).  
  
```csharp  
static IEnumerable<XElement> ConvertAddress(XElement add)  
{  
    List<XElement> fragment = new List<XElement>() {  
        new XElement("NAME", (string)add.Element("Name")),  
        new XElement("STREET", (string)add.Element("Street")),  
        new XElement("CITY", (string)add.Element("City")),  
        new XElement("ST", (string)add.Element("State")),  
        new XElement("POSTALCODE", (string)add.Element("Zip")),  
        new XElement("COUNTRY", (string)add.Element("Country"))  
    };  
    return fragment;  
}  
  
static void Main(string[] args)  
{  
    XElement po = XElement.Load("PurchaseOrder.xml");  
    XElement newPo = new XElement("PO",  
        new XElement("ID", (string)po.Attribute("PurchaseOrderNumber")),  
        new XElement("DATE", (DateTime)po.Attribute("OrderDate")),  
        ConvertAddress(  
            (from el in po.Elements("Address")  
            where (string)el.Attribute("Type") == "Shipping"  
            select el)  
            .First()  
        )  
    );  
    Console.WriteLine(newPo);  
}  
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
 [Proiezioni e trasformazioni (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
