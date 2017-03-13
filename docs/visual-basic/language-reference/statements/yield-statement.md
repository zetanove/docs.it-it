---
title: "Istruzione Yield (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Yield"
helpviewer_keywords: 
  - "iteratori, istruzione Yield [Visual Basic]"
  - "iteratori [Visual Basic]"
  - "Yield (istruzione) [Visual Basic]"
ms.assetid: f33126c5-d7c4-43e2-8e36-4ae3f0703d97
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Istruzione Yield (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Invia il successivo elemento di una raccolta a un'istruzione di `For Each...Next`.  
  
## Sintassi  
  
```  
Yield expression  
```  
  
#### Parametri  
  
|||  
|-|-|  
|Termine|Definizione|  
|`expression`|Necessario.  Un'espressione che sono implicitamente convertibile nel tipo di funzione o iteratori di accesso a `Get` contenente l'istruzione di `Yield`.|  
  
## Note  
 L'istruzione di `Yield` restituisce un elemento di una raccolta alla volta.  L'istruzione di `Yield` viene incluso in una funzione iteratori o in una funzione di accesso di `Get`, che eseguono le iterazioni personalizzate in una raccolta.  
  
 Si utilizza una funzione di iteratore utilizzando [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md) o una query LINQ.  Ogni iterazione del ciclo di `For Each` chiama la funzione di iteratore.  Quando un'istruzione di `Yield` viene raggiunto la funzione di iteratore, `expression` viene restituito e la posizione corrente nel codice vengono mantenute.  L'esecuzione verrà riavviata da tale percorso alla successiva apertura della funzione di iteratore è denominata.  
  
 Una conversione implicita deve esistere dal tipo di `expression` nell'istruzione di `Yield` al tipo restituito dell'iteratore.  
  
 È possibile utilizzare un'istruzione di `Return` o di `Exit Function` per terminare l'iterazione.  
  
 "Yield" non è una parola riservata e ha un significato speciale solo quando viene utilizzato in una funzione di `Iterator` o in una funzione di accesso di `Get`.  
  
 Per ulteriori informazioni sulle funzioni iteratori e sulle funzioni di accesso di `Get`, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Funzioni e funzioni di accesso get di iteratore  
 La dichiarazione di una funzione iteratori o di una funzione di accesso `Get` deve soddisfare i seguenti requisiti:  
  
-   Deve includere un modificatore di [Iteratore](../../../visual-basic/language-reference/modifiers/iterator.md).  
  
-   Il tipo restituito deve essere <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, o <xref:System.Collections.Generic.IEnumerator%601>.  
  
-   Non può avere parametri di `ByRef`.  
  
 Una funzione iteratori non può verificarsi di un evento, in un costruttore di istanza, in un costruttore statico, o un distruttore statico.  
  
 Una funzione iteratori può essere una funzione anonima.  Per ulteriori informazioni, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Gestione delle eccezioni  
 Un'istruzione di `Yield` può essere in un blocco di `Try` di [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  Un blocco `Try` con un'istruzione `Yield` può contenere blocchi `Catch` e può presentare un blocco `Finally`.  
  
 Un'istruzione `Yield` non può trovarsi all'interno di un blocco `Catch` o di un blocco `Finally`.  
  
 Se il corpo di `For Each` \(l'esterno della funzione iteratori\) genera un'eccezione, un blocco di `Catch` nella funzione iteratori non viene eseguito, ma un blocco di `Finally` nella funzione di iteratore viene eseguito.  Un blocco `Catch` in una funzione iteratore rileva solo le eccezioni che si verificano nella funzione iteratore.  
  
## Implementazione tecnica  
 Il codice seguente restituisce `IEnumerable (Of String)` da una funzione iteratori e quindi scorrere gli elementi di `IEnumerable (Of String)`.  
  
```vb  
Dim elements As IEnumerable(Of String) = MyIteratorFunction()  
    …  
For Each element As String In elements  
Next  
```  
  
 La chiamata a `MyIteratorFunction` non esegue il corpo della funzione.  Anziché la chiamata `IEnumerable(Of String)` nella variabile di `elements`.  
  
 In un'iterazione del ciclo di `For Each`, il metodo di <xref:System.Collections.IEnumerator.MoveNext%2A> viene chiamato per `elements`.  Questa chiamata viene eseguito il corpo di `MyIteratorFunction` fino a raggiungere la successiva istruzione di `Yield`.  L'istruzione di `Yield` restituisce un'espressione che determina non solo il valore della variabile di `element` per l'utilizzo dal corpo del ciclo ma anche la proprietà di <xref:System.Collections.Generic.IEnumerator%601.Current%2A> di elementi, che è `IEnumerable (Of String)`.  
  
 In ogni iterazione successiva del ciclo di `For Each`, l'esecuzione del corpo iteratori continua da dove era stato interrotto, ancora arrestando quando raggiunge un'istruzione di `Yield`.  Il ciclo di `For Each` completa quando la fine della funzione iteratori o un'istruzione di `Exit Function` o di `Return` viene soddisfatta.  
  
## Esempio  
 L'esempio seguente contiene un'istruzione di `Yield` presente in un ciclo di [Per… next](../../../visual-basic/language-reference/statements/for-next-statement.md).  Ogni iterazione del corpo dell'istruzione [For Each](../../../visual-basic/language-reference/statements/for-each-next-statement.md) in `Main` crea una chiamata alla funzione iteratore di `Power`.  Ogni chiamata alla funzione iteratori procederà all'esecuzione di un'istruzione di `Yield`, che si verifica durante l'iterazione successiva del ciclo di `For…Next`.  
  
 Il tipo restituito del metodo di iteratore è <xref:System.Collections.Generic.IEnumerable%601>, un tipo di interfaccia iteratori.  Quando il metodo di iteratore viene chiamato, restituisce un oggetto enumerabile che include potenze di un numero.  
  
 [!code-vb[VbVbalrStatements#98](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/yield-statement_1.vb)]  
  
## Esempio  
 Il seguente esempio viene illustrata una funzione di accesso `Get` che è un iteratore.  La dichiarazione di proprietà include un modificatore di `Iterator`.  
  
 [!code-vb[VbVbalrStatements#99](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/yield-statement_2.vb)]  
  
 Per ulteriori esempi, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Requisiti  
 [!INCLUDE[vs_dev11_long](../../../csharp/includes/vs-dev11-long-md.md)]  
  
## Vedere anche  
 [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md)   
 [Statements](../../../visual-basic/language-reference/statements/index.md)