---
title: "Class Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Class"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "class modules"
  - "Class statement"
  - "classes [Visual Basic], fields"
  - "fields, of classes"
  - "class types, class statements"
  - "classes [Visual Basic], creating"
  - "classes [Visual Basic], data members"
  - "data members, of classes"
ms.assetid: f2664f38-eb5a-4d4b-a374-1d041521fb6c
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# Class Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di dichiarare il nome di una classe e introduce la definizione delle variabili, delle proprietà, degli eventi e delle routine corrispondenti.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ MustInherit | NotInheritable ] [ Partial ] _  
Class name [ ( Of typelist ) ]  
    [ Inherits classname ]  
    [ Implements interfacenames ]  
    [ statements ]  
End Class  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`attributelist`|Parametro facoltativo.  Vedere [Elenco degli attributi](../../../visual-basic/language-reference/statements/attribute-list.md).|  
|`accessmodifier`|Parametro facoltativo.  ad esempio uno dei seguenti:<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).|  
|`Shadows`|Parametro facoltativo.  Vedere [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md).|  
|`MustInherit`|Parametro facoltativo.  Vedere [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md).|  
|`NotInheritable`|Parametro facoltativo.  Vedere [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md).|  
|`Partial`|Parametro facoltativo.  Indica che si tratta di una definizione parziale della classe.  Vedere [Partial](../../../visual-basic/language-reference/modifiers/partial.md).|  
|`name`|Obbligatorio.  Nome della classe.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`Of`|Parametro facoltativo.  Specifica che si tratta di una classe generica.|  
|`typelist`|Obbligatoria se si utilizza la parola chiave [Of](../../../visual-basic/language-reference/statements/of-clause.md).  Elenco di parametri di tipo per la classe.  Vedere [Elenco dei tipi](../../../visual-basic/language-reference/statements/type-list.md).|  
|`Inherits`|Parametro facoltativo.  Indica che la classe eredita membri di un'altra classe.  Vedere [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md).|  
|`classname`|Obbligatoria se si utilizza l'istruzione `Inherits`.  Nome della classe dalla quale deriva la classe.|  
|`Implements`|Parametro facoltativo.  Indica che la classe consente di implementare i membri di una o più interfacce.  Vedere [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md).|  
|`interfacenames`|Obbligatoria se si utilizza l'istruzione `Implements`.  Nomi delle interfacce implementate dalla classe.|  
|`statements`|Parametro facoltativo.  Istruzioni che definiscono i membri della classe corrente.|  
|`End Class`|Obbligatorio.  Consente di terminare la definizione `Class`.|  
  
## Note  
 Istruzione `Class` che definisce un nuovo tipo di dati.  Una *classe* rappresenta un blocco predefinito fondamentale per la programmazione orientata agli oggetti \(OOP\).  Per ulteriori informazioni, vedere [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md).  
  
 È possibile utilizzare `Class` solo a livello di modulo o di spazio dei nomi.  In altri termini, il *contesto della dichiarazione* per una classe deve essere un file di origine, uno spazio dei nomi, una classe, una struttura, un modulo o un'interfaccia e non può essere una routine o un blocco.  Per ulteriori informazioni, vedere [Declaration Contexts and Default Access Levels](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md).  
  
 Ciascuna istanza di una classe presenta una durata indipendente da tutte le altre istanze.  In questo caso la durata ha inizio quando viene creata da una clausola [New Operator](../../../visual-basic/language-reference/operators/new-operator.md) o da una funzione quale <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A> e termina dopo che tutte le variabili che fanno riferimento all'istanza sono state impostate su [Nothing](../../../visual-basic/language-reference/nothing.md) o sulle istanze di altre classi.  
  
 L'accesso predefinito delle classi è di tipo [Friend](../../../visual-basic/language-reference/modifiers/friend.md).  È possibile modificarne i livelli di accesso mediante gli appositi modificatori.  Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## Regole  
  
-   **Annidamento.** È possibile definire una classe all'interno di un'altra classe.  La classe esterna viene denominata *classe contenente* e la relativa classe interna viene denominata *classe annidata*.  
  
-   **Ereditarietà.** Se la classe utilizza l'[Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md), è possibile specificare una sola interfaccia o classe di base.  Una classe non può ereditare da più elementi.  
  
     Una classe non può ereditare da un'altra classe che dispone di un livello di accesso più restrittivo.  Ad esempio una classe `Public` non può ereditare da una classe `Friend`.  
  
     Una classe non può ereditare da una classe annidata all'interno di essa.  
  
-   **Implementazione.** Se la classe utilizza l'[Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md), è necessario implementare ogni membro definito da ogni interfaccia specificata in `interfacenames`.  Un'eccezione a questa regola è costituita dalla reimplementazione di un membro della classe base.  Per ulteriori informazioni, vedere "Reimplementazione" in [Implements](../../../visual-basic/language-reference/statements/implements-clause.md).  
  
-   **Proprietà predefinita.** Una classe può specificare soltanto una proprietà come *proprietà predefinita*.  Per ulteriori informazioni, vedere [Default](../../../visual-basic/language-reference/modifiers/default.md).  
  
## Comportamento  
  
-   **Livello di accesso.** In una classe è possibile dichiarare ogni membro con un proprio livello di accesso.  L'accesso predefinito dei membri di una classe è di tipo [Public](../../../visual-basic/language-reference/modifiers/public.md), ad eccezione delle variabili e delle costanti che presentano l'accesso predefinito [Private](../../../visual-basic/language-reference/modifiers/private.md).  Se una classe dispone di un accesso più limitato di quello dei suoi membri, il livello di accesso della classe è prioritario.  
  
-   **Ambito.** Una classe appartiene allo spazio dei nomi, alla classe, alla struttura o al modulo in cui è contenuta.  
  
     L'ambito di un ogni membro di un classe è l'intera classe.  
  
     **Durata.** Visual Basic non supporta le classi static.  Dal punto di vista funzionale un modulo si comporta come una classe static.  Per ulteriori informazioni, vedere [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md).  
  
     Le durate dei membri di classe dipendono dalla modalità e dal percorso della dichiarazione.  Per ulteriori informazioni, vedere [Lifetime in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md).  
  
-   **Qualificazione.** Il codice all'esterno di una classe deve qualificare il nome di un membro con il nome della classe.  
  
     Se il codice all'interno di una classe annidata crea un riferimento non qualificato a un elemento di programmazione, questo verrà cercato innanzitutto nella classe annidata, quindi nella classe che lo contiene e così via fino a raggiungere l'elemento più esterno.  
  
## Classi e moduli  
 Questi elementi hanno molte similitudini, ma vi sono anche alcune differenze significative.  
  
-   **Terminologia.** Nelle versioni precedenti di Visual Basic vengono riconosciuti due tipi di moduli: *moduli di classe* \(file con estensione cls\) e *moduli standard*  \(file con estensione bas\).  La versione corrente li definisce *classi* e *moduli*, rispettivamente.  
  
-   **Membri condivisi.** È possibile controllare se un membro di una classe è un membro condiviso o dell'istanza.  
  
-   **Orientamento dell'oggetto.** Le classi sono orientate agli oggetti mentre i moduli no.  È possibile creare una o più istanze di una classe.  Per ulteriori informazioni, vedere [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md).  
  
## Esempio  
 Nell'esempio seguente viene utilizzata un'istruzione `Class` per definire una classe e numerosi membri.  
  
 [!code-vb[VbVbalrStatements#62](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/class-statement_1.vb)]  
  
## Vedere anche  
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Structures and Classes](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)   
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Object Lifetime: How Objects Are Created and Destroyed](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Procedura: utilizzare una classe generica](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)