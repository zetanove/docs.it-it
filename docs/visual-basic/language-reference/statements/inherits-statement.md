---
title: "Inherits Statement | Microsoft Docs"
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
  - "vb.Inherits"
  - "Inherits"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Inherits statement"
  - "Inherits statement, syntax"
ms.assetid: 9e6fe042-9af3-4341-8093-fc3537770cf2
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Inherits Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente alla classe o interfaccia corrente di ereditare gli attributi, le variabili, i campi, le proprietà, le routine e gli eventi da un'altra classe o interfaccia.  
  
## Sintassi  
  
```  
Inherits basetypenames  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`basetypenames`|Obbligatorio.  Nome della classe dalla quale deriva la classe.<br /><br /> In alternativa<br /><br /> Nomi delle interfacce dalle quali deriva lì'interfaccia.  Utilizzare le virgole per separare più nomi.|  
  
## Note  
 È necessario che l'istruzione `Inherits` sia utilizzata nella prima riga non vuota e non riservata a commenti di una definizione di classe o di interfaccia.  Inserire tale istruzioni immediatamente dopo l'istruzione `Class` o `Interface`.  
  
 È possibile utilizzare `Inherits` solo in una classe o interfaccia.  Ciò significa che il contesto della dichiarazione per un'ereditarietà non può essere un file di origine, spazio dei nomi, struttura, modulo, routine o blocco.  
  
## Regole  
  
-   **Ereditarietà della classe.** Se una classe utilizza l'istruzione `Inherits` è possibile specificare una sola classe di base.  
  
     Una classe non può ereditare da una classe annidata all'interno di essa.  
  
-   **Ereditarietà di interfaccia.** Se un'interfaccia utilizzata l'istruzione `Inherits`, è possibile specificare una o più interfacce di base.  È possibile ereditare da due interfacce anche se ognuna di esse definisce un membro con lo stesso nome.  In questo caso il codice di implementazione deve utilizzare la qualifica per specificare quale membro sta implementando.  
  
     Un'interfaccia non può ereditare da un'altra interfaccia con un livello di accesso più restrittivo.  Un'interfaccia `Public`, ad esempio, non può ereditare da un'interfaccia con accesso `Friend`.  
  
     Un'interfaccia non può ereditare da un'interfaccia annidata all'interno di essa.  
  
 Un esempio di ereditarietà di classe in .NET Framework è la classe <xref:System.ArgumentException>, che eredita dalla classe <xref:System.SystemException>.  Questo fornisce a <xref:System.ArgumentException> tutte le proprietà e le routine predefinite richieste da eccezioni del sistema, quali la proprietà <xref:System.Exception.Message%2A> e il metodo <xref:System.Exception.ToString%2A>.  
  
 Un esempio di ereditarietà di interfaccia in .NET Framework è la classe <xref:System.Collections.ICollection>, che eredita dall'interfaccia <xref:System.Collections.IEnumerable>.  Con questa operazione <xref:System.Collections.ICollection> eredita la definizione dell'enumeratore richiesto per scorrere una raccolta.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata l'istruzione `Inherits` per illustrare come una classe denominata `thisClass` può ereditare tutti i membri di una classe base denominata `anotherClass`.  
  
 [!code-vb[VbVbalrStatements#37](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/inherits-statement_1.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata l'ereditarietà di interfacce multiple.  
  
 [!code-vb[VbVbalrStatements#38](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/inherits-statement_2.vb)]  
  
 L'interfaccia denominata `thisInterface` comprende ora tutte le definizioni nelle interfacce <xref:System.IComparable>, <xref:System.IDisposable> e <xref:System.IFormattable>. I membri ereditati forniscono rispettivamente il confronto specifico per tipo di due oggetti, mediante il rilascio delle risorse allocate, e l'espressione del valore di un oggetto come `String`.  Una classe che implementa `thisInterface` deve implementare ogni membro di ogni interfaccia base.  
  
## Vedere anche  
 [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)   
 [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Inheritance Basics](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)