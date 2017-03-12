---
title: "Constant and Literal Data Types (Visual Basic) | Microsoft Docs"
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
  - "declaring constants, literal data types"
  - "data types [Visual Basic], declaring"
  - "constants, declaring"
  - "explicit declarations"
  - "literals, coercing data type"
  - "declarations, data types"
ms.assetid: 057206d2-3a5b-40b9-b3af-57446f9b52fa
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Constant and Literal Data Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un letterale è un valore che viene espresso come se stesso piuttosto che come valore di variabile o risultato di un'espressione, come ad esempio il numero 3 o la stringa "Hello".  Una costante è un nome significativo che viene utilizzato in luogo di un letterale e mantiene lo stesso valore nel corso del programma, contrariamente a una variabile, il cui valore può cambiare.  
  
 Se [Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md) e `Off` e [Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) è `On`, è necessario dichiarare tutte le costanti in modo esplicito con un tipo di dati.  Nell'esempio riportato di seguito il tipo di dati di `MyByte` è dichiarato in modo esplicito come `Byte`:  
  
 [!code-vb[VbVbalrConstants#1](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/visualbasic/constant-and-literal-dat_1.vb)]  
  
 Se `Option Infer` è `On` o `Option Strict` è `Off`, è possibile dichiarare una costante senza specificare un tipo di dati con una clausola `As`.  Il compilatore determina il tipo della costante dal tipo dell'espressione.  In base all'impostazione predefinita, per un valore letterale di numero integer viene impostato il tipo di dati `Integer`.  Il tipo di dati predefinito per i numeri a virgola mobile è `Double`, mentre le parole chiave `True` e `False` specificano una costante di tipo `Boolean`.  
  
## Assegnazione forzata di valori letterali e tipi  
 In alcuni casi è possibile che si desideri assegnare in modo forzato un valore letterale a un particolare tipo di dati, ad esempio quando si assegna un valore letterale integrale particolarmente elevato a una variabile di tipo `Decimal`.  L'esempio riportato di seguito provoca un errore:  
  
```  
Dim myDecimal as Decimal  
myDecimal = 100000000000000000000   ' This causes a compiler error.  
```  
  
 L'errore deriva dalla rappresentazione del valore letterale.  Il tipo di dati `Decimal` è in grado di contenere un valore così elevato, ma il valore letterale è stato rappresentato in modo implicito come `Long`, che non è in grado di contenerlo.  
  
 È possibile assegnare in modo forzato un valore letterale a un particolare tipo di dati in due modi: aggiungendovi un carattere di tipo o inserendolo all'interno di caratteri di contenimento.  È necessario che il carattere di tipo o i caratteri di contenimento precedano e\/o seguano immediatamente il valore letterale, senza la frapposizione di spazi o caratteri di qualunque tipo.  
  
 Per correggere l'esempio precedente, è possibile aggiungere il carattere di tipo `D` al valore letterale, in modo che venga rappresentato come `Decimal`:  
  
 [!code-vb[VbVbalrConstants#2](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/visualbasic/constant-and-literal-dat_2.vb)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo corretto di caratteri di tipo e caratteri di contenimento:  
  
 [!code-vb[VbVbalrConstants#3](../../../../visual-basic/programming-guide/language-features/constants-enums/codesnippet/visualbasic/constant-and-literal-dat_3.vb)]  
  
 Nella tabella seguente sono riportati i caratteri di contenimento e i caratteri tipo disponibili in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
||||  
|-|-|-|  
|Tipo di dati|Carattere di contenimento|Carattere identificativo del tipo|  
|`Boolean`|\(nessuno\)|\(nessuno\)|  
|`Byte`|\(nessuno\)|\(nessuno\)|  
|`Char`||C|  
|`Date`|\#|\(nessuno\)|  
|`Decimal`|\(nessuno\)|D o @|  
|`Double`|\(nessuno\)|R o \#|  
|`Integer`|\(nessuno\)|I o %|  
|`Long`|\(nessuno\)|L o &|  
|`Short`|\(nessuno\)|S|  
|`Single`|\(nessuno\)|F o \!|  
|`String`||\(nessuno\)|  
  
## Vedere anche  
 [User\-Defined Constants](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)   
 [How to: Declare A Constant](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)   
 [Constants Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Option Explicit Statement](../../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Enumerations Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [How to: Declare an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md)