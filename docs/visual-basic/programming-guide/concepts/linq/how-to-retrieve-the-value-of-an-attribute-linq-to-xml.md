---
title: 'Procedura: recuperare il valore di un attributo (LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 5f4b3790-c83f-4eb3-a889-e3587edf3ca1
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a1661b1ea00eb7e377fc4d8a57ba27a558052b46
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-visual-basic"></a>Procedura: recuperare il valore di un attributo (LINQ to XML) (Visual Basic)
In questo argomento viene illustrato come ottenere il valore di attributi. Esistono due modi: È possibile eseguire il cast un <xref:System.Xml.Linq.XAttribute>al tipo desiderato; l'operatore di conversione esplicito converte quindi il contenuto dell'elemento o attributo al tipo specificato.</xref:System.Xml.Linq.XAttribute> In alternativa, è possibile utilizzare il <xref:System.Xml.Linq.XAttribute.Value%2A>proprietà.</xref:System.Xml.Linq.XAttribute.Value%2A> L'esecuzione del cast costituisce in genere l'approccio migliore. Se si esegue il cast dell'attributo a un tipo nullable, sarà più semplice scrivere il codice quando si recupera il valore di un attributo che potrebbe o meno esistere. Per esempi di questa tecnica, vedere [procedura: recuperare il valore di un elemento (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md).  
  
## <a name="example"></a>Esempio  
 In Visual Basic è possibile usare la proprietà integrata dell'attributo per recuperare il valore di un attributo.  
  
```vb  
Dim root As XElement = <Root Attr="abcde"/>  
Console.WriteLine(root)  
Dim str As String = root.@Attr  
Console.WriteLine(str)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>Esempio  
 In Visual Basic è possibile usare la proprietà integrata dell'attributo per impostare il valore di un attributo. Se inoltre si usa la proprietà integrata dell'attributo per impostare il valore di un attributo non esistente, l'attributo verrà creato.  
  
```vb  
Dim root As XElement = <Root Att1="content"/>  
root.@Att1 = "new content"  
root.@Att2 = "new attribute"  
Console.WriteLine(root)  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root Att1="new content" Att2="new attribute" />  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come recuperare il valore di un attributo quando l'attributo è in uno spazio dei nomi. Per ulteriori informazioni, vedere [utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root aw:Attr="abcde"/>  
        Dim str As String = root.@aw:Attr  
        Console.WriteLine(str)  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```  
abcde  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Assi LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
