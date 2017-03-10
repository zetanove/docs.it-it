---
title: "Return Values for the CStr Function (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "times, CStr Function return values"
  - "type conversion"
  - "dates [Visual Basic], CStr Function return values"
  - "CStr function"
  - "strings [Visual Basic], return value"
  - "Date data type, converting"
  - "dates [Visual Basic]"
  - "String data type, converting"
ms.assetid: 3aa744e7-1419-45d5-85e3-e5abc2953673
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Return Values for the CStr Function (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nella tabella riportata di seguito vengono descritti i valori restituiti da `CStr` per i diversi tipi di dati di `expression`.  
  
|Se il tipo di `expression` è|`CStr` restituisce|  
|----------------------------------|------------------------|  
|[Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|Una stringa contenente "True" o "False".|  
|[Date Data Type](../../../visual-basic/language-reference/data-types/date-data-type.md)|Una stringa contenente un valore `Date` \(data e ora\) nel formato data breve impostato nel sistema.|  
|[Numeric Data Types](../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)|Una stringa che rappresenta il numero.|  
  
## CStr e Date  
 Il tipo `Date` contiene sempre informazioni sia relative alla data sia relative all'ora.  Ai fini della conversione del tipo, Visual Basic considera 1\/1\/0001 \(1 gennaio dell'anno 1\) come *valore neutro* per la data e 00:00:00 \(mezzanotte\) come valore neutro per l'ora.  `CStr` non include valori neutri nella stringa risultante.  Se ad esempio il valore `#January 1, 0001 9:30:00#` viene convertito in una stringa, il risultato sarà "9:30:00 AM" e le informazioni sulla data non verranno visualizzate.  Le informazioni relative alla data sono comunque incluse nel valore `Date` originale e possono essere recuperate con funzioni come <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A>.  
  
> [!NOTE]
>  La funzione `CStr` esegue la conversione in base alle impostazioni cultura correnti dell'applicazione.  Per ottenere la rappresentazione in forma di stringa di un numero in impostazioni cultura specifiche, utilizzare il metodo `ToString(IFormatProvider)` del numero.  Utilizzare ad esempio <xref:System.Double.ToString%2A?displayProperty=fullName> per la conversione di un valore di tipo `Double` in `String`.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A>   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md)   
 [Date Data Type](../../../visual-basic/language-reference/data-types/date-data-type.md)