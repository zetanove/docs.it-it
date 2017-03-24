---
title: Digitare i caratteri (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- '&H prefix for hexadecimal values'
- hexadecimal literals
- F literal type character
- '& identifier type character'
- type characters
- octal literals
- literals, hexadecimal
- '&O prefix for octal values'
- literals, default types
- defaults, literal types
- C literal type character
- type characters, literal
- $ identifier type character
- L literal type character
- UI literal type characters
- default literal types
- D literal type character
- literals, octal
- S literal type character
- '! identifier type character'
- US literal type characters
- '% identifier type character'
- data types [Visual Basic], type characters
- characters, identifier type
- type characters, identifier
- '# identifier type character'
- identifier type characters
- literal type characters
- I literal type character
- R literal type character
- '@ identifier type character'
- UL literal type characters
- literal types, default
ms.assetid: 6353cb9b-6ee4-4af6-a5a8-88ce39f90cc5
caps.latest.revision: 22
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6e112e7d221ef8e7a660094306bbb242c988e843
ms.lasthandoff: 03/13/2017

---
# <a name="type-characters-visual-basic"></a>Caratteri tipo (Visual Basic)
Oltre a specificare un tipo di dati in un'istruzione di dichiarazione, è possibile forzare il tipo di dati di alcuni elementi di programmazione con un *tipo di carattere*. Il tipo di carattere deve seguire immediatamente l'elemento, senza i caratteri di qualsiasi tipo.  
  
 Il tipo di carattere non è parte del nome dell'elemento. Un elemento definito con un carattere di tipo può fare riferimento senza il carattere di tipo.  
  
## <a name="identifier-type-characters"></a>Caratteri di tipo identificatore  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce un set di *caratteri identificatori di tipo*, che è possibile utilizzare in una dichiarazione per specificare il tipo di dati di una variabile o costante. Nella tabella seguente mostra i caratteri di tipo identificatore disponibile con esempi di utilizzo.  
  
|Carattere di tipo identificatore|Tipo di dati|Esempio|  
|-------------------------------|---------------|-------------|  
|`%`|`Integer`|`Dim L%`|  
|`&`|`Long`|`Dim M&`|  
|`@`|`Decimal`|`Const W@ = 37.5`|  
|`!`|`Single`|`Dim Q!`|  
|`#`|`Double`|`Dim X#`|  
|`$`|`String`|`Dim V$ = "Secret"`|  
  
 Non esiste alcun carattere di tipo identificatore per il `Boolean`, `Byte`, `Char`, `Date`, `Object`, `SByte`, `Short`, `UInteger`, `ULong`, o `UShort` tipi di dati, o per qualsiasi tipo di dati compositi, ad esempio matrici o strutture.  
  
 In alcuni casi, è possibile aggiungere il `$` carattere per un [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] funzione, ad esempio `Left$` anziché `Left`, per ottenere un valore restituito di tipo `String`.  
  
 In tutti i casi, il carattere di tipo identificatore deve seguire immediatamente il nome dell'identificatore.  
  
## <a name="literal-type-characters"></a>Caratteri di tipo effettivo  
 Oggetto *letterale* è una rappresentazione testuale di un determinato valore di un tipo di dati.  
  
### <a name="default-literal-types"></a>Tipi di valore letterale predefinito  
 Il modulo di un valore letterale come appare nel codice in genere determina il tipo di dati. Nella tabella seguente vengono illustrati questi tipi di valore predefinito.  
  
|Formato testuale del valore letterale|Tipo di dati predefinito|Esempio|  
|-----------------------------|-----------------------|-------------|  
|Numerico, senza parte frazionaria|`Integer`|`2147483647`|  
|Numerico, senza parte frazionaria, troppo grande per`Integer`|`Long`|`2147483648`|  
|Numerico, parte frazionaria|`Double`|`1.2`|  
|Racchiuso tra virgolette doppie|`String`|`"A"`|  
|Racchiuso tra simboli di cancelletto|`Date`|`#5/17/1993 9:32 AM#`|  
  
### <a name="forced-literal-types"></a>Tipi letterali forzati  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce un set di *caratteri di tipo letterale*, indica che è possibile utilizzare per imporre un valore letterale può assumere un tipo di dati diverso da quello dal form. Fatto questo, aggiungendo il carattere alla fine del valore letterale. Nella tabella seguente mostra i caratteri di tipo letterale disponibili con esempi di utilizzo.  
  
|Carattere di tipo letterale|Tipo di dati|Esempio|  
|----------------------------|---------------|-------------|  
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
  
 Non esiste alcun carattere di tipo letterale per il `Boolean`, `Byte`, `Date`, `Object`, `SByte`, o `String` tipi di dati, o per qualsiasi tipo di dati compositi, ad esempio matrici o strutture.  
  
 Valori letterali possono inoltre utilizzare i caratteri identificatori di tipo (`%`, `&`, `@`, `!`, `#`, `$`), analogamente a variabili, costanti ed espressioni. Tuttavia, caratteri di tipo letterale (`S`, `I`, `L`, `D`, `F`, `R`, `C`) può essere utilizzato solo con i valori letterali.  
  
 In tutti i casi, il carattere di tipo letterale deve seguire immediatamente il valore letterale.  
  
## <a name="hexadecimal-and-octal-literals"></a>Valori letterali esadecimali e ottali  
 Generalmente, il compilatore interpreta un valore letterale integer per il sistema di numero decimale (base 10). È possibile forzare letterale sia un valore integer esadecimale (base 16) con il `&H` prefisso ed è possibile imporle ottale (base 8) con il `&O` prefisso. Le cifre che seguono il prefisso devono essere appropriate per il sistema numerico. Questa condizione è illustrata nella tabella seguente.  
  
|Numero di base|Prefisso|Cifre valide|Esempio|  
|-----------------|------------|------------------------|-------------|  
|Esadecimale (base 16)|`&H`|0-9 e a-F|`&HFFFF`|  
|Ottale (base 8)|`&O`|0-7|`&O77`|  
  
 È possibile seguire un valore letterale con prefisso con un carattere di tipo letterale. Nell'esempio seguente viene illustrata questa operazione.  
  
```  
Dim counter As Short = &H8000S  
Dim flags As UShort = &H8000US  
```  
  
 Nell'esempio precedente, `counter` ha il valore decimale compreso tra -32768, e `flags` ha il valore decimale-32768.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Tipi di dati elementari](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Dichiarazione di variabile](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)
