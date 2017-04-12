---
title: Ambito degli spazi dei nomi predefinito in Visual Basic | Documenti di Microsoft
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
ms.assetid: d4cce80c-342f-4097-be8b-40ab0bfa90ba
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c0152250cf7cfb4b6cadbcaab60eaad8ec2fb5ee
ms.lasthandoff: 03/13/2017


---
# <a name="scope-of-default-namespaces-in-visual-basic"></a>Ambito degli spazi dei nomi predefinito in Visual Basic
Gli spazi dei nomi rappresentati nell'albero XML non sono inclusi nell'ambito delle query. Se si dispone di codice XML in uno spazio dei nomi predefinito, è comunque necessario dichiarare un <xref:System.Xml.Linq.XNamespace>variabile e combinarla con il nome locale per creare un nome completo da utilizzare nella query.</xref:System.Xml.Linq.XNamespace>  
  
 Uno dei problemi più comuni che viene riscontrato durante l'esecuzione di query su alberi XML è che, se l'albero XML include uno spazio dei nomi predefinito, lo sviluppatore scrive talvolta la query come se il codice XML non fosse incluso in uno spazio dei nomi.  
  
 Nel primo set di esempi riportati in questo argomento viene illustrato il tipico caricamento del codice XML in uno spazio dei nomi predefinito e l'esecuzione errata di query su tale codice.  
  
 Nel secondo set di esempi sono illustrate le correzioni necessarie da effettuare per poter eseguire query su codice XML in uno spazio dei nomi.  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono illustrate la creazione di codice XML in uno spazio dei nomi e una query che restituisce un set di risultati vuoto.  
  
### <a name="code"></a>Codice  
  
```vb  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root xmlns='http://www.adventure-works.com'>  
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
        Console.WriteLine("Result set follows:")  
        For Each el As XElement In c1  
            Console.WriteLine(CInt(el))  
        Next  
        Console.WriteLine("End of result set")  
    End Sub  
End Module  
```  
  
### <a name="comments"></a>Commenti  
 Il risultato ottenuto dall'esempio è il seguente:  
  
```  
Result set follows:  
End of result set  
```  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono illustrate la creazione di codice XML in uno spazio dei nomi e una query codificata correttamente.  
  
 Contrariamente all'esempio di codice errato precedente, l'approccio corretto quando si utilizza Visual Basic consiste nel dichiarare e inizializzare uno spazio dei nomi globale predefinito. In questo modo tutte le proprietà XML vengono inserite nello spazio dei nomi predefinito. Non è necessario apportare altre modifiche all'esempio per fare in modo che venga eseguito correttamente.  
  
### <a name="code"></a>Codice  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root xmlns='http://www.adventure-works.com'>  
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
        Console.WriteLine("Result set follows:")  
        For Each el As XElement In c1  
            Console.WriteLine(el.Value)  
        Next  
        Console.WriteLine("End of result set")  
    End Sub  
End Module  
```  
  
### <a name="comments"></a>Commenti  
 Il risultato ottenuto dall'esempio è il seguente:  
  
```  
Result set follows:  
1  
2  
3  
End of result set  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
