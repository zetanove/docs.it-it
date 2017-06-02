---
title: "Convalida di un documento XML nel DOM | Microsoft Docs"
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
ms.assetid: 2c61c920-d0f8-4c72-bfcc-6524570f3060
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Convalida di un documento XML nel DOM
La classe <xref:System.Xml.XmlDocument> non esegue la convalida del codice XML nel DOM \(Document Object Model\) in base a uno schema XSD \(XML Schema Definition Language\) o a una DTD \(Document Type Definition\) per impostazione predefinita. Viene solo verificata la correttezza del formato XML.  
  
 Per eseguire la convalida del codice XML nel modello DOM, è possibile convalidare il codice XML durante il caricamento nel DOM passando una convalida dello schema <xref:System.Xml.XmlReader> al metodo <xref:System.Xml.XmlDocument.Load%2A> della classe <xref:System.Xml.XmlDocument> oppure convalidare un documento XML non convalidato in precedenza nel DOM usando il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>.  
  
## Convalida di un documento XML durante il caricamento nel DOM  
 La classe <xref:System.Xml.XmlDocument> convalida i dati XML durante il caricamento nel DOM quando un <xref:System.Xml.XmlReader> di convalida viene passato al metodo <xref:System.Xml.XmlDocument.Load%2A> della classe <xref:System.Xml.XmlDocument>.  
  
 Una volta eseguita la convalida, vengono applicati i valori predefiniti dello schema, i valori di testo vengono convertiti in valori di tipo atomic in base alle necessità e le informazioni sui tipi vengono associate agli elementi delle informazioni convalidate.  Di conseguenza, i dati XML tipizzati sostituiscono i dati XML in precedenza non tipizzati.  
  
### Creazione di un XmlReader di convalida di XML Schema  
 Per creare un tipo <xref:System.Xml.XmlReader> di convalida di XML Schema, attenersi alla seguente procedura.  
  
1.  Creare una nuova istanza di <xref:System.Xml.XmlReaderSettings>.  
  
2.  Aggiungere un XML Schema alla proprietà <xref:System.Xml.XmlReaderSettings.Schemas%2A> dell'istanza di <xref:System.Xml.XmlReaderSettings>.  
  
3.  Specificare `Schema` come proprietà <xref:System.Xml.XmlReaderSettings.ValidationType%2A>.  
  
4.  È possibile eventualmente specificare la proprietà <xref:System.Xml.XmlReaderSettings.ValidationFlags%2A> e un evento <xref:System.Xml.XmlReaderSettings.ValidationEventHandler> per gestire gli errori di convalida degli schemi e gli avvisi rilevati durante la convalida.  
  
5.  Infine, passare l'oggetto <xref:System.Xml.XmlReaderSettings> al metodo <xref:System.Xml.XmlReader.Create%2A> della classe <xref:System.Xml.XmlReader> insieme al documento XML, creando un tipo <xref:System.Xml.XmlReader> di convalida dello schema.  
  
### Esempio  
 Nell'esempio di codice seguente un tipo <xref:System.Xml.XmlReader> di convalida dello schema esegue la convalida dei dati XML caricati nel DOM.  Vengono apportate modifiche non valide al documento XML che viene quindi nuovamente convalidato, determinando errori di convalida dello schema.  Infine, uno degli errori viene corretto e quindi una parte del documento XML viene parzialmente convalidata.  
  
 [!code-cpp[XmlDocumentValidation.Load#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlDocumentValidation.Load/CPP/XmlDocumentValidationExample.cpp#1)]
 [!code-csharp[XmlDocumentValidation.Load#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlDocumentValidation.Load/CS/XmlDocumentValidationExample.cs#1)]
 [!code-vb[XmlDocumentValidation.Load#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlDocumentValidation.Load/VB/XmlDocumentValidationExample.vb#1)]  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Nell'esempio il file `contosoBooks.xsd` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
 Quando si convalidano i dati XML durante il caricamento nel DOM, è necessario prendere in considerazione quanto segue.  
  
-   Nell'esempio precedente, viene chiamato l'oggetto <xref:System.Xml.XmlReaderSettings.ValidationEventHandler> ogni volta che viene rilevato un tipo non valido.  Se non è impostato un oggetto <xref:System.Xml.XmlReaderSettings.ValidationEventHandler> sull'oggetto <xref:System.Xml.XmlReader> di convalida, quando viene chiamato <xref:System.Xml.XmlDocument.Load%2A> viene generata un'eccezione <xref:System.Xml.Schema.XmlSchemaValidationException> se un tipo di attributo o di elemento non corrisponde al tipo specificato nello schema di convalida.  
  
-   Quando un documento XML viene caricato in un oggetto <xref:System.Xml.XmlDocument> con uno schema associato che definisce valori predefiniti, l'oggetto <xref:System.Xml.XmlDocument> tratta tali valori predefiniti come se si trovassero nel documento XML.  Pertanto la proprietà <xref:System.Xml.XmlReader.IsEmptyElement%2A> restituisce sempre un valore `false` per un elemento ottenuto automaticamente dallo schema.  Anche se è incluso nel documento XML, è stato scritto come elemento vuoto.  
  
## Convalida di un documento XML nel DOM  
 Il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument> esegue la convalida dei dati XML caricati nel DOM in base agli schemi nella proprietà <xref:System.Xml.XmlDocument.Schemas%2A> dell'oggetto <xref:System.Xml.XmlDocument>.  Una volta eseguita la convalida, vengono applicati i valori predefiniti dello schema, i valori di testo vengono convertiti in valori di tipo atomic in base alle necessità e le informazioni sui tipi vengono associate agli elementi delle informazioni convalidate.  Di conseguenza, i dati XML tipizzati sostituiscono i dati XML in precedenza non tipizzati.  
  
 L'esempio seguente è simile a quello riportato sopra in "Convalida di un documento XML durante il caricamento nel DOM".  In questo esempio, il documento XML non viene convalidato durante il caricamento nel DOM, bensì dopo che è stato caricato nel DOM usando il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>.  Il metodo <xref:System.Xml.XmlDocument.Validate%2A> esegue la convalida del documento XML in base agli schemi XML contenuti nella proprietà <xref:System.Xml.XmlDocument.Schemas%2A> del <xref:System.Xml.XmlDocument>.  Vengono apportate modifiche non valide al documento XML che viene quindi riconvalidato, determinando errori di convalida dello schema.  Infine, uno degli errori viene corretto e quindi una parte del documento XML viene parzialmente convalidata.  
  
 [!code-csharp[XmlDocumentValidation.Validate#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlDocumentValidation.Validate/CS/XmlDocumentValidationExample.cs#1)]
 [!code-vb[XmlDocumentValidation.Validate#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlDocumentValidation.Validate/VB/XmlDocumentValidationExample.vb#1)]  
  
 Nell'esempio vengono accettati come input i file `contosoBooks.xml` e `contosoBooks.xsd` a cui si fa riferimento in "Convalida di un documento XML durante il caricamento nel DOM".  
  
## Gestione degli errori di convalida e degli avvisi  
 Gli errori di convalida di XML Schema vengono segnalati durante la convalida dei dati XML caricati nel DOM.  Viene inviata una notifica per tutti gli errori di convalida dello schema rilevati durante la convalida dei dati XML in fase di caricamento o durante la convalida di un documento XML non convalidato in precedenza.  
  
 Gli errori di convalida sono gestiti dal tipo <xref:System.Xml.Schema.ValidationEventHandler>.  Se un tipo <xref:System.Xml.Schema.ValidationEventHandler> è stato assegnato all'istanza di <xref:System.Xml.XmlReaderSettings> o passato al metodo<xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>, il <xref:System.Xml.Schema.ValidationEventHandler> gestirà gli errori di convalida degli schemi. In caso contrario, viene generata un'eccezione <xref:System.Xml.Schema.XmlSchemaValidationException> quando viene rilevato un errore di convalida.  
  
> [!NOTE]
>  I dati XML vengono caricati nel DOM indipendentemente dagli errori di convalida dello schema, a meno che il tipo <xref:System.Xml.Schema.ValidationEventHandler> non generi un'eccezione che interrompe il processo.  
>   
>  Non vengono segnalati avvisi di convalida dello schema, a meno che non sia stato specificato il flag <xref:System.Xml.Schema.XmlSchemaValidationFlags> nell'oggetto <xref:System.Xml.XmlReaderSettings>.  
  
 Per gli esempi che illustrano il tipo <xref:System.Xml.Schema.ValidationEventHandler>, vedere "Convalida di un documento XML durante il caricamento nel DOM" e "Convalida di un documento XML nel DOM" riportati in precedenza.  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XmlReader>   
 <xref:System.Xml.Schema.ValidationEventHandler>   
 <xref:System.Xml.XmlReaderSettings>   
 [Elaborazione di dati XML con il modello DOM](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)   
 [Utilizzo di schemi XML](../../../../docs/standard/data/xml/working-with-xml-schemas.md)