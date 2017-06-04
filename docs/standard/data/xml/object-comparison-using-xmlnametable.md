---
title: "Confronto di oggetti con XmlNameTable | Microsoft Docs"
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
ms.assetid: 8d94e041-d340-4ddf-9a2c-d7319e3f4f86
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Confronto di oggetti con XmlNameTable
Al momento della creazione, ogni **XmlDocument** dispone di una tabella dei nomi creata specificamente per quel documento.  Quando il codice XML viene caricato nel documento o vengono creati nuovi elementi o attributi, i nomi di attributi ed elementi vengono inseriti nella **XmlNameTable**.  È possibile inoltre creare un **XmlDocument** usando una **NameTable** esistente di un altro documento.  Quando gli **XmlDocument** vengono creati con il costruttore che accetta un parametro **XmlNameTable**, il documento ha accesso ai nomi dei nodi, agli spazi dei nomi e ai prefissi già archiviati nella **XmlNameTable**.  Indipendentemente da come viene caricata la tabella dei nomi, una volta che i nomi vengono archiviati nella tabella, potranno essere confrontati rapidamente, usando il confronto degli oggetti invece del confronto delle stringhe.  È possibile inoltre aggiungere stringhe alla tabella dei nomi usando il metodo [NameTable.Add](frlrfSystemXmlNameTableClassAddTopic).  Nell'esempio di codice seguente viene illustrata la creazione di una tabella dei nomi e l'aggiunta alla tabella della stringa **MyString**.  Successivamente viene creato un **XmlDocument** usando quella tabella e i nomi degli elementi e degli attributi contenuti in **Myfile.xml** vengono aggiunti alla tabella dei nomi esistente.  
  
```vb  
Dim nt As New NameTable()  
nt.Add("MyString")  
Dim doc As New XmlDocument(nt)  
doc.Load("Myfile.xml")  
```  
  
```csharp  
NameTable nt = new NameTable();  
nt.Add("MyString");  
XmlDocument doc = new XmlDocument(nt);  
doc.Load("Myfile.xml");  
```  
  
 Nell'esempio di codice seguente viene illustrata la creazione di un documento, l'aggiunta di due nuovi elementi al documento, che implica anche l'aggiunta alla tabella dei nomi del documento, e il confronto degli oggetti in base ai nomi.  
  
```vb  
Dim doc1 As XmlDocument = imp.CreateDocument()  
Dim node1 As XmlElement = doc.CreateElement("node1")  
Dim doc2 As XmlDocument = imp.CreateDocument()  
Dim node2 As XmlElement = doc.CreateElement("node2")  
if (CType(node1.Name, object) = CType(node2.Name, object))  
```  
  
```csharp  
XmlDocument doc1 = imp.CreateDocument();  
node1 = doc1.CreateElement ("node1");  
XmlDocument doc2 = imp.CreateDocument();  
node2 = doc2.CreateElement ("node1");  
if (((object)node1.Name) == ((object)node2.Name))  
{ ...  
```  
  
 In genere, il passaggio di una tabella dei nomi tra due documenti si verifica quando lo stesso tipo di documento viene elaborato ripetutamente, come nel caso di documenti d'ordine in un sito Web di e\-commerce, in modo conforme a uno schema XSD \(XML Schema Definition Language\) o a una DTD \(Document Type Definition\), dove si ripetono le stesse stringhe.  Usando la stessa tabella dei nomi si ottengono migliori prestazioni in quanto lo stesso nome di elemento ricorre in più documenti.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)