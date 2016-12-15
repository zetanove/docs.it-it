---
title: "Inheritance Basics (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "derived classes, inheritance"
  - "MyClass keyword, using"
  - "MyBase keyword, using"
  - "Inherits statement, inheritance"
  - "overriding, Overridable keyword"
  - "MustInherit keyword, using"
  - "Overrides keyword, using"
  - "inheritance"
  - "MustInherit classes"
  - "MustOverride keyword, using"
  - "classes [Visual Basic], derived"
  - "NotInheritable keyword, using"
  - "base classes, extending properties and methods"
  - "NotOverridable keyword, using"
  - "base classes, inheritance"
  - "abstract classes, inheritance"
  - "overriding, Overrides keyword"
ms.assetid: dfc8deba-f5b3-4d1d-a937-7cb826446fc5
caps.latest.revision: 23
caps.handback.revision: 23
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Inheritance Basics (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'istruzione `Inherits` consente di dichiarare una nuova classe, denominata *classe derivata*, basata su una classe esistente, nota come *classe base*.  Nelle classi derivate vengono ereditati e possono essere estesi proprietà, metodi, eventi, campi e costanti definiti nella classe base.  Nella sezione seguente vengono descritte alcune delle regole dell'ereditarietà e i modificatori che possono essere utilizzati per modificare le modalità con cui le classi ereditano o sono ereditate:  
  
-   Per impostazione predefinita, tutte le classi sono ereditabili a meno che non siano contrassegnate dalla parola chiave `NotInheritable`.  A una classe è consentito ereditare da altre classi del progetto o da classi di altri assembly cui il progetto fa riferimento.  
  
-   A differenza dei linguaggi che consentono l'ereditarietà multipla, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente solo l'ereditarietà singola nelle classi. In altre parole, alle classi derivate è consentito ereditare da una sola classe base.  Sebbene nelle classi non sia consentita l'ereditarietà multipla, al loro interno è consentito implementare più interfacce in grado di svolgere in modo efficace la stessa funzione.  
  
-   Per impedire l'esposizione di elementi limitati di una classe base, è necessario che il tipo di accesso di una classe derivata sia uguale o più restrittivo di quello della classe base.  Una classe `Public` non può ad esempio ereditare una classe `Friend` o `Private` e una classe `Friend` non può ereditare una classe `Private`.  
  
## Modificatori di ereditarietà  
 Per supportare l'ereditarietà in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] sono stati introdotti le istruzioni e i modificatori a livello di classe:  
  
-   Istruzione `Inherits` \- Consente di specificare la classe base.  
  
-   Modificatore `NotInheritable` \- Utilizzato per impedire ai programmatori di utilizzare la classe come classe base.  
  
-   Modificatore `MustInherit` \- Consente di specificare che la classe può essere utilizzata solo come classe base.  Non è possibile creare direttamente istanze delle classi `MustInherit`. Tali classi possono essere create soltanto come istanze di classe base di una classe derivata.  In altri linguaggi di programmazione, come C\+\+ e C\#, questo tipo di classe viene indicato con il termine *classe astratta*.  
  
## Override di proprietà e metodi nelle classi derivate  
 In base all'impostazione predefinita, in una classe derivata vengono ereditati metodi e proprietà della classe base relativa.  Se è necessario che una proprietà o un metodo ereditato si comportino in modo diverso nella classe derivata è possibile eseguirne l'*override*.  È possibile definire una nuova implementazione del metodo nella classe derivata.  I seguenti modificatori consentono di controllare le modalità di override di proprietà e metodi:  
  
-   `Overridable` \- Consente di eseguire l'override di una proprietà o di un metodo di una classe all'interno di una classe derivata.  
  
-   `Overrides` \- Consente di eseguire l'override di una proprietà o di un metodo `Overridable` definito nella classe base.  
  
-   `NotOverridable` \- Consente di impedire l'override di una proprietà o un metodo in una classe che eredita.  Per impostazione predefinita, i metodi `Public` sono `NotOverridable`.  
  
-   `MustOverride` \- Utilizzato per eseguire l'override della proprietà o del metodo in una classe derivata.  Quando si utilizza la parola chiave `MustOverride`, la definizione del metodo consiste solo dell'istruzione `Sub`, `Function` o `Property`.  Non sono consentite altre istruzioni, in modo specifico, `End Sub` o `End Function`.  I metodi `MustOverride` devono essere dichiarati nelle classi `MustInherit`.  
  
 Si supponga di voler definire delle classi per la gestione dello stipendio.  È possibile definire una classe `Payroll` generica contenente un metodo `RunPayroll` che consente di calcolare lo stipendio di una settimana tipica.  `Payroll` potrà quindi essere utilizzata come classe base per una classe `BonusPayroll` più specializzata che consenta la distribuzione di bonus ai dipendenti.  
  
 La classe `BonusPayroll` può ereditare il metodo `PayEmployee`, definito nella classe base `Payroll`, ed eseguirne l'override.  
  
 Nell'esempio seguente viene definita una classe base `Payroll,` e una classe derivata `BonusPayroll`, nella quale viene eseguito l'override del metodo ereditato `PayEmployee`.  Attraverso la routine `RunPayroll` vengono creati e quindi passati un oggetto `Payroll` e un oggetto `BonusPayroll` a una funzione denominata `Pay`, che consente di eseguire il metodo `PayEmployee` di entrambi gli oggetti.  
  
 [!code-vb[VbVbalrOOP#28](../../../../visual-basic/misc/codesnippet/VisualBasic/inheritance-basics_1.vb)]  
  
## La parola chiave MyBase  
 La parola chiave `MyBase` si comporta come una variabile oggetto che fa riferimento alla classe di base dell'istanza corrente di una classe.  `MyBase` viene spesso utilizzata per accedere ai membri della classe di base sottoposti a override o nascosti in una classe derivata.  Nello specifico, `MyBase.New` viene utilizzato per chiamare in modo esplicito un costruttore di classe base da un costruttore di classe derivata.  
  
 Si supponga, ad esempio, di progettare una classe derivata che consente di eseguire l'override di un metodo ereditato dalla classe base.  Con il metodo sottoposto a override è possibile chiamare il metodo della classe base e modificare il valore restituito come indicato nel frammento di codice seguente:  
  
 [!code-vb[VbVbalrOOP#109](../../../../visual-basic/misc/codesnippet/VisualBasic/inheritance-basics_2.vb)]  
  
 Nell'elenco seguente sono indicate le limitazioni relative all'utilizzo di `MyBase`:  
  
-   `MyBase` si riferisce alla classe base immediatamente superiore nella gerarchia e ai relativi membri ereditati.  Non può essere utilizzata per accedere ai membri `Private` della classe.  
  
-   `MyBase` è una parola chiave e non un oggetto reale.  Non è pertanto possibile assegnare `MyBase` a una variabile, passarla a routine o utilizzarla in un confronto `Is`.  
  
-   Il metodo qualificato da `MyBase` non necessita di una definizione nella classe base immediata. È invece possibile definire tale metodo in una classe base ereditata in modo indiretto.  Affinché un riferimento qualificato da `MyBase` venga compilato correttamente, è necessario che una classe base contenga un metodo corrispondente al nome e ai tipi di parametri presenti nella chiamata.  
  
-   Non è possibile utilizzare `MyBase` per chiamare metodi `MustOverride` della classe base.  
  
-   `MyBase` non può essere utilizzato per qualificare se stesso.  Pertanto, il codice seguente non è valido:  
  
     `MyBase.MyBase.BtnOK_Click()`  
  
-   `MyBase` non può essere utilizzato nei moduli.  
  
-   Se la classe base si trova in un assembly diverso, non sarà possibile utilizzare `MyBase` per accedere ai membri della classe base contrassegnati come `Friend`.  
  
 Per ulteriori informazioni e un altro esempio, vedere [How to: Access a Variable Hidden by a Derived Class](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md).  
  
## La parola chiave MyClass  
 La parola chiave `MyClass` si comporta come una variabile oggetto che fa riferimento all'istanza corrente di una classe nella sua implementazione originale.  `MyClass` è simile a `Me`,  tuttavia tutte le chiamate di metodi e proprietà effettuate su `MyClass` vengono considerate come se il metodo o la proprietà fosse [NotOverridable](../../../../visual-basic/language-reference/modifiers/notoverridable.md).  Il metodo o la proprietà, quindi, non sono influenzati dall'override in una classe derivata.  
  
-   `MyClass` è una parola chiave e non un oggetto reale.  Non è pertanto possibile assegnare `MyClass` a una variabile, passarla a routine o utilizzarla in un confronto `Is`.  
  
-   `MyClass` si riferisce alla classe che la contiene e ai relativi membri ereditati.  
  
-   `MyClass` può essere utilizzata come qualificatore per i membri `Shared`.  
  
-   Non è possibile utilizzare `MyClass` in un metodo `Shared`. È tuttavia possibile utilizzare questa parola chiave in un metodo di istanza per accedere a un membro condiviso di una classe.  
  
-   `MyClass` non può essere utilizzata nei moduli standard.  
  
-   `MyClass` può essere utilizzata per qualificare un metodo definito in una classe base e per il quale non è disponibile un'implementazione in tale classe.  Questo riferimento ha lo stesso significato di `MyBase.`*Method*.  
  
 Nell'esempio seguente viene effettuato un confronto tra `Me` e `MyClass`:  
  
```  
Class baseClass  
    Public Overridable Sub testMethod()  
        MsgBox("Base class string")  
    End Sub  
    Public Sub useMe()  
        ' The following call uses the calling class's method, even if   
        ' that method is an override.  
        Me.testMethod()  
    End Sub  
    Public Sub useMyClass()  
        ' The following call uses this instance's method and not any  
        ' override.  
        MyClass.testMethod()  
    End Sub  
End Class  
Class derivedClass : Inherits baseClass  
    Public Overrides Sub testMethod()  
        MsgBox("Derived class string")  
    End Sub  
End Class  
Class testClasses  
    Sub startHere()  
        Dim testObj As derivedClass = New derivedClass()  
        ' The following call displays "Derived class string".  
        testObj.useMe()  
        ' The following call displays "Base class string".  
        testObj.useMyClass()  
    End Sub  
End Class  
```  
  
 Anche se `derivedClass` effettua l'override di `testMethod`, la parola chiave `MyClass` in `useMyClass` annulla gli effetti dell'override e la chiamata viene risolta dal compilatore nella versione di classe base di `testMethod`.  
  
## Vedere anche  
 [Inherits Statement](../../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)