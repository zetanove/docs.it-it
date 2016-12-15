---
title: "How to: Force an Argument to Be Passed by Value (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "procedures, arguments"
  - "procedures, parameters"
  - "procedure arguments"
  - "Visual Basic code, procedures"
  - "arguments [Visual Basic], ByVal"
  - "arguments [Visual Basic], passing by value"
  - "procedure parameters"
  - "procedures, calling"
  - "arguments [Visual Basic], in parentheses"
  - "procedure arguments, in parentheses"
  - "arguments [Visual Basic], changing value"
ms.assetid: 77b4f2d2-1055-4c2f-a521-874d1db86946
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Force an Argument to Be Passed by Value (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

La dichiarazione di routine determina il meccanismo di passaggio.  Se un parametro viene dichiarato [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] si prevede che l'argomento corrispondente venga passato per riferimento.  In questo modo la routine può modificare il valore dell'elemento di programmazione sottostante all'argomento nel codice chiamante.  Se si desidera proteggere l'elemento sottostante da tale modifica, è possibile eseguire l'override del meccanismo di passaggio `ByRef` nella chiamata di routine racchiudendo il nome dell'argomento tra parentesi.  Tali parentesi vengono aggiunte a quelle che racchiudono l'elenco di argomenti nella chiamata.  
  
 Non è possibile eseguire l'override di un meccanismo [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) mediante il codice chiamante.  
  
### Per imporre il passaggio di un argomento per valore  
  
-   Se il parametro corrispondente viene dichiarato `ByVal` nella routine, non è necessario eseguire operazioni aggiuntive in  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], in quanto è già previsto che l'argomento venga passato per valore.  
  
-   Se il parametro corrispondente viene dichiarato `ByRef` nella routine, racchiudere l'argomento tra parentesi nella chiamata di routine.  
  
## Esempio  
 Nell'esempio riportato di seguito viene eseguito l'override di una dichiarazione di parametro `ByRef`.  Si osservino i due livelli di parentesi nella chiamata che impone `ByVal`.  
  
 [!code-vb[VbVbcnProcedures#39](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-force-an-argument-to-be-passed-by-value_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#40](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-force-an-argument-to-be-passed-by-value_2.vb)]  
  
 Quando `str` è racchiuso tra parentesi aggiuntive all'interno dell'elenco di argomenti, non è possibile modificare il valore della routine `setNewString` nel codice chiamante e in `MsgBox` viene visualizzato il messaggio "Cannot be replaced if passed ByVal".  Quando il valore `str` non è racchiuso tra parentesi aggiuntive, la routine può modificarlo e in `MsgBox` viene visualizzato il messaggio "This is a new value for the inString argument."  
  
## Compilazione del codice  
 Quando si passa una variabile tramite riferimento, è necessario usare la parola chiave `ByRef` per specificare tale meccanismo.  
  
 Per impostazione predefinita, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli argomenti vengono passati per valore.   È comunque buona norma di programmazione includere la parola chiave [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) con ogni parametro dichiarato,  al fine di agevolare la lettura del codice.  
  
## Programmazione efficiente  
 Se una routine dichiara un parametro [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), la corretta esecuzione del codice potrebbe dipendere dalla possibilità o meno di modificare l'elemento sottostante nel codice chiamante.  Se il codice chiamante esegue l'override di questo meccanismo di chiamata racchiudendo l'argomento tra parentesi o se passa un argomento non modificabile, non sarà possibile modificare l'elemento sottostante mediante la routine.  Ciò potrebbe generare risultati imprevisti nel codice chiamante.  
  
## Sicurezza di .NET Framework  
 Esiste sempre un rischio potenziale quando si consente che una routine modifichi il valore sottostante un argomento nel codice chiamante.  Accertarsi che la modifica del valore sia prevista e verificare la validità del valore prima di utilizzarlo.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Differences Between Modifiable and Nonmodifiable Arguments](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [Differences Between Passing an Argument By Value and By Reference](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [How to: Change the Value of a Procedure Argument](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [How to: Protect a Procedure Argument Against Value Changes](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)