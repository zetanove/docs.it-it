---
title: 'Procedura: unire due raccolte (LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 5a5758d4-906b-4285-908d-5b930db192e6
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 169a2ca7fb7fdc7b4cccdaab6547c6bb1a66072c
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-join-two-collections-linq-to-xml-visual-basic"></a>Procedura: unire due raccolte (LINQ to XML) (Visual Basic)
Un elemento o un attributo di un documento XML può talvolta fare riferimento a un altro elemento o attributo. Ad esempio, il [File XML di esempio: Customers e Orders (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md) documento XML contiene un elenco di clienti e un elenco di ordini. Ogni elemento `Customer` contiene un attributo `CustomerID`. Ogni elemento `Order` contiene un elemento `CustomerID`. L'elemento `CustomerID` di ciascun ordine si riferisce all'attributo `CustomerID` di un cliente.  
  
 L'argomento [File XSD di esempio: Customers e Orders](../../../../visual-basic/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders.md) contiene uno schema XSD che può essere utilizzato per convalidare il documento. Lo schema usa le funzionalità `xs:key` e `xs:keyref` di XSD per stabilire che l'attributo `CustomerID` dell'elemento `Customer` è una chiave e per stabilire una relazione tra l'elemento `CustomerID` in ogni elemento `Order` e l'attributo `CustomerID` in ogni elemento `Customer`.  
  
 Con [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile sfruttare questa relazione usando la clausola `Join`.  
  
 Notare che, poiché non è disponibile nessun indice, una tale operazione di join sarà caratterizzata da prestazioni ridotte in fase di esecuzione.  
  
 Per ulteriori informazioni su `Join`, vedere [operazioni Join (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/join-operations.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente gli elementi `Customer` vengono uniti agli elementi `Order` tramite join e viene generato un nuovo documento XML che include l'elemento `CompanyName` negli ordini.  
  
 Prima di eseguire la query, l'esempio verifica che il documento sia conforme con lo schema in [File XSD di esempio: Customers e Orders](../../../../visual-basic/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders.md). Tale convalida assicura la corretta esecuzione della clausola di join.  
  
 La query recupera prima tutti gli elementi `Customer` e quindi li unisce agli elementi `Order` tramite join. Vengono selezionati solo gli ordini relativi ai clienti il cui valore di `CustomerID` è maggiore di "K". Viene quindi proiettato un nuovo elemento `Order` che contiene le informazioni del cliente all'interno di ciascun ordine.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: Customers e Orders (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md).  
  
 Questo esempio viene utilizzato lo schema XSD seguente: [File XSD di esempio: Customers e Orders](../../../../visual-basic/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders.md).  
  
 Notare che le unioni tramite join eseguite in questo modo comportano problemi. I join vengono eseguiti tramite una ricerca lineare, pertanto l'assenza di tabelle hash o indici influisce negativamente sulle prestazioni.  
  
```vb  
Public Class Program  
    Public Shared errors As Boolean = False  
  
    Public Shared Function LamValidEvent(ByVal o As Object, _  
                 ByVal e As ValidationEventArgs) As Boolean  
        Console.WriteLine("{0}", e.Message)  
        errors = True  
    End Function  
  
    Shared Sub Main()  
        Dim schemas As New XmlSchemaSet()  
        schemas.Add("", "CustomersOrders.xsd")  
  
        Console.Write("Attempting to validate, ")  
        Dim custOrdDoc As XDocument = XDocument.Load("CustomersOrders.xml")  
  
        custOrdDoc.Validate(schemas, Function(o, e) LamValidEvent(0, e))  
        If errors Then  
            Console.WriteLine("custOrdDoc did not validate")  
        Else  
            Console.WriteLine("custOrdDoc validated")  
        End If  
  
        If Not errors Then  
            'Join customers and orders, and create a new XML document with  
            ' a different shape.  
            'The new document contains orders only for customers with a  
            ' CustomerID > 'K'.  
            Dim custOrd As XElement = custOrdDoc.<Root>.FirstOrDefault  
            Dim newCustOrd As XElement = _  
                <Root>  
                    <%= From c In custOrd.<Customers>.<Customer> _  
                        Join o In custOrd.<Orders>.<Order> _  
                        On c.@CustomerID Equals o.<CustomerID>.Value _  
                        Where c.@CustomerID.CompareTo("K") > 0 _  
                        Select _  
                        <Order>  
                            <CustomerID><%= c.@CustomerID %></CustomerID>  
                            <%= c.<CompanyName> %>  
                            <%= c.<ContactName> %>  
                            <%= o.<EmployeeID> %>  
                            <%= o.<OrderDate> %>  
                        </Order> _  
                    %>  
                </Root>  
            Console.WriteLine(newCustOrd)  
        End If  
    End Sub  
End Class  
```  
  
 L'output del codice è il seguente:  
  
```  
Attempting to validate, custOrdDoc validated  
<Root>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-03-21T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-05-22T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-06-25T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-10-27T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>6</EmployeeID>  
    <OrderDate>1997-11-10T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>4</EmployeeID>  
    <OrderDate>1998-02-12T00:00:00</OrderDate>  
  </Order>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tecniche di Query (LINQ to XML) avanzate (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
