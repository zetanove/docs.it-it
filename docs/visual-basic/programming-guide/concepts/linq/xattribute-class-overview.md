---
title: Cenni preliminari sulla classe XAttribute (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 7781580a-9583-4a1b-ae1e-91c5936eb0b1
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1ce5f4be6006908b35057854f89432471fd9f06b
ms.lasthandoff: 03/13/2017

---
# <a name="xattribute-class-overview-visual-basic"></a>Cenni preliminari sulla classe XAttribute (Visual Basic)
Gli attributi sono coppie nome/valore associate a un elemento. La <xref:System.Xml.Linq.XAttribute>classe rappresenta gli attributi XML.</xref:System.Xml.Linq.XAttribute>  
  
## <a name="overview"></a>Panoramica  
 Le modalità di utilizzo degli attributi in [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] sono simili a quelle degli elementi. I relativi costruttori sono simili. I metodi usati per recuperare le relative raccolte sono simili. Oggetto [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] espressione di query per una raccolta di attributi sembra molto simile a un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] espressione per una raccolta di elementi di query.  
  
 L'ordine con cui gli attributi vengono aggiunti a un elemento viene mantenuto. Quando si scorrono gli attributi, questi vengono visualizzati nell'ordine in cui sono stati aggiunti.  
  
## <a name="the-xattribute-constructor"></a>Costruttore XAttribute  
 Il seguente costruttore della <xref:System.Xml.Linq.XAttribute>classe è quello che verrà utilizzato più comunemente:</xref:System.Xml.Linq.XAttribute>  
  
|Costruttore|Descrizione|  
|-----------------|-----------------|  
|`XAttribute(XName name, object content)`|Crea un <xref:System.Xml.Linq.XAttribute>oggetto.</xref:System.Xml.Linq.XAttribute> L'argomento `name` specifica il nome dell'attributo, mentre `content` ne specifica il contenuto.|  
  
### <a name="creating-an-element-with-an-attribute"></a>Creazione di un elemento con un attributo  
 Il codice seguente viene illustrato un elemento che contiene un attributo mediante valori letterali XML in Visual Basic:  
  
```vb  
Dim phone As XElement = <Phone Type="Home">555-555-5555</Phone>  
Console.WriteLine(phone)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Phone Type="Home">555-555-5555</Phone>  
```  
  
### <a name="functional-construction-of-attributes"></a>Costruzione funzionale di attributi  
 È possibile costruire <xref:System.Xml.Linq.XAttribute>in linea con la costruzione di oggetti <xref:System.Xml.Linq.XElement>oggetti, come indicato di seguito:</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XAttribute>  
  
```vb  
Dim c As XElement = _  
    <Customers>  
        <Customer>  
            <Name>John Doe</Name>  
            <PhoneNumbers>  
                <Phone type="home">555-555-5555</Phone>  
                <Phone type="work">666-666-6666</Phone>  
            </PhoneNumbers>  
        </Customer>  
    </Customers>  
Console.WriteLine(c)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Customers>  
  <Customer>  
    <Name>John Doe</Name>  
    <PhoneNumbers>  
      <Phone type="home">555-555-5555</Phone>  
      <Phone type="work">666-666-6666</Phone>  
    </PhoneNumbers>  
  </Customer>  
</Customers>  
```  
  
### <a name="attributes-are-not-nodes"></a>Attributi non nodi  
 Esistono alcune differenze tra attributi ed elementi. <xref:System.Xml.Linq.XAttribute>oggetti non sono nodi nella struttura ad albero XML.</xref:System.Xml.Linq.XAttribute> ma sono coppie nome/valore associate a un elemento XML. A differenza del modello DOM (Document Object Model), questa definizione rispecchia maggiormente la struttura del codice XML. Sebbene <xref:System.Xml.Linq.XAttribute>oggetti non siano effettivamente nodi dell'albero XML, utilizzo <xref:System.Xml.Linq.XAttribute>è molto simile all'utilizzo di oggetti <xref:System.Xml.Linq.XElement>oggetti.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XAttribute>  
  
 Questa distinzione è di fondamentale importanza solo per gli sviluppatori che scrivono codice che riguarda gli alberi XML a livello di nodo. Non interessa quindi la maggior parte degli sviluppatori.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Cenni preliminari sulla programmazione XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
