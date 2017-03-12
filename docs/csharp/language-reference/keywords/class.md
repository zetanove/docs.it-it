---
title: "class (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "class_CSharpKeyword"
  - "class"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "class (parola chiave) [C#]"
ms.assetid: b95d8815-de18-4c3f-a8cc-a0a53bdf8690
caps.latest.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# class (Riferimenti per C#)
Per la dichiarazione delle classi viene utilizzata la parola chiave `class`, come illustrato nell'esempio seguente:  
  
```  
  
      class TestClass  
{  
    // Methods, properties, fields, events, delegates   
    // and nested classes go here.  
}  
```  
  
## Note  
 Solo l'ereditarietà singola è consentita in c.  In altre parole, una classe può ereditare l'implementazione da una sola classe base.  Una classe è tuttavia in grado di implementare più di un'interfaccia.  Nella tabella che segue sono illustrati esempi di ereditarietà di classe e di implementazione di interfaccia.  
  
|Ereditarietà|Esempio|  
|------------------|-------------|  
|Nessuno|`class ClassA { }`|  
|Single|`class DerivedClass: BaseClass { }`|  
|Nessuna, implementa due interfacce|`class ImplClass: IFace1, IFace2 { }`|  
|Singola, implementa un'interfaccia|`class ImplDerivedClass: BaseClass, IFace1 { }`|  
  
 Le classi dichiarate direttamente all'interno di uno spazio dei nomi, non annidate all'interno di altre classi, è possibile [pubblico](../../../csharp/language-reference/keywords/public.md) o [interno](../../../csharp/language-reference/keywords/internal.md).  Le classi sono `internal` per impostazione predefinita.  
  
 I membri della classe, incluse le classi annidate, è possibile [pubblico](../../../csharp/language-reference/keywords/public.md), `protected internal`, [protetta](../../../csharp/language-reference/keywords/protected.md), [interno](../../../csharp/language-reference/keywords/internal.md), o [privato](../../../csharp/language-reference/keywords/private.md).  I membri sono [privato](../../../csharp/language-reference/keywords/private.md) per impostazione predefinita.  
  
 Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 È possibile dichiarare le classi generiche con parametri di tipo.  Per ulteriori informazioni, vedere [Classi generiche](../../../csharp/programming-guide/generics/generic-classes.md).  
  
 Una classe può contenere dichiarazioni dei seguenti membri:  
  
-   [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
-   [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
-   [Costanti](../../../csharp/programming-guide/classes-and-structs/constants.md)  
  
-   [Campi](../../../csharp/programming-guide/classes-and-structs/fields.md)  
  
-   [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)  
  
-   [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)  
  
-   [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
  
-   [Eventi](../../../csharp/programming-guide/events/index.md)  
  
-   [Delegati](../../../csharp/programming-guide/delegates/index.md)  
  
-   [Classi](../../../csharp/programming-guide/classes-and-structs/classes.md)  
  
-   [Interfacce](../../../csharp/programming-guide/interfaces/index.md)  
  
-   [Strutture](../../../csharp/programming-guide/classes-and-structs/structs.md)  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata la dichiarazione di costruttori, metodi e campi di classi.  Viene inoltre descritta la creazione di istanze di oggetti e la stampa di dati di un'istanza.  In questo esempio vengono dichiarate due classi, la classe `Child`, che contiene due campi privati \(`name` e `age`\) e due metodi pubblici.  La seconda classe, `StringTest`, viene utilizzata per contenere `Main`.  
  
 [!code-cs[csrefKeywordsTypes#5](../../../csharp/language-reference/keywords/codesnippet/csharp/class_1.cs)]  
  
## Commenti  
 Si noti, nell'esempio precedente, che è possibile accedere ai campi privati \(`name` e `age`\) solo tramite i metodi pubblici della classe `Child`.  Non è quindi possibile stampare il nome del bambino dal metodo `Main` utilizzando un'istruzione come quella riportata di seguito.  
  
```  
Console.Write(child1.name);   // Error  
```  
  
 L'accesso ai membri privati di `Child` da `Main` è possibile solo se `Main` è un membro della classe.  
  
 Tipi una classe interna dichiarata senza un'impostazione predefinita al modificatore di accesso a `private`, i membri dati in questo esempio rimane sempre `private` se la parola chiave è stata rimossa.  
  
 Si noti infine che per l'oggetto creato mediante il costruttore predefinito \(`child3`\), il campo dell'età è stato inizializzato su zero per impostazione predefinita.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)