---
title: Cenni preliminari sulla classe XDocument (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 45cb7e71-196a-47da-bfe9-7a5589db1eed
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
ms.openlocfilehash: 31111b23adb019aad3ad55787c073dc02446291d
ms.lasthandoff: 03/13/2017

---
# <a name="xdocument-class-overview-visual-basic"></a>Cenni preliminari sulla classe XDocument (Visual Basic)
In questo argomento introduce la <xref:System.Xml.Linq.XDocument>classe.</xref:System.Xml.Linq.XDocument>  
  
## <a name="overview-of-the-xdocument-class"></a>Cenni preliminari sulla classe XDocument  
 La <xref:System.Xml.Linq.XDocument>classe contiene le informazioni necessarie per un documento XML valido.</xref:System.Xml.Linq.XDocument> ovvero una dichiarazione XML, istruzioni di elaborazione e commenti.  
  
 Si noti che è necessario solo creare <xref:System.Xml.Linq.XDocument>oggetti se richiesta la funzionalità specifica fornita dalla <xref:System.Xml.Linq.XDocument>classe.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XDocument> In molti casi, è possibile utilizzare direttamente con <xref:System.Xml.Linq.XElement>.</xref:System.Xml.Linq.XElement> Utilizzo diretto di <xref:System.Xml.Linq.XElement>è un modello di programmazione più semplice.</xref:System.Xml.Linq.XElement>  
  
 <xref:System.Xml.Linq.XDocument>deriva da <xref:System.Xml.Linq.XContainer>.</xref:System.Xml.Linq.XContainer></xref:System.Xml.Linq.XDocument> pertanto può contenere nodi figlio. Tuttavia, <xref:System.Xml.Linq.XDocument>gli oggetti possono avere un solo elemento figlio <xref:System.Xml.Linq.XElement>nodo.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> in conformità allo standard XML, secondo il quale un documento XML può contenere un unico elemento radice.  
  
## <a name="components-of-xdocument"></a>Componenti di XDocument  
 Un <xref:System.Xml.Linq.XDocument>può contenere i seguenti elementi:</xref:System.Xml.Linq.XDocument>  
  
-   Un <xref:System.Xml.Linq.XDeclaration>oggetto.</xref:System.Xml.Linq.XDeclaration> <xref:System.Xml.Linq.XDeclaration>Consente di specificare le parti pertinenti di una dichiarazione XML: la versione XML, la codifica del documento, e se il documento XML è autonomo.</xref:System.Xml.Linq.XDeclaration>  
  
-   Un <xref:System.Xml.Linq.XElement>oggetto.</xref:System.Xml.Linq.XElement> Si tratta del nodo radice del documento XML.  
  
-   Un numero qualsiasi di <xref:System.Xml.Linq.XProcessingInstruction>oggetti.</xref:System.Xml.Linq.XProcessingInstruction> Un'istruzione di elaborazione comunica informazioni a un'applicazione che elabora l'XML.  
  
-   Un numero qualsiasi di <xref:System.Xml.Linq.XComment>oggetti.</xref:System.Xml.Linq.XComment> I commenti saranno elementi di pari livello dell'elemento radice. Il <xref:System.Xml.Linq.XComment>oggetto non può essere il primo argomento nell'elenco perché non è valido per un documento XML per iniziare con un commento.</xref:System.Xml.Linq.XComment>  
  
-   Un <xref:System.Xml.Linq.XDocumentType>per DTD.</xref:System.Xml.Linq.XDocumentType>  
  
 Quando si serializza un <xref:System.Xml.Linq.XDocument>, anche se `XDocument.Declaration` è `null`, l'output includerà una dichiarazione XML se il writer `Writer.Settings.OmitXmlDeclaration` impostato su `false` (predefinito).</xref:System.Xml.Linq.XDocument>  
  
 Per impostazione predefinita, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] imposta la versione su "1.0" e la codifica su "utf-8".  
  
## <a name="using-xelement-without-xdocument"></a>Uso di XElement senza XDocument  
 Come accennato in precedenza, il <xref:System.Xml.Linq.XElement>è la classe principale nel [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] interfaccia di programmazione.</xref:System.Xml.Linq.XElement> In molti casi l'applicazione non richiederà la creazione di un documento. Utilizzando la <xref:System.Xml.Linq.XElement>classe, creare una struttura ad albero XML, aggiungervi altri alberi XML, modificare la struttura ad albero XML e salvare tale</xref:System.Xml.Linq.XElement>  
  
## <a name="using-xdocument"></a>Uso di XDocument  
 Per costruire un <xref:System.Xml.Linq.XDocument>, usare la costruzione funzionale, proprio come si trattasse di costruire <xref:System.Xml.Linq.XElement>oggetti.</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument>  
  
 Il codice seguente crea un <xref:System.Xml.Linq.XDocument>oggetto e relativi oggetti contenuti associati.</xref:System.Xml.Linq.XDocument>  
  
```vb  
Dim doc As XDocument = <?xml version="1.0" encoding="utf-8"?>  
                       <!--This is a comment.-->  
                       <?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>  
                       <Pubs>  
                           <Book>  
                               <Title>Artifacts of Roman Civilization</Title>  
                               <Author>Moreno, Jordao</Author>  
                           </Book>  
                           <Book>  
                               <Title>Midieval Tools and Implements</Title>  
                               <Author>Gazit, Inbar</Author>  
                           </Book>  
                       </Pubs>  
                       <!--This is another comment.-->  
doc.Save("test.xml")  
```  
  
 Quando si esamina il file test.xml, si ottiene l'output seguente:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!--This is a comment.-->  
<?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>  
<Pubs>  
  <Book>  
    <Title>Artifacts of Roman Civilization</Title>  
    <Author>Moreno, Jordao</Author>  
  </Book>  
  <Book>  
    <Title>Midieval Tools and Implements</Title>  
    <Author>Gazit, Inbar</Author>  
  </Book>  
</Pubs>  
<!--This is another comment.-->  
```  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Cenni preliminari sulla programmazione XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
