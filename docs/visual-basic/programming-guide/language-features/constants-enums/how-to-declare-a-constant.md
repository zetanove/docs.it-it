---
title: 'Procedura: dichiarare una costante (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.constant
dev_langs:
- VB
helpviewer_keywords:
- Integer data type, declaring constants
- Single data type, declaring constants
- Const statement [Visual Basic], declaring constants
- procedures, declaration
- data types [Visual Basic], constants
- Long data type, declaring constants
- Visual Basic code, declaring variables and constants
- Double data type, declaring constants
- Boolean data type, declaring constants
- modules, declaring constants
- Byte data type, declaring constants
- constants, declaring
- Date data type, declaring constants
- String data type, declaring constants
- declaring constants, const keyword
- Currency data type, declaring constants and variants
- module-level constants and variables
- Object data type, declaring constants
ms.assetid: f901b4fa-481f-4621-822e-427060577ad1
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 401d0feb85fccf94a25308d38c3c75198ef9294c
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-a-constant-visual-basic"></a>Procedura: dichiarare una costante (Visual Basic)
Utilizzare il `Const` istruzione per dichiarare una costante e impostarne il valore. Dichiarando una costante, assegnare un nome significativo a un valore. Dopo aver dichiarata una costante, non può essere modificato o assegnato un nuovo valore.  
  
 Dichiarare una costante all'interno di una routine o nella sezione relativa alle dichiarazioni di modulo, classe o struttura. Classe o le costanti a livello di struttura sono `Private` per impostazione predefinita, ma possono anche essere dichiarati come `Public`, `Friend`, `Protected`, o `Protected Friend` per il livello appropriato di accesso al codice.  
  
 La costante deve avere un nome simbolico valido (le regole sono identiche a quelle per la creazione di nomi di variabile) e un'espressione costituita da stringhe o numerici costanti e operatori (ma non chiamate di funzioni).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-declare-a-constant"></a>Per dichiarare una costante  
  
-   Scrivere una dichiarazione che include un identificatore di accesso, il `Const` (parola chiave) e un'espressione, come negli esempi seguenti:  
  
     [!code-vb[VbEnumsTask n.&8;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-a-constant_1.vb)]  
  
     Quando [Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md) è `Off` e [Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) è `On`, è necessario dichiarare una costante in modo esplicito specificando un tipo di dati (`Boolean`, `Byte`, `Char`, `DateTime`, `Decimal`, `Double`, `Integer`, `Long`, `Short`, `Single`, o `String`).  
  
     Quando `Option Infer` è `On` o `Option Strict` è `Off`, è possibile dichiarare una costante senza specificare un tipo di dati con un `As` clausola. Il compilatore determina il tipo della costante dal tipo dell'espressione. Per ulteriori informazioni, vedere [costante e tipi di dati letterali](constant-and-literal-data-types.md).  
  
### <a name="to-declare-a-constant-that-has-an-explicitly-stated-data-type"></a>Per dichiarare una costante con un tipo di dati specificata in modo esplicito  
  
-   Scrivere una dichiarazione che include il `As` (parola chiave) e un esplicita tipo di dati, come negli esempi seguenti:  
  
     [!code-vb[9 VbEnumsTask](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-a-constant_2.vb)]  
  
     È possibile dichiarare più costanti in una singola riga, anche se il codice più leggibile se si dichiara una sola costante per ogni riga. Se si dichiarano più costanti in una singola riga, devono tutti avere lo stesso livello di accesso (`Public`, `Private`, `Friend`, `Protected`, o `Protected Friend`).  
  
### <a name="to-declare-multiple-constants-on-a-single-line"></a>Per dichiarare più costanti in una singola riga  
  
-   Le dichiarazioni, separarli con una virgola e uno spazio, come nell'esempio seguente:  
  
    ```  
    Public Const Four As Integer = 4, Five As Integer = 5, Six As Integer = 44  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Const (istruzione)](../../../../visual-basic/language-reference/statements/const-statement.md)   
 [Tipi di dati costanti e letterali](constant-and-literal-data-types.md)   
 [Cenni preliminari sulle costanti](constants-overview.md)
 [come: dichiarare una costante](how-to-declare-a-constant.md)
 [costanti definite dall'utente](user-defined-constants.md)
 [tipi di dati costanti e letterali](constant-and-literal-data-types.md)
 [procedura: raggruppare i valori costanti correlate](how-to-group-related-constant-values-together.md)
 [Cenni preliminari sulle enumerazioni](enumerations-overview.md)
 [come: dichiarare enumerazioni](how-to-declare-enumerations.md)
 [come: fare riferimento a un membro di enumerazione](how-to-refer-to-an-enumeration-member.md)
 [qualifica di nomi ed enumerazioni](enumerations-and-name-qualification.md)
 [procedura: scorrere un'enumerazione](how-to-iterate-through-an-enumeration.md)
 [come: determinare la stringa Associata a un valore di enumerazione](how-to-determine-the-string-associated-with-an-enumeration-value.md)
 [quando utilizzare un'enumerazione](when-to-use-an-enumeration.md)

 [Cenni preliminari sulle enumerazioni](enumerations-overview.md)   
 [Cenni preliminari sulle costanti](constants-overview.md)   
 [Procedura: dichiarare un'enumerazione](how-to-declare-enumerations.md)   
 [Qualifica di nomi ed enumerazioni](enumerations-and-name-qualification.md)   
 [Istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Costanti ed enumerazioni](../../../../visual-basic/language-reference/constants-and-enumerations.md)

