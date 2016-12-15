---
title: "Scope in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "module scope"
  - "scope, levels"
  - "module level"
  - "procedures, scope"
  - "declared elements, scope"
  - "namespaces, scope"
  - "scope, declared elements"
  - "scope, about scope"
  - "levels of scope"
  - "block scope"
  - "scope, Visual Basic"
  - "procedure scope"
ms.assetid: 208106fe-79c9-4eec-93c6-55f08548895f
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Scope in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'*ambito* di un elemento dichiarato è tutto l'insieme del codice che può fare riferimento a esso senza qualificarne il nome o renderlo disponibile tramite un'[Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  L'ambito di un elemento può essere relativo a uno dei livelli che seguono:  
  
|Livello|Descrizione|  
|-------------|-----------------|  
|Ambito blocco|Disponibile solo all'interno del blocco di codice in cui viene dichiarato|  
|Ambito routine|Disponibile per tutto il codice all'interno della routine in cui viene dichiarato|  
|Ambito modulo|Disponibile per tutto il codice all'interno del modulo, della classe o della struttura in cui viene dichiarato|  
|Ambito spazio dei nomi|Disponibile per tutto il codice all'interno dello spazio dei nomi in cui viene dichiarato|  
  
 Questi livelli di ambito vanno dal più ristretto \(blocco\) al più ampio \(spazio dei nomi\), dove per *ambito più ristretto* si intende il gruppo più piccolo di codice che può fare riferimento all'elemento senza qualifica.  Per ulteriori informazioni, vedere "Livelli di ambito" in questa pagina.  
  
## Specifica dell'ambito e definizione delle variabili  
 Specificare l'ambito di un elemento quando lo si dichiara.  L'ambito può dipendere dai fattori che seguono:  
  
-   L'area \(blocco, routine, modulo, classe o struttura\) nella quale l'elemento viene dichiarato  
  
-   Lo spazio dei nomi contenente la dichiarazione dell'elemento  
  
-   Il livello di accesso dichiarato per l'elemento  
  
 Prestare attenzione quando si definiscono variabili con lo stesso nome ma ambito diverso, perché questa operazione può comportare risultati non previsti.  Per ulteriori informazioni, vedere [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
## Livelli di ambito  
 Un elemento di programmazione è disponibile in tutta l'area nella quale viene dichiarato.  Tutti i codici nella stessa area possono fare riferimento all'elemento senza qualificarne il nome.  
  
### Ambito blocco  
 Un blocco è un insieme di istruzioni incluse nelle istruzioni di dichiarazione di inizio e fine, quale quella riportata di seguito:  
  
-   `Do` e `Loop`.  
  
-   `For` \[`Each`\] e `Next`  
  
-   `If` e `End If`.  
  
-   `Select` e `End Select`.  
  
-   `SyncLock` e `End SyncLock`.  
  
-   `Try` e `End Try`.  
  
-   `While` e `End While`.  
  
-   `With` e `End With`.  
  
 Una variabile dichiarata in un blocco può essere utilizzata solo all'interno di quel blocco.  Nell'esempio che segue l'ambito della variabile integer `cube` è il blocco tra `If` e `End If`. Non è più possibile fare riferimento a `cube` quando l'esecuzione esce dal blocco.  
  
```  
If n < 1291 Then  
    Dim cube As Integer  
    cube = n ^ 3  
End If  
```  
  
> [!NOTE]
>  Anche se l'ambito di una variabile è limitato a un blocco, la relativa durata resta quella dell'intera routine.  Se si inserisce il blocco più volte durante la routine, ciascuna variabile di blocco conserva il rispettivo valore precedente.  Per evitare risultati imprevisti in questo caso, è consigliabile inizializzare le variabili di blocco all'inizio del blocco.  
  
### Ambito routine  
 Un elemento dichiarato all'interno di una routine non è disponibile all'esterno di essa.  Solamente la routine che contiene la dichiarazione può utilizzarlo.  Le variabili a questo livello sono note anche come *variabili locali* e vengono dichiarate con l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md), con o senza la parola chiave [Static](../../../../visual-basic/language-reference/modifiers/static.md).  
  
 Ambiti routine e ambiti blocco sono strettamente correlati tra loro.  Se una variabile viene dichiarata all'interno di una routine ma all'esterno di eventuali blocchi interni alla routine, è possibile considerarla come dotata di ambito blocco, dove il blocco è l'intera routine.  
  
> [!NOTE]
>  Tutti gli elementi locali, anche se si tratta di variabili `Static`, sono privati rispetto alla routine nella quale sono visualizzati.  Non è possibile dichiarare un elemento utilizzando la parola chiave [Public](../../../../visual-basic/language-reference/modifiers/public.md) all'interno di una routine.  
  
### Ambito modulo  
 Per comodità, la singola espressione *a livello di modulo* fa riferimento ai moduli, alle classi e alle strutture.  È possibile dichiarare elementi a questo livello collocando l'istruzione di dichiarazione all'esterno di eventuali routine o blocchi ma internamente al modulo, alla classe o alla struttura.  
  
 Quando si effettua una dichiarazione a livello di modulo, il livello di accesso scelto determina l'ambito.  Anche lo spazio dei nomi che contiene il modulo, la classe o la struttura ha effetto sull'ambito.  
  
 Gli elementi per i quali si dichiara il livello di accesso [Private](../../../../visual-basic/language-reference/modifiers/private.md) sono disponibili per tutte le routine di quel modulo, ma non per il codice presente in un modulo diverso.  Se non si utilizzano parole chiave del livello di accesso, per l'istruzione `Dim` a livello di modulo verrà utilizzata l'impostazione predefinita `Private`.  È tuttavia possibile indicare l'ambito e il livello di accesso in modo più chiaro, utilizzando la parola chiave `Private` nell'istruzione `Dim`.  
  
 Nell'esempio che segue tutte le routine definite nel modulo possono fare riferimento alla variabile di stringa `strMsg`.  Quando viene chiamata la seconda routine, il contenuto della variabile di stringa `strMsg` viene visualizzato in una finestra di dialogo.  
  
```  
' Put the following declaration at module level (not in any procedure).  
Private strMsg As String  
' Put the following Sub procedure in the same module.  
Sub initializePrivateVariable()  
    strMsg = "This variable cannot be used outside this module."  
End Sub  
' Put the following Sub procedure in the same module.  
Sub usePrivateVariable()  
    MsgBox(strMsg)  
End Sub  
```  
  
### Ambito spazio dei nomi  
 Se si dichiara un elemento a livello di modulo, utilizzando la parola chiave [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) o [Public](../../../../visual-basic/language-reference/modifiers/public.md), tale elemento diventa disponibile per tutte le routine nello spazio dei nomi in cui è dichiarato.  Modificando l'esempio precedente come indicato di seguito, è possibile fare riferimento alla variabile di stringa `strMsg` da qualsiasi parte di codice nello spazio dei nomi della relativa dichiarazione.  
  
```  
' Include this declaration at module level (not inside any procedure).  
Public strMsg As String  
```  
  
 L'ambito spazio dei nomi include spazi dei nomi annidati.  Un elemento disponibile dall'interno di uno spazio dei nomi è disponibile anche dall'interno di qualsiasi spazio dei nomi annidato nel primo.  
  
 Se il progetto non contiene alcuna [Namespace Statement](../../../../visual-basic/language-reference/statements/namespace-statement.md), ogni elemento del progetto sarà contenuto nello stesso spazio dei nomi.  In questo caso, l'ambito spazio dei nomi può essere considerato come ambito del progetto.  Anche gli elementi `Public` di un modulo, una classe o una struttura sono disponibili per qualsiasi progetto che faccia riferimento al rispettivo progetto.  
  
## Scelta dell'ambito  
 Quando si dichiara una variabile, per la scelta del relativo ambito è necessario tenere presenti i punti riportati di seguito.  
  
### Vantaggi delle variabili locali  
 Le variabili locali sono da preferire per qualsiasi tipo di calcolo temporaneo per i motivi che seguono:  
  
-   **Prevenzione dei conflitti di nomi.** I nomi delle variabili locali non sono soggetti a conflitti.  È possibile, ad esempio, creare numerose routine diverse contenenti una variabile denominata `intTemp`.  Fino a quando ciascuna variabile `intTemp` viene dichiarata come variabile locale, ogni routine riconosce solo la propria versione di `intTemp`.  Ogni singola routine può modificare il valore nella propria `intTemp` locale senza effetto sulle variabili `intTemp` nelle altre routine.  
  
-   **Consumo di memoria.** Le variabili locali occupano memoria solo durante l'esecuzione della rispettiva routine.  Questa memoria viene rilasciata quando la routine viene restituita al codice chiamante.  Al contrario, le variabili [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) e [Static](../../../../visual-basic/language-reference/modifiers/static.md) occupano risorse di memoria finché l'applicazione non termina l'esecuzione. Si consiglia pertanto di utilizzarle solo quando necessario.  Le *variabili di istanza* occupano memoria finché l'istanza continua a esistere, pertanto sono meno efficienti delle variabili locali, tuttavia potenzialmente più efficienti delle variabili `Shared` o `Static`.  
  
### Riduzione dell'ambito  
 In generale, quando si dichiara una variabile o una costante, è buona norma di programmazione rendere l'ambito il più ristretto possibile. L'ambito blocco è il più ristretto.  Questo consente di ridurre l'utilizzo della memoria e la possibilità che il codice faccia erroneamente riferimento alla variabile sbagliata.  Analogamente, si consiglia di dichiarare una variabile [Static](../../../../visual-basic/language-reference/modifiers/static.md) solo quando è necessario conservarne il valore tra le chiamate di routine.  
  
## Vedere anche  
 [Declared Element Characteristics](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [How to: Control the Scope of a Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)   
 [Lifetime in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)