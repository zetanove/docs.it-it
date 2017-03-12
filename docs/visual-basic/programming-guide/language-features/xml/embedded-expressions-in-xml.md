---
title: "Embedded Expressions in XML (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.XmlEmbeddedExpression"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "embedded expressions [Visual Basic]"
  - "LINQ to XML [Visual Basic], embedded expressions"
  - "XML literals [Visual Basic], embedded expressions"
ms.assetid: bf2eb779-b751-4b7c-854f-9f2161482352
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Embedded Expressions in XML (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le espressioni incorporate consentono di creare valori letterali XML che contengono espressioni calcolate in fase di esecuzione.  La sintassi per un'espressione incorporata è `<%=` `expression` `%>`, che è la stessa sintassi utilizzata in [!INCLUDE[vstecasp](../../../../csharp/language-reference/preprocessor-directives/includes/vstecasp-md.md)].  
  
 Ad esempio, è possibile creare un valore letterale di un elemento XML combinando espressioni incorporate con contenuto di testo letterale.  
  
 [!code-vb[VbXMLSamples#27](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/embedded-expressions-in-_1.vb)]  
  
 Se `isbnNumber` contiene il numero intero 12345 e `modifiedDate` contiene la data 3\/5\/2006, quando questo codice viene eseguito, il valore di `book` è:  
  
```  
<book category="fiction" isbn="12345">  
  <modifiedDate>3/5/2006</modifiedDate>  
</book>  
```  
  
## Posizione e convalida delle espressioni incorporate  
 Le espressioni incorporate possono essere incluse solo in particolari posizioni all'interno di espressioni letterali XML.  La posizione nell'espressione controlla quali tipi possono venire restituiti dall'espressione e come viene gestito `Nothing`.  Nella tabella seguente vengono descritti le posizioni e i tipi di espressioni incorporate consentiti.  
  
||||  
|-|-|-|  
|Posizione in un valore letterale|Tipo di espressione|Gestione di `Nothing`|  
|Nome dell'elemento XML|<xref:System.Xml.Linq.XName>|delle modifiche a..."|  
|Contenuto dell'elemento XML|`Object` o matrice di `Object`|Ignorato|  
|Nome di attributo dell'elemento XML|<xref:System.Xml.Linq.XName>|Errore, a meno che anche il valore dell'attributo sia `Nothing`|  
|Valore dell'attributo dell'elemento XML|`Object`|Dichiarazione di un attributo ignorata.|  
|Attributo dell'elemento XML.|<xref:System.Xml.Linq.XAttribute> o una raccolta di <xref:System.Xml.Linq.XAttribute>|Ignorato|  
|Elemento radice del documento XML|Oggetto <xref:System.Xml.Linq.XElement> o una raccolta di un oggetto <xref:System.Xml.Linq.XElement> e un numero arbitrario di oggetti <xref:System.Xml.Linq.XProcessingInstruction> e oggetti <xref:System.Xml.Linq.XComment>|Ignorato|  
  
-   Esempio di espressione incorporata in un nome dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#32](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/embedded-expressions-in-_2.vb)]  
  
-   Esempio di espressione incorporata nel contenuto dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#33](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/embedded-expressions-in-_3.vb)]  
  
-   Esempio di espressione incorporata nel nome di attributo dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#34](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/embedded-expressions-in-_4.vb)]  
  
-   Esempio di espressione incorporata nel valore dell'attributo dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#35](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/embedded-expressions-in-_5.vb)]  
  
-   Esempio di espressione incorporata in un attributo dell'elemento XML:  
  
     [!code-vb[VbXMLSamples#36](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/embedded-expressions-in-_6.vb)]  
  
-   Esempio di espressione incorporata nell'elemento radice del documento XML:  
  
     [!code-vb[VbXMLSamples#37](../../../../visual-basic/language-reference/operators/codesnippet/visualbasic/embedded-expressions-in-_7.vb)]  
  
 Se si abilita `Option Strict`, il compilatore controlla che il tipo di ogni espressione incorporata venga convertito al tipo più ampio richiesto.  L'unica eccezione è per l'elemento radice di un documento XML, che viene verificato quando il codice è in esecuzione.  Se si compila senza `Option Strict`, è possibile incorporare espressioni di tipo `Object` e il tipo viene verificato in fase di esecuzione.  
  
 Nelle posizioni dove il contenuto èi facoltativo, le espressioni incorporate che contengono `Nothing` vengono ignorate.  Questo significa che non è necessario controllare che contenuto dell'elemento, i valori dell'attributo e gli elementi di una matrice non siano `Nothing` prima di utilizzare un valore letterale XML.  I valori richiesti, ad esempio nomi dell'elemento e dell'attributo, non possono essere `Nothing`.  
  
 Per ulteriori informazioni sull'utilizzo di un'espressione incorporata in un particolare tipo di valore letterale, vedere [XML Document Literal](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md), [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## Regole di ambito  
 Il compilatore converte ogni valore letterale XML in una chiamata del costruttore per il tipo di valore letterale adatto.  Il contenuto del valore letterale e le espressioni incorporate in un valore letterale XML vengono passati come argomenti al costruttore.  Questi significa che tutti gli elementi di programmazione di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] disponibili per un valore letterale XML sono anche disponibili per le espressioni incorporate.  
  
 All'interno di un valore letterale XML, è possibile accedere ai prefissi dello spazio dei nomi XML dichiarati con l'istruzione `Imports`.  È possibile dichiarare un nuovo prefisso dello spazio dei nomi XML, o nascondere un prefisso dello spazio dei nomi XML esistente, in un elemento utilizzando l'attributo `xmlns`.  Il nuovo spazio dei nomi è disponibile per i nodi figlio di tale elemento, ma non per i valori letterali XML nelle espressioni incorporate.  
  
> [!NOTE]
>  Quando si dichiara un prefisso dello spazio dei nomi XML utilizzando l'attributo dello spazio dei nomi `xmlns`, il valore dell'attributo deve essere una stringa costante.  In questo caso, l'utilizzo dell'attributo `xmlns` è simile all'utilizzo dell'istruzione `Imports` per dichiarare un spazio dei nomi XML.  Non è possibile utilizzare un'espressione incorporata per specificare il valore dello spazio dei nomi XML.  
  
## Vedere anche  
 [Creating XML in Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML Document Literal](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML Element Literal](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [XML Literals Overview](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)