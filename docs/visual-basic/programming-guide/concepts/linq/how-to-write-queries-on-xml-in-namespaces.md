---
title: 'Procedura: scrivere query in XML negli spazi dei nomi (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 7d4131b5-3288-414f-b77c-b2edc2a1f465
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5af26b7ec0a2ab465917cd0ee62f65a97f5f0e40
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-write-queries-on-xml-in-namespaces-visual-basic"></a>Procedura: scrivere query in XML negli spazi dei nomi (Visual Basic)
Per scrivere una query su codice XML in uno spazio dei nomi, è necessario utilizzare <xref:System.Xml.Linq.XName>oggetti con lo spazio dei nomi corretto.</xref:System.Xml.Linq.XName>  
  
 In Visual Basic, l'approccio più comune consiste nel definire uno spazio dei nomi globale, quindi usare valori letterali e proprietà XML che usano lo spazio dei nomi globale. È possibile definire uno spazio dei nomi globale predefinito, nel qual caso gli elementi dei valori letterali XML saranno inclusi nello spazio dei nomi per impostazione predefinita. In alternativa, è possibile definire uno spazio dei nomi globale con un prefisso e quindi usare il prefisso come richiesto nei valori letterali e nelle proprietà XML. Come con altri tipi di XML, gli attributi non sono mai inclusi in alcuno spazio dei nomi per impostazione predefinita.  
  
 Il primo set di esempi in questo argomento viene illustrato come creare una struttura ad albero XML in uno spazio dei nomi predefinito. Il secondo set viene illustrato come creare una struttura ad albero XML in uno spazio dei nomi con un prefisso.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene creato un albero XML incluso in uno spazio dei nomi predefinito. Viene quindi recuperata una raccolta di elementi.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child>1</Child>  
                <Child>2</Child>  
                <Child>3</Child>  
                <AnotherChild>4</AnotherChild>  
                <AnotherChild>5</AnotherChild>  
                <AnotherChild>6</AnotherChild>  
            </Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(el.Value)  
        Next  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```  
1  
2  
3  
```  
  
## <a name="example"></a>Esempio  
 In Visual Basic, tuttavia, la scrittura di query in un albero XML che usa uno spazio dei nomi con un prefisso, è piuttosto diversa dall'esecuzione di query in un albero XML con uno spazio dei nomi predefinito. Lo spazio dei nomi con un prefisso viene in genere importato usando l'istruzione `Imports`. Il prefisso viene quindi usato nei nomi di elementi e attributi quando si crea l'albero XML. Il prefisso viene inoltre usato durante l'esecuzione di query su un albero XML tramite proprietà XML.  
  
 Nell'esempio seguente viene creata una struttura ad albero XML inclusa in uno spazio dei nomi con un prefisso. Viene quindi recuperata una raccolta di elementi.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child>1</aw:Child>  
                <aw:Child>2</aw:Child>  
                <aw:Child>3</aw:Child>  
                <aw:AnotherChild>4</aw:AnotherChild>  
                <aw:AnotherChild>5</aw:AnotherChild>  
                <aw:AnotherChild>6</aw:AnotherChild>  
            </aw:Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<aw:Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(CInt(el))  
        Next  
    End Sub  
End Module  
```  
  
 Questo esempio produce il seguente output:  
  
```  
1  
2  
3  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
