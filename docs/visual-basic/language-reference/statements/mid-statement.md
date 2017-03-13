---
title: "Mid Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.MidB"
  - "vb.Mid"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "substrings, Mid statement"
  - "strings [Visual Basic], substrings"
  - "Mid statement"
  - "strings [Visual Basic], replacing"
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Mid Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Sostituisce un determinato numero di caratteri in una variabile `String` con caratteri di un'altra stringa.  
  
## Sintassi  
  
```  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## Parti  
 `Target`  
 Obbligatorio.  Nome della variabile `String` da modificare.  
  
 `Start`  
 Obbligatorio.  Espressione `Integer`.  Posizione del carattere in `Target`, dove inizia la sostituzione del testo.  `Start` utilizza un indice in base uno.  
  
 `Length`  
 Parametro facoltativo.  Espressione `Integer`.  Numero di caratteri da sostituire.  Se omessa, verrà utilizzato l'intera variabile `String`.  
  
 `StringExpression`  
 Obbligatorio.  Espressione `String` che sostituisce una parte di `Target`.  
  
## Eccezioni  
  
|Tipo di eccezione|Condizione|  
|-----------------------|----------------|  
|<xref:System.ArgumentException>|`Start` \<\= 0 oppure `Length` \< 0.|  
  
## Note  
 Il numero di caratteri sostituiti è sempre inferiore o uguale al numero di caratteri presenti in `Target`.  
  
 In Visual Basic sono disponibili una funzione <xref:Microsoft.VisualBasic.Strings.Mid%2A> e un'istruzione `Mid`.  Entrambi gli elementi operano su un numero specificato di caratteri in una stringa, ma la funzione `Mid` restituisce i caratteri, mentre l'istruzione `Mid` li sostituisce.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Strings.Mid%2A>.  
  
> [!NOTE]
>  L'istruzione `MidB` delle versioni precedenti di Visual Basic sostituisce una sottostringa in byte, anziché in caratteri.  Viene utilizzata soprattutto per la conversione di stringhe in applicazioni del set di caratteri a byte doppio \(DBCS\).  Tutte le stringhe di Visual Basic sono in Unicode e l'istruzione `MidB` non è più supportata.  
  
## Esempio  
 Nell'esempio riportato di seguito l'istruzione `Mid` viene utilizzata per sostituire un numero specificato di caratteri in una variabile stringa con caratteri di un'altra stringa.  
  
 [!code-vb[VbVbalrStrings#5](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/mid-statement_1.vb)]  
  
## Requisiti  
 **Spazio dei nomi:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **Modulo:** `Strings`  
  
 **Assembly:** [!INCLUDE[vbprvbruntime](../../../visual-basic/language-reference/objects/includes/vbprvbruntime-md.md)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 [Strings](../../../visual-basic/programming-guide/language-features/strings/index.md)   
 [Introduction to Strings in Visual Basic](../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)