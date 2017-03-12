---
title: "How to: Transform XML by Using LINQ (Visual Basic) | Microsoft Docs"
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
  - "XML [Visual Basic], transforming"
  - "LINQ to XML [Visual Basic], transforming XML"
ms.assetid: 815687f4-0bc2-4c0b-adc6-d78744aa356f
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Transform XML by Using LINQ (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

[XML Literals](../../../../visual-basic/language-reference/xml-literals/index.md) rende più facile la lettura dell'XML da un'origine e lo trasforma in un nuovo formato XML.  È possibile utilizzare le query LINQ per recuperare il contenuto da trasformare, o modificare il contenuto di un documento esistente in un nuovo formato XML.  
  
 Nell'esempio in questo argomento viene trasformato il contenuto da un documento di origine XML a HTML, per visualizzarlo in un browser.  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Trasformare un documento XML  
  
1.  In Visual Studio, creare un nuovo progetto di Visual Basic. nel modello di progetto **Applicazione console**.  
  
2.  Fare doppio clic sul file Module1.vb creato nel progetto per modificare il codice Visual Basic.  Aggiungere il seguente codice a `Sub Main` del modulo `Module1`.  Questo codice crea il documento XML di origine come oggetto <xref:System.Xml.Linq.XDocument>.  
  
    ```vb#  
    Dim catalog =   
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
              Get the expert insights, practical code samples,   
              and best practices you need   
              to advance your expertise with <technology>Visual   
              Basic .NET</technology>.   
              Learn how to create faster, more reliable applications  
              based on professional,   
              pragmatic guidance by today's top <audience>developers</audience>.  
            </Description>  
          </Book>  
        </Catalog>  
    ```  
  
     [How to: Load XML from a File, String, or Stream](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md).  
  
3.  Dopo il codice per creare il documento XML di origine, aggiungere il codice seguente per recuperare tutti gli elementi \<Book\> dall'oggetto e trasformarli in un documento HTML.  L'elenco di elementi \<Book\> viene creato utilizzando una query LINQ che restituisce una raccolta di oggetti <xref:System.Xml.Linq.XElement> che contengono l'HTML trasformato.  È possibile utilizzare espressioni incorporate per inserire i valori dal documento di origine nel nuovo formato XML.  
  
     Il documento HTML risultante è scritto in un file utilizzando il metodo <xref:System.Xml.Linq.XElement.Save%2A>.  
  
    ```vb#  
    Dim htmlOutput =   
      <html>  
        <body>  
          <%= From book In catalog.<Catalog>.<Book>   
              Select <div>  
                       <h1><%= book.<Title>.Value %></h1>  
                       <h3><%= "By " & book.<Author>.Value %></h3>  
                        <h3><%= "Price = " & book.<Price>.Value %></h3>  
                        <h2>Description</h2>  
                        <%= TransformDescription(book.<Description>(0)) %>  
                        <hr/>  
                      </div> %>  
        </body>  
      </html>  
  
    htmlOutput.Save("BookDescription.html")  
    ```  
  
4.  Dopo `Sub Main` di `Module1`, aggiungere un nuovo metodo \(`Sub`\) per trasformare un nodo \<Description\> nel formato HTML specificato.  Questo metodo viene chiamato dal codice nel passaggio precedente e viene utilizzato per mantenere il formato degli elementi \<Description\>.  
  
     Questo metodo sostituisce i sottoelementi dell'elemento \<Description\> con HTML.  Il metodo `ReplaceWith` viene utilizzato per mantenere il percorso dei sottoelementi.  Il contenuto trasformato dell'elemento \<Description\> viene incluso in un elemento del paragrafo \(\<p\>\) HTML.  La proprietà <xref:System.Xml.Linq.XContainer.Nodes%2A> viene utilizzata per recuperare il contenuto trasformato dell'elemento \<Description\>.  In tal modo viene garantito che i sottoelementi vengano inclusi nel contenuto trasformato.  
  
     Aggiungere il codice riportato di seguito dopo `Sub Main` di `Module1`.  
  
    ```vb#  
    Public Function TransformDescription(ByVal desc As XElement) As XElement  
  
      ' Replace <technology> elements with <b>.  
      Dim content = (From element In desc...<technology>).ToList()  
  
      If content.Count > 0 Then  
        For i = 0 To content.Count - 1  
          content(i).ReplaceWith(<b><%= content(i).Value %></b>)  
        Next  
      End If  
  
      ' Replace <audience> elements with <i>.  
      content = (From element In desc...<audience>).ToList()  
  
      If content.Count > 0 Then  
        For i = 0 To content.Count - 1  
          content(i).ReplaceWith(<i><%= content(i).Value %></i>)  
        Next  
      End If  
  
      ' Return the updated contents of the <Description> element.  
      Return <p><%= desc.Nodes %></p>  
    End Function  
    ```  
  
5.  Salvare le modifiche.  
  
6.  Premere F5 per eseguire il codice.  Il documento salvato risultante sarà simile al seguente:  
  
    ```  
    <?xml version="1.0"?>  
    <html>  
      <body>  
        <div>  
          <h1>XML Developer's Guide</h1>  
          <h3>By Garghentini, Davide</h3>  
          <h3>Price = 44.95</h3>  
          <h2>Description</h2>  
          <p>  
            An in-depth look at creating applications  
            with <b>XML</b>. For   
            <i>beginners</i> or   
            <i>advanced</i> developers.  
          </p>  
          <hr />  
        </div>  
        <div>  
          <h1>Developing Applications with Visual Basic .NET</h1>  
          <h3>By Spencer, Phil</h3>  
          <h3>Price = 45.95</h3>  
          <h2>Description</h2>  
          <p>  
            Get the expert insights, practical code   
            samples, and best practices you need   
            to advance your expertise with <b>Visual   
            Basic .NET</b>. Learn how to create faster,  
            more reliable applications based on  
            professional, pragmatic guidance by today's   
            top <i>developers</i>.  
          </p>  
          <hr />  
        </div>  
      </body>  
    </html>  
    ```  
  
## Vedere anche  
 [XML Literals](../../../../visual-basic/language-reference/xml-literals/index.md)   
 [Manipulating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [How to: Load XML from a File, String, or Stream](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)