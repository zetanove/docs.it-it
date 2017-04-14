---
title: "Modifica delle dichiarazioni dello spazio dei nomi in un documento XML | Microsoft Docs"
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
ms.assetid: a2758f40-e497-4964-8d8d-1bb68af14dcd
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Modifica delle dichiarazioni dello spazio dei nomi in un documento XML
Le dichiarazioni dello spazio dei nomi e gli attributi **xmlns** vengono esposti da **XmlDocument** come parte del modello a oggetti del documento  e archiviati in **XmlDocument**, affinché il documento mantenga la posizione degli attributi quando viene salvato.  La modifica di questi attributi, non ha effetto sulle proprietà **Name**, **NamespaceURI** e **Prefix** degli altri nodi già presenti nell'albero.  Ad esempio, se si carica il documento seguente, l'elemento `test` ha il **NamespaceURI** `123.`  
  
```  
<test xmlns="123"/>  
```  
  
 Se si rimuove l'attributo `xmlns` nel modo seguente, l'elemento `test` l'elemento ha ancora il **NamespaceURI** di `123`.  
  
```vb  
doc.documentElement.RemoveAttribute("xmlns")  
```  
  
```csharp  
doc.documentElement.RemoveAttribute("xmlns");  
```  
  
 Analogamente, se si aggiunge un attributo `xmlns` diverso all'elemento `doc` nel seguente modo, l'elemento `test` ha ancora il **NamespaceURI** `123`.  
  
```vb  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
```csharp  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
 La modifica degli attributi `xmlns` non avrà quindi alcun effetto fino a quando l'oggetto **XmlDocument** non verrà salvato e ricaricato.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)