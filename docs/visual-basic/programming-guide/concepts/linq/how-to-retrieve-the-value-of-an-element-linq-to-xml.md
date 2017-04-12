---
title: 'Procedura: recuperare il valore di un elemento (LINQ to XML) (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 76b9b2a5-b3ba-49da-ba74-82100e1bd21c
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d38928df51006a8db9417d34ccbe6cd03091db66
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-the-value-of-an-element-linq-to-xml-visual-basic"></a>Procedura: recuperare il valore di un elemento (LINQ to XML) (Visual Basic)
In questo argomento viene illustrato come ottenere il valore degli elementi. Questa operazione può essere eseguita in due modi. È possibile eseguire il cast un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XAttribute>al tipo desiderato.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> L'operatore di conversione esplicito converte quindi il contenuto dell'elemento o dell'attributo nel tipo specificato e lo assegna alla variabile. In alternativa, è possibile utilizzare il <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName>proprietà o <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>proprietà.</xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName> </xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName>  
  
 Con Visual Basic, l'approccio migliore consiste nell'utilizzare il <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName>proprietà.</xref:System.Xml.Linq.XElement.Value%2A?displayProperty=fullName>  
  
## <a name="example"></a>Esempio  
 Per recuperare il valore di un elemento, sufficiente eseguire il cast di <xref:System.Xml.Linq.XElement>oggetto al tipo desiderato.</xref:System.Xml.Linq.XElement> È sempre possibile eseguire il cast di un elemento in una stringa, come segue:  
  
```vb  
Dim e As XElement = <StringElement>abcde</StringElement>  
Console.WriteLine(e)  
Console.WriteLine("Value of e:" & e.Value)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="example"></a>Esempio  
 È anche possibile eseguire il cast di elementi in tipi diversi da stringa. Ad esempio, se un elemento contiene un Integer, è possibile eseguirne il cast in `int`, come illustrato nel codice seguente:  
  
```vb  
Dim e As XElement = <Age>44</Age>  
Console.WriteLine(e)  
Console.WriteLine("Value of e:" & CInt(e))  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<Age>44</Age>  
Value of e:44  
```  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]provides explicit cast operators for the following data types: `string`, `bool`, `bool?`, `int`, `int?`, `uint`, `uint?`, `long`, `long?`, `ulong`, `ulong?`, `float`, `float?`, `double`, `double?`, `decimal`, `decimal?`, `DateTime`, `DateTime?`, `TimeSpan`, `TimeSpan?`, `GUID`, and `GUID?`.  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]fornisce gli stessi operatori di cast per <xref:System.Xml.Linq.XAttribute>oggetti.</xref:System.Xml.Linq.XAttribute>  
  
## <a name="example"></a>Esempio  
 È possibile utilizzare il <xref:System.Xml.Linq.XElement.Value%2A>proprietà per recuperare il contenuto di un elemento:</xref:System.Xml.Linq.XElement.Value%2A>  
  
```vb  
Dim e As XElement = <StringElement>abcde</StringElement>  
Console.WriteLine(e)  
Console.WriteLine("Value of e:" & e.Value)  
```  
  
 Questo esempio produce il seguente output:  
  
```  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="example"></a>Esempio  
 A volte, si tenta di recuperare il valore di un elemento anche se non si è certi che esista. In questo caso, quando si assegna l'elemento sottoposto a cast a un tipo nullable (sia `string` o uno dei tipi nullable di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]), se l'elemento non esiste l'oggetto assegnato variabile viene semplicemente impostata su `Nothing`. Il codice seguente viene dimostrato che quando l'elemento potrebbe o non esistere, è preferibile eseguire il cast anziché usare la <xref:System.Xml.Linq.XElement.Value%2A>proprietà.</xref:System.Xml.Linq.XElement.Value%2A>  
  
```vb  
Dim root As XElement = <Root>  
                           <Child1>child 1 content</Child1>  
                           <Child2>2</Child2>  
                       </Root>  
  
' The following assignments show why it is easier to use  
' casting when the element might or might not exist.  
  
Dim c1 As String = CStr(root.Element("Child1"))  
Console.WriteLine("c1:{0}", IIf(c1 Is Nothing, "element does not exist", c1))  
  
Dim c2 As Nullable(Of Integer) = CType(root.Element("Child2"), Nullable(Of Integer))  
Console.WriteLine("c2:{0}", IIf(Not (c2.HasValue), "element does not exist", c2.ToString()))  
  
Dim c3 As String = CStr(root.Element("Child3"))  
Console.WriteLine("c3:{0}", IIf(c3 Is Nothing, "element does not exist", c3))  
  
Dim c4 As Nullable(Of Integer) = CType(root.Element("Child4"), Nullable(Of Integer))  
Console.WriteLine("c4:{0}", IIf(Not (c4.HasValue), "element does not exist", c4.ToString()))  
  
Console.WriteLine()  
  
' The following assignments show the required code when using  
' the Value property when the attribute might or might not exist.  
' Notice that this is more difficult than the casting approach.  
  
Dim e1 As XElement = root.Element("Child1")  
Dim v1 As String  
If (e1 Is Nothing) Then  
    v1 = Nothing  
Else  
    v1 = e1.Value  
End If  
Console.WriteLine("v1:{0}", IIf(v1 Is Nothing, "element does not exist", v1))  
  
Dim e2 As XElement = root.Element("Child2")  
Dim v2 As Nullable(Of Integer)  
If (e2 Is Nothing) Then  
    v2 = Nothing  
Else  
    v2 = e2.Value  
End If  
Console.WriteLine("v2:{0}", IIf(Not (v2.HasValue), "element does not exist", v2))  
  
Dim e3 As XElement = root.Element("Child3")  
Dim v3 As String  
If (e3 Is Nothing) Then  
    v3 = Nothing  
Else  
    v3 = e3.Value  
End If  
Console.WriteLine("v3:{0}", IIf(v3 Is Nothing, "element does not exist", v3))  
  
Dim e4 As XElement = root.Element("Child4")  
Dim v4 As Nullable(Of Integer)  
If (e4 Is Nothing) Then  
    v4 = Nothing  
Else  
    v4 = e4.Value  
End If  
Console.WriteLine("v4:{0}", IIf(Not (v4.HasValue), "element does not exist", v4))  
```  
  
 L'output del codice è il seguente:  
  
```  
c1:child 1 content  
c2:2  
c3:element does not exist  
c4:element does not exist  
  
v1:child 1 content  
v2:2  
v3:element does not exist  
v4:element does not exist  
```  
  
 In generale, è possibile scrivere codice più semplice quando si usa il cast per recuperare il contenuto di elementi e attributi.  
  
## <a name="see-also"></a>Vedere anche  
 [Assi LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
