---
title: "Accesso agli attributi nel DOM | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: ce2df341-a1a4-4e97-8e1b-cd45b8e3e71e
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Accesso agli attributi nel DOM
Gli attributi sono proprietà dell'elemento, non elementi figlio dell'elemento.  Questa distinzione è importante, a causa dei metodi usati per navigare all'interno dei nodi di pari livello, dei nodi padre e dei nodi figlio nel DOM \(Document Object Model\) XML.  Ad esempio, per navigare da un elemento a un attributo o tra più attributi non vengono usati i metodi **PreviousSibling** e **NextSibling**.  Un attributo è una proprietà di un elemento e appartiene a tale elemento. Presenta infatti una proprietà **OwnerElement** e non una proprietà **parentNode** e dispone di metodi di navigazione diversi.  
  
 Quando il nodo corrente è un elemento, è necessario usare il metodo **HasAttribute** per verificare la presenza di eventuali attributi associati all'elemento.  Una volta appurato che l'elemento dispone di attributi, sono disponibili diversi metodi per accedere agli attributi.  Per recuperare un singolo attributo dall'elemento, è possibile usare i metodi **GetAttribute** e **GetAttributeNode** di **XmlElement** oppure recuperare tutti gli attributi in una raccolta.  Quest'ultimo metodo può rivelarsi utile quando è necessario scorrere la raccolta.  Per recuperare tutti gli attributi dall'elemento, usare la proprietà **Attributes** dell'elemento per recuperare tutti gli attributi in una raccolta.  
  
## Recupero di tutti gli attributi in una raccolta  
 Se si desidera inserire in una raccolta tutti gli attributi di un nodo dell'elemento, chiamare la proprietà **XmlElement.Attributes**.  In questo modo si ottiene **XmlAttributeCollection** in cui sono contenuti tutti gli attributi di un elemento.  La classe **XmlAttributeCollection** eredita dalla mappa **XmlNamedNode**.  Nei metodi e nelle proprietà disponibili nella raccolta sono inoltre inclusi quelli disponibili in una mappa di nodi denominata, oltre ai metodi e alle proprietà specifici della classe **XmlAttributeCollection**, quale la proprietà **ItemOf** o il metodo **Append**.  Ogni elemento della raccolta di attributi rappresenta un nodo **XmlAttribute**.  Per individuare il numero di attributi di un elemento, recuperare la classe **XmlAttributeCollection** e usare la proprietà **Count** per verificare il numero dei nodi **XmlAttribute** presenti nella raccolta.  
  
 Nell'esempio di codice seguente viene illustrato come recuperare una raccolta di attributi e come scorrerla usando il metodo **Count** per l'indice del ciclo.  Inoltre, nel codice viene illustrato come recuperare un singolo attributo dalla raccolta e visualizzarne il valore.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
Public Class Sample  
  
    Public Shared Sub Main()  
  
        Dim doc As XmlDocument = New XmlDocument()  
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" & _  
               "<title>The Handmaid's Tale</title>" & _  
               "<price>14.95</price>" & _  
               "</book>")  
  
        ' Move to an element.   
        Dim myElement As XmlElement = doc.DocumentElement  
  
        ' Create an attribute collection from the element.  
        Dim attrColl As XmlAttributeCollection = myElement.Attributes  
  
        ' Show the collection by iterating over it.  
        Console.WriteLine("Display all the attributes in the collection...")  
        Dim i As Integer  
        For i = 0 To attrColl.Count - 1  
            Console.Write("{0} = ", attrColl.ItemOf(i).Name)  
            Console.Write("{0}", attrColl.ItemOf(i).Value)  
            Console.WriteLine()  
        Next  
  
        ' Retrieve a single attribute from the collection; specifically, the  
        ' attribute with the name "misc".  
        Dim attr As XmlAttribute = attrColl("misc")  
  
        ' Retrieve the value from that attribute.  
        Dim miscValue As String = attr.InnerXml  
  
        Console.WriteLine("Display the attribute information.")  
        Console.WriteLine(miscValue)  
  
    End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
  
public class Sample  
{  
  
    public static void Main()  
    {  
        XmlDocument doc = new XmlDocument();  
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" +  
                      "<title>The Handmaid's Tale</title>" +  
                      "<price>14.95</price>" +  
                      "</book>");  
  
        // Move to an element.  
        XmlElement myElement = doc.DocumentElement;  
  
        // Create an attribute collection from the element.  
        XmlAttributeCollection attrColl = myElement.Attributes;  
  
        // Show the collection by iterating over it.  
        Console.WriteLine("Display all the attributes in the collection...");  
        for (int i = 0; i < attrColl.Count; i++)  
        {  
            Console.Write("{0} = ", attrColl[i].Name);  
            Console.Write("{0}", attrColl[i].Value);  
            Console.WriteLine();  
        }  
  
        // Retrieve a single attribute from the collection; specifically, the  
        // attribute with the name "misc".  
        XmlAttribute attr = attrColl["misc"];  
  
        // Retrieve the value from that attribute.  
        String miscValue = attr.InnerXml;  
  
        Console.WriteLine("Display the attribute information.");  
        Console.WriteLine(miscValue);  
  
    }  
}  
```  
  
 In questo esempio viene visualizzato il seguente l'output:  
  
 **Output**  
  
 Vengono visualizzati tutti gli attributi nella raccolta.  
  
```  
genre = novel  
ISBN = 1-861001-57-5  
misc = sale item  
Display the attribute information.  
sale item  
```  
  
 È possibile recuperare le informazioni contenute in una raccolta di attributi in base al nome o al numero di indice.  Nell'esempio precedente è stato illustrato come recuperare i dati in base al nome.  Nell'esempio successivo viene illustrato come recuperare i dati in base al numero di indice.  
  
 Dal momento che **XmlAttributeCollection** è una raccolta che è possibile scorrere in base al nome o all'indice, nell'esempio viene illustrato come selezionare il primo attributo della raccolta usando un indice in base zero e il seguente file, **baseuri.xml**, come input.  
  
### Input  
  
```  
<!-- XML fragment -->  
<book genre="novel">  
  <title>Pride And Prejudice</title>  
</book>  
```  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.IO  
Imports System.Xml  
  
Public Class Sample  
  
    Public Shared Sub Main()  
        ' Create the XmlDocument.  
        Dim doc As New XmlDocument()  
        doc.Load("http://localhost/baseuri.xml")  
  
        ' Display information on the attribute node. The value  
        ' returned for BaseURI is 'http://localhost/baseuri.xml'.  
        Dim attr As XmlAttribute = doc.DocumentElement.Attributes(0)  
        Console.WriteLine("Name of the attribute:  {0}", attr.Name)  
        Console.WriteLine("Base URI of the attribute:  {0}", attr.BaseURI)  
        Console.WriteLine("The value of the attribtue:  {0}", attr.InnerText)  
    End Sub 'Main   
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
  
public class Sample  
{  
  public static void Main()  
  {  
    // Create the XmlDocument.  
    XmlDocument doc = new XmlDocument();  
  
    doc.Load("http://localhost/baseuri.xml");  
  
    // Display information on the attribute node. The value  
    // returned for BaseURI is 'http://localhost/baseuri.xml'.  
    XmlAttribute attr = doc.DocumentElement.Attributes[0];  
    Console.WriteLine("Name of the attribute:  {0}", attr.Name);  
    Console.WriteLine("Base URI of the attribute:  {0}", attr.BaseURI);  
    Console.WriteLine("The value of the attribtue:  {0}", attr.InnerText);  
  }  
}  
```  
  
## Recupero di un singolo nodo Attribute  
 Per rimuovere un singolo nodo di attributo da un elemento, viene usato il metodo <xref:System.Xml.XmlElement.GetAttributeNode%2A?displayProperty=fullName> che restituisce un oggetto di tipo **XmlAttribute**.  Se si dispone di **XmlAttribute**, tutti i metodi e le proprietà disponibili nella classe [XmlAttribute Members](frlrfsystemxmlxmlattributeclasstopic), ad esempio la ricerca di **OwnerElement**, sono disponibili in tale oggetto.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
Public Class Sample  
  
    Public Shared Sub Main()  
  
        Dim doc As XmlDocument = New XmlDocument()  
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" & _  
               "<title>The Handmaid's Tale</title>" & _  
               "<price>14.95</price>" & _  
               "</book>")  
  
        ' Move to an element.  
        Dim root As XmlElement  
        root = doc.DocumentElement  
  
        ' Get an attribute.  
        Dim attr As XmlAttribute  
        attr = root.GetAttributeNode("ISBN")  
  
        ' Display the value of the attribute.  
        Dim attrValue As String  
        attrValue = attr.InnerXml  
        Console.WriteLine(attrValue)  
  
    End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
  
 public class Sample  
 {  
      public static void Main()  
      {  
    XmlDocument doc = new XmlDocument();  
     doc.LoadXml("<book genre='novel' ISBN='1-861003-78' misc='sale item'>" +  
                   "<title>The Handmaid's Tale</title>" +  
                   "<price>14.95</price>" +  
                   "</book>");   
  
    // Move to an element.  
     XmlElement root = doc.DocumentElement;  
  
    // Get an attribute.  
     XmlAttribute attr = root.GetAttributeNode("ISBN");  
  
    // Display the value of the attribute.  
     String attrValue = attr.InnerXml;  
     Console.WriteLine(attrValue);  
  
    }  
}  
```  
  
 È anche possibile riprodurre l'esempio precedente, in cui dalla raccolta di attributi viene recuperato un singolo nodo Attribute.  Nell'esempio di codice seguente viene illustrato come scrivere una sola riga di codice per recuperare un singolo attributo in base al numero di indice dal livello radice dell'albero di documenti XML, nota anche come proprietà **DocumentElement**.  
  
```  
XmlAttribute attr = doc.DocumentElement.Attributes[0];  
```  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)