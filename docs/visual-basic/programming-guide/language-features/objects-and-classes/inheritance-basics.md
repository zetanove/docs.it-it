---
title: "Nozioni fondamentali sull&quot;ereditarietà (Visual Basic) | Documenti di Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- derived classes, inheritance
- MyClass keyword, using
- MyBase keyword, using
- Inherits statement, inheritance
- overriding, Overridable keyword
- MustInherit keyword, using
- Overrides keyword, using
- inheritance
- MustInherit classes
- MustOverride keyword, using
- classes [Visual Basic], derived
- NotInheritable keyword, using
- base classes, extending properties and methods
- NotOverridable keyword, using
- base classes, inheritance
- abstract classes, inheritance
- overriding, Overrides keyword
ms.assetid: dfc8deba-f5b3-4d1d-a937-7cb826446fc5
caps.latest.revision: 23
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
ms.openlocfilehash: 58aee9f8c348eb06daec2b8c9e332f3f2775bcb6
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="inheritance-basics-visual-basic"></a>Nozioni fondamentali sull'ereditarietà (Visual Basic)
Il `Inherits` istruzione viene utilizzata per dichiarare una nuova classe, denominata un *derivata*, in base a una classe esistente, nota come un *classe di base*. Le classi derivate ereditano e possono estendere, proprietà, metodi, eventi, campi e le costanti definite nella classe di base. Nella sezione seguente vengono descritte alcune delle regole per l'ereditarietà e i modificatori che è possibile utilizzare per modificare le classi modo ereditano o vengono ereditati:  
  
-   Per impostazione predefinita, tutte le classi sono ereditabili a meno che non contrassegnato con il `NotInheritable` (parola chiave). Le classi possono ereditare da altre classi nel progetto o dalle classi in altri assembly che fa riferimento al progetto.  
  
-   A differenza dei linguaggi che consentono l'ereditarietà multipla, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente l'ereditarietà singola solo nelle classi; ovvero le classi derivate possono avere una sola classe base. Sebbene l'ereditarietà multipla non è consentita nelle classi, le classi possono implementare più interfacce, che possono raggiungere la stessa funzione.  
  
-   Per impedire l'esposizione agli elementi in una classe base, il tipo di accesso di una classe derivata deve essere uguale o più restrittivo rispetto alla classe di base. Ad esempio, un `Public` classe non può ereditare un `Friend` o `Private` (classe) e un `Friend` classe non può ereditare un `Private` (classe).  
  
## <a name="inheritance-modifiers"></a>Modificatori di ereditarietà  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]vengono presentate le istruzioni seguenti a livello di classe e modificatori per supportare l'ereditarietà:  
  
-   `Inherits`istruzione: specifica la classe base.  
  
-   `NotInheritable`modificatore-impedisce ai programmatori di utilizzo della classe come classe base.  
  
-   `MustInherit`modificatore: Specifica che la classe è può essere utilizzata come classe di base. Le istanze di `MustInherit` le classi non possono essere create direttamente; essi possono essere create solo istanze della classe di base di una classe derivata. (Altri linguaggi di programmazione, ad esempio C++ e c#, utilizzano il termine *classe astratta* per descrivere tale classe.)  
  
## <a name="overriding-properties-and-methods-in-derived-classes"></a>Override di proprietà e metodi nelle classi derivate  
 Per impostazione predefinita, una classe derivata eredita le proprietà e metodi della classe base. Se una proprietà o metodo ha un comportamento diverso nella classe derivata può essere *sottoposto a override*. Vale a dire, è possibile definire una nuova implementazione del metodo nella classe derivata. I seguenti modificatori consentono di controllare le modalità di override di proprietà e metodi:  
  
-   `Overridable`-Consente di una proprietà o metodo in una classe può essere sottoposto a override in una classe derivata.  
  
-   `Overrides`: Esegue l'override di un `Overridable` proprietà o metodo definito nella classe di base.  
  
-   `NotOverridable`-Impedisce una proprietà o metodo viene sottoposto a override in una classe che eredita. Per impostazione predefinita, `Public` metodi sono `NotOverridable`.  
  
-   `MustOverride`È necessario che una classe derivata eseguono l'override di proprietà o metodo. Quando il `MustOverride` parola chiave viene utilizzata, la definizione del metodo è costituita solo il `Sub`, `Function`, o `Property` istruzione. Le altre istruzioni non sono consentite in modo specifico, non `End Sub` o `End Function` istruzione. `MustOverride`i metodi devono essere dichiarati `MustInherit` classi.  
  
 Si supponga che si desidera definire classi per la gestione delle retribuzioni. È possibile definire un oggetto generico `Payroll` classe che contiene un `RunPayroll` metodo che calcola retribuzioni per una settimana tipica. È quindi possibile utilizzare `Payroll` come classe base per una più specializzato `BonusPayroll` (classe), che può essere utilizzata durante la distribuzione di bonus ai dipendenti.  
  
 Il `BonusPayroll` classe può ereditare ed eseguire l'override, il `PayEmployee` metodo definito nella base `Payroll` (classe).  
  
 Nell'esempio seguente definisce una classe base, `Payroll,` e una classe derivata, `BonusPayroll`, che esegue l'override di un metodo ereditato, `PayEmployee`. Una routine, `RunPayroll`, crea e passa quindi un `Payroll` oggetto e un `BonusPayroll` oggetto a una funzione, `Pay`, che esegue il `PayEmployee` metodo di entrambi gli oggetti.  
  
 [!code-vb[28 VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/inheritance-basics_1.vb)]  
  
## <a name="the-mybase-keyword"></a>La parola chiave MyBase  
 Il `MyBase` (parola chiave) si comporta come una variabile oggetto che fa riferimento alla classe di base dell'istanza corrente di una classe. `MyBase`viene spesso utilizzato per accedere ai membri di classe di base sottoposti a override o nascosti in una classe derivata. In particolare, `MyBase.New` viene utilizzato per chiamare in modo esplicito un costruttore di classe di base da un costruttore di classe derivata.  
  
 Si supponga, ad esempio, che si progetta una classe derivata che esegue l'override di un metodo ereditato dalla classe di base. Il metodo sottoposto a override può chiamare il metodo nella classe di base e modificare il valore restituito, come illustrato nel frammento di codice seguente:  
  
 [!code-vb[VbVbalrOOP&#109;](../../../../visual-basic/misc/codesnippet/VisualBasic/inheritance-basics_2.vb)]  
  
 Nell'elenco seguente descrive le restrizioni sull'utilizzo di `MyBase`:  
  
-   `MyBase`fa riferimento alla classe base immediata e i relativi membri ereditati. Non può essere utilizzato per accedere a `Private` membri della classe.  
  
-   `MyBase`è una parola chiave, non un oggetto reale. `MyBase`non può essere assegnato a una variabile, passare alle procedure o utilizzato in un `Is` confronto.  
  
-   Il metodo che `MyBase` qualifica non deve essere definito nella classe base immediata; potrebbe invece essere definita in una classe base ereditata indirettamente. Affinché un riferimento qualificato da `MyBase` per compilare correttamente, una classe di base deve contenere un metodo corrispondente al nome e i tipi di parametri presenti nella chiamata.  
  
-   Non è possibile utilizzare `MyBase` chiamare `MustOverride` metodi della classe di base.  
  
-   `MyBase`non può essere utilizzato per qualificare se stesso. Pertanto, il codice seguente non è valido:  
  
     `MyBase.MyBase.BtnOK_Click()`  
  
-   `MyBase`non può essere utilizzata nei moduli.  
  
-   `MyBase`non può essere utilizzato per accedere ai membri di classe di base che sono contrassegnati come `Friend` se la classe di base si trova in un assembly diverso.  
  
 Per ulteriori informazioni e un altro esempio, vedere [procedura: accedere a una variabile nascosta da una classe derivata](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md).  
  
## <a name="the-myclass-keyword"></a>La parola chiave MyClass  
 Il `MyClass` (parola chiave) si comporta come una variabile oggetto che fa riferimento all'istanza corrente di una classe sua implementata originale. `MyClass`è simile a `Me`, ma tutti i metodi e proprietà chiamare su `MyClass` viene trattato come se fosse il metodo o proprietà [NotOverridable](../../../../visual-basic/language-reference/modifiers/notoverridable.md). Pertanto, il metodo o proprietà non è interessata eseguendo l'override in una classe derivata.  
  
-   `MyClass`è una parola chiave, non un oggetto reale. `MyClass`non può essere assegnato a una variabile, passare alle procedure o utilizzato in un `Is` confronto.  
  
-   `MyClass`fa riferimento a tale classe e i relativi membri ereditati.  
  
-   `MyClass`può essere utilizzato come qualificatore per `Shared` i membri.  
  
-   `MyClass`non può essere utilizzato all'interno di un `Shared` (metodo), ma può essere utilizzato all'interno di un metodo di istanza per accedere a un membro di una classe condiviso.  
  
-   `MyClass`non può essere utilizzata nei moduli standard.  
  
-   `MyClass`può essere utilizzato per qualificare un metodo definito in una classe base e che non ha un'implementazione del metodo fornito in tale classe. Questo riferimento ha lo stesso significato di `MyBase.` *metodo*.  
  
 Nell'esempio seguente vengono confrontate `Me` e `MyClass`.  
  
```vb
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
  
 Anche se `derivedClass` sostituzioni `testMethod`, `MyClass` (parola chiave) in `useMyClass` Annulla gli effetti dell'esecuzione dell'override e i compilatore risolve la chiamata alla versione della classe base di `testMethod`.  
  
## <a name="see-also"></a>Vedere anche  
 [Inherits (istruzione)](../../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Me, My, MyBase e MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)

