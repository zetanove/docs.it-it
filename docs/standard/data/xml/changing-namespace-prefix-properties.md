---
title: "Modifica delle propriet&#224; del prefisso dello spazio dei nomi | Microsoft Docs"
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
ms.assetid: d5c87cbe-4d69-429f-aad5-3103c2ca2770
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Modifica delle propriet&#224; del prefisso dello spazio dei nomi
La classe **XmlNode** consente di modificare il prefisso dello spazio dei nomi associato a un determinato nodo.  Nel codice seguente, ad esempio, viene mostrata la modifica del prefisso di un elemento.  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "b"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<a:test xmlns:a='123' xmlns:b='456'/>");  
XmlElement e = doc.DocumentElement;         
e.Prefix = "b";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **Output**  
  
```  
<b:test xmlns:a="123" xmlns:b="456" />  
```  
  
 La modifica del prefisso di un nodo non comporta cambiamenti dello spazio dei nomi.  Lo spazio dei nomi può essere impostato solo al momento della creazione del nodo.  Quando si mantiene fissa l'albero, i nuovi attributi dello spazio dei nomi possono essere mantenuti fissi per soddisfare il prefisso impostato.  Se non è possibile creare il nuovo spazio dei nomi, il prefisso viene modificato in modo che il nodo conservi il nome locale e lo spazio dei nomi.  Nell'esempio seguente viene illustrato come aggiungere un attributo dello spazio dei nomi.  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.LoadXml("<test xmlns='123'/>")  
Dim e as XmlElement = doc.DocumentElement  
e.Prefix = "a"  
Console.WriteLine(doc.InnerXml)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.LoadXml("<test xmlns='123'/>");  
XmlElement e = doc.DocumentElement;         
e.Prefix = "a";  
Console.WriteLine(doc.InnerXml);  
```  
  
 **Output**  
  
```  
<a:test xmlns="123" xmlns:a="123" />  
```  
  
 Dal momento che l'albero era rimasto fisso su una stringa in seguito alla chiamata a **doc.InnerXml**, l'attributo `xmlns:a='123'` è stato aggiunto per mantenere lo spazio dei nomi dell'elemento `test`.  Era `'123'`, ed è rimasto `'123'`.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)