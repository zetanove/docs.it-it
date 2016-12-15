---
title: "Operator Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.operator"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "operators [Visual Basic]"
  - "procedures, operator"
  - "Narrowing keyword, conversion operators"
  - "Visual Basic code, operators"
  - "Widening keyword, conversion operators"
  - "syntax, Operator procedures"
  - "operators [Visual Basic], overloading"
  - "overloaded operators"
  - "operator overloading"
  - "operator procedures"
  - "Operator statement"
  - "CType function, Operator statement"
ms.assetid: b12ec4af-1ad7-4a17-865b-c5ee96320ae5
caps.latest.revision: 28
caps.handback.revision: 28
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Operator Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di dichiarare il simbolo dell'operatore, gli operandi e il codice che definiscono una routine operatore su una classe o una struttura.  
  
## Sintassi  
  
```  
[ <attrlist> ] Public [ Overloads ] Shared [ Shadows ] [ Widening | Narrowing ]   
Operator operatorsymbol ( operand1 [, operand2 ]) [ As [ <attrlist> ] type ]  
    [ statements ]  
    [ statements ]  
    Return returnvalue  
    [ statements ]  
End Operator  
```  
  
## Parti  
 `attrlist`  
 Parametro facoltativo.  Vedere [Elenco degli attributi](../../../visual-basic/language-reference/statements/attribute-list.md).  
  
 `Public`  
 Obbligatorio.  Indica che questa routine operatore è dotata di un accesso [Public](../../../visual-basic/language-reference/modifiers/public.md).  
  
 `Overloads`  
 Parametro facoltativo.  Vedere [Overloads](../../../visual-basic/language-reference/modifiers/overloads.md).  
  
 `Shared`  
 Obbligatorio.  Indica che questa routine operatore è una routine [Shared](../../../visual-basic/language-reference/modifiers/shared.md).  
  
 `Shadows`  
 Parametro facoltativo.  Vedere [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md).  
  
 `Widening`  
 Obbligatorio per un operatore di conversione a meno che non si specifichi `Narrowing`.  Indica che questa routine operatore definisce una conversione [Widening](../../../visual-basic/language-reference/modifiers/widening.md).  Vedere "Conversioni di ampliamento e restrizione" in questa pagina della Guida.  
  
 `Narrowing`  
 Obbligatorio per un operatore di conversione a meno che non si specifichi `Widening`.  Indica che questa routine operatore definisce una conversione [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md).  Vedere "Conversioni di ampliamento e restrizione" in questa pagina della Guida.  
  
 `operatorsymbol`  
 Obbligatorio.  Il simbolo o l'identificatore dell'operatore definito da questa routine operatore.  
  
 `operand1`  
 Obbligatorio.  Il nome e il tipo del singolo operando di un operatore unario \(incluso un operatore di conversione\) o l'operando di sinistra di un operatore binario.  
  
 `operand2`  
 Obbligatorio per gli operatori binari.  Il nome e il tipo dell'operando di destra di un operatore binario.  
  
 `operand1` e `operand2` sono composti dalla sintassi e dalle parti elencate di seguito:  
  
 `[ ByVal ] operandname [ As operandtype ]`  
  
|Parte|Descrizione|  
|-----------|-----------------|  
|`ByVal`|Facoltativo, ma il meccanismo di passaggio deve essere [ByVal](../../../visual-basic/language-reference/modifiers/byval.md).|  
|`operandname`|Obbligatorio.  Nome della variabile che rappresenta questo operando.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`operandtype`|Facoltativo a meno che `Option Strict` sia `On`.  Tipo di dati di questo operando.|  
  
 `type`  
 Facoltativo a meno che `Option Strict` sia `On`.  Tipo di dati del valore restituito dalla routine operatore.  
  
 `statements`  
 Parametro facoltativo.  Blocco di istruzioni eseguite dalla routine operatore.  
  
 `returnvalue`  
 Obbligatorio.  Il valore restituito dalla routine operatore al codice che effettua la chiamata.  
  
 `End` `Operator`  
 Obbligatorio.  Termina la definizione di questa routine operatore.  
  
## Note  
 È possibile utilizzare `Operator` solo in una classe o struttura.  In altre parole il *contesto della dichiarazione* di un operatore non può essere un file di origine, uno spazio dei nomi, un modulo, un'interfaccia, una routine o un blocco.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Tutti gli operatori devono essere `Public Shared`.  Non è possibile specificare `ByRef`, `Optional` o `ParamArray` per uno dei due operandi.  
  
 Non è possibile utilizzare il simbolo dell'operatore o l'identificatore per contenere un valore restituito.  È necessario utilizzare l'istruzione `Return` ed è necessario che specifichi un valore.  È possibile inserire un numero illimitato di istruzioni `Return` in qualsiasi punto di una routine.  
  
 La definizione di un'operatore in questo modo viene denominata *overload dell'operatore*, sia che si usi o meno la parola chiave `Overloads`.  Nella tabella riportata di seguito sono elencati gli operatori che è possibile definire.  
  
|Type|Operatori|  
|----------|---------------|  
|Unario|`+`, `-`, `IsFalse`, `IsTrue`, `Not`|  
|Binary|`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`|  
|Conversione \(unario\)|`CType`|  
  
 Si noti che l'operatore `=` nell'elenco binario è l'operatore di confronto e non l'operatore di assegnazione.  
  
 Quando si definisce `CType`, è necessario specificare `Widening` o `Narrowing`.  
  
## Coppie associate  
 È necessario definire alcuni operatori come coppie associate.  Se si definisce ciascun operatore di tale coppia, è necessario definire anche l'altro.  Le coppie associate sono le seguenti:  
  
-   `=` e `<>`.  
  
-   `>` e `<`.  
  
-   `>=` e `<=`.  
  
-   `IsTrue` e `IsFalse`.  
  
## Limitazioni relative ai tipi di dati  
 È necessario che ogni operatore definito implichi la classe o la struttura nella quale la si definisce.  In altre parole è necessario che la classe o la struttura venga specificata come tipo di dati di quanto segue:  
  
-   L'operando di un operatore unario.  
  
-   Almeno uno degli operandi di un operatore binario.  
  
-   L'operando o il tipo restituito di un operatore di conversione.  
  
 Alcuni operatori hanno limitazioni relative ai tipi di dati, come illustrato di seguito:  
  
-   Se si definiscono gli operatori `IsTrue` e `IsFalse`questi devono restituire entrambi il tipo `Boolean`.  
  
-   Se si definiscono gli operatori `<<` e `>>` questi devono entrambi specificare il tipo `Integer` per il `operandtype` di `operand2`.  
  
 Non è necessario che il tipo restituito corrisponda al tipo dell'altro operando.  Un operatore di confronto come `=` o `<>`, ad esempio, è in grado di restituire `Boolean` anche se nessuno dei due operandi è `Boolean`.  
  
## Operatori logici e bit per bit  
 In Visual Basic gli operatori `And`, `Or`, `Not` e `Xor` sono in grado di eseguire operazioni logiche o bit per bit.  Tuttavia se si definisce uno di questi operatori su una classe o struttura, è possibile definire solo il suo funzionamento bit per bit.  
  
 Non è possibile definire l'operatore `AndAlso` direttamente con un'istruzione `Operator`.  Tuttavia è possibile utilizzare `AndAlso` se si sono soddisfatte le condizioni seguenti:  
  
-   È stato definito `And` sugli stessi tipi di operandi che si desidera utilizzare per `AndAlso`.  
  
-   La definizione di`And` restituirà lo stesso tipo della classe o della struttura nella quale si è definita.  
  
-   È stato definito l'operatore `IsFalse` nella classe o nella struttura nelle quali si è definito `And`.  
  
 Analogamente, è possibile utilizzare `OrElse` se si è definito `Or` sugli stessi operandi, con il tipo restituito della classe o struttura e si è definito `IsTrue` nella classe o struttura.  
  
## Conversioni di ampliamento e restrizione  
 Una *conversione di ampliamento* ha sempre esito positivo in fase di esecuzione, mentre una *conversione di restrizione* può non riuscire.  Per ulteriori informazioni, vedere [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
 Se si dichiara che una routine di conversione sia di `Widening`, è necessario che il codice della routine non generi alcun errore.  In altre parole:  
  
-   Deve sempre restituire un valore valido del tipo `type`.  
  
-   Deve gestire tutte le eccezioni possibili e le altre condizioni di errore.  
  
-   Deve gestire qualsiasi errore restituito da qualsiasi routine da lei chiamata.  
  
 Se esiste anche solo una possibilità che la routine di conversione non abbia esito positivo, o che possa causare un'eccezione non gestita, è necessario dichiararla come `Narrowing`.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene utilizzata l'istruzione `Operator` per definire il contorno di una struttura che include routine di operatore per gli operatori `And`, `Or`, `IsFalse` e `IsTrue`.  Gli operatori `And` e `Or` accettano entrambi due operatori di tipo `abc` e restituiscono il tipo `abc`.  Gli operatori `IsFalse` e `IsTrue` accettano entrambi un singolo operando di tipo `abc` e restituiscono il tipo `Boolean`.  Queste definizioni consentono al codice che effettua la chiamata di utilizzare `And`, `AndAlso`, `Or` e `OrElse` con operandi di tipo `abc`.  
  
 [!code-vb[VbVbalrStatements#44](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/operator-statement_1.vb)]  
  
## Vedere anche  
 [IsFalse Operator](../../../visual-basic/language-reference/operators/isfalse-operator.md)   
 [IsTrue Operator](../../../visual-basic/language-reference/operators/istrue-operator.md)   
 [Widening](../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [How to: Define an Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [How to: Define a Conversion Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [How to: Call an Operator Procedure](../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [How to: Use a Class that Defines Operators](../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)