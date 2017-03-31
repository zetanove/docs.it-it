---
title: 'Procedura: Controllare i prefissi dello spazio dei nomi (C#) (LINQ to XML) | Microsoft Docs'
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
ms.assetid: 64de5186-b81a-4ddd-8327-8693df59a01b
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
ms.openlocfilehash: 96bc6d1187aa72f8653cd01b2027306009634fd5
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-control-namespace-prefixes-c-linq-to-xml"></a>Procedura: controllare i prefissi dello spazio dei nomi (C#) (LINQ to XML)
In questo argomento viene descritto come controllare i prefissi degli spazi dei nomi durante la serializzazione di un albero XML.  
  
 In molte situazioni non è necessario controllare i prefissi degli spazi dei nomi.  
  
 Tuttavia, determinati strumenti di programmazione XML richiedono il controllo specifico dei prefissi degli spazi dei nomi. Ad esempio, si potrebbe stare modificando un foglio di stile XSLT o un documento XAML contenente espressioni XPath incorporate che fanno riferimento a prefissi di spazi dei nomi specifici; in questo caso è importante che il documento sia serializzato con tali prefissi specifici.  
  
 Ciò rappresenta il motivo più comune per il controllo dei prefissi degli spazi dei nomi.  
  
 Il controllo dei prefissi degli spazi dei nomi viene richiesto anche quando si desidera che gli utenti modifichino manualmente il documento XML e si desidera creare prefissi che l'utente può digitare con maggior comodità. Ad esempio, se si intende generare un documento XSD, le convenzioni degli schemi consigliano l'uso di `xs` o `xsd` come prefisso per lo spazio dei nomi dello schema.  
  
 Per controllare i prefissi degli spazi dei nomi, si inseriscono attributi che dichiarano gli spazi dei nomi. Se si dichiarano gli spazi dei nomi con prefissi specifici, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] tenterà di rispettare tali prefissi durante la serializzazione.  
  
 Per creare un attributo che dichiara uno spazio dei nomi con un prefisso, viene creato un attributo in cui lo spazio dei nomi del nome dell'attributo è <xref:System.Xml.Linq.XNamespace.Xmlns%2A> e il nome dell'attributo è il prefisso dello spazio dei nomi. Il valore dell'attributo è l'URI dello spazio dei nomi.  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono dichiarati due spazi dei nomi. Viene specificato che lo spazio dei nomi `http://www.adventure-works.com` ha il prefisso `aw` e lo spazio dei nomi `www.fourthcoffee.com` ha il prefisso `fc`.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
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
<aw:Root xmlns:aw="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Uso degli spazi dei nomi XML (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)
