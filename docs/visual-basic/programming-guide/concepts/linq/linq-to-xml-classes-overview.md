---
title: Panoramica (Visual Basic) di classi LINQ to XML | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: f11b62b5-d522-4c23-92ae-23186dc16447
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 12885f93bb7e56dd66d36090d41700195313e944
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-classes-overview-visual-basic"></a>LINQ to XML panoramica delle classi (Visual Basic)
In questo argomento fornisce un elenco del [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] classi il <xref:System.Xml.Linq>dello spazio dei nomi e una breve descrizione di ogni.</xref:System.Xml.Linq>  
  
## <a name="linq-to-xml-classes"></a>Classi LINQ to XML  
  
### <a name="xattribute-class"></a>Classe XAttribute  
 <xref:System.Xml.Linq.XAttribute>rappresenta un attributo XML.</xref:System.Xml.Linq.XAttribute> Per informazioni dettagliate ed esempi, vedere [Cenni preliminari sulla classe XAttribute (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xattribute-class-overview.md).  
  
### <a name="xcdata-class"></a>Classe XCData  
 <xref:System.Xml.Linq.XCData>rappresenta un nodo di testo.</xref:System.Xml.Linq.XCData>  
  
### <a name="xcomment-class"></a>Classe XComment  
 <xref:System.Xml.Linq.XComment>rappresenta un commento XML.</xref:System.Xml.Linq.XComment>  
  
### <a name="xcontainer-class"></a>Classe XContainer  
 <xref:System.Xml.Linq.XContainer>è una classe base astratta per tutti i nodi che possono avere nodi figlio.</xref:System.Xml.Linq.XContainer> Le seguenti classi derivano dalla <xref:System.Xml.Linq.XContainer>classe:</xref:System.Xml.Linq.XContainer>  
  
-   <xref:System.Xml.Linq.XElement>  
  
-   <xref:System.Xml.Linq.XDocument></xref:System.Xml.Linq.XDocument>  
  
### <a name="xdeclaration-class"></a>Classe XDeclaration  
 <xref:System.Xml.Linq.XDeclaration>rappresenta una dichiarazione XML.</xref:System.Xml.Linq.XDeclaration> Una dichiarazione XML viene usata per dichiarare la versione XML e la codifica di un documento XML. Inoltre, una dichiarazione XML specifica se il documento XML è autonomo o meno. Se il documento è autonomo non sono presenti dichiarazioni di markup esterne in una DTD esterna o in un'entità parametro esterna a cui è fatto riferimento dal subset interno.  
  
### <a name="xdocument-class"></a>Classe XDocument  
 <xref:System.Xml.Linq.XDocument>rappresenta un documento XML.</xref:System.Xml.Linq.XDocument> Per informazioni dettagliate ed esempi, vedere [Cenni preliminari sulla classe XDocument (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xdocument-class-overview.md).  
  
### <a name="xdocumenttype-class"></a>Classe XDocumentType  
 <xref:System.Xml.Linq.XDocumentType>rappresenta un XML definizione DTD (Document Type).</xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xelement-class"></a>Classe XElement  
 <xref:System.Xml.Linq.XElement>rappresenta un elemento XML.</xref:System.Xml.Linq.XElement> Per informazioni dettagliate ed esempi, vedere [Cenni preliminari sulla classe XElement (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xelement-class-overview.md).  
  
### <a name="xname-class"></a>Classe XName  
 <xref:System.Xml.Linq.XName>rappresenta i nomi di elementi (<xref:System.Xml.Linq.XElement>) e attributi (<xref:System.Xml.Linq.XAttribute>).</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement></xref:System.Xml.Linq.XName> Per informazioni dettagliate ed esempi, vedere [Cenni preliminari sulla classe XDocument (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/xdocument-class-overview.md).  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è progettato per semplificare il più possibile i nomi XML. Essendo molto complessi, i nomi XML vengono spesso considerati un argomento avanzato in XML. In effetti questa complessità non deriva dagli spazi dei nomi, utilizzati regolarmente dagli sviluppatori nella programmazione, ma dai prefissi di spazio dei nomi. I prefissi di spazio dei nomi possono risultare utili per ridurre le sequenze di tasti richieste durante l'input XML o per migliorare la leggibilità di XML. Tuttavia, i prefissi rappresentano spesso solo una scelta rapida per utilizzare lo spazio dei nomi XML completo e nella maggior parte dei casi non sono necessari. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]i nomi XML vengono semplificati risolvendo tutti i prefissi di spazio dei nomi XML corrispondente. I prefissi sono disponibili se sono necessari, tramite il <xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A>(metodo).</xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A>  
  
 Se è necessario, è possibile controllare i prefissi di spazio dei nomi. In alcune circostanze, se si usano altri sistemi XML, ad esempio XSLT o XAML, è necessario controllare i prefissi di spazio dei nomi. Ad esempio se in un'espressione XPath incorporata in un foglio di stile XSLT vengono usati i prefissi di spazio dei nomi, è necessario assicurarsi che il documento XML venga serializzato con prefissi di spazio dei nomi corrispondenti a quelli usati nell'espressione XPath.  
  
### <a name="xnamespace-class"></a>Classe XNamespace  
 <xref:System.Xml.Linq.XNamespace>rappresenta uno spazio dei nomi per un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XAttribute>.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement></xref:System.Xml.Linq.XNamespace> Gli spazi dei nomi sono un componente di un <xref:System.Xml.Linq.XName>.</xref:System.Xml.Linq.XName>  
  
### <a name="xnode-class"></a>Classe XNode  
 <xref:System.Xml.Linq.XNode>è una classe astratta che rappresenta i nodi di un albero XML.</xref:System.Xml.Linq.XNode> Le seguenti classi derivano dalla <xref:System.Xml.Linq.XNode>classe:</xref:System.Xml.Linq.XNode>  
  
-   <xref:System.Xml.Linq.XText></xref:System.Xml.Linq.XText>  
  
-   <xref:System.Xml.Linq.XContainer></xref:System.Xml.Linq.XContainer>  
  
-   <xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XComment>  
  
-   <xref:System.Xml.Linq.XProcessingInstruction></xref:System.Xml.Linq.XProcessingInstruction>  
  
-   <xref:System.Xml.Linq.XDocumentType></xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xnodedocumentordercomparer-class"></a>Classe XNodeDocumentOrderComparer  
 <xref:System.Xml.Linq.XNodeDocumentOrderComparer>fornisce funzionalità per confrontare nodi per l'ordine del documento.</xref:System.Xml.Linq.XNodeDocumentOrderComparer>  
  
### <a name="xnodeequalitycomparer-class"></a>Classe XNodeEqualityComparer  
 <xref:System.Xml.Linq.XNodeEqualityComparer>fornisce funzionalità per confrontare nodi per l'uguaglianza di valori.</xref:System.Xml.Linq.XNodeEqualityComparer>  
  
### <a name="xobject-class"></a>Classe XObject  
 <xref:System.Xml.Linq.XObject>è una classe base astratta di <xref:System.Xml.Linq.XNode>e <xref:System.Xml.Linq.XAttribute>.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XNode></xref:System.Xml.Linq.XObject> Fornisce funzionalità di annotazione ed evento.  
  
### <a name="xobjectchange-class"></a>Classe XObjectChange  
 <xref:System.Xml.Linq.XObjectChange>Specifica il tipo di evento quando viene generato un evento per un <xref:System.Xml.Linq.XObject>.</xref:System.Xml.Linq.XObject></xref:System.Xml.Linq.XObjectChange>  
  
### <a name="xobjectchangeeventargs-class"></a>Classe XObjectChangeEventArgs  
 <xref:System.Xml.Linq.XObjectChangeEventArgs>Fornisce dati per il <xref:System.Xml.Linq.XObject.Changing>e <xref:System.Xml.Linq.XObject.Changed>gli eventi.</xref:System.Xml.Linq.XObject.Changed> </xref:System.Xml.Linq.XObject.Changing></xref:System.Xml.Linq.XObjectChangeEventArgs>  
  
### <a name="xprocessinginstruction-class"></a>Classe XProcessingInstruction  
 <xref:System.Xml.Linq.XProcessingInstruction>rappresenta un'istruzione di elaborazione XML.</xref:System.Xml.Linq.XProcessingInstruction> Un'istruzione di elaborazione comunica informazioni a un'applicazione che elabora l'XML.  
  
### <a name="xtext-class"></a>Classe XText  
 <xref:System.Xml.Linq.XText>rappresenta un nodo di testo.</xref:System.Xml.Linq.XText> Nella maggior parte dei casi non è necessario usare questa classe, che viene usata principalmente per contenuto misto.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Cenni preliminari sulla programmazione XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
