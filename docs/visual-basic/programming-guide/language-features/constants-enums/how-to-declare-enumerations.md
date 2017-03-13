---
title: "How to: Declare Enumerations (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declarations, enumerations"
  - "enumerations [Visual Basic], declaring"
  - "declaring enumerations"
ms.assetid: db4ca1c3-f429-4c81-ae81-29e0157b29fd
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# How to: Declare Enumerations (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per creare un'enumerazione, utilizzare l'istruzione `Enum` nella sezione dichiarazioni di una classe o di un modulo.  Non è possibile dichiarare un'enumerazione all'interno di un metodo.  Per specificare il livello di accesso appropriato, utilizzare `Private`, `Protected`, `Friend` o `Public`.  
  
 A un tipo `Enum` sono associati un nome, un tipo sottostante e un insieme di campi, ognuno dei quali rappresenta una costante.  Il nome deve essere un qualificatore di [!INCLUDE[vbprvblong](../../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] valido.  Il tipo sottostante deve corrispondere a uno dei tipi Integer, ovvero `Byte`, `Short`, `Long` o `Integer`.  `Integer` è l'impostazione predefinita.  Le enumerazioni sono sempre fortemente tipizzate e non sono interscambiabili con tipi di numeri integer.  
  
 Non è consentito assegnare alle enumerazioni valori a virgola mobile.  Se a un'enumerazione viene assegnato un valore a virgola mobile con `Option Strict On`, si verificherà un errore di compilazione.  Se `Option Strict` è impostata su `Off`, il valore verrà convertito automaticamente nel tipo `Enum`.  
  
 Per informazioni sui nomi e sull'utilizzo dell'istruzione `Imports` per evitare la qualifica dei nomi, vedere [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md).  
  
### Per dichiarare un'enumerazione  
  
1.  Scrivere una dichiarazione che includa un livello di accesso al codice, la parola chiave `Enum` e un nome valido, come negli esempi che seguono, in ognuno dei quali viene dichiarata una `Enum` differente.  
  
     [!code-vb[VbEnumsTask#3](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_1.vb)]  
  
2.  Definire le costanti nell'enumerazione.  Per impostazione predefinita, la prima costante di un'enumerazione viene inizializzata a `0`, mentre le costanti successive vengono inizializzate a un valore pari a un incremento di 1 rispetto alla costante precedente.  L'enumerazione che segue,`Days`, contiene ad esempio la costante `Sunday` con il valore `0`, la costante `Monday` con il valore `1`, la costante `Tuesday` con il valore `2` e così via.  
  
     [!code-vb[VbEnumsTask#4](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_2.vb)]  
  
3.  È possibile assegnare in modo esplicito i valori alle costanti di un'enumerazione utilizzando un'istruzione di assegnazione.  Può essere assegnato qualsiasi valore integer, compresi i numeri negativi.  Le costanti con valori inferiori a zero, ad esempio, possono rappresentare condizioni di errore.  Nell'enumerazione che segue alla costante `Invalid` viene assegnato esplicitamente il valore `–1` e alla costante `Sunday` viene assegnato il valore `0`.  Poiché è la prima costante dell'enumerazione, `Saturday` viene inoltre inizializzata al valore `0`.  Il valore di `Monday` è `1` \(un incremento di uno rispetto al valore di `Sunday`\), il valore di `Tuesday` è `2` e così via.  
  
     [!code-vb[VbEnumsTask#5](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_3.vb)]  
  
### Per dichiarare un'enumerazione come un tipo esplicito  
  
-   Specificare il tipo dell'enumerazione tramite la clausola `As`, come illustrato nell'esempio seguente.  
  
     [!code-vb[VbEnumsTask#6](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-enumerations_4.vb)]  
  
## Vedere anche  
 [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [How to: Refer to an Enumeration Member](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [How to: Iterate Through An Enumeration in Visual Basic](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [How to: Determine the String Associated with an Enumeration Value](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [When to Use an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [Constants Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Constant and Literal Data Types](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md)