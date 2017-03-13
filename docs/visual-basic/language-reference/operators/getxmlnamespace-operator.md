---
title: "GetXmlNamespace Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.GetXmlNamespace"
  - "GetXmlNamespace"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "GetXmlNamespace operator"
  - "GetXmlNamespace keyword"
ms.assetid: d0d28cfd-0755-4896-ae0b-4981aa35517c
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# GetXmlNamespace Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Ottiene l'oggetto <xref:System.Xml.Linq.XNamespace> che corrisponde al prefisso dello spazio dei nomi XML specificato.  
  
## Sintassi  
  
```  
GetXmlNamespace(xmlNamespacePrefix)  
```  
  
## Parti  
 `xmlNamespacePrefix`  
 Parametro facoltativo.  Stringa che identifica il prefisso dello spazio dei nomi XML.  Se viene fornita, questa stringa deve essere un identificatore XML valido.  Per ulteriori informazioni, vedere [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).  Se non viene specificato alcun prefisso, verrà restituito lo spazio dei nomi predefinito.  Se non è specificato uno spazio dei nomi predefinito, verrà restituito lo spazio dei nomi vuoto.  
  
## Valore restituito  
 Oggetto <xref:System.Xml.Linq.XNamespace> che corrisponde al prefisso dello spazio dei nomi XML.  
  
## Note  
 L'operatore `GetXmlNamespace` ottiene l'oggetto <xref:System.Xml.Linq.XNamespace> che corrisponde al prefisso dello spazio dei nomi XML `xmlNamespacePrefix`.  
  
 È possibile utilizzare i prefissi degli spazi dei nomi XML direttamente nei valori letterali XML e nelle proprietà axis XML.  Tuttavia, è necessario utilizzare l'operatore `GetXmlNamespace` per convertire un prefisso degli spazi dei nomi a un oggetto <xref:System.Xml.Linq.XNamespace> prima che sia possibile utilizzarlo nel codice.  È possibile aggiungere un nome dell'elemento non qualificato a un oggetto <xref:System.Xml.Linq.XNamespace> per ottenere un oggetto <xref:System.Xml.Linq.XName> completo, che viene richiesto da vari metodi [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)].  
  
## Esempio  
 Nell'esempio riportato di seguito viene importato `ns` come un prefisso dello spazio dei nomi XML.  Il prefisso dello spazio dei nomi viene quindi utilizzato per creare un valore letterale XML e accedere al primo nodo figlio che dispone del nome completo `ns:phone`.  Tale nodo figlio viene quindi passato alla subroutine `ShowName`, che costruisce un nome completo utilizzando l'operatore `GetXmlNamespace`.  La subroutine `ShowName` passa quindi il nome completo al metodo <xref:System.Xml.Linq.XNode.Ancestors%2A> per ottenere il nodo padre `ns:contact`.  
  
 [!code-vb[VbXMLSamples#38](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/getxmlnamespace-operator_1.vb)]  
  
 Quando viene chiamato `TestGetXmlNamespace.RunSample()`, viene visualizzata una finestra di messaggio che contiene il seguente testo:  
  
 `Name: Patrick Hines`  
  
## Vedere anche  
 [Imports Statement \(XML Namespace\)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Accessing XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)