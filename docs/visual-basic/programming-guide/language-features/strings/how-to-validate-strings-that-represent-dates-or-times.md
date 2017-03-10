---
title: "How to: Validate Strings That Represent Dates or Times (Visual Basic) | Microsoft Docs"
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
  - "strings [Visual Basic], validating"
  - "String data type, validation"
ms.assetid: ae7d4b29-3436-4032-bdbf-4650eb1c8e19
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# How to: Validate Strings That Represent Dates or Times (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nell'esempio di codice illustrato di seguito viene impostato un valore `Boolean` che indica se una stringa rappresenta una data o un'ora valide.  
  
## Esempio  
 [!code-vb[VbVbcnRegEx#2](../../../../visual-basic/programming-guide/language-features/strings/codesnippet/visualbasic/how-to-validate-strings-_1.vb)]  
  
## Compilazione del codice  
 Sostituire `("01/01/03")` e `"9:30 PM"` con la data e l'ora che si desidera convalidare.  È possibile sostituire la stringa con un'altra stringa definita a livello di codice con una variabile `String` o con un metodo che restituisce una stringa come `InputBox`.  
  
## Programmazione efficiente  
 Utilizzare questo metodo per convalidare la stringa prima di cercare di convertire la variabile `String` in una variabile `DateTime`.  Verificando prima la data o l'ora, è possibile evitare la generazione di un'eccezione in fase di esecuzione.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Information.IsDate%2A>   
 <xref:Microsoft.VisualBasic.Interaction.InputBox%2A>   
 [Validating Strings in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)