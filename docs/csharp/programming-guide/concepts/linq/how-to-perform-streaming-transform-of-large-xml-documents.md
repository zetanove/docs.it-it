---
title: 'Procedura: Eseguire la trasformazione del flusso di documenti XML di grandi dimensioni (C#) | Microsoft Docs'
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
ms.assetid: 5f16d1f8-5370-4b55-b0c8-e497df163037
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 02919c2e1e76991a3b37533da57b5c3ce4ded3c6
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-perform-streaming-transform-of-large-xml-documents-c"></a>Procedura: Eseguire la trasformazione del flusso di documenti XML di grandi dimensioni (C#)
A volte è necessario trasformare file XML di grandi dimensioni e scrivere l'applicazione in modo tale che il footprint di memoria dell'applicazione sia prevedibile. Se si tenta di popolare un albero XML con un file XML molto grande, l'uso della memoria sarà proporzionale alla dimensione del file (ovvero, eccessivo). Pertanto, è necessario usare una tecnica di flusso in sostituzione.  
  
 Le tecniche di flusso sono maggiormente indicate nelle situazioni in cui è necessario elaborare solo una volta il documento di origine ed è possibile elaborare gli elementi in base all'ordine in cui sono riportati nel documento. Alcuni operatori di query standard, come ad esempio <xref:System.Linq.Enumerable.OrderBy%2A>, eseguono l'iterazione dell'origine, raccolgono tutti i dati, li ordinano e infine restituiscono il primo elemento della sequenza. Si noti che se si usa un operatore di query che materializza l'origine prima di restituire il primo elemento, non verrà mantenuto un footprint di memoria ridotto per l'applicazione.  
  
 Anche se viene usata la tecnica descritta in [Procedura: Generare un flusso di frammenti XML con accesso a informazioni di intestazione (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md), se si tenta di assemblare un albero XML che contiene il documento trasformato, l'uso della memoria sarà eccessivo.  
  
 Sono disponibili due approcci principali: il primo consiste nell'usare le caratteristiche di elaborazione posticipata di <xref:System.Xml.Linq.XStreamingElement>. Un altro approccio consiste nel creare un oggetto <xref:System.Xml.XmlWriter> e usare le funzionalità di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per scrivere elementi in <xref:System.Xml.XmlWriter>. In questo argomento vengono descritti entrambi gli approcci.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente si basa sull'esempio in [Procedura: Generare un flusso di frammenti XML con accesso a informazioni di intestazione (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md).  
  
 In questo esempio vengono usate le funzionalità di esecuzione posticipata di <xref:System.Xml.Linq.XStreamingElement> per generare il flusso di output. È possibile trasformare un documento di dimensioni molto grandi mantenendo un footprint di memoria ridotto.  
  
 Si noti che il metodo dell'asse personalizzato (`StreamCustomerItem`) è stato scritto in modo tale da prevedere un documento contenente elementi `Customer`, `Name` e `Item`, disposti come nel documento Source.xml seguente. Tuttavia, un'implementazione più solida sarebbe in grado di analizzare un documento non valido.  
  
 Il documento seguente, Source.xml, è il documento di origine:  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>   
<Root>  
  <Customer>  
    <Name>A. Datum Corporation</Name>  
    <Item>  
      <Key>0001</Key>  
    </Item>  
    <Item>  
      <Key>0002</Key>  
    </Item>  
    <Item>  
      <Key>0003</Key>  
    </Item>  
    <Item>  
      <Key>0004</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Fabrikam, Inc.</Name>  
    <Item>  
      <Key>0005</Key>  
    </Item>  
    <Item>  
      <Key>0006</Key>  
    </Item>  
    <Item>  
      <Key>0007</Key>  
    </Item>  
    <Item>  
      <Key>0008</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Southridge Video</Name>  
    <Item>  
      <Key>0009</Key>  
    </Item>  
    <Item>  
      <Key>0010</Key>  
    </Item>  
  </Customer>  
</Root>  
```  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null)  
                        {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    XStreamingElement root = new XStreamingElement("Root",  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        )  
    );  
    root.Save("Test.xml");  
    Console.WriteLine(File.ReadAllText("Test.xml"));  
}  
```  
  
 L'output del codice è il seguente:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  
## <a name="example"></a>Esempio  
 L'esempio seguente si basa sull'esempio in [Procedura: Generare un flusso di frammenti XML con accesso a informazioni di intestazione (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md).  
  
 In questo esempio viene usata la funzionalità di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] per scrivere elementi in <xref:System.Xml.XmlWriter>. È possibile trasformare un documento di dimensioni molto grandi mantenendo un footprint di memoria ridotto.  
  
 Si noti che il metodo dell'asse personalizzato (`StreamCustomerItem`) è stato scritto in modo tale da prevedere un documento contenente elementi `Customer`, `Name` e `Item`, disposti come nel documento Source.xml seguente. Tuttavia, un'implementazione più affidabile convaliderebbe il documento di origine con uno schema XSD oppure verrebbe preparata per analizzare un documento non valido.  
  
 In questo esempio viene usato lo stesso documento di origine, Source.xml, dell'esempio precedente in questo argomento. Viene inoltre prodotto esattamente lo stesso output.  
  
 È preferibile usare <xref:System.Xml.Linq.XStreamingElement> per il flusso di XML di output, piuttosto che scrivere un oggetto <xref:System.Xml.XmlWriter>.  
  
```csharp  
static IEnumerable<XElement> StreamCustomerItem(string uri)  
{  
    using (XmlReader reader = XmlReader.Create(uri))  
    {  
        XElement name = null;  
        XElement item = null;  
  
        reader.MoveToContent();  
  
        // Parse the file, save header information when encountered, and yield the  
        // Item XElement objects as they are created.  
  
        // loop through Customer elements  
        while (reader.Read())  
        {  
            if (reader.NodeType == XmlNodeType.Element  
                && reader.Name == "Customer")  
            {  
                // move to Name element  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.Element &&  
                        reader.Name == "Name")  
                    {  
                        name = XElement.ReadFrom(reader) as XElement;  
                        break;  
                    }  
                }  
  
                // loop through Item elements  
                while (reader.Read())  
                {  
                    if (reader.NodeType == XmlNodeType.EndElement)  
                        break;  
                    if (reader.NodeType == XmlNodeType.Element  
                        && reader.Name == "Item")  
                    {  
                        item = XElement.ReadFrom(reader) as XElement;  
                        if (item != null) {  
                            XElement tempRoot = new XElement("Root",  
                                new XElement(name)  
                            );  
                            tempRoot.Add(item);  
                            yield return item;  
                        }  
                    }  
                }  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    IEnumerable<XElement> srcTree =  
        from el in StreamCustomerItem("Source.xml")  
        select new XElement("Item",  
            new XElement("Customer", (string)el.Parent.Element("Name")),  
            new XElement(el.Element("Key"))  
        );  
    XmlWriterSettings xws = new XmlWriterSettings();  
    xws.OmitXmlDeclaration = true;  
    xws.Indent = true;  
    using (XmlWriter xw = XmlWriter.Create("Output.xml", xws)) {  
        xw.WriteStartElement("Root");  
        foreach (XElement el in srcTree)  
            el.WriteTo(xw);  
        xw.WriteEndElement();  
    }  
  
    string str = File.ReadAllText("Output.xml");  
    Console.WriteLine(str);  
}  
```  
  
 L'output del codice è il seguente:  
  
```xml  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0001</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0002</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0008</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0009</Key>  
  </Item>  
  <Item>  
    <Customer>Southridge Video</Customer>  
    <Key>0010</Key>  
  </Item>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione LINQ to XML avanzata (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
