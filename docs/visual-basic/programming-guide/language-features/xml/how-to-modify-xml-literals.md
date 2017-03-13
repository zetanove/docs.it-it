---
title: "How to: Modify XML Literals (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML axis [Visual Basic], Value"
  - "XML literals [Visual Basic]"
  - "XML literals [Visual Basic], modifying"
ms.assetid: 4e864522-a37a-43a2-8236-af80277c5482
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# How to: Modify XML Literals (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente di modificare agevolmente i valori letterali XML.  È possibile aggiungere o eliminare elementi e attributi nonché sostituire un elemento esistente con un nuovo elemento XML.  In questo argomento vengono forniti molti esempi di come modificare un valore letterale XML esistente.  
  
### Modificare il valore di un valore letterale XML  
  
1.  Per modificare il valore di un valore letterale XML, ottenere un riferimento al valore letterale XML e impostare la proprietà `Value` sul valore desiderato.  
  
     Nell'esempio di codice seguente viene illustrato come aggiornare il valore di tutti gli elementi \<Price\> in un documento XML.  
  
     [!code-vb[VbXmlSamples2#4](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_1.vb)]  
  
     Di seguito vengono illustrati il codice XML di origine e quello modificato, derivati dall'esempio.  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>47.20</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>48.25</Price>  
      </Book>  
    </Catalog>  
    ```  
  
    > [!NOTE]
    >  La proprietà `Value` si riferisce al primo elemento XML in una raccolta.  Se nella raccolta sono presenti più elementi che hanno lo stesso nome, l'impostazione della proprietà `Value` ha effetto solo sul primo elemento nella raccolta.  
  
### Per aggiungere un attributo a un valore letterale XML  
  
1.  Per aggiungere un attributo a un valore letterale XML, ottenere innanzi tutto un riferimento al valore letterale XML.  È quindi possibile aggiungere un attributo aggiungendo una nuova proprietà axis dell'attributo XML.  È anche possibile aggiungere un nuovo oggetto <xref:System.Xml.Linq.XAttribute> al valore letterale XML tramite il metodo <xref:System.Xml.Linq.XContainer.Add%2A>.  Nell'esempio seguente vengono illustrate entrambe le opzioni.  
  
     [!code-vb[VbXmlSamples2#5](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_2.vb)]  
  
     Di seguito vengono illustrati il codice XML di origine e quello modificato, derivati dall'esempio.  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" >  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
    ```  
  
     Per ulteriori informazioni sulle proprietà axis degli attributi XML, vedere [XML Attribute Axis Property](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md).  
  
### Per aggiungere un elemento a un valore letterale XML  
  
1.  Per aggiungere un elemento a un valore letterale XML, ottenere innanzi tutto un riferimento al valore letterale XML.  È quindi possibile aggiungere un nuovo oggetto <xref:System.Xml.Linq.XElement> come ultimo sottoelemento dell'elemento utilizzando il metodo <xref:System.Xml.Linq.XContainer.Add%2A>.  Poi è possibile aggiungere un nuovo oggetto <xref:System.Xml.Linq.XElement> come primo sottoelemento dell'elemento utilizzando il metodo <xref:System.Xml.Linq.XContainer.AddFirst%2A>.  
  
     Per aggiungere un elemento nuovo in un percorso specifico rispetto agli altri sottoelementi, prima ottenere un riferimento a un sottoelemento adiacente.  È quindi possibile aggiungere un nuovo oggetto <xref:System.Xml.Linq.XElement> prima del sottoelemento adiacente utilizzando il metodo <xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>.  È anche possibile aggiungere un nuovo oggetto <xref:System.Xml.Linq.XElement> dopo il sottoelemento adiacente utilizzando il metodo <xref:System.Xml.Linq.XNode.AddAfterSelf%2A>.  
  
     Ognuna di queste tecniche è illustrata negli esempi seguenti:  
  
     [!code-vb[VbXmlSamples2#6](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_3.vb)]  
  
     Di seguito vengono illustrati il codice XML di origine e quello modificato, derivati dall'esempio.  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" >  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" >  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk000"></Book>  
      <Book id="bk331">  
        <Publisher>Microsoft Press</Publisher>  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
        <PublishDate>2005-2-14</PublishDate>  
      </Book>  
      <Book id="bk999"></Book>  
    </Catalog>  
    ```  
  
### Rimuovere un elemento o un attributo da un valore letterale XML.  
  
1.  Per rimuovere un elemento o un attributo da un valore letterale XML, ottenere un riferimento all'elemento o attributo e chiamare il metodo `Remove`, come illustrato nell'esempio seguente.  
  
     [!code-vb[VbXmlSamples2#7](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_4.vb)]  
  
     Di seguito vengono illustrati il codice XML di origine e quello modificato, derivati dall'esempio.  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" genre="Computer" editorEmail="someone@example.com">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk000"></Book>  
      <Book id="bk331" genre="Computer" editorEmail="someone@example.com">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book>  
      <Book id="bk999"></Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101" editorEmail="someone@example.com">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
      </Book>  
      <Book id="bk000"></Book>  
      <Book id="bk331" editorEmail="someone@example.com">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
      </Book> </Catalog>  
    ```  
  
     Per rimuovere tutti gli elementi o attributi da un valore letterale XML, ottenere un riferimento al valore letterale XML e chiamare il metodo <xref:System.Xml.Linq.XElement.RemoveAll%2A>.  
  
### Modificare un valore letterale XML  
  
1.  Per modificare il nome di un elemento XML, innanzi tutto ottenere un riferimento all'elemento.  È quindi possibile creare un nuovo oggetto <xref:System.Xml.Linq.XElement>che ha un nuovo nome e passa il nuovo oggetto <xref:System.Xml.Linq.XElement> al metodo <xref:System.Xml.Linq.XNode.ReplaceWith%2A> dell'oggetto <xref:System.Xml.Linq.XElement> esistente.  
  
     Se l'elemento che si sta sostituendo ha sottoelementi che devono essere mantenuti, impostare il valore del nuovo oggetto <xref:System.Xml.Linq.XElement> sulla proprietà <xref:System.Xml.Linq.XContainer.Nodes%2A> dell'elemento esistente.  In tal modo si imposterà il valore del nuovo elemento sull'XML interno dell'elemento esistente.  In alternativa, è possibile impostare il valore del nuovo elemento sulla proprietà `Value` dell'elemento esistente.  
  
     Nell'esempio di codice seguente vengono sostituiti tutti gli elementi \<Description\> con un elemento \<Abstract\>.  Il contenuto dell'elemento \<Description\> viene mantenuto nel nuovo elemento \<Abstract\> utilizzando la proprietà <xref:System.Xml.Linq.XContainer.Nodes%2A> dell'oggetto <xref:System.Xml.Linq.XElement>. di \<Description\>  
  
     [!code-vb[VbXmlSamples2#8](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_5.vb)]  
  
     Di seguito vengono illustrati il codice XML di origine e quello modificato, derivati dall'esempio.  
  
    ```  
    Source XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <Price>44.95</Price>  
        <Description>  
          An in-depth look at creating applications  
          with <technology>XML</technology>. For   
          <audience>beginners</audience> or   
          <audience>advanced</audience> developers.  
        </Description>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <Price>45.95</Price>  
        <Description>  
          Get the expert insights, practical code samples, and best  
          practices you need to advance your expertise with   
          <technology>Visual Basic .NET</technology>.   
          Learn how to create faster, more reliable applications  
          based on professional, pragmatic guidance by today's top  
          <audience>developers</audience>.  
        </Description>  
      </Book>  
    </Catalog>  
  
    Modified XML:  
    <?xml version="1.0"?>  
    <Catalog>  
      <Book id="bk101">  
        <Author>Garghentini, Davide</Author>  
        <Title>XML Developer's Guide</Title>  
        <MSRP>44.95</MSRP>     <Abstract>  
          An in-depth look at creating applications  
          with <technology>XML</technology>. For   
          <audience>beginners</audience> or   
          <audience>advanced</audience> developers.  
        </Abstract>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <MSRP>45.95</MSRP>     <Abstract>  
          Get the expert insights, practical code samples, and best  
          practices you need to advance your expertise with   
          <technology>Visual Basic .NET</technology>.   
          Learn how to create faster, more reliable applications  
          based on professional, pragmatic guidance by today's top  
          <audience>developers</audience>.  
        </Abstract>  
      </Book>  
    </Catalog>  
    ```  
  
## Vedere anche  
 [Manipulating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [How to: Load XML from a File, String, or Stream](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)