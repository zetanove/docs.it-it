---
title: 'Procedura: caricare XML da un File, stringa o flusso (Visual Basic) | Documenti di Microsoft'
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
- XML [Visual Basic], loading
- LINQ to XML [Visual Basic], loading XML from files
ms.assetid: 2b02dcec-4cca-4575-b4ad-89ceb87b984c
caps.latest.revision: 13
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 242c8b79cbe1329b6f53e9fd4e5495d4a157e08c
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-load-xml-from-a-file-string-or-stream-visual-basic"></a>Procedura: caricare XML da un file, da una stringa o da un flusso (Visual Basic)
È possibile creare [valori letterali XML](../../../../visual-basic/language-reference/xml-literals/index.md) e popolarli con i contenuti da un'origine esterna, ad esempio un file, una stringa o un flusso, utilizzando vari metodi. Questi metodi sono illustrati negli esempi seguenti.  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-load-xml-from-a-file"></a>Per caricare XML da un file  
  
-   Per popolare un valore letterale XML come un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>oggetto da un file, utilizzare il `Load` (metodo).</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> Questo metodo può richiedere un percorso del file, un flusso di testo o flusso XML come input.  
  
     Esempio di codice seguente viene illustrato l'utilizzo di <xref:System.Xml.Linq.XDocument.Load%28System.String%29>metodo per popolare un <xref:System.Xml.Linq.XDocument>oggetto con XML da un file di testo.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XDocument.Load%28System.String%29>  
  
     [!code-vb[VbXMLSamples&#43;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-load-xml-from-a-file-string-or-stream_1.vb)]  
  
### <a name="to-load-xml-from-a-string"></a>Per caricare XML da una stringa  
  
-   Per popolare un valore letterale XML come un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>dell'oggetto da una stringa, è possibile utilizzare il `Parse` (metodo).</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
     Esempio di codice seguente viene illustrato l'utilizzo di <xref:System.Xml.Linq.XDocument.Parse%28System.String%29?displayProperty=fullName>metodo per popolare un <xref:System.Xml.Linq.XDocument>oggetto con XML da una stringa.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XDocument.Parse%28System.String%29?displayProperty=fullName>  
  
     [!code-vb[VbXMLSamples&#47;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-load-xml-from-a-file-string-or-stream_2.vb)]  
  
### <a name="to-load-xml-from-a-stream"></a>Per caricare XML da un flusso  
  
-   Per popolare un valore letterale XML come un <xref:System.Xml.Linq.XElement>o <xref:System.Xml.Linq.XDocument>dell'oggetto da un flusso, è possibile utilizzare il `Load` metodo o <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=fullName>(metodo).</xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=fullName> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
 Esempio di codice seguente viene illustrato l'utilizzo di <xref:System.Xml.Linq.XNode.ReadFrom%2A>metodo per popolare un <xref:System.Xml.Linq.XDocument>oggetto con XML da un flusso XML.</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XNode.ReadFrom%2A>  
  
 [!code-vb[VbXMLSamples n.&46;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-load-xml-from-a-file-string-or-stream_3.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName>   
 <xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=fullName></xref:System.Xml.Linq.XNode.ReadFrom%2A?displayProperty=fullName>   
 [Valori letterali XML](../../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [Modifica di XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)

