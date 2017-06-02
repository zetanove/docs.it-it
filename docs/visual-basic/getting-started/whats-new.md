---
title: "Novità in Visual Basic | Microsoft Docs"
ms.date: 2017-04-27
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- VB.StartPage.WhatsNew
dev_langs:
- VB
helpviewer_keywords:
- new features, Visual Basic
- what's new [Visual Basic]
- Visual Basic, what's new
ms.assetid: d7e97396-7f42-4873-a81c-4ebcc4b6ca02
caps.latest.revision: 145
author: rpetrusha
ms.author: ronpet
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
ms.translationtype: Human Translation
ms.sourcegitcommit: d3f21e32c162133e70a124da125c30afc7303738
ms.openlocfilehash: 18544a0311e24cf427111e364421db6e9fc27326
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="whats-new-for-visual-basic"></a>Novità in Visual Basic

Questo argomento elenca i nomi delle funzionalità principali per ogni versione di Visual Basic con le descrizioni dettagliate delle funzionalità nuove e migliorate nell'ultima versione del linguaggio.
  
## <a name="current-version"></a>Versione corrente

Visual Basic / Visual Studio .NET 2017   
Per le funzionalità nuove, vedere [Visual Basic 2017](#visual-basic-2017)

## <a name="previous-versions"></a>Versioni precedenti

Visual Basic/Visual Studio .NET 2015   
Per le funzionalità nuove, vedere [Visual Basic 14](#visual-basic-14)

Visual Basic/Visual Studio .NET 2013  
Technology Preview della piattaforma del compilatore .NET ("Roslyn")

Visual Basic/Visual Studio .NET 2012   
Parole chiave `Async` e `await`, iteratori, attributi relativi alle informazioni sul chiamante

Visual Basic, Visual Studio .NET 2010   
Proprietà implementate automaticamente, inizializzatori di insieme, continuazione di riga implicita, elementi dinamici, covarianza/controvarianza generica, accesso agli spazi dei nomi globali

Visual Basic/Visual Studio .NET 2008   
Language Integrated Query (LINQ), valori letterali XML, inferenza del tipo di variabile locale, inizializzatori di oggetto, tipi anonimi, metodi di estensione, inferenza del tipo `var` locale, espressioni lambda, operatore `if`, metodi parziali, tipi di valore nullable  

Visual Basic/Visual Studio .NET 2005   
Tipo `My` e tipi di helper (accesso all'app, al computer, al file system, alla rete)

Visual Basic/Visual Studio .NET 2003   
Operatori di scorrimento bit, dichiarazione di variabile del ciclo

Visual Basic/Visual Studio .NET 2002   
Prima versione di Visual Basic .NET

## <a name="visual-basic-2017"></a>Visual Basic 2017

[Tuple](../programming-guide/language-features/data-types/tuples.md)

Le tuple sono una semplice struttura dei dati che viene solitamente usata per restituire più valori da una singola chiamata al metodo. In genere, per restituire più valori da un metodo, è necessario eseguire una delle operazioni seguenti:

- Definire un tipo personalizzato (`Class` o `Structure`). Si tratta di una soluzione complicata.

- Definire uno o più parametri `ByRef` e restituire un valore dal metodo.
 
Grazie al supporto per tuple di Visual Basic è possibile definire rapidamente una tupla, assegnare facoltativamente nomi semantici ai rispettivi valori e recuperare rapidamente i relativi valori. L'esempio seguente esegue il wrapping di una chiamata al metodo <xref:System.Int32.TryParse%2A> e restituisce una tupla.

[!code-vb[Tuple](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

A questo punto è possibile chiamare il metodo e gestire la tupla restituita con codice simile al seguente.

[!code-vb[ReturnTuple](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)] 

**Valori letterali binari e separatori di cifre**

È possibile definire un valore letterale binario usando il prefisso `&B` o `&b`. È anche possibile usare il carattere di sottolineatura `_` come separatore di cifre per rendere il codice più leggibile. Nell'esempio seguente vengono usate entrambe le funzionalità per assegnare un valore `Byte` e visualizzarlo come un numero decimale, esadecimale e binario.

[!code-vb[Binary](../../../samples/snippets/visualbasic/getting-started/bin-example.vb#1)]

Per altre informazioni, vedere la sezione dedicata alle assegnazioni di valori letterali dei tipi di dati [Byte](../language-reference/data-types/byte-data-type.md#literal-assignments), [Integer](../language-reference/data-types/integer-data-type.md#literal-assignments), [Long](../language-reference/data-types/long-data-type.md#literal-assignments), [Short](../language-reference/data-types/short-data-type.md#literal-assignments), [SByte](../language-reference/data-types/sbyte-data-type.md#literal-assignments), [UInteger](../language-reference/data-types/uinteger-data-type.md#literal-assignments), [ULong](../language-reference/data-types/ulong-data-type.md#literal-assignments) e [UShort](../language-reference/data-types/ushort-data-type.md#literal-assignments).

**Supporto per valori di riferimento restituiti C#** 

A partire da C# 7, C# supporta i valori di riferimento restituiti. Pertanto, quando la chiamata al metodo riceve un valore di riferimento restituito, lo può modificare. Visual Basic non consente di creare metodi con valori di riferimento restituiti, ma consente di usare e modificare tali valori.

Ad esempio, la classe `Sentence` seguente scritta in C# include un metodo `FindNext` che rileva la parola successiva in una frase che inizia con una sottostringa specificata. La stringa viene restituita come valore di riferimento restituito. Una variabile `Boolean` passata dal riferimento al metodo indica se la ricerca ha avuto esito positivo. A questo punto il chiamante non solo può leggere il valore restituito, ma lo può anche modificare. Tale modifica si riflette sulla classe `Sentence`.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-returns.cs)]

In parole semplici, è possibile modificare la parola trovata nella frase usando un codice simile al seguente. Si noti che non si sta assegnando un valore al metodo, ma all'espressione che il metodo restituisce, ovvero il valore di riferimento restituito.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#1)]

Esiste tuttavia un problema con questo codice. Se non viene trovata una corrispondenza, il metodo restituisce la prima parola. L'esempio non esamina il valore dell'argomento `Boolean` per determinare se viene trovata una corrispondenza. Modifica quindi la prima parola se non esiste corrispondenza. Nell'esempio seguente questo problema viene risolto sostituendo la prima parola con la parola stessa se non esiste corrispondenza.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#2)]

Una soluzione migliore consiste nell'usare un metodo helper al quale il riferimento passa il valore di riferimento restituito. Il metodo helper può quindi modificare l'argomento passato dal riferimento. Nell'esempio seguente viene eseguita questa operazione.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return-helper.vb#1)]

Per altre informazioni, vedere [Reference Return Values](../programming-guide/language-features/procedures/ref-return-values.md) (Valori di riferimento restituiti).

## <a name="visual-basic-14"></a>Visual Basic 14

[Nameof](../../csharp/language-reference/keywords/nameof.md)  
 È possibile ottenere il nome di stringa non qualificato di un tipo o di un membro, da usare in un messaggio di errore senza definire una stringa a livello di codice.  In questo modo il codice sarà corretto anche durante il refactoring.  Questa funzionalità è utile anche per l'associazione di collegamenti MVC (Modello-Vista-Controller) e la generazione di eventi di modifica di proprietà.  
  
[Interpolazione di stringhe](../../csharp/language-reference/keywords/interpolated-strings.md)  
 È possibile usare espressioni di interpolazione di stringhe per costruire stringhe.  Un'espressione di stringa interpolata è simile a una stringa di modello che contiene espressioni.  In relazione agli argomenti, è più facile comprendere una stringa interpolata che la [formattazione composita](../../standard/base-types/composite-format.md).  
  
[Indicizzazione e accesso ai membri condizionali null](../../csharp/language-reference/operators/null-conditional-operators.md)  
È possibile verificare la presenza di valori null con una sintassi molto leggera prima di eseguire un'operazione di accesso ai membri (`?.`) o di indice (`?[]`).  Questi operatori consentono di scrivere meno codice per gestire i controlli null, soprattutto per l'ordinamento decrescente delle strutture di dati.  Se l'operando di sinistra o il riferimento a un oggetto è null, le operazioni restituiscono null.  
  
[Valori letterali stringa multilinea](../../visual-basic/programming-guide/language-features/strings/string-basics.md)  
 I valori letterali stringa possono contenere sequenze di nuove righe.  Non è più necessario usare `<xml><![CDATA[...text with newlines...]]></xml>.Value` come soluzione alternativa.  
  
Commenti  
È possibile inserire commenti dopo le continuazioni di riga implicita, all'interno delle espressioni dell'inizializzatore e tra i termini delle espressioni LINQ.  
  
 Risoluzione dei nomi completi più intelligente  
 In precedenza, con un codice come `Threading.Thread.Sleep(1000)`, Visual Basic cercava lo spazio dei nomi "Threading", individuava un'ambiguità tra System.Threading e System.Windows.Threading e quindi segnalava un errore.  Visual Basic ora prende in considerazione entrambi gli spazi dei nomi possibili.  Se si visualizza l'elenco di completamento, l'editor di Visual Studio elenca i membri di entrambi i tipi in questo elenco.  
  
 Valori letterali data con anno all'inizio  
 I valori letterali data possono avere il formato aaaa-mm-gg, `#2015-03-17 16:10 PM#`.  
  
 Proprietà dell'interfaccia readonly  
 È possibile implementare proprietà dell'interfaccia readonly usando una proprietà readonly.  L'interfaccia garantisce la funzionalità minima e le classi di implementazione non smettono di consentire l'impostazione della proprietà.  
  
 [TypeOf \<espressione> IsNot \<tipo>](../../visual-basic/language-reference/operators/typeof-operator.md)  
 Per una maggiore leggibilità del codice, ora è possibile usare `TypeOf` con `IsNot`.  
  
 [#Disable Warning \<ID> e #Enable Warning \<ID>](../../visual-basic/language-reference/directives/directives.md)  
 È possibile disabilitare e abilitare avvisi specifici per le aree all'interno di un file di origine.  
  
 Miglioramenti dei commenti ai documenti XML  
 Quando si scrivono commenti ai documenti, si accede a Smart Editor e al supporto per la compilazione per la convalida di nomi di parametro, la corretta gestione di `crefs` (generics, operatori e così via), la colorazione e il refactoring.  
  
 [Definizioni di interfacce e moduli parziali](../../visual-basic/language-reference/modifiers/partial.md)  
 Oltre a classi e struct, è possibile dichiarare interfacce e moduli parziali.  
  
 [Direttive #Region in corpi di metodo](../../visual-basic/language-reference/directives/region-directive.md)  
 È possibile inserire delimitatori #Region...#End Region in qualsiasi punto di un file, nelle funzioni o nei corpi delle funzioni.  
  
 [Le definizioni Overrides sono overload impliciti](../../visual-basic/language-reference/modifiers/overrides.md)  
 Se si aggiunge il modificatore `Overrides` a una definizione, il compilatore aggiunge in modo implicito `Overloads`. In questo modo è possibile digitare meno codice nella maggior parte dei casi.  
  
 CObj consentito negli argomenti degli attributi  
 Il compilatore generava un errore indicante che CObj(...), se usato nelle costruzioni degli attributi, non era una costante.  
  
 Dichiarazione e utilizzo di metodi ambigui da interfacce diverse  
 In precedenza il codice seguente restituiva errori che impedivano di dichiarare `IMock` o di chiamare `GetDetails` (se questi erano stati dichiarati in c#):  
  
```vb  
Interface ICustomer  
  Sub GetDetails(x As Integer)  
End Interface  
  
Interface ITime  
  Sub GetDetails(x As String)  
End Interface  
  
Interface IMock : Inherits ICustomer, ITime  
  Overloads Sub GetDetails(x As Char)  
End Interface  
  
Interface IMock2 : Inherits ICustomer, ITime  
End Interface  
```  
  
 Ora il compilatore userà le normali regole di risoluzione dell'overload per scegliere l'oggetto `GetDetails` più appropriato da chiamare ed è possibile dichiarare le relazioni tre le interfacce in Visual Basic, come quelle mostrate nell'esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Novità di Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/ide/whats-new-in-visual-studio)

