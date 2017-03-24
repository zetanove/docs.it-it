---
title: "await (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "await_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "await [C#]"
  - "await (parola chiave) [C#]"
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
caps.latest.revision: 36
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 36
---
# await (Riferimenti per C#)
L'operatore `await` viene applicato a un'attività in un metodo asincrono per sospendere l'esecuzione del metodo finché l'attività di cui si è in attesa non viene completata.  L'attività rappresenta il lavoro attualmente in fase di esecuzione.  
  
 Il metodo asincrono in cui `await` viene usato deve essere modificato dalla parola chiave [async](../../../csharp/language-reference/keywords/async.md).  Tale metodo, definito usando il modificatore `async` e contenente di solito una o più espressioni `await`, viene denominato *metodo asincrono*.  
  
> [!NOTE]
>  Le parole chiave `async` e `await` sono state introdotte in Visual Studio 2012.  Per un'introduzione alla programmazione asincrona, vedere [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  
  
 L'attività a cui si applica l'operatore `await` è solitamente il valore restituito da una chiamata a un metodo che implementa il [modello asincrono basato su attività](http://go.microsoft.com/fwlink/?LinkId=204847).  Gli esempi includono i valori di tipo <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>.  
  
 Nel seguente codice, l'elemento <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> del metodo <xref:System.Net.Http.HttpClient> restituisce un elemento `Task\<byte[]>`, ovvero `getContentsTask`.  L'attività è una promessa di produrre la matrice di byte effettiva una volta completata l'attività.  L'operatore `await` viene applicato a `getContentsTask` per sospendere l'esecuzione in `SumPageSizesAsync` fino al completamento di `getContentsTask`.  Nel frattempo, il controllo viene restituito al chiamante di `SumPageSizesAsync`.  Quando `getContentsTask` termina, l'espressione `await` restituisce una matrice di byte.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
> [!IMPORTANT]
>  Per l'esempio completo, vedere [Procedura dettagliata: accesso al Web tramite Async e Await](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  È possibile scaricare l'esempio da [Esempi di codice per gli sviluppatori](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409) nel sito Web Microsoft.  L'esempio è nel progetto AsyncWalkthrough\_HttpClient.  
  
 Come mostrato nell'esempio precedente, se `await` viene applicato al risultato di una chiamata a un metodo che restituisce un elemento `Task<TResult>`, il tipo dell'espressione `await` è TResult.  Se `await` viene applicato al risultato di una chiamata a un metodo che restituisce un elemento `Task`, il tipo dell'espressione `await` è void.  Nell'esempio che segue viene illustrata la differenza.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 Un'espressione `await` non blocca il thread su cui è in esecuzione.  Comporta invece la registrazione, tramite il compilatore, della parte restante del metodo asincrono come continuazione dell'attività di cui si è in attesa.  Il controllo quindi viene restituito al chiamante del metodo asincrono.  Al termine dell'attività, ne richiama la continuazione e l'esecuzione del metodo asincrono riprende da dove era stata interrotta.  
  
 Un'espressione `await` può trovarsi solo nel corpo di un metodo che la contiene, di un'espressione lambda o di un metodo anonimo contrassegnato da un modificatore `async`.  Il termine *await* funge da parola chiave solo in tale contesto.  Altrove, viene interpretata come identificatore.  All'interno del metodo, dell'espressione lambda o del metodo anonimo, un'espressione `await` non può verificarsi nel corpo di una funzione sincrona, in un'espressione di query, nel blocco di un'[istruzione lock](../../../csharp/language-reference/keywords/lock-statement.md) o in un contesto [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
## Eccezioni  
 La maggior parte dei metodi asincroni restituisce <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>.  Le proprietà dell'attività restituita contengono informazioni sullo stato e sulla cronologia, ad esempio se l'attività è stata completata, se il metodo asincrono ha generato un'eccezione o è stato annullato e il risultato finale.  L'operatore `await` accede a tali proprietà.  
  
 Se si è in attesa di un metodo asincrono che restituisce un'attività che genera un'eccezione, tramite l'operatore `await` viene rigenerata l'eccezione.  
  
 Se si è in attesa di un metodo asincrono che restituisce un'attività che è stato annullato, tramite l'operatore `await` viene rigenerata un'eccezione <xref:System.OperationCanceledException>.  
  
 Una singola attività in uno stato di errore può rispecchiare più eccezioni.  Ad esempio, l'attività può essere il risultato di una chiamata a <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>.  Quando si attende tale attività, l'operazione await rigenera solo una delle eccezioni.  Tuttavia, non è possibile prevedere quale delle eccezioni verrà rigenerata.  
  
 Per esempi di gestione degli errori nei metodi asincroni, vedere [try\-catch](../../../csharp/language-reference/keywords/try-catch.md).  
  
## Esempio  
 Il seguente esempio di Windows Form illustra l'uso di `await` in un metodo asincrono, `WaitAsynchronouslyAsync`.  Contrastare il comportamento di tale metodo con il comportamento di `WaitSynchronously`.  Senza un operatore `await` applicato a un'attività, `WaitSynchronously` viene eseguito in modo sincrono nonostante l'uso del modificatore `async` nella definizione e di una chiamata a <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> nel corpo.  
  
```c#  
  
private async void button1_Click(object sender, EventArgs e)  
{  
    // Call the method that runs asynchronously.  
    string result = await WaitAsynchronouslyAsync();  
  
    // Call the method that runs synchronously.  
    //string result = await WaitSynchronously ();  
  
    // Display the result.  
    textBox1.Text += result;  
}  
  
// The following method runs asynchronously. The UI thread is not  
// blocked during the delay. You can move or resize the Form1 window   
// while Task.Delay is running.  
public async Task<string> WaitAsynchronouslyAsync()  
{  
    await Task.Delay(10000);  
    return "Finished";  
}  
  
// The following method runs synchronously, despite the use of async.  
// You cannot move or resize the Form1 window while Thread.Sleep  
// is running because the UI thread is blocked.  
public async Task<string> WaitSynchronously()  
{  
    // Add a using directive for System.Threading.  
    Thread.Sleep(10000);  
    return "Finished";  
}  
```  
  
## Vedere anche  
 [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura dettagliata: accesso al Web tramite Async e Await](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [async](../../../csharp/language-reference/keywords/async.md)