---
title: "Recupero di nodi non ordinati in base al nome o all&#39;indice | Microsoft Docs"
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
ms.assetid: 2038a90b-92af-4a0a-baaa-08e688d95194
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Recupero di nodi non ordinati in base al nome o all&#39;indice
**XmlNamedNodeMap** è descritto nelle specifiche W3C come NamedNodeMap. La sua funzione è quella di gestire un set di nodi non ordinato con la capacità di fare riferimento ai nodi in base al nome o all'indice.  L'unico modo per accedere a un **XmlNamedNodeMap** è quando un **XmlNamedNodeMap** viene restituito tramite un metodo o una proprietà.  Sono disponibili tre metodi o proprietà da cui viene restituito un **XmlNamedNodeMap**:  
  
-   XmlElement.Attributes  
  
-   XmlDocumentType.Entities  
  
-   XmlDocumentType.Notations  
  
 La proprietà **XmlDocumentType.Entities**, ad esempio, consente di recuperare la raccolta di nodi **XmlEntity** presenti nella dichiarazione del tipo di documento.  Questa raccolta viene restituita come **XmlNamedNodeMap**, ed è possibile scorrerla con la proprietà **Count** e visualizzare le informazioni relative all'entità.  Per un esempio di scorrimento in **XmlNamedNodeMap**, vedere [Proprietà XmlDocumentType.Entities](frlrfSystemXmlXmlDocumentTypeClassEntitiesTopic).  
  
 **XmlAttributeCollection** deriva da **XmlNamedNodeMap** e solo gli attributi sono modificabili, mentre le notazioni e le entità sono in sola lettura.  Usando **XmlNamedNodeMap** per gli attributi, è possibile ottenere nodi per quegli attributi in base ai relativi nomi XML.  Questo rappresenta un metodo semplice per la modifica della raccolta di attributi su un nodo di elemento,  a differenza di **XmlNodeList**, che implementa anch'esso l'interfaccia **IEnumerable**, ma con una funzione di accesso all'indice anziché una stringa.  I metodi **RemoveNamedItem** e **SetNamedItem** vengono usati solo in relazione a un **XmlAttributeCollection**.  L'aggiunta o la rimozione da una raccolta di attributi, sia tramite l'implementazione **AttributeCollection** o **XmlNamedNodeMap**, modifica la raccolta di attributi sull'elemento.  Nell'esempio di codice seguente viene illustrato come spostare un attributo e come crearne uno nuovo.  
  
```vb  
Imports System  
Imports System.Xml  
  
Class test  
  
    Public Shared Sub Main()  
        Dim doc As New XmlDocument()  
        doc.LoadXml("<root> <child1 attr1='val1' attr2='val2'> text1 </child1> <child2 attr3='val3'> text2 </child2> </root> ")  
  
        ' Get the attributes of node "child2 "  
        Dim ac As XmlAttributeCollection = doc.DocumentElement.ChildNodes(1).Attributes  
  
        ' Print out the number of attributes and their names.  
        Console.WriteLine(("Number of Attributes: " + ac.Count))  
        Dim i As Integer  
        For i = 0 To ac.Count - 1  
            Console.WriteLine((i + 1 + ".  Attribute Name: '" + ac(i).Name + "'  Attribute Value:  '" + ac(i).Value + "'"))  
        Next i  
        ' Get the 'attr1' from child1.  
        Dim attr As XmlAttribute = doc.DocumentElement.ChildNodes(0).Attributes(0)  
  
        ' Add this attribute to the attributecollection "ac".  
        ac.SetNamedItem(attr)  
  
        ''attr1' will be removed from 'child1' and added to 'child2'.  
        ' Print out the number of attributes and their names.  
        Console.WriteLine(("Number of Attributes: " + ac.Count))  
  
        For i = 0 To ac.Count - 1  
            Console.WriteLine((i + 1 + ".  Attribute Name: '" + ac(i).Name + "'  Attribute Value:  '" + ac(i).Value + "'"))  
        Next i  
        ' Create a new attribute and add to the collection.  
        Dim attr2 As XmlAttribute = doc.CreateAttribute("attr4")  
        attr2.Value = "val4"  
        ac.SetNamedItem(attr2)  
  
        ' Print out the number of attributes and their names.  
        Console.WriteLine(("Number of Attributes: " + ac.Count))  
  
        For i = 0 To ac.Count - 1  
            Console.WriteLine((i + 1 + ".  Attribute Name: '" + ac(i).Name + "'  Attribute Value:  '" + ac(i).Value + "'"))  
        Next i  
    End Sub 'Main  
End Class 'test  
```  
  
```csharp  
using System;  
using System.Xml;  
class test {  
    public static void Main() {  
        XmlDocument doc = new XmlDocument();  
        doc.LoadXml( "<root> <child1 attr1='val1' attr2='val2'> text1 </child1> <child2 attr3='val3'> text2 </child2> </root> " );  
  
        // Get the attributes of node "child2"  
        XmlAttributeCollection ac = doc.DocumentElement.ChildNodes[1].Attributes;  
  
        // Print out the number of attributes and their names.  
        Console.WriteLine( "Number of Attributes: "+ac.Count );  
        for( int i = 0; i < ac.Count; i++ )  
            Console.WriteLine( (i+1) + ".  Attribute Name: '" +ac[i].Name+ "'  Attribute Value:  '"+ ac[i].Value +"'" );   
  
        // Get the 'attr1' from child1.  
        XmlAttribute attr = doc.DocumentElement.ChildNodes[0].Attributes[0];  
  
        // Add this attribute to the attributecollection "ac".  
        ac.SetNamedItem( attr );  
  
        // 'attr1' will be removed from 'child1' and added to 'child2'.  
        // Print out the number of attributes and their names.  
        Console.WriteLine( "Number of Attributes: "+ac.Count );          
        for( int i = 0; i < ac.Count; i++ )  
            Console.WriteLine( (i+1) + ".  Attribute Name: '" +ac[i].Name+ "'  Attribute Value:  '"+ ac[i].Value +"'" );   
  
        // Create a new attribute and add to the collection.  
        XmlAttribute attr2 = doc.CreateAttribute( "attr4" );  
        attr2.Value = "val4";  
        ac.SetNamedItem( attr2 );  
  
        // Print out the number of attributes and their names.  
        Console.WriteLine( "Number of Attributes: "+ac.Count );          
        for( int i = 0; i < ac.Count; i++ )  
            Console.WriteLine( (i+1) + ".  Attribute Name: '" +ac[i].Name+ "'  Attribute Value:  '"+ ac[i].Value +"'" );           
  
    }  
}  
```  
  
 Un ulteriore esempio di codice che illustra la rimozione di un attributo da un **AttributeCollection** è riportato in [Metodo XmlNamedNodeMap.RemoveNamedItem](frlrfSystemXmlXmlNamedNodeMapClassRemoveNamedItemTopic).  Per altre informazioni sui metodi e sulle proprietà, vedere [Membri XmlNameNodeMap](frlrfSystemXmlXmlNamedNodeMapMembersTopic).  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)