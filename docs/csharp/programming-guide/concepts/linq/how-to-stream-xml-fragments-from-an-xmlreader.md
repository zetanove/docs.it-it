---
title: 'Procedura: Flusso di frammenti XML da un XmlReader (C#) | Documentazione Microsoft'
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
ms.assetid: 4a8f0e45-768a-42e2-bc5f-68bdf0e0a726
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 06e2cf4b350fecf8e8310519c573ac140f05267a
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-c"></a>Procedura: Flusso di frammenti XML da un XmlReader (C#)
Quando è necessario elaborare file XML di grandi dimensioni, potrebbe risultare impossibile caricare in memoria l'intero albero XML. In questo argomento viene illustrato come eseguire un flusso di frammenti usando un <xref:System.Xml.XmlReader>.  
  
 Uno dei modi più efficaci per usare un <xref:System.Xml.XmlReader> per leggere oggetti <xref:System.Xml.Linq.XElement> consiste nella scrittura del proprio metodo dell'asse personalizzato. Un metodo dell'asse restituisce in genere una raccolta, ad esempio <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XElement>, come illustrato nell'esempio di questo argomento. Nel metodo dell'asse personalizzato, dopo avere creato il frammento XML chiamando il metodo <xref:System.Xml.Linq.XNode.ReadFrom%2A>, restituire la raccolta usando `yield return`. In questo modo si fornisce la semantica di esecuzione posticipata al metodo dell'asse personalizzato.  
  
 Quando si crea un albero XML da un oggetto <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlReader> deve essere posizionato su un elemento. Il metodo <xref:System.Xml.Linq.XNode.ReadFrom%2A> non restituisce risultati fino a quando non ha letto il tag di chiusura dell'elemento.  
  
 Per creare un albero parziale, è possibile creare un'istanza di <xref:System.Xml.XmlReader>, posizionare il lettore sul nodo da convertire in un albero <xref:System.Xml.Linq.XElement> e quindi creare l'oggetto <xref:System.Xml.Linq.XElement>.  
  
 L'argomento [Procedura: Generare un flusso di frammenti XML con accesso a informazioni di intestazione (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-stream-xml-fragments-with-access-to-header-information.md) contiene informazioni e un esempio su come generare un flusso per un documento più complesso.  
  
 L'argomento [Procedura: Eseguire la trasformazione del flusso di documenti XML di grandi dimensioni (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-perform-streaming-transform-of-large-xml-documents.md) contiene un esempio dell'utilizzo di LINQ to XML per trasformare documenti XML di dimensioni estremamente grandi mantenendo un footprint di memoria ridotto.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene creato un metodo dell'asse personalizzato. È possibile sottoporlo a query tramite una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]. Il metodo dell'asse personalizzato `StreamRootChildDoc` è progettato specificamente per leggere un documento contenente un elemento `Child` ripetuto.  
  
```csharp  
static IEnumerable<XElement> StreamRootChildDoc(StringReader stringReader)  
{  
    using (XmlReader reader = XmlReader.Create(stringReader))  
    {  
        reader.MoveToContent();  
        // Parse the file and display each of the nodes.  
        while (reader.Read())  
        {  
            switch (reader.NodeType)  
            {  
                case XmlNodeType.Element:  
                    if (reader.Name == "Child") {  
                        XElement el = XElement.ReadFrom(reader) as XElement;  
                        if (el != null)  
                            yield return el;  
                    }  
                    break;  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    string markup = @"<Root>  
      <Child Key=""01"">  
        <GrandChild>aaa</GrandChild>  
      </Child>  
      <Child Key=""02"">  
        <GrandChild>bbb</GrandChild>  
      </Child>  
      <Child Key=""03"">  
        <GrandChild>ccc</GrandChild>  
      </Child>  
    </Root>";  
  
    IEnumerable<string> grandChildData =  
        from el in StreamRootChildDoc(new StringReader(markup))  
        where (int)el.Attribute("Key") > 1  
        select (string)el.Element("GrandChild");  
  
    foreach (string str in grandChildData) {  
        Console.WriteLine(str);  
    }  
}  
```  
  
 Questo esempio produce il seguente output:  
  
```  
bbb  
ccc  
```  
  
 In questo esempio il documento di origine è molto piccolo. Tuttavia, anche contenesse milioni di elementi `Child`, il footprint di memoria di questo esempio sarebbe comunque ridotto.  
  
## <a name="see-also"></a>Vedere anche  
 [Analisi di codice XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)
