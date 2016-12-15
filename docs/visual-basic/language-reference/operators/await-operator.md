---
title: "Await Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.Await"
helpviewer_keywords: 
  - "Await operator [Visual Basic]"
  - "Await [Visual Basic]"
ms.assetid: 6b1ce283-e92b-4ba7-b081-7be7b3d37af9
caps.latest.revision: 30
caps.handback.revision: 30
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Await Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Applicare l'operatore `Await` a un operando in un metodo o in un'espressione lambda asincroni per sospendere l'esecuzione del metodo finché l'attività di cui si è in attesa non viene completata.  L'attività rappresenta il lavoro in corso.  
  
 Il metodo in cui `Await` viene utilizzato deve avere un modificatore [Async](../../../visual-basic/language-reference/modifiers/async.md).  Un metodo di questo tipo, definito utilizzando il modificatore `Async` e contenente in genere una o più espressioni `Await`, viene definito *metodo asincrono*.  
  
> [!NOTE]
>  Le parole chiave `Await` e `Async` introdotte in Visual Studio 2012.  Per un'introduzione alla programmazione asincrona, vedere [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Solitamente l'attività a cui si applica l'operatore `Await` è il valore restituito da una chiamata a un metodo che implementa il [modello asincrono basato su attività](http://go.microsoft.com/fwlink/?LinkId=204847), ovvero un <xref:System.Threading.Tasks.Task> o un <xref:System.Threading.Tasks.Task%601>.  
  
 Nel codice seguente, tramite il metodo <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> di <xref:System.Net.Http.HttpClient> restituisce un oggetto `getContentsTask`, `Task(Of Byte())`.  L'attività è una promessa di produrre l'array di byte affettivo una volta completata l'operazione.  L'operatore `Await` viene applicato a `getContentsTask` per sospendere l'esecuzione in `SumPageSizesAsync` finché `getContentsTask` non sia completo.  Contemporaneamente, viene restituito il controllo al chiamante di `SumPageSizesAsync`.  Al termine di `getContentsTask`, l'espressione `Await` restituisce una matrice di byte.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
> [!IMPORTANT]
>  Per l'esempio completo, vedere [Procedura dettagliata: accesso al Web tramite Async e Await](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  È possibile scaricare l'esempio da [Esempi di codice dello sviluppatore](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409) sul sito Web Microsoft.  L'esempio è incluso nel progetto AsyncWalkthrough\_HttpClient.  
  
 Se `Await` viene applicata al risultato di una chiamata a un metodo che restituisce un `Task(Of TResult)`, il tipo dell'espressione `Await` è TResult.  Se `Await` viene applicata al risultato di una chiamata a un metodo che restituisce `Task`, l'espressione `Await` non restituisce un valore.  Nell'esempio riportato di seguito vengono illustrate le differenze.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 Un'espressione o un'istruzione `Await` non blocca il thread su cui è in esecuzione.  L'operazione comporta invece la registrazione, tramite il compilatore, della parte restante del metodo asincrono dopo l'espressione `Await`, come continuazione nell'attività attesa.  Il controllo viene restituito al chiamante del metodo asincrono.  Quando l'attività viene completata, richiama la relativa continuazione e l'esecuzione del metodo async viene ripresa nel punto dove era stata interrotta.  
  
 Un'espressione `Await` può verificarsi solo nel corpo di un metodo che la contiene o di un'espressione lambda contrassegnata da un modificatore `Async`.  Il termine *Await* funge da parola chiave solo in tale contesto.  In altre situazioni, viene interpretato come identificatore.  All'interno del metodo o dell'espressione lambda asincroni, un'espressione `Await` non può comparire in un'espressione di query, nei blocchi `catch` o `finally` di un'istruzione [Try... catch... finally](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md), nell'espressione di una variabile di controllo di un ciclo `For` o `For Each`, o nel corpo di un'istruzione [SyncLock](../../../visual-basic/language-reference/statements/synclock-statement.md).  
  
## Eccezioni  
 Tramite la maggior parte dei metodi asincroni viene restituito un oggetto <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>.  Le proprietà dell'attività restituita contengono informazioni sul relativo stato e cronologia, come se l'attività è stata completata, se il metodo async ha provocato un'eccezione o è stato annullato e qual è il risultato finale.  L'operatore `Await` accede a quelle proprietà.  
  
 Se si attende un metodo asincrono tramite cui viene restituita un'attività che comporta un'eccezione, tramite l'operatore  `Await` viene rigenerata l'eccezione.  
  
 Se si attende un metodo asincrono che restituisce un'attività che è stato annullato, tramite l'operatore `Await` viene rigenerata un'eccezione <xref:System.OperationCanceledException>.  
  
 Una singola attività in uno stato di errore può rispecchiare più eccezioni.  Ad esempio, l'attività potrebbe essere il risultato di una chiamata al metodo <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>.  Quando si attende tale attività, l'operazione di attesa esegue il rethrow di una sola delle eccezioni.  Tuttavia, non è possibile prevedere le eccezioni che vengono generate di nuovo.  
  
 Per esempi di gestione degli errori in metodi asincroni, vedere [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## Esempio  
 Nell'esempio seguente di Windows Form viene illustrato l'utilizzo di `Await` in un metodo async, `WaitAsynchronouslyAsync`.  Contrapporre il comportamento di tale metodo con il comportamento di `WaitSynchronously`.  Senza un operatore `Await`, `WaitSynchronously` viene eseguito in modo sincrono nonostante l'uso del modificatore `Async` nella definizione e in una chiamata a <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName> nel corpo.  
  
```vb  
Private Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
    ' Call the method that runs asynchronously.  
    Dim result As String = Await WaitAsynchronouslyAsync()  
  
    ' Call the method that runs synchronously.  
    'Dim result As String = Await WaitSynchronously()  
  
    ' Display the result.  
    TextBox1.Text &= result  
End Sub  
  
' The following method runs asynchronously. The UI thread is not  
' blocked during the delay. You can move or resize the Form1 window   
' while Task.Delay is running.  
Public Async Function WaitAsynchronouslyAsync() As Task(Of String)  
    Await Task.Delay(10000)  
    Return "Finished"  
End Function  
  
' The following method runs synchronously, despite the use of Async.  
' You cannot move or resize the Form1 window while Thread.Sleep  
' is running because the UI thread is blocked.  
Public Async Function WaitSynchronously() As Task(Of String)  
    ' Import System.Threading for the Sleep method.  
    Thread.Sleep(10000)  
    Return "Finished"  
End Function  
```  
  
## Vedere anche  
 [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura dettagliata: accesso al Web tramite Async e Await](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [Async](../../../visual-basic/language-reference/modifiers/async.md)