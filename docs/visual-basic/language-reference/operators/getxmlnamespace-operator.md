---
title: Operatore GetXmlNamespace (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.GetXmlNamespace
- GetXmlNamespace
dev_langs:
- VB
helpviewer_keywords:
- GetXmlNamespace operator
- GetXmlNamespace keyword
ms.assetid: d0d28cfd-0755-4896-ae0b-4981aa35517c
caps.latest.revision: 14
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
ms.openlocfilehash: 929ba4edae9e155245228670424a3898896da807
ms.lasthandoff: 03/13/2017

---
# <a name="getxmlnamespace-operator-visual-basic"></a>Operatore GetXmlNamespace (Visual Basic)
Ottiene il <xref:System.Xml.Linq.XNamespace>oggetto che corrisponde al prefisso dello spazio dei nomi XML specificato.</xref:System.Xml.Linq.XNamespace>  
  
## <a name="syntax"></a>Sintassi  
  
```  
GetXmlNamespace(xmlNamespacePrefix)  
```  
  
## <a name="parts"></a>Parti  
 `xmlNamespacePrefix`  
 Facoltativo. Stringa che identifica il prefisso dello spazio dei nomi XML. Se fornito, questa stringa deve essere un identificatore XML valido. Per ulteriori informazioni, vedere [attributi e i nomi di elementi XML dichiarato](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md). Se non viene specificato alcun prefisso, viene restituito lo spazio dei nomi predefinito. Se viene specificato nessuno spazio dei nomi predefinito, viene restituito lo spazio dei nomi vuoto.  
  
## <a name="return-value"></a>Valore restituito  
 Il <xref:System.Xml.Linq.XNamespace>oggetto che corrisponde al prefisso dello spazio dei nomi XML.</xref:System.Xml.Linq.XNamespace>  
  
## <a name="remarks"></a>Note  
 Il `GetXmlNamespace` operatore ottiene il <xref:System.Xml.Linq.XNamespace>oggetto che corrisponde al prefisso dello spazio dei nomi XML `xmlNamespacePrefix`.</xref:System.Xml.Linq.XNamespace>  
  
 È possibile utilizzare i prefissi dello spazio dei nomi XML direttamente in valori letterali XML e le proprietà axis XML. Tuttavia, è necessario utilizzare il `GetXmlNamespace` per convertire un prefisso dello spazio dei nomi a un <xref:System.Xml.Linq.XNamespace>dell'oggetto prima che sia possibile utilizzarlo nel codice.</xref:System.Xml.Linq.XNamespace> È possibile aggiungere un nome di elemento non qualificato di un <xref:System.Xml.Linq.XNamespace>oggetto da ottenere un nome completo <xref:System.Xml.Linq.XName>dell'oggetto, quale molti [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] metodi richiedono.</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XNamespace>  
  
## <a name="example"></a>Esempio  
 L'esempio seguente importa `ns` come un prefisso dello spazio dei nomi XML. Viene quindi utilizzato il prefisso dello spazio dei nomi per creare valori letterali XML e accedere al primo nodo figlio con il nome completo `ns:phone`. Viene quindi passato come nodo figlio per il `ShowName` subroutine, che costruisce un nome completo utilizzando il `GetXmlNamespace` operatore. Il `ShowName` subroutine passa quindi il nome completo per il <xref:System.Xml.Linq.XNode.Ancestors%2A>per ottenere l'elemento padre `ns:contact` nodo.</xref:System.Xml.Linq.XNode.Ancestors%2A>  
  
 [!code-vb[VbXMLSamples&#38;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/getxmlnamespace-operator_1.vb)]  
  
 Quando si chiama `TestGetXmlNamespace.RunSample()`, viene visualizzata una finestra di messaggio che contiene il testo seguente:  
  
 `Name: Patrick Hines`  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Imports (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Accesso a XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
