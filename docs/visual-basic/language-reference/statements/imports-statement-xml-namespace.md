---
title: "Imports Statement (XML Namespace) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ImportsXmlns"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "XML namespace [Visual Basic], importing"
  - "imports [Visual Basic]"
  - "Imports statement [Visual Basic]"
  - "namespaces [Visual Basic], importing"
ms.assetid: 1f4d50a6-08c7-4c2e-8206-ccae35fcd1b4
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Imports Statement (XML Namespace)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Importa i prefissi dello spazio dei nomi XML per l'utilizzo in valori letterali XML e proprietà axis XML.  
  
## Sintassi  
  
```  
Imports <xmlns:xmlNamespacePrefix = "xmlNamespaceName">  
```  
  
## Parti  
 `xmlNamespacePrefix`  
 Parametro facoltativo.  Stringa tramite cui gli elementi e gli attributi XML possono fare riferimento a `xmlNamespaceName`.  Se non viene fornito alcun `xmlNamespacePrefix`, lo spazio dei nomi XML importato è quello predefinito.  Deve essere un identificatore XML valido.  Per ulteriori informazioni, vedere [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).  
  
 `xmlNamespaceName`  
 Obbligatorio.  Stringa che identifica lo spazio dei nomi XML importato.  
  
## Note  
 È possibile utilizzare l'istruzione `Imports` per definire spazi dei nomi XML globali che possono venire utilizzati con valori letterali XML e proprietà axis XML oppure come parametri passati all'operatore `GetXmlNamespace`.  \(Per informazioni sull'utilizzo dell'istruzione `Imports` per importare un alias che può essere usato quando si utilizzano i nomi di tipo nel codice, vedere [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)\). La sintassi per dichiarare uno spazio dei nomi XML utilizzando l'istruzione `Imports` è identica alla sintassi utilizzata in XML.  Pertanto, è possibile copiare una dichiarazione dello spazio dei nomi da un file XML e usarla in un'istruzione `Imports`.  
  
 I prefissi dello spazio dei nomi XML sono utili quando si vuole creare ripetutamente elementi XML provenienti dallo stesso spazio dei nomi.  Il prefisso dello spazio dei nomi XML dichiarato con l'istruzione `Imports` è globale nel senso che è disponibile per tutto il codice nel file.  È possibile utilizzarlo quando si creano valori letterali di un elemento XML e quando si accede alle proprietà axis XML.  Per ulteriori informazioni, vedere [XML Element Literal](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md) e [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md).  
  
 Se si definisce uno spazio dei nomi XML globale senza un prefisso dello spazio dei nomi \(ad esempio, `Imports <xmlns="http://SomeNameSpace>"`\), tale spazio dei nomi viene considerato lo spazio dei nomi XML predefinito.  Lo spazio dei nomi XML predefinito viene utilizzato per qualsiasi valore letterale di un elemento XML o proprietà axis dell'attributo XML che non specificano in modo esplicito uno spazio dei nomi.  Viene utilizzato lo spazio dei nomi predefinito anche quando lo spazio dei nomi specificato è vuoto \(cioè, `xmlns=""`\).  Lo spazio dei nomi XML predefinito non viene applicato agli attributi XML nei valori letterali XML o alle proprietà axis dell'attributo XML che non hanno uno spazio dei nomi.  
  
 Gli *spazi dei nomi XML locali*, cioè gli spazi dei nomi XML definiti in un valore letterale XML, hanno la precedenza rispetto agli spazi dei nomi XML definiti globali dall'istruzione `Imports`.  Gli spazi dei nomi XML definiti dall'istruzione `Imports` hanno la precedenza rispetto agli spazi dei nomi XML importati per un progetto Visual Basic..  Se un valore letterale XML definisce uno spazio dei nomi XML, tale spazio dei nomi locale non si applica alle espressioni incorporate.  
  
 Gli spazi dei nomi XML globali seguono lo stesse regole di ambito e di definizione degli spazi dei nomi .NET Framework.  Di conseguenza, è possibile includere un'istruzione `Imports` per definire uno spazio dei nomi XML globale ovunque sia possibile importare uno spazio dei nomi .NET Framework.  Questo vale sia per i file di codice che per gli spazi dei nomi importati a livello di progetto.  Per ulteriori informazioni sugli spazi dei nomi importati a livello di progetto, vedere [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic).  
  
 Ogni file di origine può contenere un numero indefinito di istruzioni `Imports`.  Queste devono essere specificate dopo le dichiarazioni di opzione, come l'istruzione `Option Strict`, e devono precedere le dichiarazioni degli elementio di programmazione, come l'istruzione `Module` o `Class`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come importare uno spazio dei nomi XML predefinito e uno spazio dei nomi XML identificato con il prefisso `ns`.  Vengono quindi creati i valori letterali XML che utilizzano entrambi gli spazi dei nomi.  
  
 [!code-vb[VbXMLSamples#45](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/imports-statement-xml-na_1.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
```  
<ns:outer xmlns="http://DefaultNamespace"   
          xmlns:ns="http://NewNamespace">  
  <ns:innerElement></ns:innerElement>  
  <siblingElement></siblingElement>  
  <innerElement />  
</ns:outer>  
```  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene importato il prefisso `ns` dello spazio dei nomi.  Viene quindi creato un valore letterale XML che utilizza il prefisso dello spazio dei nomi e visualizza il formato finale dell'elemento.  
  
 [!code-vb[VbXMLSamples#22](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/imports-statement-xml-na_2.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
```  
<ns:outer xmlns:ns="http://SomeNamespace">  
  <ns:middle xmlns:ns="http://NewNamespace">  
    <ns:inner1 />  
    <inner2 xmlns="http://SomeNamespace" />  
  </ns:middle>  
</ns:outer>  
```  
  
 Il compilatore converte il prefisso dello spazio dei nomi XML da prefisso globale a una definizione del prefisso locale.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene importato il prefisso `ns` dello spazio dei nomi.  Viene quindi utilizzato il prefisso dello spazio dei nomi per creare un valore letterale XML e accedere al primo nodo figlio con il nome completo `ns:name`.  
  
 [!code-vb[VbXMLSamples#19](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/imports-statement-xml-na_3.vb)]  
  
 Verrà visualizzato il seguente testo:  
  
 `Patrick Hines`  
  
## Vedere anche  
 [XML Element Literal](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML Axis Properties](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [Names of Declared XML Elements and Attributes](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)   
 [GetXmlNamespace Operator](../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)