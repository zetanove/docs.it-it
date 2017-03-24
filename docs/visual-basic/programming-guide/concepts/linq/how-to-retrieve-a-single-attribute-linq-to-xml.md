---
title: 'Procedura: recuperare un singolo attributo (LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 11b938d7-c011-4048-900e-8b9183c41c94
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 35f477ead2bdcfdf78781459f93a755dbc89e5cc
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml-visual-basic"></a>Procedura: recuperare un singolo attributo (LINQ to XML) (Visual Basic)
In questo argomento viene illustrato come recuperare un singolo attributo di un elemento, dato il relativo nome. Questa procedura è utile per la scrittura di espressioni di query in cui si desidera trovare un elemento con un attributo specifico.  
  
 Il <xref:System.Xml.Linq.XElement.Attribute%2A>metodo la <xref:System.Xml.Linq.XElement>classe restituisce il <xref:System.Xml.Linq.XAttribute>con il nome specificato.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement.Attribute%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzato il <xref:System.Xml.Linq.XElement.Attribute%2A>(metodo).</xref:System.Xml.Linq.XElement.Attribute%2A>  
  
```vb  
Dim cust As XElement = <PhoneNumbers>  
                           <Phone type="home">555-555-5555</Phone>  
                           <Phone type="work">555-555-6666</Phone>  
                       </PhoneNumbers>  
Dim elList = From el In cust...<Phone>  
For Each e As XElement In elList  
    Console.WriteLine(e.@type)  
Next  
```  
  
 In questo esempio vengono individuati tutti i discendenti dell'albero denominato `Phone` e quindi l'attributo denominato `type`.  
  
 L'output del codice è il seguente:  
  
```  
home  
work  
```  
  
## <a name="example"></a>Esempio  
 Se si desidera recuperare il valore dell'attributo, è possibile eseguirne il cast, come nel caso degli <xref:System.Xml.Linq.XElement>oggetti.</xref:System.Xml.Linq.XElement> Nell'esempio che segue viene illustrato quanto descritto.  
  
```vb  
Dim cust As XElement = <PhoneNumbers>  
                           <Phone type="home">555-555-5555</Phone>  
                           <Phone type="work">555-555-6666</Phone>  
                       </PhoneNumbers>  
Dim elList As IEnumerable(Of XElement) = _  
    From el In cust...<Phone> _  
    Select el  
For Each el As XElement In elList  
    Console.WriteLine(el.@type)  
Next  
```  
  
 L'output del codice è il seguente:  
  
```  
home  
work  
```  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]provides explicit cast operators for the <xref:System.Xml.Linq.XAttribute> class to `string`, `bool`, `bool?`, `int`, `int?`, `uint`, `uint?`, `long`, `long?`, `ulong`, `ulong?`, `float`, `float?`, `double`, `double?`, `decimal`, `decimal?`, `DateTime`, `DateTime?`, `TimeSpan`, `TimeSpan?`, `GUID`, and `GUID?`.</xref:System.Xml.Linq.XAttribute>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato lo stesso codice per un attributo all'interno di uno spazio dei nomi. Per ulteriori informazioni, vedere [utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim cust As XElement = _  
            <aw:PhoneNumbers>  
                <aw:Phone aw:type="home">555-555-5555</aw:Phone>  
                <aw:Phone aw:type="work">555-555-6666</aw:Phone>  
            </aw:PhoneNumbers>  
        Dim elList As IEnumerable(Of XElement) = _  
            From el In cust...<aw:Phone> _  
            Select el  
        For Each el As XElement In elList  
            Console.WriteLine(el.@aw:type)  
        Next  
    End Sub  
End Module  
```  
  
 L'output del codice è il seguente:  
  
```  
home  
work  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Assi LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
