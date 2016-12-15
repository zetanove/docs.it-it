---
title: "How to: Declare A Constant (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.constant"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Integer data type, declaring constants"
  - "Single data type, declaring constants"
  - "Const statement [Visual Basic], declaring constants"
  - "procedures, declaration"
  - "data types [Visual Basic], constants"
  - "Long data type, declaring constants"
  - "Visual Basic code, declaring variables and constants"
  - "Double data type, declaring constants"
  - "Boolean data type, declaring constants"
  - "modules, declaring constants"
  - "Byte data type, declaring constants"
  - "constants, declaring"
  - "Date data type, declaring constants"
  - "String data type, declaring constants"
  - "declaring constants, const keyword"
  - "Currency data type, declaring constants and variants"
  - "module-level constants and variables"
  - "Object data type, declaring constants"
ms.assetid: f901b4fa-481f-4621-822e-427060577ad1
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Declare A Constant (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'istruzione `Const` consente di dichiarare una costante e di impostarne il valore.  Mediante la dichiarazione di una costante è possibile assegnare a un valore un nome significativo.  Dopo aver dichiarato una costante, non è possibile modificarla o assegnarle un nuovo valore.  
  
 È possibile dichiarare una costante all'interno di una routine oppure nella sezione dichiarazioni di un modulo, una classe o una struttura.  Le costanti a livello di classe o di struttura sono `Private` per impostazione predefinita, ma possono anche essere dichiarate come `Public`, `Friend`, `Protected` o `Protected Friend` per il livello di accesso al codice appropriato.  
  
 È necessario che alla costante siano assegnati un nome simbolico valido \(le regole sono uguali a quelle per la creazione dei nomi di variabili\) e un'espressione costituita da costanti numeriche o stringa e operatori, ma non chiamate di funzioni.  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### Per dichiarare una costante  
  
-   Scrivere una dichiarazione in cui siano inclusi un identificatore di accesso, la parola chiave `Const` e un'espressione, come illustrato negli esempi seguenti:  
  
     [!code-vb[VbEnumsTask#8](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-a-constant_1.vb)]  
  
     Se [Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md) è `Off` e [Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) è `On`, è necessario dichiarare una costante in modo esplicito specificando un tipo di dati \(`Boolean`, `Byte`, `Char`, `DateTime`, `Decimal`, `Double`, `Integer`, `Long`, `Short`, `Single` o `String`\).  
  
     Se `Option Infer` è `On` o `Option Strict` è `Off`, è possibile dichiarare una costante senza specificare un tipo di dati con una clausola `As`.  Il compilatore determina il tipo della costante dal tipo dell'espressione.  Per ulteriori informazioni, vedere [Constant and Literal Data Types](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md).  
  
### Per dichiarare una costante con un tipo di dati indicato in modo esplicito  
  
-   Scrivere una dichiarazione in cui siano inclusi la parola chiave `As` e un tipo di dati esplicito, come illustrato negli esempi seguenti:  
  
     [!code-vb[VbEnumsTask#9](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-a-constant_2.vb)]  
  
     È possibile dichiarare più costanti sulla stessa riga, anche se il codice risulterà più leggibile se si dichiara una sola costante per riga.  Se si dichiarano più costanti in una singola riga, devono presentare tutte lo stesso livello di accesso \(`Public`, `Private`, `Friend`, `Protected` o `Protected Friend`\).  
  
### Per dichiarare più costanti sulla stessa riga  
  
-   Separare le dichiarazione con una virgola e uno spazio, come illustrato nell'esempio seguente:  
  
    ```  
    Public Const Four As Integer = 4, Five As Integer = 5, Six As Integer = 44  
    ```  
  
## Vedere anche  
 [Const Statement](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [Constant and Literal Data Types](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [Constants and Enumerations](../../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [Enumerations Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [Constants Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [How to: Declare an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md)