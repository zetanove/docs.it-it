---
title: Creazione di alberi XML in C# (LINQ to XML) | Microsoft Docs
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
ms.assetid: cc74234a-0bac-4327-9c8c-5a2ead15b595
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
ms.openlocfilehash: 92ba0d345183ec503d61254355f948f82a18f053
ms.lasthandoff: 03/13/2017

---
# <a name="creating-xml-trees-in-c-linq-to-xml"></a>Creazione di alberi in C# (LINQ to XML)
In questa sezione vengono fornite informazioni sulla creazione di alberi XML in C#.  
  
 Per informazioni sull'uso dei risultati delle query LINQ come contenuto per un oggetto <xref:System.Xml.Linq.XElement>, vedere [Costruzione funzionale (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/functional-construction-linq-to-xml.md).  
  
## <a name="constructing-elements"></a>Costruzione di elementi  
 Le firme dei costruttori <xref:System.Xml.Linq.XElement> e <xref:System.Xml.Linq.XAttribute> consentono di passare al costruttore il contenuto dell'elemento o dell'attributo sotto forma di argomenti. Poiché uno dei costruttori accetta un numero variabile di argomenti, è possibile passare un qualsiasi numero di elementi figlio. Ognuno degli elementi figlio può naturalmente contenere elementi figlio. Per qualsiasi elemento è possibile aggiungere un qualsiasi numero di attributi.  
  
 Quando si aggiungono oggetti <xref:System.Xml.Linq.XNode> (incluso <xref:System.Xml.Linq.XElement>) o <xref:System.Xml.Linq.XAttribute>, se il nuovo contenuto non ha un padre, gli oggetti vengono semplicemente collegati all'albero XML. Se invece il nuovo contenuto include già elementi padre e fa parte di un altro albero XML, viene duplicato e quindi collegato all'albero XML. Tale comportamento è illustrato nell'ultimo esempio di questo argomento.  
  
 Per creare un oggetto `contacts` <xref:System.Xml.Linq.XElement>, è possibile usare il codice seguente:  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 Se i rientri sono stati impostati correttamente, il codice per costruire oggetti <xref:System.Xml.Linq.XElement> è molto simile alla struttura del codice XML sottostante.  
  
## <a name="xelement-constructors"></a>Costruttori XElement  
 La classe <xref:System.Xml.Linq.XElement> usa i costruttori seguenti per la costruzione funzionale. Notare che esistono altri costruttori per <xref:System.Xml.Linq.XElement>, che tuttavia non vengono elencati in questa sede perché non usati per la costruzione funzionale.  
  
|Costruttore|Descrizione|  
|-----------------|-----------------|  
|`XElement(XName name, object content)`|Crea un oggetto <xref:System.Xml.Linq.XElement>. Il parametro `name` specifica il nome dell'elemento, mentre il parametro `content` ne specifica il contenuto.|  
|`XElement(XName name)`|Crea un oggetto <xref:System.Xml.Linq.XElement> con il relativo <xref:System.Xml.Linq.XName> inizializzato sul nome specificato.|  
|`XElement(XName name, params object[] content)`|Crea un oggetto <xref:System.Xml.Linq.XElement> con il relativo <xref:System.Xml.Linq.XName> inizializzato sul nome specificato. Gli attributi e/o elementi figlio vengono creati dal contenuto dell'elenco di parametri.|  
  
 Il parametro `content` è estremamente flessibile. Supporta qualsiasi tipo di oggetto che sia un elemento figlio valido di un oggetto <xref:System.Xml.Linq.XElement>. Ai tipi diversi di oggetti passati in questo parametro si applicano le regole seguenti:  
  
-   Una stringa viene aggiunta come contenuto di tipo testo.  
  
-   Un oggetto <xref:System.Xml.Linq.XElement> viene aggiunto come elemento figlio.  
  
-   Un oggetto <xref:System.Xml.Linq.XAttribute> viene aggiunto come attributo.  
  
-   Un oggetto <xref:System.Xml.Linq.XProcessingInstruction>, <xref:System.Xml.Linq.XComment> o <xref:System.Xml.Linq.XText> viene aggiunto come contenuto figlio.  
  
-   Viene enumerato un oggetto <xref:System.Collections.IEnumerable> e queste regole vengono applicate in modo ricorsivo ai risultati.  
  
-   Per qualsiasi altro tipo viene chiamato il metodo `ToString` e il risultato viene aggiunto come contenuto di tipo testo.  
  
### <a name="creating-an-xelement-with-content"></a>Creazione di un XElement con contenuto  
 È possibile creare un oggetto <xref:System.Xml.Linq.XElement> con contenuto semplice usando una sola chiamata al metodo. A tale scopo, specificare il contenuto come secondo parametro, come illustrato di seguito:  
  
```csharp  
XElement n = new XElement("Customer", "Adventure Works");  
Console.WriteLine(n);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
 È possibile passare come contenuto qualsiasi tipo di oggetto. Ad esempio, nel codice seguente viene creato un elemento il cui contenuto è un numero a virgola mobile:  
  
```csharp  
XElement n = new XElement("Cost", 324.50);  
Console.WriteLine(n);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Cost>324.5</Cost>  
```  
  
 Il numero a virgola mobile viene sottoposto a boxing e quindi passato al costruttore. Il numero boxed viene convertito in una stringa e usato come contenuto dell'elemento.  
  
### <a name="creating-an-xelement-with-a-child-element"></a>Creazione di un XElement con un elemento figlio  
 Se si passa un'istanza della classe <xref:System.Xml.Linq.XElement> come argomento del contenuto, il costruttore crea un elemento con un elemento figlio:  
  
```csharp  
XElement shippingUnit = new XElement("ShippingUnit",  
    new XElement("Cost", 324.50)  
);  
Console.WriteLine(shippingUnit);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<ShippingUnit>  
  <Cost>324.5</Cost>  
</ShippingUnit>  
```  
  
### <a name="creating-an-xelement-with-multiple-child-elements"></a>Creazione di un XElement con più elemento figlio  
 È possibile passare un numero di oggetti <xref:System.Xml.Linq.XElement> per il contenuto. Ogni oggetto <xref:System.Xml.Linq.XElement> viene incluso come elemento figlio.  
  
```csharp  
XElement address = new XElement("Address",  
    new XElement("Street1", "123 Main St"),  
    new XElement("City", "Mercer Island"),  
    new XElement("State", "WA"),  
    new XElement("Postal", "68042")  
);  
Console.WriteLine(address);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Address>  
  <Street1>123 Main St</Street1>  
  <City>Mercer Island</City>  
  <State>WA</State>  
  <Postal>68042</Postal>  
</Address>  
```  
  
 Estendendo l'esempio precedente, è possibile creare un intero albero XML, come illustrato di seguito:  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),                                                   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
Console.WriteLine(contacts);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Contacts>  
  <Contact>  
    <Name>Patrick Hines</Name>  
    <Phone>206-555-0144</Phone>  
    <Address>  
      <Street1>123 Main St</Street1>  
      <City>Mercer Island</City>  
      <State>WA</State>  
      <Postal>68042</Postal>  
    </Address>  
  </Contact>  
</Contacts>  
```  
  
### <a name="creating-an-empty-element"></a>Creazione di un elemento vuoto  
 Per creare un oggetto <xref:System.Xml.Linq.XElement> vuoto, non viene passato alcun contenuto al costruttore. Nell'esempio seguente creato un elemento vuoto.  
  
```csharp  
XElement n = new XElement("Customer");  
Console.WriteLine(n);  
```  
  
 Questo esempio produce il seguente output:  
  
```xml  
<Customer />  
```  
  
### <a name="attaching-vs-cloning"></a>Collegamento e clonazione  
 Come indicato in precedenza, quando si aggiungono oggetti <xref:System.Xml.Linq.XNode> (incluso <xref:System.Xml.Linq.XElement>) o <xref:System.Xml.Linq.XAttribute>, se il nuovo contenuto non ha un padre, gli oggetti vengono semplicemente collegati all'albero XML. Se invece il nuovo contenuto include già elementi padre e fa parte di un altro albero XML, viene duplicato e quindi collegato all'albero XML.  
  
```csharp  
// Create a tree with a child element.  
XElement xmlTree1 = new XElement("Root",  
    new XElement("Child1", 1)  
);  
  
// Create an element that is not parented.  
XElement child2 = new XElement("Child2", 2);  
  
// Create a tree and add Child1 and Child2 to it.  
XElement xmlTree2 = new XElement("Root",  
    xmlTree1.Element("Child1"),  
    child2  
);  
  
// Compare Child1 identity.  
Console.WriteLine("Child1 was {0}",  
    xmlTree1.Element("Child1") == xmlTree2.Element("Child1") ?  
    "attached" : "cloned");  
  
// Compare Child2 identity.  
Console.WriteLine("Child2 was {0}",  
    child2 == xmlTree2.Element("Child2") ?  
    "attached" : "cloned");  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Child1 was cloned  
Child2 was attached  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di alberi XML (C#)](../../../../csharp/programming-guide/concepts/linq/creating-xml-trees.md)
