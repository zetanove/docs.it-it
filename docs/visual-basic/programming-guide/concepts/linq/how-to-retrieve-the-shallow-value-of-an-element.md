---
title: 'Procedura: recuperare il valore superficiale di un elemento (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 730a6670-fb8c-41fc-8a1b-eb97a837e432
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 39a0648bb3fd09b9e323560b447be3cc445d5b7f
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-the-shallow-value-of-an-element-visual-basic"></a>Procedura: recuperare il valore superficiale di un elemento (Visual Basic)
In questo argomento viene illustrato come ottenere il valore superficiale di un elemento. Per valore superficiale si intende un valore che appartiene solo all'elemento specifico, a differenza del valore completo che include i valori di tutti gli elementi discendenti concatenati in una singola stringa.  
  
 Quando si recupera un valore dell'elemento tramite il cast o la <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName>proprietà, si recupera il valore completo.</xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName> Per recuperare il valore superficiale, è possibile usare il metodo di estensione `ShallowValue`, come illustrato nell'esempio seguente. Il recupero del valore superficiale risulta utile quando si desidera selezionare gli elementi in base al relativo contenuto.  
  
 Nell'esempio seguente viene dichiarato un metodo di estensione che recupera il valore superficiale di un elemento. Questo metodo di estensione viene quindi usato in una query per elencare tutti gli elementi che contengono un valore calcolato.  
  
## <a name="example"></a>Esempio  
 Il file di testo seguente, Report.xml, è l'origine di questo esempio.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Report>  
  <Section>  
    <Heading>  
      <Column Name="CustomerId">=Customer.CustomerId.Heading</Column>  
      <Column Name="Name">=Customer.Name.Heading</Column>  
    </Heading>  
    <Detail>  
      <Column Name="CustomerId">=Customer.CustomerId</Column>  
      <Column Name="Name">=Customer.Name</Column>  
    </Detail>  
  </Section>  
</Report>  
```  
  
```vb  
Module Module1  
    <System.Runtime.CompilerServices.Extension()> _  
    Public Function ShallowValue(ByVal xe As XElement)  
        Return xe _  
               .Nodes() _  
               .OfType(Of XText)() _  
               .Aggregate(New StringBuilder(), _  
                              Function(s, c) s.Append(c), _  
                              Function(s) s.ToString())  
    End Function  
  
    Sub Main()  
        Dim root As XElement = XElement.Load("Report.xml")  
  
        Dim query As IEnumerable(Of XElement) = _  
            From el In root.Descendants() _  
            Where (el.ShallowValue().StartsWith("=")) _  
            Select el  
  
        For Each q As XElement In query  
            Console.WriteLine("{0}{1}{2}", _  
                q.Name.ToString().PadRight(8), _  
                q.Attribute("Name").ToString().PadRight(20), _  
                q.ShallowValue())  
        Next  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Column  Name="CustomerId"   =Customer.CustomerId.Heading  
Column  Name="Name"         =Customer.Name.Heading  
Column  Name="CustomerId"   =Customer.CustomerId  
Column  Name="Name"         =Customer.Name  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Assi LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
