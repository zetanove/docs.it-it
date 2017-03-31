---
title: 'Procedura: Trovare discendenti di un elemento figlio (XPath-LINQ to XML) (C#) | Microsoft Docs'
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
ms.assetid: 505b7512-bb8b-4f85-abbf-491f039c961e
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 29fdf6976c3f35c35f6cd70b1b4fadc056b2d64d
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-find-descendants-of-a-child-element-xpath-linq-to-xml-c"></a>Procedura: Trovare discendenti di un elemento figlio (XPath-LINQ to XML) (C#)
In questo argomento viene illustrato come ottenere gli elementi discendenti di un elemento figlio con un determinato nome.  
  
 L'espressione XPath è:  
  
 `./Paragraph//Text/text()`  
  
## <a name="example"></a>Esempio  
 In questo esempio sono simulati i problemi di estrazione di testo da una rappresentazione XML di un documento di elaborazione testi. Vengono dapprima selezionati tutti gli elementi `Paragraph` e quindi tutti gli elementi discendenti `Text` di ogni elemento `Paragraph`. Gli elementi discendenti `Text` dell'elemento `Comment` non vengono selezionati.  
  
```csharp  
XElement root = XElement.Parse(  
@"<Root>  
  <Paragraph>  
    <Text>This is the start of</Text>  
  </Paragraph>  
  <Comment>  
    <Text>This comment is not part of the paragraph text.</Text>  
  </Comment>  
  <Paragraph>  
    <Annotation Emphasis='true'>  
      <Text> a sentence.</Text>  
    </Annotation>  
  </Paragraph>  
  <Paragraph>  
    <Text>  This is a second sentence.</Text>  
  </Paragraph>  
</Root>");  
  
// LINQ to XML query  
string str1 =  
    root  
    .Elements("Paragraph")  
    .Descendants("Text")  
    .Select(s => s.Value)  
    .Aggregate(  
        new StringBuilder(),  
        (s, i) => s.Append(i),  
        s => s.ToString()  
    );  
  
// XPath expression  
string str2 =  
    ((IEnumerable)root.XPathEvaluate("./Paragraph//Text/text()"))  
    .Cast<XText>()  
    .Select(s => s.Value)  
    .Aggregate(  
        new StringBuilder(),  
        (s, i) => s.Append(i),  
        s => s.ToString()  
    );  
  
if (str1 == str2)  
    Console.WriteLine("Results are identical");  
else  
    Console.WriteLine("Results differ");  
Console.WriteLine(str2);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Results are identical  
This is the start of a sentence.  This is a second sentence.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to XML per gli utenti di XPath (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
