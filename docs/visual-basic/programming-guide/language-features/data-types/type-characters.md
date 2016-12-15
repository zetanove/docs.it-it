---
title: "Type Characters (Visual Basic) | Microsoft Docs"
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
  - "&H prefix for hexadecimal values"
  - "hexadecimal literals"
  - "F literal type character"
  - "& identifier type character"
  - "type characters"
  - "octal literals"
  - "literals, hexadecimal"
  - "&O prefix for octal values"
  - "literals, default types"
  - "defaults, literal types"
  - "C literal type character"
  - "type characters, literal"
  - "$ identifier type character"
  - "L literal type character"
  - "UI literal type characters"
  - "default literal types"
  - "D literal type character"
  - "literals, octal"
  - "S literal type character"
  - "! identifier type character"
  - "US literal type characters"
  - "% identifier type character"
  - "data types [Visual Basic], type characters"
  - "characters, identifier type"
  - "type characters, identifier"
  - "# identifier type character"
  - "identifier type characters"
  - "literal type characters"
  - "I literal type character"
  - "R literal type character"
  - "@ identifier type character"
  - "UL literal type characters"
  - "literal types, default"
ms.assetid: 6353cb9b-6ee4-4af6-a5a8-88ce39f90cc5
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type Characters (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Oltre a specificare un tipo di dati in un'istruzione di dichiarazione, è possibile definire il tipo di dati di alcuni elementi di programmazione mediante un *carattere tipo*.  È necessario che il carattere tipo segua immediatamente l'elemento, senza che si frappongano altri caratteri.  
  
 Il carattere tipo non fa parte del nome dell'elemento.  È possibile fare riferimento a un elemento definito con un carattere tipo senza utilizzare tale carattere tipo.  
  
## Caratteri identificatori di tipo  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce un insieme di *caratteri identificatori di tipo*, che è possibile utilizzare in una dichiarazione per specificare il tipo di dati di una variabile o costante.  Nella tabella che segue sono illustrati i caratteri identificatori di tipo disponibili, con esempi di utilizzo.  
  
|Carattere identificatore di tipo|Tipo di dati|Esempio|  
|--------------------------------------|------------------|-------------|  
|`%`|`Integer`|`Dim L%`|  
|`&`|`Long`|`Dim M&`|  
|`@`|`Decimal`|`Const W@ = 37.5`|  
|`!`|`Single`|`Dim Q!`|  
|`#`|`Double`|`Dim X#`|  
|`$`|`String`|`Dim V$ = "Secret"`|  
  
 Non esiste alcun carattere identificatore di tipo per i tipi di dati `Boolean`, `Byte`, `Char`, `Date`, `Object`, `SByte`, `Short`, `UInteger`, `ULong` o `UShort` né per alcun tipo di dati composito, come le matrici o le strutture.  
  
 In alcuni casi, è possibile aggiungere il carattere `$` a una funzione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], ad esempio `Left$` anziché `Left`, per ottenere un valore restituito di tipo `String`.  
  
 In tutti i casi è necessario che il carattere identificatore di tipo segua immediatamente il nome dell'identificatore.  
  
## Carattere di tipo letterale  
 Un *valore letterale* è una rappresentazione testuale di un particolare valore di un tipo di dati.  
  
### Tipi letterali predefiniti  
 Il formato con cui viene visualizzato un valore letterale nel codice ne determina in genere il tipo di dati.  Nella tabella che segue sono riportati i tipi predefiniti.  
  
|Forma testuale del valore letterale|Tipo di dati predefinito|Esempio|  
|-----------------------------------------|------------------------------|-------------|  
|Numerico, senza parte frazionaria|`Integer`|`2147483647`|  
|Numerico, senza parte frazionaria, troppo grande per `Integer`|`Long`|`2147483648`|  
|Numerico, parte frazionaria|`Double`|`1.2`|  
|Racchiuso tra virgolette doppie.|`String`|`"A"`|  
|Racchiuso tra simboli di cancelletto|`Date`|`#5/17/1993 9:32 AM#`|  
  
### Tipi letterali forzati  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce un insieme di *caratteri di tipo letterale*, che è possibile utilizzare per definire il tipo di un valore letterale in modo diverso da quello indicato dalla forma della rappresentazione stessa.  Per far questo è necessario aggiungere il carattere al termine della rappresentazione.  Nella tabella che segue sono illustrati i caratteri di tipo letterale disponibili, con esempi di utilizzo.  
  
|Carattere di tipo letterale|Tipo di dati|Esempio|  
|---------------------------------|------------------|-------------|  
|`S`|`Short`|`I = 347S`|  
|`I`|`Integer`|`J = 347I`|  
|`L`|`Long`|`K = 347L`|  
|`D`|`Decimal`|`X = 347D`|  
|`F`|`Single`|`Y = 347F`|  
|`R`|`Double`|`Z = 347R`|  
|`US`|`UShort`|`L = 347US`|  
|`UI`|`UInteger`|`M = 347UI`|  
|`UL`|`ULong`|`N = 347UL`|  
|`C`|`Char`|`Q = "."C`|  
  
 Non esiste alcun carattere di tipo letterale per i tipi di dati `Boolean`, `Byte`, `Date`, `Object`, `SByte` o `String` né per alcun tipo di dati composito, come le matrici o le strutture.  
  
 I valori letterali, analogamente a variabili, costanti ed espressioni, possono inoltre utilizzare i caratteri identificatori di tipo \(`%`, `&`, `@`, `!`, `#`, `$`\).  I caratteri di tipo letterale, tuttavia, \(`S`, `I`, `L`, `D`, `F`, `R`, `C`\) possono essere utilizzati solo con valori letterali.  
  
 In tutti i casi è necessario che il carattere di tipo letterale segua immediatamente il valore letterale.  
  
## Valori letterali esadecimali e ottali  
 Il compilatore generalmente interpreta un valore letterale integer come valore del sistema numerico decimale \(base 10\).  È possibile far sì che un valore letterale integer diventi esadecimale \(base 16\) utilizzando il prefisso `&H` e ottale \(base 8\) utilizzando il prefisso `&O`.  Le cifre che seguono il prefisso devono essere adatte al sistema numerico in uso.  come illustrato nella tabella che segue:  
  
|Base numerica|Prefisso|Cifre valide|Esempio|  
|-------------------|--------------|------------------|-------------|  
|Esadecimale \(base 16\)|`&H`|0\-9 e A\-F|`&HFFFF`|  
|Ottale \(base 8\)|`&O`|0\-7|`&O77`|  
  
 È possibile inserire un carattere di tipo letterale dopo un valore letterale con prefisso.  Questa operazione viene illustrata nell'esempio che segue.  
  
```  
Dim counter As Short = &H8000S  
Dim flags As UShort = &H8000US  
```  
  
 Nell'esempio precedente, `counter` ha il valore decimale \-32768 e `flags` ha il valore decimale \+32768.  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)