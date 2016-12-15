---
title: "Shared (Visual Basic) | Microsoft Docs"
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
  - "vb.Shared"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Shared keyword"
  - "members, shared"
  - "shared members"
  - "nonshared"
  - "shared elements"
  - "elements, shared"
ms.assetid: 2bf7cf2c-b0dd-485e-8749-b5d674dab4cd
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Shared (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che uno o più elementi di programmazione dichiarati sono alla fine associati a una classe o a una struttura, non a una specifica istanza della classe o della struttura.  
  
## Note  
  
## Utilizzo di Shared  
 Quando un membro di una classe o di una struttura è condiviso, è disponibile per tutte le istanze. Quando invece *non è condiviso*, ogni istanza dovrà conservare la propria copia.  Questa condizione risulta utile, ad esempio, se il valore di una variabile è applicabile all'intera applicazione.  Se la variabile viene dichiarata `Shared`, tutte le istanze accederanno allo stesso percorso di archiviazione e, se per una delle istanze viene modificato il valore della variabile, tutte le istanze accederanno al valore aggiornato.  
  
 La condivisione non altera il livello di accesso di un membro.  Ad esempio, un membro della classe può essere condiviso e privato \(accessibile solo dall'interno della classe\), o non condiviso e pubblico.  Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare la parola chiave `Shared` solo a livello di modulo.  In altri termini, il contesto della dichiarazione per un elemento `Shared` deve essere una classe o una struttura e non può essere un file di origine, uno spazio dei nomi o una routine.  
  
-   **Modificatori combinati.** Non è possibile specificare `Shared` insieme a [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md), [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md), [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md), [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md) o [Static](../../../visual-basic/language-reference/modifiers/static.md) nella stessa dichiarazione.  
  
-   **Accesso.** È possibile accedere a un elemento condiviso qualificandolo con il nome della relativa classe o struttura, non con il nome di variabile di una specifica istanza di tale classe o struttura.  Non è necessario neppure creare un'istanza di una classe o di una struttura per accedere ai relativi membri condivisi.  
  
     Nell'esempio riportato di seguito viene effettuata una chiamata alla routine condivisa <xref:System.Double.IsNaN%2A> esposta dalla struttura <xref:System.Double>.  
  
     `If Double.IsNaN(result) Then MsgBox("Result is mathematically undefined.")`  
  
-   **Condivisione implicita.** Non è possibile utilizzare il modificatore `Shared` in un'[Const Statement](../../../visual-basic/language-reference/statements/const-statement.md), ma le costanti sono condivise in modo implicito.  Analogamente, non è possibile dichiarare un membro di un modulo o di un'interfaccia come `Shared`, ma tali elementi sono condivisi in modo implicito.  
  
## Comportamento  
  
-   **Archiviazione.** Una variabile o un evento condiviso viene archiviato in memoria una sola volta, indipendentemente dal numero di istanze create della relativa classe o struttura.  Analogamente, una routine o una proprietà condivisa contiene un solo insieme di variabili locali.  
  
-   **Accesso mediante una variabile di istanza.** È possibile accedere a un elemento condiviso qualificandolo con il nome di una variabile che contiene una specifica istanza della relativa classe o struttura.  Anche se in genere questo sistema funziona correttamente, il compilatore genera un messaggio di avviso ed effettua l'accesso mediante il nome della classe o della struttura anziché della variabile.  
  
-   **Accesso mediante un'espressione di istanza.** Se si accede a un elemento condiviso mediante un'espressione che restituisce un'istanza della relativa classe o struttura, il compilatore effettua l'accesso mediante il nome della classe o della struttura, anziché valutare l'espressione.  In questo modo si ottengono risultati imprevisti se l'espressione, oltre a restituire l'istanza, doveva eseguire altre operazioni.  Questa condizione è illustrata nell'esempio che segue.  
  
    ```  
    Sub main()  
        shareTotal.total = 10  
        ' The preceding line is the preferred way to access total.  
        Dim instanceVar As New shareTotal  
        instanceVar.total += 100  
        ' The preceding line generates a compiler warning message and  
        ' accesses total through class shareTotal instead of through  
        ' the variable instanceVar. This works as expected and adds  
        ' 100 to total.  
        returnClass().total += 1000  
        ' The preceding line generates a compiler warning message and  
        ' accesses total through class shareTotal instead of calling  
        ' returnClass(). This adds 1000 to total but does not work as  
        ' expected, because the MsgBox in returnClass() does not run.  
        MsgBox("Value of total is " & CStr(shareTotal.total))  
    End Sub  
    Public Function returnClass() As shareTotal  
        MsgBox("Function returnClass() called")  
        Return New shareTotal  
    End Function  
    Public Class shareTotal  
        Public Shared total As Integer  
    End Class  
    ```  
  
     Nell'esempio precedente il compilatore genera un messaggio di avviso tutte e due le volte in cui il codice accede alla variabile condivisa `total` mediante un'istanza.  In ciascun caso, l'accesso viene effettuato direttamente mediante la classe `shareTotal` e non viene utilizzata alcuna istanza.  Nel caso della chiamata alla routine `returnClass`, non viene neppure generata una chiamata a `returnClass`, pertanto l'azione aggiuntiva di visualizzazione di "Function returnClass\(\) called" non viene eseguita.  
  
 Il modificatore `Shared` può essere utilizzato nei seguenti contesti:  
  
 [Istruzione Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Istruzione Operator](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Static](../../../visual-basic/language-reference/modifiers/static.md)   
 [Lifetime in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)