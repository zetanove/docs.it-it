---
title: Gestione di coppie nome-valore (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 57ac2072-d9f5-432b-84f0-a889c62fd813
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 54db297ecd39e37492dcf8bb4de4f64476662670
ms.lasthandoff: 03/13/2017


---
# <a name="maintaining-namevalue-pairs-visual-basic"></a>Gestione di coppie nome/valore (Visual Basic)
In molte applicazioni è necessario gestire informazioni che è preferibile mantenere come coppie nome/valore. Queste informazioni potrebbero essere di configurazione o impostazioni globali. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] include alcuni metodi che consentono di mantenere facilmente coppie nome/valore. È possibile mantenere le informazioni come attributi o come un set di elementi figlio.  
  
 Una differenza tra il mantenere le informazioni come attributi o come elementi figlio è che gli attributi prevedono un vincolo in base al quale per un elemento può esistere un unico attributo con un nome specifico. Questa limitazione non si applica invece agli elementi figlio.  
  
## <a name="setattributevalue-and-setelementvalue"></a>SetAttributeValue e SetElementValue  
 I due metodi che facilitano il mantenimento nome/valore sono coppie <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>e <xref:System.Xml.Linq.XElement.SetElementValue%2A>.</xref:System.Xml.Linq.XElement.SetElementValue%2A> </xref:System.Xml.Linq.XElement.SetAttributeValue%2A> Si tratta di metodi contraddistinti da una semantica simile.  
  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>può aggiungere, modificare o rimuovere gli attributi di un elemento.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   Se si chiama <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>con un nome di un attributo che non esiste, il metodo crea un nuovo attributo e lo aggiunge all'elemento specificato.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   Se si chiama <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>con un nome di un attributo esistente e specificato il contenuto, il contenuto dell'attributo viene sostituito con il contenuto specificato.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
-   Se si chiama <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>con un nome di un attributo e si specifica null per il contenuto, l'attributo viene rimosso dal relativo elemento padre.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
 <xref:System.Xml.Linq.XElement.SetElementValue%2A>può aggiungere, modificare o rimuovere gli elementi figlio di un elemento.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   Se si chiama <xref:System.Xml.Linq.XElement.SetElementValue%2A>con un nome di un elemento figlio che non esiste, il metodo crea un nuovo elemento e lo aggiunge all'elemento specificato.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   Se si chiama <xref:System.Xml.Linq.XElement.SetElementValue%2A>con un nome di un elemento esistente e specificato il contenuto, il contenuto dell'elemento viene sostituito con il contenuto specificato.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
-   Se si chiama <xref:System.Xml.Linq.XElement.SetElementValue%2A>con un nome di un elemento esistente e si specifica null per il contenuto, l'elemento viene rimosso dal relativo elemento padre.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un elemento senza attributi. Viene quindi utilizzato il <xref:System.Xml.Linq.XElement.SetAttributeValue%2A>per creare e gestire un elenco di coppie nome/valore.</xref:System.Xml.Linq.XElement.SetAttributeValue%2A>  
  
```vb  
' Create an element with no content.  
Dim root As XElement = <Root/>  
  
' Add a number of name/value pairs as attributes.  
root.SetAttributeValue("Top", 22)  
root.SetAttributeValue("Left", 20)  
root.SetAttributeValue("Bottom", 122)  
root.SetAttributeValue("Right", 300)  
root.SetAttributeValue("DefaultColor", "Color.Red")  
Console.WriteLine(root)  
  
' Replace the value of Top.  
root.SetAttributeValue("Top", 10)  
Console.WriteLine(root)  
  
' Remove DefaultColor.  
root.SetAttributeValue("DefaultColor", Nothing)  
Console.WriteLine(root)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<Root Top="22" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" DefaultColor="Color.Red" />  
<Root Top="10" Left="20" Bottom="122" Right="300" />  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un elemento senza elementi figlio. Viene quindi utilizzato il <xref:System.Xml.Linq.XElement.SetElementValue%2A>per creare e gestire un elenco di coppie nome/valore.</xref:System.Xml.Linq.XElement.SetElementValue%2A>  
  
```vb  
' Create an element with no content.  
Dim root As XElement = <Root/>  
  
' Add a number of name/value pairs as elements.  
root.SetElementValue("Top", 22)  
root.SetElementValue("Left", 20)  
root.SetElementValue("Bottom", 122)  
root.SetElementValue("Right", 300)  
root.SetElementValue("DefaultColor", "Color.Red")  
Console.WriteLine(root)  
Console.WriteLine("----")  
  
' Replace the value of Top.  
root.SetElementValue("Top", 10)  
Console.WriteLine(root)  
Console.WriteLine("----")  
  
' Remove DefaultColor.  
root.SetElementValue("DefaultColor", Nothing)  
Console.WriteLine(root)  
  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<Root>  
  <Top>22</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
  <DefaultColor>Color.Red</DefaultColor>  
</Root>  
----  
<Root>  
  <Top>10</Top>  
  <Left>20</Left>  
  <Bottom>122</Bottom>  
  <Right>300</Right>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement.SetAttributeValue%2A></xref:System.Xml.Linq.XElement.SetAttributeValue%2A>   
 <xref:System.Xml.Linq.XElement.SetElementValue%2A></xref:System.Xml.Linq.XElement.SetElementValue%2A>   
 [Modifica di strutture ad albero XML (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
