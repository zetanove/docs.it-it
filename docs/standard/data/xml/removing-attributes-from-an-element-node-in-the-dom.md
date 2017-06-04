---
title: "Rimozione di attributi da un nodo di elemento nel DOM | Microsoft Docs"
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
ms.assetid: 7ede6f9e-a3ac-49a4-8488-ab8360a44aa4
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Rimozione di attributi da un nodo di elemento nel DOM
Sono disponibili numerosi metodi per rimuovere gli attributi.  Una tecnica consiste nel rimuoverli dalla raccolta di attributi.  Per eseguire questa operazione, attenersi alla procedura seguente:  
  
1.  Ottenere la raccolta di attributi dall'elemento usando `XmlAttributeCollection attrs = elem.Attributes;`.  
  
2.  Rimuovere l'attributo dalla raccolta di attributi, usando uno dei metodi seguenti:  
  
    -   Usare il metodo <xref:System.Xml.XmlAttributeCollection.Remove%2A> per rimuovere un attributo specifico.  
  
    -   Usare il metodo <xref:System.Xml.XmlAttributeCollection.RemoveAll%2A> per rimuovere tutti gli attributi dalla raccolta e lasciarne privo l'elemento.  
  
    -   Usare il metodo <xref:System.Xml.XmlAttributeCollection.RemoveAt%2A> per rimuovere un attributo dalla raccolta usando il relativo numero di indice.  
  
 I metodi seguenti consentono di rimuovere gli attributi dal nodo dell'elemento.  
  
-   Usare il metodo <xref:System.Xml.XmlElement.RemoveAllAttributes%2A> per rimuovere la raccolta di attributi.  
  
-   Usare il metodo <xref:System.Xml.XmlElement.RemoveAttribute%2A> per rimuovere un singolo attributo dalla raccolta in base al nome.  
  
-   Usare il metodo <xref:System.Xml.XmlElement.RemoveAttributeAt%2A> per rimuovere un singolo attributo dalla raccolta in base al numero di indice.  
  
 Un'altra alternativa consiste nell'ottenere l'elemento, ottenere l'attributo dalla raccolta di attributi e rimuovere direttamente il nodo dell'attributo.  Per ottenere l'attributo dalla raccolta di attributi, è possibile usare un nome, `XmlAttribute attr = attrs["attr_name"];`, un indice, `XmlAttribute attr = attrs[0];`, o qualificare completamente il nome con lo spazio dei nomi `XmlAttribute attr = attrs["attr_localName", "attr_namespace"]`.  
  
 Qualunque sia il metodo usato per rimuovere gli attributi, la rimozione di attributi definiti come attributi predefiniti nella DTD è soggetta ad alcuni limiti specifici.  Non è possibile rimuovere gli attributi predefiniti a meno che non venga rimosso l'elemento al quale appartengono.  Gli attributi predefiniti devono essere sempre presenti negli elementi per cui sono dichiarati.  Quando si rimuove un attributo predefinito da un tipo <xref:System.Xml.XmlAttributeCollection> o da un tipo <xref:System.Xml.XmlElement>, viene inserito un attributo di sostituzione nel tipo <xref:System.Xml.XmlAttributeCollection> dell'elemento, inizializzato in base al valore predefinito che era stato dichiarato.  Se un elemento è stato definito come `<book att1="1" att2="2" att3="3"></book>`, si avrà un elemento `book` con tre attributi predefiniti dichiarati.  L'implementazione DOM XML garantisce che fintanto che esisterà, l'elemento `book`  avrà questi tre attributi predefiniti, `att1`, `att2` e `att3`.  
  
 Quando viene chiamato con <xref:System.Xml.XmlAttribute>, il metodo <xref:System.Xml.XmlAttributeCollection.RemoveAll%2A> imposta il valore dell'attributo su String.Empty, in quanto un attributo non può esistere senza un valore.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)