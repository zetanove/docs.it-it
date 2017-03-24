---
title: 'Procedura: eseguire la convalida tramite XSD (LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: a0fe88d4-4e77-49e7-90de-8953feeccc21
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c6df61013b0007e5943060f8926b21d189a01519
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-validate-using-xsd-linq-to-xml-visual-basic"></a>Procedura: eseguire la convalida tramite XSD (LINQ to XML) (Visual Basic)
Il <xref:System.Xml.Schema>dello spazio dei nomi contiene metodi di estensione che semplificano la convalida di un albero XML rispetto a un file XML Schema Definition Language (XSD).</xref:System.Xml.Schema> Per ulteriori informazioni, vedere il <xref:System.Xml.Schema.Extensions.Validate%2A>documentazione relativa al metodo.</xref:System.Xml.Schema.Extensions.Validate%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un <xref:System.Xml.Schema.XmlSchemaSet>, quindi vengono convalidati due <xref:System.Xml.Linq.XDocument>oggetti rispetto allo schema.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Schema.XmlSchemaSet> Uno dei documenti è valido, l'altro non lo è.  
  
```vb  
Dim errors As Boolean = False  
  
Private Sub XSDErrors(ByVal o As Object, ByVal e As ValidationEventArgs)  
    Console.WriteLine("{0}", e.Message)  
    errors = True  
End Sub  
  
Sub Main()  
    Dim xsdMarkup As XElement = _  
        <xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'>  
            <xsd:element name='Root'>  
                <xsd:complexType>  
                    <xsd:sequence>  
                        <xsd:element name='Child1' minOccurs='1' maxOccurs='1'/>  
                        <xsd:element name='Child2' minOccurs='1' maxOccurs='1'/>  
                    </xsd:sequence>  
                </xsd:complexType>  
            </xsd:element>  
        </xsd:schema>  
    Dim schemas As XmlSchemaSet = New XmlSchemaSet()  
    schemas.Add("", xsdMarkup.CreateReader)  
  
    Dim doc1 As XDocument = _  
        <?xml version='1.0'?>  
        <Root>  
            <Child1>content1</Child1>  
            <Child2>content1</Child2>  
        </Root>  
  
    Dim doc2 As XDocument = _  
        <?xml version='1.0'?>  
        <Root>  
            <Child1>content1</Child1>  
            <Child3>content1</Child3>  
        </Root>  
  
    Console.WriteLine("Validating doc1")  
    errors = False  
    doc1.Validate(schemas, AddressOf XSDErrors)  
    Console.WriteLine("doc1 {0}", IIf(errors = True, "did not validate", "validated"))  
  
    Console.WriteLine()  
    Console.WriteLine("Validating doc2")  
    errors = False  
    doc2.Validate(schemas, AddressOf XSDErrors)  
    Console.WriteLine("doc2 {0}", IIf(errors = True, "did not validate", "validated"))  
End Sub  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Validating doc1  
doc1 validated  
  
Validating doc2  
The element 'Root' has invalid child element 'Child3'. List of possible elements expected: 'Child2'.  
doc2 did not validate  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente verifica che il documento XML da [File XML di esempio: Customers e Orders (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md) è valido per lo schema di [File XSD di esempio: Customers e Orders](../../../../visual-basic/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders.md). Viene quindi modificato il documento XML di origine. Viene cambiato l'attributo `CustomerID` sul primo cliente. Dopo la modifica, gli ordini faranno riferimento a un cliente che non esiste, quindi il documento XML non verrà più convalidato.  
  
 In questo esempio viene utilizzato il documento XML seguente: [File XML di esempio: Customers e Orders (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md).  
  
 Questo esempio viene utilizzato lo schema XSD seguente: [File XSD di esempio: Customers e Orders](../../../../visual-basic/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders.md).  
  
```vb  
Dim errors As Boolean = False  
  
Private Sub XSDErrors(ByVal o As Object, ByVal e As ValidationEventArgs)  
    Console.WriteLine("{0}", e.Message)  
    errors = True  
End Sub  
  
Sub Main()  
    Dim schemas As XmlSchemaSet = New XmlSchemaSet()  
    schemas.Add("", "CustomersOrders.xsd")  
  
    Console.WriteLine("Attempting to validate")  
    Dim custOrdDoc As XDocument = XDocument.Load("CustomersOrders.xml")  
    errors = False  
    custOrdDoc.Validate(schemas, AddressOf XSDErrors)  
    Console.WriteLine("custOrdDoc {0}", IIf(errors, "did not validate", "validated"))  
  
    Console.WriteLine()  
    ' Modify the source document so that it will not validate.  
    custOrdDoc.<Root>.<Orders>.<Order>.<CustomerID>(0).Value = "AAAAA"  
    Console.WriteLine("Attempting to validate after modification")  
    errors = False  
    custOrdDoc.Validate(schemas, AddressOf XSDErrors)  
    Console.WriteLine("custOrdDoc {0}", IIf(errors, "did not validate", "validated"))  
End Sub  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Attempting to validate  
custOrdDoc validated  
  
Attempting to validate after modification  
The key sequence 'AAAAA' in Keyref fails to refer to some key.  
custOrdDoc did not validate  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Schema.Extensions.Validate%2A></xref:System.Xml.Schema.Extensions.Validate%2A>   
 [Creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
