---
title: Pre-atomizzazione di oggetti XName (LINQ to XML) (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 06ea104b-f44c-4bb2-9c34-889ae025c80d
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 519b64a96e03e098d7325cfb779bcd5d53db3741
ms.lasthandoff: 03/13/2017


---
# <a name="pre-atomization-of-xname-objects-linq-to-xml-visual-basic"></a>Pre-atomizzazione di oggetti XName (LINQ to XML) (Visual Basic)
Per migliorare le prestazioni in LINQ to XML, è possibile pre-atomizzare <xref:System.Xml.Linq.XName>oggetti.</xref:System.Xml.Linq.XName> Pre-atomizzazione significa che si assegna una stringa di un <xref:System.Xml.Linq.XName>dell'oggetto prima di creare la struttura ad albero XML usando i costruttori del <xref:System.Xml.Linq.XElement>e <xref:System.Xml.Linq.XAttribute>classi.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XName> Quindi, anziché passare una stringa al costruttore, che utilizzerebbe la conversione implicita da stringa a <xref:System.Xml.Linq.XName>, si passa l'inizializzato <xref:System.Xml.Linq.XName>oggetto.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XName>  
  
 Questa operazione consente di migliorare le prestazioni quando si crea un albero XML di grandi dimensioni in cui sono ripetuti nomi specifici. A tale scopo, è necessario dichiarare e inizializzare <xref:System.Xml.Linq.XName>oggetti prima di costruire la struttura ad albero XML, quindi utilizzare il <xref:System.Xml.Linq.XName>oggetti anziché specificare le stringhe per i nomi di elementi e attributi.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XName> Questa tecnica può consentire un miglioramento significativo delle prestazioni se si crea un numero elevato di elementi (o attributi) con lo stesso nome.  
  
 Se si decide di usare la pre-atomizzazione, è prima necessario testarla nel proprio scenario.  
  
## <a name="example"></a>Esempio  
 Nell'esempio che segue viene illustrato quanto descritto.  
  
```vb  
Dim Root__1 As XName = "Root"  
Dim Data As XName = "Data"  
Dim ID As XName = "ID"  
  
Dim root__2 As New XElement(Root__1, New XElement(Data, New XAttribute(ID, "1"), "4,100,000"), New XElement(Data, New XAttribute(ID, "2"), "3,700,000"), New XElement(Data, New XAttribute(ID, "3"), "1,150,000"))  
  
Console.WriteLine(root__2)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <Data ID="1">4,100,000</Data>  
  <Data ID="2">3,700,000</Data>  
  <Data ID="3">1,150,000</Data>  
</Root>  
```  
  
 Nell'esempio seguente è illustrata la stessa tecnica per un documento XML in uno spazio dei nomi:  
  
```vb  
Dim aw As XNamespace = "http://www.adventure-works.com"  
Dim Root__1 As XName = aw + "Root"  
Dim Data As XName = aw + "Data"  
Dim ID As XName = "ID"  
  
Dim root__2 As New XElement(Root__1, New XAttribute(XNamespace.Xmlns + "aw", aw), New XElement(Data, New XAttribute(ID, "1"), "4,100,000"), New XElement(Data, New XAttribute(ID, "2"), "3,700,000"), New XElement(Data, New XAttribute(ID, "3"), "1,150,000"))  
  
Console.WriteLine(root__2)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Data ID="1">4,100,000</aw:Data>  
  <aw:Data ID="2">3,700,000</aw:Data>  
  <aw:Data ID="3">1,150,000</aw:Data>  
</aw:Root>  
```  
  
 L'esempio seguente è più simile a quello che potrebbe verificarsi in un caso reale. In questo esempio il contenuto dell'elemento viene fornito da una query:  
  
```vb  
Dim Root__1 As XName = "Root"  
Dim Data As XName = "Data"  
Dim ID As XName = "ID"  
  
Dim t1 As DateTime = DateTime.Now  
Dim root__2 As New XElement(Root__1, From i In System.Linq.Enumerable.Range(1, 100000)New XElement(Data, New XAttribute(ID, i), i * 5))  
Dim t2 As DateTime = DateTime.Now  
  
Console.WriteLine("Time to construct:{0}", t2 - t1)  
```  
  
 L'esempio precedente offre prestazioni migliori rispetto all'esempio seguente, in cui i nomi non sono pre-atomizzati:  
  
```vb  
Dim t1 As DateTime = DateTime.Now  
Dim root As New XElement("Root", From i In System.Linq.Enumerable.Range(1, 100000)New XElement("Data", New XAttribute("ID", i), i * 5))  
Dim t2 As DateTime = DateTime.Now  
  
Console.WriteLine("Time to construct:{0}", t2 - t1)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Prestazioni (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)   
 [Scomporre oggetti XName e XNamespace (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/atomized-xname-and-xnamespace-objects-linq-to-xml.md)
