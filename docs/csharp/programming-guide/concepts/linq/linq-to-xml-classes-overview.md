---
title: Panoramica delle classi LINQ to XML (C#) | Microsoft Docs
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
ms.assetid: bf666100-5392-4968-97f4-f6b9d3287d7b
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
ms.openlocfilehash: f75a7a2aa3f9fca867562807595c6387b0be23d4
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-classes-overview-c"></a>Panoramica delle classi LINQ to XML (C#)
Questo argomento include un elenco delle classi [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] nello spazio dei nomi <xref:System.Xml.Linq> e una breve descrizione di ogni classe.  
  
## <a name="linq-to-xml-classes"></a>Classi LINQ to XML  
  
### <a name="xattribute-class"></a>Classe XAttribute  
 <xref:System.Xml.Linq.XAttribute> rappresenta un attributo XML. Per informazioni dettagliate ed esempi, vedere [Panoramica della classe XAttribute (C#)](../../../../csharp/programming-guide/concepts/linq/xattribute-class-overview.md).  
  
### <a name="xcdata-class"></a>Classe XCData  
 <xref:System.Xml.Linq.XCData> rappresenta un nodo di testo CDATA.  
  
### <a name="xcomment-class"></a>Classe XComment  
 <xref:System.Xml.Linq.XComment> rappresenta un commento XML.  
  
### <a name="xcontainer-class"></a>Classe XContainer  
 <xref:System.Xml.Linq.XContainer> è una classe base astratta per tutti i nodi che possono avere nodi figlio. Le classi seguenti derivano dalla classe <xref:System.Xml.Linq.XContainer>:  
  
-   <xref:System.Xml.Linq.XElement>  
  
-   <xref:System.Xml.Linq.XDocument>  
  
### <a name="xdeclaration-class"></a>Classe XDeclaration  
 <xref:System.Xml.Linq.XDeclaration> rappresenta una dichiarazione XML. Una dichiarazione XML viene usata per dichiarare la versione XML e la codifica di un documento XML. Inoltre, una dichiarazione XML specifica se il documento XML è autonomo o meno. Se il documento è autonomo non sono presenti dichiarazioni di markup esterne in una DTD esterna o in un'entità parametro esterna a cui è fatto riferimento dal subset interno.  
  
### <a name="xdocument-class"></a>Classe XDocument  
 <xref:System.Xml.Linq.XDocument> rappresenta un documento XML. Per informazioni dettagliate ed esempi, vedere [Panoramica della classe XDocument (C#)](../../../../csharp/programming-guide/concepts/linq/xdocument-class-overview.md).  
  
### <a name="xdocumenttype-class"></a>Classe XDocumentType  
 <xref:System.Xml.Linq.XDocumentType> rappresenta un Document Type Definition (DTD) XML.  
  
### <a name="xelement-class"></a>Classe XElement  
 <xref:System.Xml.Linq.XElement> rappresenta un elemento XML. Per informazioni dettagliate ed esempi, vedere [Panoramica della classe XElement (C#)](../../../../csharp/programming-guide/concepts/linq/xelement-class-overview.md).  
  
### <a name="xname-class"></a>Classe XName  
 <xref:System.Xml.Linq.XName> rappresenta i nomi di elementi (<xref:System.Xml.Linq.XElement>) e attributi (<xref:System.Xml.Linq.XAttribute>). Per informazioni dettagliate ed esempi, vedere [Panoramica della classe XDocument (C#)](../../../../csharp/programming-guide/concepts/linq/xdocument-class-overview.md).  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è progettato per semplificare il più possibile i nomi XML. Essendo molto complessi, i nomi XML vengono spesso considerati un argomento avanzato in XML. In effetti questa complessità non deriva dagli spazi dei nomi, utilizzati regolarmente dagli sviluppatori nella programmazione, ma dai prefissi di spazio dei nomi. I prefissi di spazio dei nomi possono risultare utili per ridurre le sequenze di tasti richieste durante l'input XML o per migliorare la leggibilità di XML. Tuttavia, i prefissi rappresentano spesso solo una scelta rapida per utilizzare lo spazio dei nomi XML completo e nella maggior parte dei casi non sono necessari. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] i nomi XML vengono semplificati risolvendo tutti i prefissi nello spazio dei nomi XML corrispondente. Se necessari, i prefissi sono disponibili attraverso il metodo <xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A>.  
  
 Se è necessario, è possibile controllare i prefissi di spazio dei nomi. In alcune circostanze, se si usano altri sistemi XML, ad esempio XSLT o XAML, è necessario controllare i prefissi di spazio dei nomi. Ad esempio se in un'espressione XPath incorporata in un foglio di stile XSLT vengono usati i prefissi di spazio dei nomi, è necessario assicurarsi che il documento XML venga serializzato con prefissi di spazio dei nomi corrispondenti a quelli usati nell'espressione XPath.  
  
### <a name="xnamespace-class"></a>Classe XNamespace  
 <xref:System.Xml.Linq.XNamespace> rappresenta uno spazio dei nomi per <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XAttribute>. Gli spazi dei nomi sono un componente di <xref:System.Xml.Linq.XName>.  
  
### <a name="xnode-class"></a>Classe XNode  
 <xref:System.Xml.Linq.XNode> è una classe astratta che rappresenta i nodi di un albero XML. Le classi seguenti derivano dalla classe <xref:System.Xml.Linq.XNode>:  
  
-   <xref:System.Xml.Linq.XText>  
  
-   <xref:System.Xml.Linq.XContainer>  
  
-   <xref:System.Xml.Linq.XComment>  
  
-   <xref:System.Xml.Linq.XProcessingInstruction>  
  
-   <xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xnodedocumentordercomparer-class"></a>Classe XNodeDocumentOrderComparer  
 <xref:System.Xml.Linq.XNodeDocumentOrderComparer> specifica la funzionalità per confrontare i nodi per rilevare l'ordine del documento.  
  
### <a name="xnodeequalitycomparer-class"></a>Classe XNodeEqualityComparer  
 <xref:System.Xml.Linq.XNodeEqualityComparer> specifica la funzionalità per confrontare nodi per rilevare l'uguaglianza di valori.  
  
### <a name="xobject-class"></a>Classe XObject  
 <xref:System.Xml.Linq.XObject> è una classe base astratta di <xref:System.Xml.Linq.XNode> e <xref:System.Xml.Linq.XAttribute>. Fornisce funzionalità di annotazione ed evento.  
  
### <a name="xobjectchange-class"></a>Classe XObjectChange  
 <xref:System.Xml.Linq.XObjectChange> specifica il tipo di evento quando viene generato un evento per <xref:System.Xml.Linq.XObject>.  
  
### <a name="xobjectchangeeventargs-class"></a>Classe XObjectChangeEventArgs  
 <xref:System.Xml.Linq.XObjectChangeEventArgs> specifica i dati per gli eventi <xref:System.Xml.Linq.XObject.Changing> e <xref:System.Xml.Linq.XObject.Changed>.  
  
### <a name="xprocessinginstruction-class"></a>Classe XProcessingInstruction  
 <xref:System.Xml.Linq.XProcessingInstruction> rappresenta un'istruzione di elaborazione XML. Un'istruzione di elaborazione comunica informazioni a un'applicazione che elabora l'XML.  
  
### <a name="xtext-class"></a>Classe XText  
 <xref:System.Xml.Linq.XText> rappresenta un nodo di testo. Nella maggior parte dei casi non è necessario usare questa classe, che viene usata principalmente per contenuto misto.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica della programmazione con LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
