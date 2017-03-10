---
title: "Miscellaneous Data Types (Visual Basic) | Microsoft Docs"
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
  - "Object data type, data types"
  - "data types [Visual Basic], choosing"
ms.assetid: 64c71a12-9057-4dbf-baca-7379c4aada69
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Miscellaneous Data Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono disponibili vari tipi di dati che non sono riconducibili né a numeri né a caratteri.  ma piuttosto rappresentano dati specifici quali valori sì\/no, valori di data\/ora e indirizzi di oggetti.  
  
 Per un confronto dettagliato dei tipi di dati di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], vedere [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## Tipo Boolean  
 Il [Boolean Data Type](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) è un valore senza segno interpretato come `True` o `False`.  L'ampiezza dei relativi dati dipende dalla piattaforma di implementazione.  Se una variabile può contenere solo valori che indicano due stati come vero\/falso, sì\/no o attivato\/disattivato, dichiararla come `Boolean`.  
  
## Tipo Date  
 Il [Date Data Type](../../../../visual-basic/language-reference/data-types/date-data-type.md) è un valore a 64 bit che contiene informazioni relative sia alla data che all'ora.  Ciascun incremento rappresenta 100 nanosecondi di tempo trascorso dall'inizio \(ore 00.00\) dell'1 gennaio dell'anno 1 del calendario gregoriano.  Se una variabile può contenere un valore data, un valore ora o entrambi, dichiararla come `Date`.  
  
## Tipo Object  
 Il [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md) è un indirizzo a 32 bit che punta a un'istanza di oggetto all'interno dell'applicazione o in un'altra applicazione.  Una variabile `Object` può fare riferimento a qualsiasi oggetto riconosciuto dall'applicazione o ai dati di qualsiasi tipo.  Ciò include sia tipi di valore, ad esempio `Integer`,  `Boolean`e istanze della struttura e tipi di riferimento, che sono istanze degli oggetti hanno creato da classi come  `String` e  <xref:System.Windows.Forms.Form>e istanze di matrice.  
  
 Se una variabile memorizza un puntatore a un'istanza di una classe che non è nota in fase di compilazione o se può puntare a vari tipi di dati, dichiararla come `Object`.  
  
 Il vantaggio di `Object` il tipo di dati è che è possibile utilizzarlo per archiviare i dati di qualsiasi tipo.  Lo svantaggio è che implica operazioni aggiuntive che prolungano i tempi di esecuzione e rallentano le prestazioni dell'applicazione.  Se si utilizza una variabile `Object` per i tipi di valore, sono necessarie operazioni di conversione *boxing* e *unboxing*.  Se la variabile viene utilizzata per i tipi di riferimento, avrà luogo l'*associazione tardiva*.  
  
## Vedere anche  
 [Type Characters](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Numeric Data Types](../../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)   
 [Character Data Types](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Early and Late Binding](../../../../visual-basic/programming-guide/language-features/early-late-binding/early-and-late-binding.md)