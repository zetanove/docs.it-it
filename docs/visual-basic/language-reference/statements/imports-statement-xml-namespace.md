---
title: Imports (istruzione) (XML Namespace) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ImportsXmlns
dev_langs:
- VB
helpviewer_keywords:
- XML namespace [Visual Basic], importing
- imports [Visual Basic]
- Imports statement [Visual Basic]
- namespaces [Visual Basic], importing
ms.assetid: 1f4d50a6-08c7-4c2e-8206-ccae35fcd1b4
caps.latest.revision: 18
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
ms.openlocfilehash: 546168994973d19336f86f4b4e9ec566f0b9dd91
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="imports-statement-xml-namespace"></a>Istruzione Imports (spazio dei nomi XML)
Importa i prefissi dello spazio dei nomi XML da utilizzare nei valori letterali XML e le proprietà axis XML.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Imports <xmlns:xmlNamespacePrefix = "xmlNamespaceName">  
```  
  
## <a name="parts"></a>Parti  
 `xmlNamespacePrefix`  
 Facoltativo. La stringa da cui XML elementi e attributi possono fare riferimento a `xmlNamespaceName`. Se nessun `xmlNamespacePrefix` viene fornito, lo spazio dei nomi XML importato è lo spazio dei nomi XML predefinito. Deve essere un identificatore XML valido. Per ulteriori informazioni, vedere [attributi e i nomi di elementi XML dichiarato](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).  
  
 `xmlNamespaceName`  
 Obbligatorio. Stringa che identifica lo spazio dei nomi XML importato.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare il `Imports` istruzione per definire spazi dei nomi XML globali che è possibile utilizzare con i valori letterali XML e le proprietà axis XML o come parametri per il `GetXmlNamespace` operatore. (Per informazioni sull'utilizzo di `Imports` per importare un alias che può essere utilizzato in cui vengono utilizzati i nomi dei tipi nel codice, vedere [istruzione Imports (tipo e Namespace .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).) La sintassi per dichiarare uno spazio dei nomi XML utilizzando il `Imports` istruzione è identica alla sintassi utilizzata in XML. Pertanto, è possibile copiare una dichiarazione dello spazio dei nomi da un file XML e utilizzarlo in un `Imports` istruzione.  
  
 Prefissi dello spazio dei nomi XML sono utili quando si desidera creare ripetutamente elementi XML che lo stesso spazio dei nomi. Il prefisso dello spazio dei nomi XML dichiarati con la `Imports` istruzione è globale nel senso che è disponibile per tutto il codice nel file. È possibile utilizzarlo quando si creano valori letterali dell'elemento XML e quando si accede a proprietà axis XML. Per ulteriori informazioni, vedere [letterale elemento XML](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md) e [proprietà Axis XML](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md).  
  
 Se si definisce uno spazio dei nomi XML globale senza un prefisso dello spazio dei nomi (ad esempio, `Imports <xmlns="http://SomeNameSpace>"`), tale spazio dei nomi viene considerato lo spazio dei nomi XML predefinito. Spazio dei nomi XML predefinito viene utilizzato per qualsiasi valori letterali dell'elemento XML o una proprietà di asse attributo XML che non specificano in modo esplicito uno spazio dei nomi. Spazio dei nomi predefinito viene utilizzato anche se lo spazio dei nomi specificato è lo spazio dei nomi vuoto (ovvero, `xmlns=""`). Spazio dei nomi XML predefinito non è applicabile agli attributi XML nei valori letterali XML o alle proprietà di asse attributo XML che non dispongono di uno spazio dei nomi.  
  
 Spazi dei nomi XML definiti in un valore letterale XML, che vengono chiamati *spazi dei nomi XML locali*, hanno la precedenza su spazi dei nomi XML definiti per il `Imports` istruzione come globale. Spazi dei nomi XML definiti per il `Imports` istruzione hanno la precedenza su spazi dei nomi XML importati per un progetto di Visual Basic. Se un valore letterale XML definisce uno spazio dei nomi XML, tale spazio dei nomi locale non è applicabile per le espressioni incorporate.  
  
 Spazi dei nomi XML globali seguono le stesse regole di ambito e definizione di spazi dei nomi .NET Framework. Di conseguenza, è possibile includere un `Imports` istruzione per definire uno spazio dei nomi XML globale ovunque sia possibile importare uno spazio dei nomi .NET Framework. Questo include i file di codice e gli spazi dei nomi importato a livello di progetto. Per informazioni sugli spazi dei nomi importato a livello di progetto, vedere [pagina riferimenti, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic).  
  
 Ogni file di origine può contenere un numero qualsiasi di `Imports` istruzioni. Queste devono seguire le dichiarazioni di opzione, ad esempio il `Option Strict` istruzione essi devono precedere dichiarazioni di elementi di programmazione, ad esempio `Module` o `Class` istruzioni.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente importa uno spazio dei nomi XML predefinito e un spazio dei nomi XML identificato con il prefisso `ns`. Crea quindi i valori letterali XML che utilizzano entrambi gli spazi dei nomi.  
  
 [!code-vb[N. VbXMLSamples&45;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/imports-statement-xml-namespace_1.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
```xml  
<ns:outer xmlns="http://DefaultNamespace"   
          xmlns:ns="http://NewNamespace">  
  <ns:innerElement></ns:innerElement>  
  <siblingElement></siblingElement>  
  <innerElement />  
</ns:outer>  
```  
  
## <a name="example"></a>Esempio  
 L'esempio seguente importa il prefisso dello spazio dei nomi XML `ns`. Crea quindi un valore letterale XML che utilizza il prefisso dello spazio dei nomi e visualizza il formato dell'elemento finale.  
  
 [!code-vb[VbXMLSamples&#22;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/imports-statement-xml-namespace_2.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
```xml  
<ns:outer xmlns:ns="http://SomeNamespace">  
  <ns:middle xmlns:ns="http://NewNamespace">  
    <ns:inner1 />  
    <inner2 xmlns="http://SomeNamespace" />  
  </ns:middle>  
</ns:outer>  
```  
  
 Si noti che il compilatore converte il prefisso dello spazio dei nomi XML da un prefisso globale a una definizione del prefisso locale.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente importa il prefisso dello spazio dei nomi XML `ns`. Il prefisso dello spazio dei nomi viene quindi usato per creare un valore letterale XML e accedere al primo nodo figlio con il nome completo `ns:name`.  
  
 [!code-vb[&#19; VbXMLSamples](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/imports-statement-xml-namespace_3.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
 `Patrick Hines`  
  
## <a name="see-also"></a>Vedere anche  
 [Valore letterale elemento XML](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Proprietà Axis XML](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [Nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)   
 [Operatore GetXmlNamespace](../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)
