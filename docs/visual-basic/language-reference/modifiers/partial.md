---
title: "Partial (Visual Basic) | Microsoft Docs"
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
  - "vb.Partial"
  - "partial"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "structures, partial"
  - "classes [Visual Basic]"
  - "partial, types [Visual Basic]"
  - "partial, structures"
  - "partial, classes [Visual Basic]"
  - "classes [Visual Basic], partial"
  - "Partial keyword [Visual Basic]"
  - "type promotion"
ms.assetid: 7adaef80-f435-46e1-970a-269fff63b448
caps.latest.revision: 36
caps.handback.revision: 36
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Partial (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Indica che una dichiarazione di tipo è una definizione parziale del tipo.  
  
 Si può dividere la definizione di un tipo tra più dichiarazioni mediante la parola chiave `Partial`.  Si può usare il numero di dichiarazioni parziali desiderato, in un numero qualsiasi di file di origine differenti.   Tutte le dichiarazioni, tuttavia, devono trovarsi nello stesso assembly e nello stesso spazio dei nomi.  
  
> [!NOTE]
>  Visual Basic supporta i *metodi parziali*, che in genere vengono implementati nelle classi parziali.  Per altre informazioni, vedere [Partial Methods](../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md) e [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md).  
  
## Sintassi  
  
```  
[ <attrlist> ] [ accessmodifier ] [ Shadows ] [ MustInherit | NotInheritable ] _  
Partial { Class | Structure | Interface | Module } name [ (Of typelist) ]  
    [ Inherits classname ]  
    [ Implements interfacenames ]  
    [ variabledeclarations ]  
    [ proceduredeclarations ]  
{ End Class | End Structure }  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`attrlist`|Parametro facoltativo.  Elenco degli attributi applicabili al tipo.  È necessario racchiudere l'[Attribute List](../../../visual-basic/language-reference/statements/attribute-list.md) tra parentesi angolari \(`< >`\).|  
|`accessmodifier`|Parametro facoltativo.  Specifica il tipo di codice che può accedere al tipo.  Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).|  
|`Shadows`|Parametro facoltativo.  Vedere [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md).|  
|`MustInherit`|Parametro facoltativo.  Vedere [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md).|  
|`NotInheritable`|Parametro facoltativo.  Vedere [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md).|  
|`name`|Necessario.  Nome del tipo.  Deve corrispondere al nome definito in tutte le altre dichiarazioni parziali dello stesso tipo.|  
|`Of`|Parametro facoltativo.  Specifica che si tratta di un tipo generico.  Vedere [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md).|  
|`typelist`|Obbligatorio se si usa [Of](../../../visual-basic/language-reference/statements/of-clause.md).  Vedere [Type List](../../../visual-basic/language-reference/statements/type-list.md).|  
|`Inherits`|Parametro facoltativo.  Vedere [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md).|  
|`classname`|Obbligatorio se si usa `Inherits`.  Nome della classe o dell'interfaccia da cui deriva la classe.|  
|`Implements`|Parametro facoltativo.  Vedere [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md).|  
|`interfacenames`|Obbligatorio se si usa `Implements`.  Nomi delle interfacce implementate dal tipo.|  
|`variabledeclarations`|Parametro facoltativo.  Istruzioni che dichiarano variabili ed eventi aggiuntivi per il tipo.|  
|`proceduredeclarations`|Parametro facoltativo.  Istruzioni che dichiarano e definiscono routine aggiuntive per il tipo.|  
|`End Class` o `End Structure`|Termina questa definizione `Class` o `Structure` parziale.|  
  
## Note  
 Visual Basic usa definizioni di classi parziali per separare il codice generato dal codice creato dall'utente in file di origine distinti.  Ad esempio, **Progettazione Windows Form** definisce classi parziali per controlli come <xref:System.Windows.Forms.Form>.  In questi controlli il codice generato non deve essere modificato.  
  
 Durante la creazione di un tipo parziale vengono applicate tutte le regole per la creazione delle classi, delle strutture, delle interfacce e dei moduli, ad esempio quelle relative all'uso dei modificatori e all'ereditarietà.  
  
## Suggerimenti  
  
-   In condizioni normali, non è consigliabile suddividere lo sviluppo di un singolo tipo in due o più dichiarazioni.  Pertanto, nella maggior parte dei casi non occorre specificare la parola chiave `Partial`.  
  
-   Per migliorare la leggibilità, ogni dichiarazione parziale di un tipo deve includere la parola chiave `Partial`.  Il compilatore consente che la parola chiave venga omessa al massimo in una dichiarazione parziale. Se viene omessa in due o più dichiarazioni, viene segnalato un errore.  
  
## Comportamento  
  
-   **Unione delle dichiarazioni** Il compilatore considera il tipo come l'unione di tutte le relative dichiarazioni parziali.  Ogni modificatore di ciascuna definizione parziale si applica all'intero tipo e ogni membro di ciascuna definizione parziale è disponibile per l'intero tipo.  
  
-   **Promozione tipo non consentita per i tipi parziali nei moduli.** Se una definizione parziale si trova all'interno di un modulo, l'effetto della promozione tipo di tale tipo viene automaticamente annullato.  In questo caso, un set di definizioni parziali può generare risultati imprevisti e persino errori del compilatore.  Per altre informazioni, vedere [Type Promotion](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md).  
  
     Il compilatore unisce le definizioni parziali solo se i relativi percorsi completi sono identici.  
  
 È possibile usare la parola chiave `Partial` nei contesti seguenti:  
  
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
## Esempio  
 L'esempio seguente suddivide la definizione della classe `sampleClass` in due dichiarazioni, ognuna delle quali definisce una routine `Sub` differente.  
  
 [!code-vb[VbVbalrKeywords#3](../../../visual-basic/language-reference/codesnippet/VisualBasic/partial_1.vb)]  
  
 Le due definizioni parziali nell'esempio precedente possono trovarsi nello stesso file di origine o in due file di origine differenti.  
  
## Vedere anche  
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Type Promotion](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)   
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Partial Methods](../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)