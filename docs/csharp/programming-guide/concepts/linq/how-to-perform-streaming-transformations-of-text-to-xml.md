---
title: 'Procedura: Eseguire trasformazioni del flusso di testo in XML (C#) | Microsoft Docs'
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
ms.assetid: 9b3bd941-d0ff-4f2d-ae41-7c3b81d8fae6
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bba371063439dfe5698ab6c3342500eec9fdc015
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-perform-streaming-transformations-of-text-to-xml-c"></a>Procedura: Eseguire trasformazioni del flusso di testo in XML (C#)
Uno degli approcci disponibili per l'elaborazione di un file di testo consiste nello scrivere un metodo di estensione che genera un flusso del file di testo, una riga alla volta, tramite il costrutto `yield return`. È quindi possibile scrivere una query LINQ che elabora il file di testo in modo posticipato lazy. Se poi si usa <xref:System.Xml.Linq.XStreamingElement> per il flusso di output, è possibile creare una trasformazione del file di testo in XML che usi una quantità minima di memoria, indipendentemente dalle dimensioni del file di testo di origine.  
  
 È necessario tener conto di alcune considerazioni in relazione alle trasformazioni di flusso. Le trasformazioni di flusso sono ideali nelle situazioni in cui è possibile elaborare l'intero file una sola volta e se è possibile elaborare le righe nell'ordine in cui sono riportate nel documento di origine. Se è necessario elaborare il file più volte o ordinare le righe prima che sia possibile elaborarle, si perderanno molti dei vantaggi associati all'utilizzo di una tecnica di flusso.  
  
## <a name="example"></a>Esempio  
 Il file di testo seguente, People.txt, è l'origine di questo esempio.  
  
```  
#This is a comment  
1,Tai,Yee,Writer  
2,Nikolay,Grachev,Programmer  
3,David,Wright,Inventor  
```  
  
 Nel codice seguente è contenuto un metodo di estensione che genera il flusso delle righe del file di testo in modo posticipato.  
  
```csharp  
public static class StreamReaderSequence  
{  
    public static IEnumerable<string> Lines(this StreamReader source)  
    {  
        String line;  
  
        if (source == null)  
            throw new ArgumentNullException("source");  
        while ((line = source.ReadLine()) != null)  
        {  
            yield return line;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        StreamReader sr = new StreamReader("People.txt");  
        XStreamingElement xmlTree = new XStreamingElement("Root",  
            from line in sr.Lines()  
            let items = line.Split(',')  
            where !line.StartsWith("#")  
            select new XElement("Person",  
                       new XAttribute("ID", items[0]),  
                       new XElement("First", items[1]),  
                       new XElement("Last", items[2]),  
                       new XElement("Occupation", items[3])  
                   )  
        );  
        Console.WriteLine(xmlTree);  
        sr.Close();  
    }  
}  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Root>  
  <Person ID="1">  
    <First>Tai</First>  
    <Last>Yee</Last>  
    <Occupation>Writer</Occupation>  
  </Person>  
  <Person ID="2">  
    <First>Nikolay</First>  
    <Last>Grachev</Last>  
    <Occupation>Programmer</Occupation>  
  </Person>  
  <Person ID="3">  
    <First>David</First>  
    <Last>Wright</Last>  
    <Occupation>Inventor</Occupation>  
  </Person>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XStreamingElement>   
 [Tecniche di query avanzate (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
