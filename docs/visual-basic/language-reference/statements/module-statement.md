---
title: "Module Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Module"
  - "vb.Module"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "modules, classes"
  - "modules"
  - "Module statement"
  - "modules, declaring"
  - "standard modules"
  - "classes [Visual Basic], vs. modules"
  - "declarations, modules"
ms.assetid: a1243afc-14a5-45df-95d5-51118aeac362
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Module Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di dichiarare il nome di un modulo e introduce la definizione di variabili, proprietà, eventi e procedure comprese dal modulo.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ]  Module name  
    [ statements ]  
End Module  
```  
  
## Parti  
 `attributelist`  
 Parametro facoltativo.  Vedere [Attribute List](../../../visual-basic/language-reference/statements/attribute-list.md).  
  
 `accessmodifier`  
 Parametro facoltativo.  ad esempio uno dei seguenti:  
  
-   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
 Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 `name`  
 Obbligatorio.  Nome di questo modulo.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
 `statements`  
 Parametro facoltativo.  Istruzioni che definiscono variabili, proprietà, eventi, metodi e tipi annidati di questo modulo.  
  
 `End Module`  
 Consente di terminare la definizione `Module`.  
  
## Note  
 Un'istruzione `Module` consente di definire un tipo di riferimento disponibile tramite il suo spazio dei nomi.  Un *modulo* \(denominato a volte *modulo standard*\)è simile a una classe ma con alcune distinzioni importanti.  Ogni modulo ha esattamente un'istanza e non deve essere creata o assegnata a una variabile.  I moduli non sono in grado di supportare interfacce di ereditarietà o implementazione.  Si noti che un modulo non è un *tipo* nello stesso senso di una classe o struttura. Non è possibile dichiarare che un elemento di programmazione abbia il tipo di dati di un modulo.  
  
 La parola chiave `Module` può essere utilizzata solo a livello di spazio dei nomi.  Il altri termini, il *contesto della dichiarazione* per un modulo deve essere costituito di un file di origine o uno spazio dei nomi e non può essere una classe, una struttura, un modulo, un'interfaccia, una routine o un blocco.  Non è possibile annidare un modulo all'interno di un altro modulo o all'interno di un tipo.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 La durata di un modulo corrisponde a quella del programma.  Poiché i suoi membri sono tutti `Shared` la loro durata corrisponde anch'essa a quella del programma.  
  
 L'impostazione predefinita dei moduli è l'accesso [Friend](../../../visual-basic/language-reference/modifiers/friend.md).  È possibile modificarne i livelli di accesso mediante gli appositi modificatori.  Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 Tutti i membri di un modulo sono `Shared` in modo implicito.  
  
## Classi e moduli  
 Questi elementi hanno molte similitudini, ma vi sono anche alcune differenze significative.  
  
-   **Terminologia.** Nelle versioni precedenti di Visual Basic vengono riconosciuti due tipi di moduli: *moduli di classe* \(file con estensione cls\) e *moduli standard*  \(file con estensione bas\).  La versione corrente li definisce *classi* e *moduli*, rispettivamente.  
  
-   **Membri condivisi.** È possibile controllare se un membro di una classe è un membro condiviso o dell'istanza.  
  
-   **Orientamento dell'oggetto.** Le classi sono orientate agli oggetti mentre i moduli no.  , quindi è possibile creare istanze come oggetti solo delle classi.  Per ulteriori informazioni, vedere [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md).  
  
## Regole  
  
-   **Modificatori.** Tutti i membri dei moduli sono considerati [Shared](../../../visual-basic/language-reference/modifiers/shared.md) in modo implicito.  Quando si dichiara un membro, non è possibile utilizzare la parola chiave `Shared` e non è possibile alterare lo stato condiviso di nessun membro.  
  
-   **Ereditarietà.** Un modulo non può ereditare da un tipo diverso da <xref:System.Object>, da cui ereditano tutti i moduli.  In particolare, un modulo non può ereditare da un'altro.  
  
     Non è possibile utilizzare l'[Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md) nella definizione di un modulo, anche per specificare <xref:System.Object>.  
  
-   **Proprietà predefinita.** Non è possibile definire proprietà predefinite in un modulo.  Per ulteriori informazioni, vedere [Default](../../../visual-basic/language-reference/modifiers/default.md).  
  
## Comportamento  
  
-   **Livello di accesso.** All'interno di un modulo è possibile dichiarare ogni membro con il suo livello di accesso personale.  L'impostazione predefinita dei membri del modulo è l'accesso [Public](../../../visual-basic/language-reference/modifiers/public.md), tranne che per variabili e costanti, la cui impostazione predefinita è l'accesso [Private](../../../visual-basic/language-reference/modifiers/private.md).  Quando un modulo ha un accesso più ristretto rispetto a uno dei suoi membri, avrà la precedenza il livello di accesso specificato del modulo.  
  
-   **Ambito.** L'ambito si trova nell'area di validità tramite il suo spazio dei nomi.  
  
     L'ambito di un membro di ogni modulo è l'intero modulo.  Si noti che tutti i membri sono sottoposti a una *promozione del tipo*, che fa sì che il loro ambito venga promosso allo spazio dei nomi contenente il modulo.  Per ulteriori informazioni, vedere [Type Promotion](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md).  
  
-   **Qualificazione.** Un progetto può contenere più moduli ed è possibile dichiarare i membri con lo stesso nome in due o più moduli.  Tuttavia è necessario qualificare qualsiasi riferimento a tale membro con il nome del modulo appropriato se il riferimento si trova al di fuori del modulo.  Per ulteriori informazioni, vedere [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
## Esempio  
 [!code-vb[VbVbalrStatements#69](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/module-statement_1.vb)]  
  
## Vedere anche  
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Type Promotion](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)