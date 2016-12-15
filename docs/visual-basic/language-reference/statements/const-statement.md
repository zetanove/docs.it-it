---
title: "Const Statement (Visual Basic) | Microsoft Docs"
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
  - "vb.Const"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Const statement [Visual Basic]"
ms.assetid: 495b318d-b7c5-4198-94f8-0790a541b07a
caps.latest.revision: 28
caps.handback.revision: 28
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Const Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di dichiarare e definire una o più costanti.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ]   
Const constantlist  
```  
  
## Parti  
 `attributelist`  
 Parametro facoltativo.  Elenco di attributi applicabili a tutte le costanti dichiarate nell'istruzione.  Vedere [Attribute List](../../../visual-basic/language-reference/statements/attribute-list.md) tra parentesi angolari \("`<`" e "`>`"\).  
  
 `accessmodifier`  
 Parametro facoltativo.  Consente di specificare il codice con cui accedere alle costanti.  Sono consentiti i valori seguenti: [Public](../../../visual-basic/language-reference/modifiers/public.md), [Protected](../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../visual-basic/language-reference/modifiers/friend.md), `Protected Friend` o [Private](../../../visual-basic/language-reference/modifiers/private.md).  
  
 `Shadows`  
 Parametro facoltativo.  Consente di ridichiarare e nascondere un elemento di programmazione nella classe base.  Vedere [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md).  
  
 `constantlist`  
 Obbligatorio.  Elenco delle costanti dichiarate in questa istruzione.  
  
 `constant` `[ ,` `constant` `... ]`  
  
 Ogni `constant` presenta la sintassi e le parti seguenti:  
  
 `constantname` `[ As` `datatype` `] =` `initializer`  
  
|Parte|Descrizione|  
|-----------|-----------------|  
|`constantname`|Obbligatorio.  Nome della costante.  Vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`datatype`|Obbligatoria se `Option Strict` è `On`.  Consente di indicare il tipo di dati della costante.|  
|`initializer`|Obbligatorio.  Espressione valutata in fase di compilazione e assegnata alla costante.|  
  
## Note  
 Se nell'applicazione è contenuto un valore che non viene mai modificato, è possibile definire una costante denominata e utilizzarla al posto di un valore letterale.  È più facile ricordare un nome che un valore.  È possibile definire la costante una sola volta e utilizzarla in numerose posizioni del codice.  Se in una versione successiva è necessario ridefinire il valore, l'istruzione `Const` è l'unico luogo in cui si dovranno effettuare modifiche.  
  
 È possibile utilizzare l'istruzione `Const` solo a livello di modulo o di routine.  In altri termini, il *contesto della dichiarazione* per una variabile deve essere una classe, una struttura, un modulo, una routine o un blocco, e non può essere un file di origine, uno spazio dei nomi o un'interfaccia.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Le costanti locali all'interno di una routine per impostazione predefinita dispongono di accesso pubblico e non è possibile utilizzare modificatori di accesso per tali variabili.  Per impostazione predefinita, le costanti dei membri di classi e moduli al di fuori di una routine dispongono di accesso privato, mentre le costanti membri di strutture dispongono di accesso pubblico.  È possibile modificarne i livelli di accesso mediante gli appositi modificatori.  
  
## Regole  
  
-   **Contesto della dichiarazione.** Una costante dichiarata a livello di modulo, al di fuori di una routine, è una *costante membro* ed è membro della classe, della struttura o del modulo che la dichiara.  
  
     Una costante dichiarata a livello di routine è una *costante locale* ed è locale per la routine o il blocco che la dichiara.  
  
-   **Attributi.** È possibile applicare gli attributi solo alle costanti membri e non alle costanti locali.  Un attributo fornisce ai metadati dell'assembly informazioni non significative per archivi temporanei quali le costanti locali.  
  
-   **Modificatori.** Per impostazione predefinita, tutte le costanti sono `Shared`, `Static` e `ReadOnly`.  Non è possibile utilizzare queste parole chiave per dichiarare una costante.  
  
     A livello di routine non è possibile utilizzare `Shadows` né i modificatori di accesso per dichiarare le costanti locali.  
  
-   **Costanti multiple.** È possibile dichiarare più costanti nella stessa istruzione di dichiarazione, specificando per ognuna la parte `constantname` e separandole con una virgola.  
  
## Regole per tipi di dati  
  
-   **Tipi di dati.** L'istruzione `Const` può dichiarare il tipo di dati di una variabile.  È possibile specificare un tipo di dati o il nome di una enumerazione.  
  
-   **Tipo predefinito.** Se non si specifica `datatype`, la costante accetta il tipo di dati di `initializer`.  Se si specificano sia la parte `datatype` che la parte `initializer`, il tipo di dati di `initializer` deve poter essere convertito in `datatype`.  Se non vengono specificate né `datatype` né `initializer`, verrà utilizzato il tipo di dati predefinito `Object`.  
  
-   **Tipi differenti.** È possibile specificare tipi diversi di dati per costanti diverse utilizzando una clausola `As` distinta per ogni variabile dichiarata.  Non è tuttavia possibile dichiarare più costanti dello stesso tipo utilizzando una clausola `As` comune.  
  
-   **Inizializzazione.** È necessario inizializzare il valore di ogni costante in `constantlist`.  Per fornire un'espressione da assegnare alla costante, viene utilizzato `initializer`.  L'espressione può essere composta da una combinazione di valori letterali, da altre costanti già definite e da membri di enumerazione già definiti.  Per combinare tali elementi è possibile utilizzare operatori aritmetici e logici.  
  
     Nella parte `initializer` non è possibile utilizzare variabili o funzioni,  ma è consentito l'utilizzo di parole chiave di conversione quali `CByte` e `CShort`.  È inoltre possibile utilizzare `AscW`, se lo si chiama con una costante `String` o un argomento `Char`, poiché è possibile eseguirne la valutazione in fase di compilazione.  
  
## Comportamento  
  
-   **Ambito.** È possibile accedere alle costanti locali solo dall'interno della routine o del blocco a cui appartengono.  È possibile accedere alle costanti membri dall'interno della classe, struttura o modulo a cui appartengono.  
  
-   **Qualificazione.** Il codice al di fuori di una classe, di una struttura o di un modulo deve qualificare il nome di una costante membro con il nome di tale classe, struttura o modulo.  Il codice al di fuori di una routine o di un blocco non può fare riferimento a costanti locali interne a tale routine o blocco.  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Const` viene utilizzata per dichiarare costanti da utilizzare in sostituzione dei valori letterali.  
  
 [!code-vb[VbVbalrStatements#13](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/const-statement_1.vb)]  
  
## Esempio  
 Se viene definita una costante con il tipo di dati `Object`, il compilatore di Visual Basic assegnerà il tipo di dati `initializer` invece che `Object`.  Nell'esempio seguente, alla costante `naturalLogBase` viene associato il tipo `Decimal` in fase di esecuzione.  
  
 [!code-vb[VbVbalrStatements#87](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/const-statement_2.vb)]  
  
 Nell'esempio precedente viene utilizzato il metodo <xref:System.Type.ToString%2A> sull'oggetto <xref:System.Type> restituito da [GetType Operator](../../../visual-basic/language-reference/operators/gettype-operator.md), poiché non è possibile convertire <xref:System.Type> in `String` utilizzando `CStr`.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 [Enum Statement](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [\#Const Directive](../../../visual-basic/language-reference/directives/const-directive.md)   
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [ReDim Statement](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Constants and Enumerations](../../../visual-basic/programming-guide/language-features/constants-enums/index.md)   
 [Constants and Enumerations](../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)