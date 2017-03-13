---
title: "Valore letterale elemento XML (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlLiteralElement"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "valore letterale elemento XML [Visual Basic]"
  - "valore letterale elemento [Visual Basic]"
  - "Valori letterali XML [Visual Basic], elemento"
ms.assetid: 95039642-7893-48b7-b23f-45a6c55d8f67
caps.latest.revision: 32
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 32
---
# Valore letterale elemento XML (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un valore letterale che rappresenta un <xref:System.Xml.Linq.XElement> oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
<name [ attributeList ] />  
-or-  
<name [ attributeList ] > [ elementContents ] </[ name ]>  
```  
  
## <a name="parts"></a>Parti  
  
-   `<`  
  
     Obbligatorio. Apre il tag dell'elemento iniziale.  
  
-   `name`  
  
     Obbligatorio. Nome dell'elemento. Il formato è uno dei seguenti:  
  
    -   Testo letterale per il nome dell'elemento del modulo [`ePrefix``:`]`eName`, dove:  
  
        |||  
        |-|-|  
        |Parte|Descrizione|  
        |`ePrefix`|Facoltativo. Prefisso dello spazio dei nomi XML per l'elemento. Deve essere uno spazio dei nomi XML globale viene definito con un `Imports` istruzione nel file o a livello di progetto, o uno spazio dei nomi XML locale definito in questo elemento o un elemento padre.|  
        |`eName`|Obbligatorio. Nome dell'elemento. Il formato è uno dei seguenti:<br /><br /> -Testo letterale. Vedere [i nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).<br />-Espressione incorporata del formato `<%=` e`NameExp` `%>`. Il tipo di `eNameExp` deve essere `String` o un tipo convertibile in modo implicito per <xref:System.Xml.Linq.XName>.|  
  
    -   Espressione incorporata del formato `<%=` `nameExp` `%>`. Il tipo di `nameExp` deve essere `String` o un tipo convertibile in modo implicito <xref:System.Xml.Linq.XName>. Un'espressione incorporata non è consentita in un tag di chiusura di un elemento.  
  
-   `attributeList`  
  
     Facoltativo. Elenco di attributi dichiarato nel valore letterale.  
  
     `attribute [ attribute ... ]`  
  
     Ogni `attribute` ha una delle sintassi seguenti:  
  
    -   Assegnazione, nel formato di attributi [`aPrefix``:`]`aName``=``aValue`, dove:  
  
        |||  
        |-|-|  
        |Parte|Descrizione|  
        |`aPrefix`|Facoltativo. Prefisso dello spazio dei nomi XML per l'attributo. Deve essere uno spazio dei nomi XML globale viene definito con un `Imports` istruzione o uno spazio dei nomi XML locale definito in questo elemento o un elemento padre.|  
        |`aName`|Obbligatorio. Nome dell'attributo. Il formato è uno dei seguenti:<br /><br /> -Testo letterale. Vedere [i nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md).<br />-Espressione incorporata del formato `<%=` `aNameExp` `%>`. Il tipo di `aNameExp` deve essere `String` o un tipo convertibile in modo implicito per <xref:System.Xml.Linq.XName>.|  
        |`aValue`|Facoltativo. Valore dell'attributo. Il formato è uno dei seguenti:<br /><br /> -Testo letterale, racchiuso tra virgolette.<br />-Espressione incorporata del formato `<%=` `aValueExp` `%>`. È consentito qualsiasi tipo.|  
  
    -   Espressione incorporata del formato `<%=` `aExp` `%>`.  
  
-   `/>`  
  
     Facoltativo. Indica che l'elemento è un elemento vuoto, senza contenuto.  
  
-   `>`  
  
     Obbligatorio. Termina il tag dell'elemento iniziale o vuoto.  
  
-   `elementContents`  
  
     Facoltativo. Contenuto dell'elemento.  
  
     `content [ content ... ]`  
  
     Ogni `content` può essere uno dei seguenti:  
  
    -   Testo letterale. Tutti gli spazi vuoti in `elementContents` diventano significativi se è presente del testo letterale.  
  
    -   Espressione incorporata del formato `<%=` `contentExp` `%>`.  
  
    -   Valore letterale elemento XML.  
  
    -   Valore letterale commento XML. Vedere [valore letterale commento XML](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md).  
  
    -   Istruzione di elaborazione XML. Vedere [valore letterale istruzione di elaborazione XML](../../../visual-basic/language-reference/xml-literals/xml-processing-instruction-literal.md).  
  
    -   Valore letterale CDATA XML. Vedere [valore letterale CDATA XML](../../../visual-basic/language-reference/xml-literals/xml-cdata-literal.md).  
  
-   `</`[`name`]`>`  
  
     Parametro facoltativo. Rappresenta il tag di chiusura per l'elemento. Facoltativo `name` parametro non è consentito quando è il risultato di un'espressione incorporata.  
  
## <a name="return-value"></a>Valore restituito  
 Un <xref:System.Xml.Linq.XElement> oggetto.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare la sintassi del valore letterale elemento XML per creare <xref:System.Xml.Linq.XElement> oggetti nel codice.  
  
> [!NOTE]
>  Un valore letterale XML può occupare più righe senza utilizzare caratteri di continuazione di riga. Questa funzionalità consente di copiare il contenuto di un documento XML e incollarlo direttamente in un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] programma.  
  
 Le espressioni incorporate il formato `<%=` `exp` `%>` consentono di aggiungere informazioni dinamiche a un valore letterale elemento XML. Per ulteriori informazioni, vedere [espressioni incorporate in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md).  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] compilatore converte il valore letterale elemento XML in chiamate per il <xref:System.Xml.Linq.XElement.%23ctor%2A> costruttore e, se necessario, il <xref:System.Xml.Linq.XAttribute.%23ctor%2A> costruttore.  
  
## <a name="xml-namespaces"></a>Spazi dei nomi XML  
 Prefissi dello spazio dei nomi XML sono utili quando è necessario creare valori letterali XML con elementi dallo spazio dei nomi stesso numero di volte nel codice. È possibile utilizzare i prefissi dello spazio dei nomi XML globali, che può essere definito utilizzando il `Imports` istruzione o i prefissi locali, che può essere definito utilizzando il `xmlns:``xmlPrefix`= "`xmlNamespace`" sintassi degli attributi. Per ulteriori informazioni, vedere [istruzione Imports (spazio dei nomi XML)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md).  
  
 In base alle regole di ambito per gli spazi dei nomi XML, i prefissi locali hanno la precedenza sui prefissi globali. Tuttavia, se un valore letterale XML definisce uno spazio dei nomi XML, tale spazio dei nomi non è disponibile per le espressioni contenute in un'espressione incorporata. L'espressione incorporata può accedere solo i nomi XML globale.  
  
 Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] compilatore converte ogni spazio dei nomi XML globale utilizzato da un valore letterale XML in una definizione dello spazio dei nomi locale nel codice generato. Spazi dei nomi XML globali non utilizzati non vengono visualizzati nel codice generato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come creare un semplice elemento XML che ha due elementi vuoti nidificati.  
  
 [!code-vb[VbXMLSamples#20](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-element-literal_1.vb)]  
  
 L'esempio mostra il testo seguente. Si noti che il valore letterale mantiene la struttura degli elementi vuoti.  
  
```  
<outer>  
  <inner1></inner1>  
  <inner2 />  
</outer>  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare le espressioni incorporate per denominare un elemento e creare attributi.  
  
 [!code-vb[VbXMLSamples#21](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-element-literal_2.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
```  
<book isbn="1234" author="My Author" year="1999" title="My Book" />  
```  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene dichiarato `ns` come un prefisso dello spazio dei nomi XML. Quindi, il prefisso dello spazio dei nomi utilizzato per creare un file XML letterale e visualizza il formato dell'elemento finale.  
  
 [!code-vb[VbXMLSamples#22](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-element-literal_3.vb)]  
  
 Questo codice visualizza il testo seguente:  
  
```  
<ns:outer xmlns:ns="http://SomeNamespace">  
  <ns:middle xmlns:ns="http://NewNamespace">  
    <ns:inner1 />  
    <inner2 xmlns="http://SomeNamespace" />  
  </ns:middle>  
</ns:outer>  
```  
  
 Si noti che il compilatore converte il prefisso dello spazio dei nomi XML globali in una definizione del prefisso dello spazio dei nomi XML. L'elemento \< ns:middle > consente di ridefinire il prefisso dello spazio dei nomi XML per l'elemento \< ns:inner1 >. Tuttavia, l'elemento \< ns:inner2 > utilizza lo spazio dei nomi definito per il `Imports` istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Xml.Linq.XElement>   
 [Nomi di elementi e attributi XML dichiarati](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)   
 [Valore letterale commento XML](../../../visual-basic/language-reference/xml-literals/xml-comment-literal.md)   
 [Valore letterale CDATA XML](../../../visual-basic/language-reference/xml-literals/xml-cdata-literal.md)   
 [Valori letterali XML](../../../visual-basic/language-reference/xml-literals/index.md)   
 [Creazione di XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [Espressioni incorporate in XML](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [Istruzione Imports (spazio dei nomi XML)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)