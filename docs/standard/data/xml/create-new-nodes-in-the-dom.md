---
title: "Creazione di nuovi nodi nel DOM | Microsoft Docs"
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
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Creazione di nuovi nodi nel DOM
Il <xref:System.Xml.XmlDocument> dispone di un metodo di creazione per tutti i tipi di nodo. Per creare il nodo, è sufficiente fornire al metodo un nome, se necessario, e un contenuto o altri parametri per i nodi che hanno un contenuto, ad esempio un nodo di tipo text. I metodi seguenti necessitano di un nome e di pochi altri parametri per creare un nodo appropriato.  
  
-   <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 Per altri tipi di nodi è necessario fornire più informazioni dei soli dati per i parametri.  
  
 Per informazioni sugli attributi, vedere [creazione di nuovi attributi per gli elementi nel DOM](../../../../docs/standard/data/xml/creating-new-attributes-for-elements-in-the-dom.md). Per informazioni sulla convalida dei nomi di elementi e attributi, vedere [(elemento XML) e la verifica del nome di attributo durante la creazione di nuovi nodi](../../../../docs/standard/data/xml/xml-element-and-attribute-name-verification-when-creating-new-nodes.md). Per creare riferimenti alle entità, vedere [la creazione di nuovi riferimenti alle entità](../../../../docs/standard/data/xml/creating-new-entity-references.md). Per informazioni su come gli spazi dei nomi influenzano l'espansione di riferimenti alle entità, vedere [Namespace influenza sull'espansione dei riferimenti alle entità per i nuovi nodi contenenti elementi e attributi](../../../../docs/standard/data/xml/namespace-affect-on-entity-ref-expansion-for-new-nodes.md).  
  
 Una volta creati i nuovi nodi, sono disponibili vari metodi per inserirli nell'albero. Nella seguente tabella sono elencati i metodi con una descrizione del punto in cui il nodo viene visualizzato nel DOM XML.  
  
|Metodo|Posizione del nodo|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|Inserito prima del nodo di riferimento. Ad esempio, per inserire il nuovo nodo ad esempio nella posizione 5:<br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> Per ulteriori informazioni, vedere il <xref:System.Xml.XmlNode.InsertBefore%2A> metodo.|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|Inserito dopo il nodo di riferimento. Ad esempio:<br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> Per ulteriori informazioni, vedere il <xref:System.Xml.XmlNode.InsertAfter%2A> metodo.|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|Il nodo viene aggiunto alla fine dell'elenco di nodi figlio per il nodo specificato. Se il nodo aggiunto è un <xref:System.Xml.XmlDocumentFragment>, l'intero contenuto del frammento del documento viene spostato nell'elenco figlio del nodo. Per ulteriori informazioni, vedere il <xref:System.Xml.XmlNode.AppendChild%2A> metodo.|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|Il nodo viene aggiunto all'inizio dell'elenco di nodi figlio per il nodo specificato. Se il nodo aggiunto è un <xref:System.Xml.XmlDocumentFragment>, l'intero contenuto del frammento del documento viene spostato nell'elenco figlio del nodo. Per ulteriori informazioni, vedere il <xref:System.Xml.XmlNode.PrependChild%2A> metodo.|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|Aggiunge un <xref:System.Xml.XmlAttribute> nodo alla fine della raccolta di attributi associata all'elemento. Per ulteriori informazioni, vedere il <xref:System.Xml.XmlAttributeCollection.Append%2A> metodo.|  
  
## <a name="see-also"></a>Vedere anche  
 [XML Document Object Model (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)