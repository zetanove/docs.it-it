---
title: LINQ to XML e DOM (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 18c36130-d598-40b7-9007-828232252978
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 88b6bddcdeec2859844f5d5f94777146d488b5fb
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-vs-dom-visual-basic"></a>LINQ to XML e DOM (Visual Basic)
In questa sezione vengono descritte alcune differenze fondamentali tra [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] e il XML attualmente più diffusa API di programmazione, il W3C Model (DOM).  
  
## <a name="new-ways-to-construct-xml-trees"></a>Nuove modalità di creazione degli alberi XML  
 In W3C DOM un albero XML viene compilata dal basso verso l'alto, ossia si crea un documento, si creano gli elementi e quindi si aggiungono gli elementi al documento.  
  
 Ad esempio, il seguente sarebbe normalmente per creare una struttura ad albero XML tramite l'implementazione Microsoft di DOM, <xref:System.Xml.XmlDocument>:</xref:System.Xml.XmlDocument>  
  
```vb  
Dim doc As XmlDocument = New XmlDocument()  
Dim name As XmlElement = doc.CreateElement("Name")  
name.InnerText = "Patrick Hines"  
Dim phone1 As XmlElement = doc.CreateElement("Phone")  
phone1.SetAttribute("Type", "Home")  
phone1.InnerText = "206-555-0144"  
Dim phone2 As XmlElement = doc.CreateElement("Phone")  
phone2.SetAttribute("Type", "Work")  
phone2.InnerText = "425-555-0145"  
Dim street1 As XmlElement = doc.CreateElement("Street1")  
street1.InnerText = "123 Main St"  
Dim city As XmlElement = doc.CreateElement("City")  
city.InnerText = "Mercer Island"  
Dim state As XmlElement = doc.CreateElement("State")  
state.InnerText = "WA"  
Dim postal As XmlElement = doc.CreateElement("Postal")  
postal.InnerText = "68042"  
Dim address As XmlElement = doc.CreateElement("Address")  
address.AppendChild(street1)  
address.AppendChild(city)  
address.AppendChild(state)  
address.AppendChild(postal)  
Dim contact As XmlElement = doc.CreateElement("Contact")  
contact.AppendChild(name)  
contact.AppendChild(phone1)  
contact.AppendChild(phone2)  
contact.AppendChild(address)  
Dim contacts As XmlElement = doc.CreateElement("Contacts")  
contacts.AppendChild(contact)  
doc.AppendChild(contacts)  
Console.WriteLine(doc.OuterXml)  
```  
  
 Questo stile di codifica non fornisce molte informazioni visive sulla struttura dell'albero XML. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]supporta questo approccio alla creazione di un albero XML, ma anche un approccio alternativo, *costruzione funzionale*. In Visual Basic, la costruzione funzionale utilizza valori letterali XML per compilare un albero XML.  
  
 Di seguito è illustrata la creazione dello stesso albero XML utilizzando [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] costruzione funzionale:  
  
```vb  
Dim contacts = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone Type="Home">206-555-0144</Phone>  
            <Phone Type="Work">425-555-0145</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
 Si noti che il rientro del codice per costruire la struttura ad albero XML illustra la struttura dell'XML sottostante.  
  
 Per ulteriori informazioni, vedere [la creazione di strutture ad albero XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md).  
  
## <a name="working-directly-with-xml-elements"></a>Utilizzo diretto di elementi XML  
 Quando si programma con XML, l'obiettivo principale riguarda in genere gli elementi XML e talvolta gli attributi. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile usare direttamente gli elementi e gli attributi XML. Ad esempio, è possibile eseguire quanto le operazioni seguenti:  
  
-   Creare elementi XML senza usare affatto un oggetto documento. In questo modo la programmazione risulta semplificata quando è necessario usare frammenti di alberi XML.  
  
-   Caricare oggetti `T:System.Xml.Linq.XElement` direttamente da un file XML.  
  
-   Serializzare oggetti `T:System.Xml.Linq.XElement` a un file o un flusso.  
  
 Al contrario, in W3C DOM il documento XML viene usato come contenitore logico per l'albero XML. In DOM i nodi XML, inclusi elementi e attributi, devono essere creati nel contesto di un documento XML. Di seguito è riportato un frammento del codice usato per creare un elemento name in DOM:  
  
```vb  
Dim doc As XmlDocument = New XmlDocument()  
Dim name As XmlElement = doc.CreateElement("Name")  
name.InnerText = "Patrick Hines"  
doc.AppendChild(name)  
```  
  
 Se si desidera usare un elemento in più documenti, è necessario importare i nodi tra documenti. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]evita questo livello di complessità.  
  
 Quando si utilizza LINQ to XML, utilizzare la <xref:System.Xml.Linq.XDocument>classe solo se si desidera aggiungere un'istruzione di elaborazione o commento relativo al livello radice del documento.</xref:System.Xml.Linq.XDocument>  
  
## <a name="simplified-handling-of-names-and-namespaces"></a>Gestione semplificata di nomi e spazi dei nomi  
 La gestione di nomi, spazi dei nomi e prefissi di spazio dei nomi è in genere un aspetto complesso della programmazione XML. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]semplifica e spazi dei nomi, eliminando la necessità di affrontare i prefissi dello spazio dei nomi. Se si desidera, è possibile controllare i prefissi di spazio dei nomi. Se tuttavia si decide di non controllare in modo esplicito i prefissi dello spazio dei nomi, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] assegnerà i prefissi dello spazio dei nomi durante la serializzazione, se sono necessari oppure eseguirà la serializzazione utilizzando spazi dei nomi predefinito se non lo sono. Se vengono utilizzati gli spazi dei nomi predefiniti, il documento risultante non conterrà prefissi di spazio dei nomi. Per ulteriori informazioni, vedere [utilizzo di spazi dei nomi XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
 Un altro problema di DOM è che non consente di modificare il nome di un nodo. È invece necessario creare un nuovo nodo e copiarvi tutti i nodi figlio, perdendo l'identità del nodo originale. [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]Per evitare questo problema consentendo di impostare il <xref:System.Xml.Linq.XName>proprietà su un nodo.</xref:System.Xml.Linq.XName>  
  
## <a name="static-method-support-for-loading-xml"></a>Supporto dei metodi statici per il caricamento di XML  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]Consente di caricare XML usando metodi statici, anziché metodi di istanza. semplificando le operazioni di caricamento e analisi. Per ulteriori informazioni, vedere [procedura: caricamento di XML da un File (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-load-xml-from-a-file.md).  
  
## <a name="removal-of-support-for-dtd-constructs"></a>Rimozione del supporto per i costrutti DTD  
 In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] la programmazione XML risulta ulteriormente semplificata tramite la rimozione del supporto per entità e riferimenti di entità. Oltre a essere complessa, la gestione di entità viene utilizzata raramente. Rimuovendone il supporto è possibile riscontrare un aumento delle prestazioni e un'interfaccia di programmazione semplificata. Quando un [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] albero viene popolato, tutte le entità DTD vengono espanse.  
  
## <a name="support-for-fragments"></a>Supporto per i frammenti  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]non fornisce un equivalente per la `XmlDocumentFragment` classe. In molti casi, tuttavia, il `XmlDocumentFragment` concetto può essere gestito dal risultato di una query tipizzata come <xref:System.Collections.Generic.IEnumerable%601>di <xref:System.Xml.Linq.XNode>, o <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Xml.Linq.XNode> </xref:System.Collections.Generic.IEnumerable%601>  
  
## <a name="support-for-xpathnavigator"></a>Supporto per XPathNavigator  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]fornisce il supporto per <xref:System.Xml.XPath.XPathNavigator>tramite metodi di estensione di <xref:System.Xml.XPath?displayProperty=fullName>dello spazio dei nomi.</xref:System.Xml.XPath?displayProperty=fullName> </xref:System.Xml.XPath.XPathNavigator> Per ulteriori informazioni, vedere <xref:System.Xml.XPath.Extensions?displayProperty=fullName>.</xref:System.Xml.XPath.Extensions?displayProperty=fullName>  
  
## <a name="support-for-white-space-and-indentation"></a>Supporto per lo spazio vuoto e il rientro  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]spazio vuoto viene gestito più agevolmente rispetto a DOM.  
  
 In uno scenario comune viene letto il codice XML rientrato, viene creata una struttura ad albero XML in memoria senza nodi di testo di tipo spazio vuoto (ossia senza conservare lo spazio vuoto), vengono eseguite alcune operazioni su XML e quindi l'XML viene salvato senza rientro. Quando si serializza l'XML con la formattazione, nell'albero XML viene conservato solo lo spazio vuoto significativo. Questo è il comportamento predefinito per [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
 In un altro scenario comune viene letto e modificato codice XML che è già stato intenzionalmente rientrato. È possibile che si desideri non modificare questo rientro in alcun modo. In [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] è possibile ottenere questo risultato conservando lo spazio vuoto durante il caricamento o l'analisi XML e disabilitando la formattazione durante la serializzazione XML.  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]spazio vuoto come viene archiviato un <xref:System.Xml.Linq.XText>nodo, anziché un specializzato <xref:System.Xml.XmlNodeType>tipo di nodo, come il DOM viene.</xref:System.Xml.XmlNodeType> </xref:System.Xml.Linq.XText>  
  
## <a name="support-for-annotations"></a>Supporto per le annotazioni  
 Gli elementi [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] supportano un set estensibile di annotazioni. Questa funzione è utile per tenere traccia di varie informazioni su un elemento, ad esempio informazioni sullo schema, informazioni su se l'elemento è associato a un'interfaccia utente o altri tipi di informazioni specifiche dell'applicazione. Per ulteriori informazioni, vedere [annotazioni LINQ to XML](http://msdn.microsoft.com/library/e2f0052d-61e2-48d4-9ea4-356c9cab35d5).  
  
## <a name="support-for-schema-information"></a>Supporto per le informazioni sullo schema  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]fornisce il supporto per la convalida XSD tramite metodi di estensione di <xref:System.Xml.Schema?displayProperty=fullName>dello spazio dei nomi.</xref:System.Xml.Schema?displayProperty=fullName> È possibile verificare che un albero XML sia conforme a un XSD. È possibile popolare l'albero XML con le informazioni sulla convalida post-schema. Per ulteriori informazioni, vedere [procedura: convalidare XSD utilizzando](http://msdn.microsoft.com/library/481a97fa-6e96-46f2-8c9a-415555fac33b) e <xref:System.Xml.Schema.Extensions>.</xref:System.Xml.Schema.Extensions>  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/getting-started-linq-to-xml.md)
