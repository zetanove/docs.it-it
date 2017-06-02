---
title: try-catch (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- try
- try_CSharpKeyword
- catch
- catch_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- catch keyword [C#]
- try-catch statement [C#]
ms.assetid: cb5503c7-bfa1-4610-8fc2-ddcd2e84c438
caps.latest.revision: 45
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 13684c7e32c52765f4d45d6a5bd2c6f8194efefe
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="try-catch-c-reference"></a>try-catch (Riferimenti per C#)
L'istruzione try-catch è costituita da un blocco `try` seguito da una o più clausole `catch`, che specificano i gestori per eccezioni diverse.  
  
## <a name="remarks"></a>Note  
 Quando viene generata un'eccezione, Common Language Runtime(CLR) cerca l'istruzione `catch` che gestisce questa eccezione. Se il metodo attualmente in esecuzione non contiene tale blocco `catch`, CLR analizza il metodo che ha chiamato il metodo corrente e così via fino allo stack di chiamate. Se non viene trovato alcun blocco `catch`, CLR visualizza un messaggio di eccezione non gestita per l'utente e interrompe l'esecuzione del programma.  
  
 Il blocco `try` contiene il codice protetto che potrebbe generare l'eccezione. Il blocco viene eseguito fino a quando non viene generata un'eccezione o viene completato correttamente. Ad esempio, il seguente tentativo di eseguire il cast di un oggetto `null` genera l'eccezione <xref:System.NullReferenceException>:  
  
```csharp  
object o2 = null;  
try  
{  
    int i2 = (int)o2;   // Error  
}  
```  
  
 Anche se la clausola `catch` può essere usata senza argomenti per intercettare qualsiasi tipo di eccezione, questo utilizzo non è consigliato. In generale, è consigliabile intercettare solo le eccezioni di cui si sa come eseguire il ripristino. Pertanto, è necessario specificare sempre un argomento di oggetto derivato da <xref:System.Exception?displayProperty=fullName>. Ad esempio:  
  
```csharp  
catch (InvalidCastException e)   
{  
}  
```  
  
 È possibile usare più clausole `catch` specifiche nella stessa istruzione try-catch. In questo caso, l'ordine delle clausole `catch` è importante perché le clausole `catch` vengono esaminate nell'ordine specificato. Intercettare le eccezioni più specifiche prima di quelle meno specifiche. Il compilatore provoca un errore se si ordinano i blocchi catch in modo che un blocco successivo non possa mai essere raggiunto.  
  
 Usando gli argomenti `catch`, è possibile filtrare le eccezioni che si desidera gestire.  È inoltre possibile usare un'espressione del predicato che esamini ulteriormente l'eccezione per decidere se gestirla.  Se l'espressione del predicato restituisce false, la ricerca di un gestore prosegue.  
  
```csharp  
catch (ArgumentException e) when (e.ParamName == "…")  
{  
}  
```  
  
 I filtri eccezioni sono preferibili per l'intercettazione e la rigenerazione (come illustrato di seguito) perché lasciano intatto lo stack.  Se un gestore successivo esegue il dump dello stack, è possibile visualizzare l'origine dell'eccezione, anziché solo l'ultima posizione in cui è stata rigenerata.  Un uso comune delle espressioni di filtro eccezioni è la registrazione.  È possibile creare una funzione predicato che restituisca sempre false da visualizzare anche in un log. È possibile registrare le eccezioni mentre si verificano senza doverle gestire e rigenerare.  
  
 Un'istruzione [throw](../../../csharp/language-reference/keywords/throw.md) può essere usata in un blocco `catch` per rigenerare l'eccezione intercettata dall'istruzione `catch`. Il seguente esempio estrae le informazioni di origine da un'eccezione <xref:System.IO.IOException> e quindi genera l'eccezione per il metodo padre.  
  
```csharp  
catch (FileNotFoundException e)  
{  
    // FileNotFoundExceptions are handled here.  
}  
catch (IOException e)  
{  
    // Extract some information from this exception, and then   
    // throw it to the parent method.  
    if (e.Source != null)  
        Console.WriteLine("IOException source: {0}", e.Source);  
    throw;  
}  
```  
  
 È possibile intercettare un'eccezione e generarne un'altra. In questo caso, specificare l'eccezione intercettata come eccezione interna, come mostrato nell'esempio seguente.  
  
```csharp  
catch (InvalidCastException e)   
{  
    // Perform some action here, and then throw a new exception.  
    throw new YourCustomException("Put your error message here.", e);  
}  
```  
  
 È anche possibile generare nuovamente un'eccezione quando una determinata condizione è true, come mostrato nell'esempio seguente.  
  
```csharp  
catch (InvalidCastException e)  
{  
    if (e.Data == null)  
    {  
        throw;  
    }  
    else  
    {  
        // Take some action.  
    }  
 }  
```  
  
 Da un blocco `try` inizializzare solo le variabili dichiarate al suo interno. In caso contrario, è possibile che si verifichi un'eccezione prima del completamento dell'esecuzione del blocco. Nel seguente esempio di codice, la variabile `n` viene inizializzata nel blocco `try`. Un tentativo di usare questa variabile al di fuori del blocco `try` nell'istruzione `Write(n)` genererà un errore del compilatore.  
  
```csharp  
static void Main()   
{  
    int n;  
    try   
    {  
        // Do not initialize this variable here.  
        n = 123;  
    }  
    catch  
    {  
    }  
    // Error: Use of unassigned local variable 'n'.  
    Console.Write(n);  
}  
```  
  
 Per altre informazioni su catch, vedere [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md).  
  
## <a name="exceptions-in-async-methods"></a>Eccezioni nei metodi asincroni  
 Un metodo asincrono viene contrassegnato da un modificatore [async](../../../csharp/language-reference/keywords/async.md) e in genere contiene una o più espressioni o istruzioni await. Un'espressione await applica l'operatore [await](../../../csharp/language-reference/keywords/await.md) a un metodo <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.  
  
 Quando il controllo raggiunge un oggetto `await` nel metodo asincrono, l'avanzamento nel metodo viene sospeso fino al completamento dell'attività attesa. Una volta completata l'attività, l'esecuzione del metodo può riprendere. Per altre informazioni, vedere [Programmazione asincrona con Async e Await](../../../csharp/programming-guide/concepts/async/index.md) e [Flusso di controllo in programmi asincroni](../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md).  
  
 L'attività completata a cui viene applicato `await` può essere in uno stato di errore a causa di un'eccezione non gestita nel metodo che restituisce l'attività. L'attesa dell'attività genera un'eccezione. Un'attività può inoltre terminare con uno stato di annullamento se viene annullato il processo asincrono che la restituisce. L'attesa di un'attività annullata genera un'eccezione `OperationCanceledException`. Per altre informazioni su come annullare un processo asincrono, vedere [Ottimizzazione dell'applicazione Async](http://msdn.microsoft.com/library/daaa32ea-c84c-4761-8230-c8292ffebd74).  
  
 Per intercettare l'eccezione, attendere l'attività in un blocco `try` e intercettare l'eccezione nel blocco `catch` associato. Per un esempio, vedere la sezione "Esempio".  
  
 Un'attività può essere in uno stato di errore perché si sono verificate più eccezioni nel metodo asincrono atteso. Ad esempio, l'attività potrebbe essere il risultato di una chiamata a <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>. Quando si attende tale attività, solo una delle eccezioni viene intercettata, ma non è possibile prevedere quale. Per un esempio, vedere la sezione "Esempio".  
  
## <a name="example"></a>Esempio  
 Nel seguente esempio, il blocco `try` contiene una chiamata al metodo `ProcessString` che potrebbe causare un'eccezione. La clausola `catch` contiene il gestore di eccezioni che visualizza solo un messaggio sullo schermo. Quando l'istruzione `throw` viene chiamata da `MyMethod`, il sistema cerca l'istruzione `catch` e visualizza il messaggio `Exception caught`.  
  
 [!code-cs[csrefKeywordsExceptions#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_1.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, vengono usati due blocchi catch e viene intercettata l'eccezione più specifica, che è la prima.  
  
 Per intercettare l'eccezione meno specifica, è possibile sostituire l'istruzione throw in `ProcessString` con l'istruzione seguente: `throw new Exception()`.  
  
 Se nell'esempio si inserisce per primo il blocco catch meno specifico, viene visualizzato il messaggio di errore seguente: `A previous catch clause already catches all exceptions of this or a super type ('System.Exception')`.  
  
 [!code-cs[csrefKeywordsExceptions#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_2.cs)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra la gestione delle eccezioni per i metodi asincroni. Per intercettare un'eccezione generata da un'attività asincrona, inserire l'espressione `await` in un blocco `try` e intercettare l'eccezione in un blocco `catch`.  
  
 Rimuovere il commento dalla riga `throw new Exception` nell'esempio per illustrare la gestione delle eccezioni. La proprietà `IsFaulted` dell'attività viene impostata su `True`, la proprietà `Exception.InnerException` dell'attività viene impostata sull'eccezione e l'eccezione viene intercettata nel blocco `catch`.  
  
 Rimuovere il commento dalla riga `throw new OperationCancelledException` per illustrare cosa accade quando si annulla un processo asincrono. La proprietà `IsCanceled` dell'attività viene impostata su `true` e l'eccezione viene intercettata nel blocco `catch`. In alcune condizioni che non si applicano a questo esempio, la proprietà `IsFaulted` dell'attività viene impostata su `true` e `IsCanceled` viene impostata su `false`.  
  
 [!code-cs[csAsyncExceptions#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_3.cs)]  
  
## <a name="example"></a>Esempio  
 Il seguente esempio illustra la gestione delle eccezioni dove più attività possono restituire più eccezioni. Il blocco `try` attende l'attività restituita da una chiamata a <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>. L'attività viene completata quando vengono completate le tre attività a cui si applica WhenAll.  
  
 Ognuna delle tre attività genera un'eccezione. Il blocco `catch` scorre le eccezioni presenti nella proprietà `Exception.InnerExceptions` dell'attività restituita da <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>.  
  
 [!code-cs[csAsyncExceptions#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-catch_4.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzioni try, throw e catch (C++)](https://docs.microsoft.com/cpp/cpp/try-throw-and-catch-statements-cpp)   
 [Istruzioni di gestione delle eccezioni](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [Procedura: Come generare in modo esplicito le eccezioni](https://msdn.microsoft.com/library/xhcbs8fz)

