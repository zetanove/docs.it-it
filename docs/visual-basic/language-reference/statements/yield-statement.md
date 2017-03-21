---
title: Istruzione yield (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Yield
helpviewer_keywords:
- iterators, Yield statement [Visual Basic]
- iterators [Visual Basic]
- Yield statement [Visual Basic]
ms.assetid: f33126c5-d7c4-43e2-8e36-4ae3f0703d97
caps.latest.revision: 22
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 393a9f4de3e801aed5932aef0e2b13d76b003965
ms.lasthandoff: 03/13/2017

---
# <a name="yield-statement-visual-basic"></a>Istruzione Yield (Visual Basic)
Invia l'elemento successivo di una raccolta a un `For Each...Next` istruzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Yield expression  
```  
  
#### <a name="parameters"></a>Parametri  
  
|Termine|Definizione|  
|---|---|  
|`expression`|Obbligatorio. Un'espressione che è implicitamente convertibile nel tipo di funzione iteratore o `Get` funzione di accesso che contiene il `Yield` istruzione.|  
  
## <a name="remarks"></a>Note  
 Il `Yield` istruzione restituisce un elemento di una raccolta in una fase. Il `Yield` istruzione è inclusa in una funzione iteratore o `Get` funzione di accesso, che consentono di eseguire iterazioni personalizzate su una raccolta.  
  
 Si utilizza una funzione iteratore tramite un [For Each... Istruzione successiva](../../../visual-basic/language-reference/statements/for-each-next-statement.md) o una query LINQ. Ogni iterazione del `For Each` ciclo chiama la funzione iteratore. Quando un `Yield` viene raggiunta l'istruzione nella funzione iteratore `expression` viene restituito, e viene mantenuta la posizione corrente nel codice. L'esecuzione viene riavviata a partire da quella posizione la volta successiva che viene chiamata la funzione iteratore.  
  
 Deve esistere una conversione implicita dal tipo di `expression` nel `Yield` istruzione per il tipo restituito dell'iteratore.  
  
 È possibile utilizzare un `Exit Function` o `Return` istruzione per terminare l'iterazione.  
  
 "Rendimento" non è una parola riservata e ha un significato speciale solo quando viene utilizzato in un `Iterator` funzione o `Get` della funzione di accesso.  
  
 Per ulteriori informazioni sulle funzioni di iteratore e `Get` funzioni di accesso, vedere [iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7).  
  
## <a name="iterator-functions-and-get-accessors"></a>Funzioni di iteratore e funzioni di accesso Get  
 La dichiarazione di una funzione iteratore o `Get` della funzione di accesso deve soddisfare i requisiti seguenti:  
  
-   Deve includere un [iteratore](../../../visual-basic/language-reference/modifiers/iterator.md) modificatore.  
  
-   Il tipo restituito deve essere <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, o <xref:System.Collections.Generic.IEnumerator%601>.</xref:System.Collections.Generic.IEnumerator%601> </xref:System.Collections.IEnumerator> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable>  
  
-   Non può avere qualsiasi `ByRef` parametri.  
  
 Una funzione iteratore non può trovarsi in un evento, costruttore di istanza, un costruttore statico o distruttore statico.  
  
 Una funzione iteratore può essere una funzione anonima. Per altre informazioni, vedere [Iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7).  
  
## <a name="exception-handling"></a>Gestione delle eccezioni  
 Un `Yield` istruzione può essere contenuta in un `Try` blocco di un [Try... Catch... Istruzione finally](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md). Oggetto `Try` blocco che ha un `Yield` istruzione possono essere presenti `Catch` blocca e può avere un `Finally` blocco.  
  
 Oggetto `Yield` istruzione non può essere all'interno di un `Catch` blocco o un `Finally` blocco.  
  
 Se il `For Each` corpo (all'esterno della funzione iteratore) genera un'eccezione, un `Catch` blocco nella funzione iteratore non viene eseguita, ma un `Finally` try nella funzione iteratore. Oggetto `Catch` blocco all'interno di una funzione iteratore intercetta solo le eccezioni che si verificano all'interno della funzione iteratore.  
  
## <a name="technical-implementation"></a>Implementazione tecnica  
 Il codice seguente restituisce un `IEnumerable (Of String)` da una funzione iteratore e quindi scorre gli elementi del `IEnumerable (Of String)`.  
  
```vb  
Dim elements As IEnumerable(Of String) = MyIteratorFunction()  
    …  
For Each element As String In elements  
Next  
```  
  
 La chiamata a `MyIteratorFunction` non esegue il corpo della funzione. La chiamata restituisce invece `IEnumerable(Of String)` nella variabile `elements`.  
  
 In un'iterazione del `For Each` ciclo, il <xref:System.Collections.IEnumerator.MoveNext%2A>viene chiamato per `elements`.</xref:System.Collections.IEnumerator.MoveNext%2A> Questa chiamata esegue il corpo di `MyIteratorFunction` fino a quando non viene raggiunta l'istruzione `Yield` successiva. Il `Yield` l'istruzione restituisce un'espressione che determina non solo il valore del `element` variabile per l'utilizzo dal corpo del ciclo, ma anche la <xref:System.Collections.Generic.IEnumerator%601.Current%2A>proprietà degli elementi, ovvero un `IEnumerable (Of String)`.</xref:System.Collections.Generic.IEnumerator%601.Current%2A>  
  
 In ogni iterazione successiva del ciclo `For Each`, l'esecuzione del corpo dell'iteratore continua da dove è stata interrotta, fermandosi ancora quando raggiunge un'istruzione `Yield`. Il `For Each` ciclo viene completato quando la fine della funzione iteratore o un `Return` o `Exit Function` viene raggiunta l'istruzione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente è presente un `Yield` istruzione all'interno di un [per... Avanti](../../../visual-basic/language-reference/statements/for-next-statement.md) ciclo. Ogni iterazione del [per ogni](../../../visual-basic/language-reference/statements/for-each-next-statement.md) corpo dell'istruzione in `Main` crea una chiamata per il `Power` funzione iteratore. Ogni chiamata alla funzione iteratore procede fino alla prossima esecuzione dell'istruzione `Yield`, che si verifica durante l'iterazione successiva del ciclo `For…Next`.  
  
 Il tipo restituito del metodo iteratore è <xref:System.Collections.Generic.IEnumerable%601>, un tipo di interfaccia iteratore.</xref:System.Collections.Generic.IEnumerable%601> Quando il metodo iteratore viene chiamato, restituisce un oggetto enumerabile che contiene le potenze di un numero.  
  
 [!code-vb[&#98; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/yield-statement_1.vb)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata una funzione di accesso `Get` che è un iteratore. La dichiarazione di proprietà include un `Iterator` modificatore.  
  
 [!code-vb[VbVbalrStatements&#99;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/yield-statement_2.vb)]  
  
 Per ulteriori esempi, vedere [iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7).  
  
## <a name="requirements"></a>Requisiti  
 [!INCLUDE[vs_dev11_long](../../../csharp/includes/vs_dev11_long_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Iteratori](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)   
 [Istruzioni](../../../visual-basic/language-reference/statements/index.md)
