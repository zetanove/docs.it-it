---
title: "How to: Search Within a String (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "strings [Visual Basic], finding"
  - "strings [Visual Basic], searching"
  - "examples [Visual Basic], strings"
ms.assetid: ae4c79e0-08ea-489f-bdb2-5eb6d355f284
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Search Within a String (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Nell'esempio riportato di seguito viene chiamato il metodo <xref:System.String.IndexOf%2A> di un oggetto <xref:System.String> allo scopo di segnalare l'indice della prima occorrenza di una sottostringa.  
  
## Esempio  
 [!code-vb[VbVbalrStrings#71](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-search-within-a-string_1.vb)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un'istruzione `Imports` che specifica lo spazio dei nomi <xref:System>.  Per ulteriori informazioni, vedere [Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
## Programmazione efficiente  
 Il metodo <xref:System.String.IndexOf%2A> indica la posizione del primo carattere della prima occorrenza della sottostringa.  L'indice è con inizio zero, ossia il primo carattere di una stringa presenta un indice pari a 0.  
  
 Se <xref:System.String.IndexOf%2A> non trova la sottostringa, restituisce \-1.  
  
 Per il metodo <xref:System.String.IndexOf%2A> viene rilevata la distinzione tra maiuscole e minuscole e vengono utilizzate le impostazioni cultura correnti.  
  
 Per un controllo ottimale degli errori, è consigliabile racchiudere la stringa di ricerca nel blocco `Try` di una costruzione[Try...Catch...Finally Statement](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## Vedere anche  
 <xref:System.String.IndexOf%2A>   
 [Try...Catch...Finally Statement](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Introduction to Strings in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [Strings](../../../../visual-basic/programming-guide/language-features/strings/index.md)