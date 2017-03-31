---
title: 'Procedura: Trovare elementi figlio in base alla posizione (XPath-LINQ to XML) (C#) | Microsoft Docs'
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
ms.assetid: e35bb269-ec86-4c96-8321-12491a0eb2c3
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ce711d5e0ce82d4fcb0351c21ac7a769c414b2a4
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-find-child-elements-based-on-position-xpath-linq-to-xml-c"></a>Procedura: Trovare elementi figlio in base alla posizione (XPath-LINQ to XML) (C#)
Talvolta si desidera individuare elementi in base alla posizione, ad esempio il secondo elemento oppure dal terzo al quinto elemento.  
  
 L'espressione XPath è:  
  
 `Test[position() >= 2 and position() <= 4]`  
  
 Sono disponibili due approcci per la scrittura di query [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] in modalità lazy. È possibile usare gli operatori <xref:System.Linq.Enumerable.Skip%2A> e <xref:System.Linq.Enumerable.Take%2A> oppure è possibile usare l'overload di <xref:System.Linq.Enumerable.Where%2A> che accetta un indice. Quando si usa l'overload di <xref:System.Linq.Enumerable.Where%2A>, viene usata un'espressione lambda che accetta due argomenti. Nell'esempio seguente sono illustrati entrambi i metodi di selezione basata sulla posizione.  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono individuati gli elementi `Test` compresi tra il secondo e il quarto. Il risultato è una raccolta di elementi.  
  
 Questo esempio usa il documento XML seguente: [File XML di esempio: configurazione di test (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-test-configuration-linq-to-xml.md).  
  
```csharp  
XElement testCfg = XElement.Load("TestConfig.xml");  
  
// LINQ to XML query  
IEnumerable<XElement> list1 =  
    testCfg  
    .Elements("Test")  
    .Skip(1)  
    .Take(3);  
  
// LINQ to XML query  
IEnumerable<XElement> list2 =  
    testCfg  
    .Elements("Test")  
    .Where((el, idx) => idx >= 1 && idx <= 3);  
  
// XPath expression  
IEnumerable<XElement> list3 =  
  testCfg.XPathSelectElements("Test[position() >= 2 and position() <= 4]");  
  
if (list1.Count() == list2.Count() &&  
    list1.Count() == list3.Count() &&  
    list1.Intersect(list2).Count() == list1.Count() &&  
    list1.Intersect(list3).Count() == list1.Count())  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Results are identical  
<Test TestId="0002" TestType="CMD">  
  <Name>Find succeeding characters</Name>  
  <CommandLine>Examp2.EXE</CommandLine>  
  <Input>abc</Input>  
  <Output>def</Output>  
</Test>  
<Test TestId="0003" TestType="GUI">  
  <Name>Convert multiple numbers to strings</Name>  
  <CommandLine>Examp2.EXE /Verbose</CommandLine>  
  <Input>123</Input>  
  <Output>One Two Three</Output>  
</Test>  
<Test TestId="0004" TestType="GUI">  
  <Name>Find correlated key</Name>  
  <CommandLine>Examp3.EXE</CommandLine>  
  <Input>a1</Input>  
  <Output>b1</Output>  
</Test>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML per gli utenti di XPath (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
