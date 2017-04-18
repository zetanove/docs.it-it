---
title: 'Procedura: modificare valori letterali XML (Visual Basic) | Documenti di Microsoft'
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
helpviewer_keywords:
- XML axis [Visual Basic], Value
- XML literals [Visual Basic]
- XML literals [Visual Basic], modifying
ms.assetid: 4e864522-a37a-43a2-8236-af80277c5482
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0ff2eba693862154d9c402748fb6797d10c4a1f8
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-modify-xml-literals-visual-basic"></a>Procedura: modificare valori letterali XML (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Consente di modificare valori letterali XML agevolmente. È possibile aggiungere o eliminare elementi e attributi ed è inoltre possibile sostituire un elemento esistente con un nuovo elemento XML. In questo argomento fornisce alcuni esempi di come modificare un valore letterale XML esistente.  
  
### <a name="to-modify-the-value-of-an-xml-literal"></a>Per modificare il valore di un valore letterale XML  
  
1.  Per modificare il valore di un valore letterale XML, ottenere un riferimento al codice XML letterale e impostare il `Value` proprietà sul valore desiderato.  
  
     Nell'esempio seguente aggiorna il valore di tutti i \<prezzo > elementi in un documento XML.  
  
     [!code-vb[VbXmlSamples2 n.&4;](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_1.vb)]  
  
     Di seguito viene illustrato XML di origine e quello modificato da questo esempio di codice.  
  
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
    >  Il `Value` proprietà fa riferimento al primo elemento XML in una raccolta. Se è presente più di un elemento che ha lo stesso nome in una raccolta, l'impostazione di `Value` proprietà influisce solo il primo elemento nella raccolta.  
  
### <a name="to-add-an-attribute-to-an-xml-literal"></a>Per aggiungere un attributo a un valore letterale XML  
  
1.  Per aggiungere un attributo a un valore letterale XML, ottenere prima un riferimento al valore letterale XML. È quindi possibile aggiungere un attributo mediante l'aggiunta di una nuova proprietà di asse attributo XML. È inoltre possibile aggiungere un nuovo <xref:System.Xml.Linq.XAttribute>oggetto per il valore letterale XML tramite il <xref:System.Xml.Linq.XContainer.Add%2A>(metodo).</xref:System.Xml.Linq.XContainer.Add%2A> </xref:System.Xml.Linq.XAttribute> Nell'esempio seguente viene illustrato entrambe le opzioni.  
  
     [!code-vb[VbXmlSamples2 n.&5;](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_2.vb)]  
  
     Di seguito viene illustrato XML di origine e quello modificato da questo esempio di codice.  
  
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
  
     Per ulteriori informazioni sulle proprietà axis dell'attributo XML, vedere [proprietà axis dell'attributo XML](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md).  
  
### <a name="to-add-an-element-to-an-xml-literal"></a>Per aggiungere un elemento a un valore letterale XML  
  
1.  Per aggiungere un elemento a un valore letterale XML, ottenere prima un riferimento al valore letterale XML. È quindi possibile aggiungere un nuovo <xref:System.Xml.Linq.XElement>oggetto come ultimo sottoelemento dell'elemento utilizzando il <xref:System.Xml.Linq.XContainer.Add%2A>(metodo).</xref:System.Xml.Linq.XContainer.Add%2A> </xref:System.Xml.Linq.XElement> È possibile aggiungere un nuovo <xref:System.Xml.Linq.XElement>oggetto come primo sottoelemento dell'elemento utilizzando il <xref:System.Xml.Linq.XContainer.AddFirst%2A>(metodo).</xref:System.Xml.Linq.XContainer.AddFirst%2A> </xref:System.Xml.Linq.XElement>  
  
     Per aggiungere un nuovo elemento in un percorso specifico rispetto agli altri sottoelementi, ottenere prima un riferimento a un sottoelemento adiacente. È quindi possibile aggiungere il nuovo <xref:System.Xml.Linq.XElement>oggetto prima del sottoelemento adiacente utilizzando il <xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>(metodo).</xref:System.Xml.Linq.XNode.AddBeforeSelf%2A> </xref:System.Xml.Linq.XElement> È inoltre possibile aggiungere il nuovo <xref:System.Xml.Linq.XElement>oggetto dopo il sottoelemento adiacente utilizzando il <xref:System.Xml.Linq.XNode.AddAfterSelf%2A>(metodo).</xref:System.Xml.Linq.XNode.AddAfterSelf%2A> </xref:System.Xml.Linq.XElement>  
  
     Nell'esempio seguente vengono illustrati esempi di ognuna di queste tecniche.  
  
     [!code-vb[6 VbXmlSamples2](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_3.vb)]  
  
     Di seguito viene illustrato XML di origine e quello modificato da questo esempio di codice.  
  
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
  
### <a name="to-remove-an-element-or-attribute-from-an-xml-literal"></a>Per rimuovere un elemento o attributo da un valore letterale XML  
  
1.  Per rimuovere un elemento o un attributo da un valore letterale XML, ottenere un riferimento per l'elemento o attributo e chiamare il `Remove` (metodo), come illustrato nell'esempio seguente.  
  
     [!code-vb[VbXmlSamples&#2;7](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_4.vb)]  
  
     Di seguito viene illustrato XML di origine e quello modificato da questo esempio di codice.  
  
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
      </Book></Catalog>  
    ```  
  
     Per rimuovere tutti gli elementi o attributi da un valore letterale XML, ottenere un riferimento al valore letterale XML e chiamare il <xref:System.Xml.Linq.XElement.RemoveAll%2A>(metodo).</xref:System.Xml.Linq.XElement.RemoveAll%2A>  
  
### <a name="to-modify-an-xml-literal"></a>Per modificare un valore letterale XML  
  
1.  Per modificare il nome di un elemento XML, ottenere prima un riferimento all'elemento. È quindi possibile creare un nuovo <xref:System.Xml.Linq.XElement>oggetto con un nuovo nome e passa il nuovo <xref:System.Xml.Linq.XElement>dell'oggetto per il <xref:System.Xml.Linq.XNode.ReplaceWith%2A>metodo dell'oggetto esistente <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XNode.ReplaceWith%2A> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement>  
  
     Se l'elemento che si sta sostituendo ha sottoelementi che devono essere mantenuti, impostare il valore del nuovo <xref:System.Xml.Linq.XElement>dell'oggetto per il <xref:System.Xml.Linq.XContainer.Nodes%2A>proprietà dell'elemento esistente.</xref:System.Xml.Linq.XContainer.Nodes%2A> </xref:System.Xml.Linq.XElement> Questo imposterà il valore del nuovo elemento per il codice XML interno dell'elemento esistente. In caso contrario, è possibile impostare il valore del nuovo elemento per il `Value` proprietà dell'elemento esistente.  
  
     Esempio di codice seguente sostituisce tutto \<descrizione > gli elementi con un \<astratta > elemento. Il contenuto di \<descrizione > elemento viene mantenuto nel nuovo \<astratta > elemento utilizzando la <xref:System.Xml.Linq.XContainer.Nodes%2A>proprietà del \<descrizione > <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XContainer.Nodes%2A>  
  
     [!code-vb[VbXmlSamples2 n.&8;](../../../../visual-basic/programming-guide/language-features/xml/codesnippet/VisualBasic/how-to-modify-xml-literals_5.vb)]  
  
     Di seguito viene illustrato XML di origine e quello modificato da questo esempio di codice.  
  
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
        <MSRP>44.95</MSRP>    <Abstract>  
          An in-depth look at creating applications  
          with <technology>XML</technology>. For   
          <audience>beginners</audience> or   
          <audience>advanced</audience> developers.  
        </Abstract>  
      </Book>  
      <Book id="bk331">  
        <Author>Spencer, Phil</Author>  
        <Title>Developing Applications with Visual Basic .NET</Title>  
        <MSRP>45.95</MSRP>    <Abstract>  
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
  
## <a name="see-also"></a>Vedere anche  
 [Modifica di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [Procedura: caricare XML da un File, stringa o flusso](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
