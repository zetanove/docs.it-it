---
title: "TPL and Traditional .NET Framework Asynchronous Programming | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tasks, with other asynchronous models"
ms.assetid: e7b31170-a156-433f-9f26-b1fc7cd1776f
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# TPL and Traditional .NET Framework Asynchronous Programming
.NET Framework offre i due modelli standard seguenti per eseguire operazioni asincrone di solo I\/O e di solo calcolo:  
  
-   Modello di programmazione asincrono \(APM, Asynchronous Programming Model\), in cui le operazioni asincrone sono rappresentate da una coppia di metodi Begin\/End come <xref:System.IO.FileStream.BeginRead%2A?displayProperty=fullName> e <xref:System.IO.Stream.EndRead%2A?displayProperty=fullName>.  
  
-   Modello asincrono basato su eventi \(EAP, Event\-based Asynchronous Pattern\), in cui le operazioni asincrone sono rappresentate da una coppia metodo\/evento denominati *OperationName*Async e *OperationName*Completed, ad esempio <xref:System.Net.WebClient.DownloadStringAsync%2A?displayProperty=fullName> e <xref:System.Net.WebClient.DownloadStringCompleted?displayProperty=fullName>.  Il modello EAP è stato introdotto in .NET Framework versione 2.0.  
  
 È possibile usare Task Parallel Library \(TPL\) in diversi modi insieme a uno dei due modelli asincroni.  È possibile esporre operazioni APM ed EAP come attività nei consumer della libreria oppure esporre i modelli APM ma usare oggetti Task per implementarli internamente.  In entrambi gli scenari, usando oggetti Task è possibile semplificare il codice e trarre vantaggio dalle utili funzionalità seguenti:  
  
-   Registrare callback, sotto forma di continuazioni di attività, in qualsiasi momento dopo l'avvio dell'attività.  
  
-   Coordinare più operazioni eseguite in risposta a un metodo `Begin_`, usando i metodi <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> e <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> il metodo <xref:System.Threading.Tasks.Task.WaitAll%2A> oppure il metodo <xref:System.Threading.Tasks.Task.WaitAny%2A>.  
  
-   Incapsulare operazioni asincrone di solo I\/O e di solo calcolo nello stesso oggetto Task.  
  
-   Monitorare lo stato dell'oggetto Task.  
  
-   Eseguire il marshalling dello stato di un'operazione a un oggetto Task usando <xref:System.Threading.Tasks.TaskCompletionSource%601>.  
  
## Wrapping di operazioni APM in un'attività  
 Le classi <xref:System.Threading.Tasks.TaskFactory?displayProperty=fullName> e <xref:System.Threading.Tasks.TaskFactory%601?displayProperty=fullName> forniscono entrambe diversi overload dei metodi <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A?displayProperty=fullName> e <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=fullName>, che permettono di incapsulare una coppia di metodi Begin\/End APM in un'unica istanza di <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>.  I diversi overload si adattano a qualsiasi coppia di metodi Begin\/End che include da zero a tre parametri di input.  
  
 Per le coppie con metodi `End` che restituiscono un valore \(`Function` in Visual Basic\), usare i metodi in <xref:System.Threading.Tasks.TaskFactory%601>, che creano un oggetto <xref:System.Threading.Tasks.Task%601>.  Per i metodi `End` che restituiscono void \(`Sub` in Visual Basic\), usare i metodi in <xref:System.Threading.Tasks.TaskFactory>, che creano un oggetto <xref:System.Threading.Tasks.Task>.  
  
 Per i pochi casi in cui il metodo `Begin` include più di tre parametri o contiene parametri `ref` o `out`, sono disponibili overload `FromAsync` aggiuntivi che incapsulano solo il metodo `End`.  
  
 L'esempio seguente mostra la firma per l'overload `FromAsync` che corrisponde ai metodi <xref:System.IO.FileStream.BeginRead%2A?displayProperty=fullName> e <xref:System.IO.FileStream.EndRead%2A?displayProperty=fullName>.  Questo overload accetta i tre parametri di input seguenti.  
  
 [!code-csharp[FromAsync#01](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#01)]
 [!code-vb[FromAsync#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#01)]  
  
 Il primo parametro è un delegato <xref:System.Func%606> che corrisponde alla firma del metodo <xref:System.IO.FileStream.BeginRead%2A?displayProperty=fullName>.  Il secondo parametro è un delegato <xref:System.Func%602> che accetta un oggetto <xref:System.IAsyncResult> e restituisce un valore `TResult`.  Poiché <xref:System.IO.FileStream.EndRead%2A> restituisce un numero intero, il compilatore deduce il tipo di `TResult` come <xref:System.Int32> e il tipo dell'attività come <xref:System.Threading.Tasks.Task>.  Gli ultimi quattro parametri sono identici a quelli nel metodo <xref:System.IO.FileStream.BeginRead%2A?displayProperty=fullName>:  
  
-   Buffer in cui archiviare i dati del file.  
  
-   Offset nel buffer in corrispondenza del quale iniziare a scrivere dati.  
  
-   Quantità massima di dati da leggere dal file.  
  
-   Oggetto facoltativo che archivia dati di stato definiti dall'utente da passare al callback.  
  
### Uso di ContinueWith per la funzionalità di callback  
 Se è necessario accedere ai dati nel file e non soltanto al numero di byte, il metodo <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> non è sufficiente.  Usare invece <xref:System.Threading.Tasks.Task>, la cui proprietà `Result` contiene i dati del file.  A questo scopo, è possibile aggiungere una continuazione all'attività originale.  La continuazione esegue le operazioni svolte in genere dal delegato <xref:System.AsyncCallback>.  La continuazione viene richiamata al termine dell'attività precedente e dopo che il buffer di dati è stato completato.  L'oggetto <xref:System.IO.FileStream> deve essere chiuso prima della restituzione.  
  
 L'esempio seguente mostra come restituire un oggetto <xref:System.Threading.Tasks.Task> che incapsula la coppia BeginRead\/EndRead della classe <xref:System.IO.FileStream>.  
  
 [!code-csharp[FromAsync#03](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#03)]
 [!code-vb[FromAsync#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#03)]  
  
 Il metodo può quindi essere chiamato nel modo seguente.  
  
 [!code-csharp[FromAsync#04](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#04)]
 [!code-vb[FromAsync#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#04)]  
  
### Fornire dati di stato personalizzati  
 Nelle tipiche operazioni <xref:System.IAsyncResult> se il delegato <xref:System.AsyncCallback> richiede dati di stato, è necessario passarli attraverso l'ultimo parametro nel metodo `Begin`, in modo che sia possibile creare un pacchetto dei dati nell'oggetto <xref:System.IAsyncResult>, che viene infine passato al metodo di callback.  Questo approccio non è in genere necessario quando si usano i metodi `FromAsync`.  Se i dati personalizzati sono noti alla continuazione, possono essere acquisiti direttamente nel delegato della continuazione.  L'esempio seguente assomiglia a quello precedente, ma invece di esaminare la proprietà `Result` dell'attività precedente, la continuazione esamina i dati di stato personalizzati, cui il delegato dell'utente della continuazione può accedere direttamente.  
  
 [!code-csharp[FromAsync#05](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#05)]
 [!code-vb[FromAsync#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#05)]  
  
### Sincronizzazione di più attività FromAsync  
 I metodi statici <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> e <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> offrono flessibilità aggiunta se vengono usati insieme ai metodi `FromAsync`.  L'esempio seguente mostra come avviare più operazioni di I\/O asincrone e quindi attenderne il completamento prima di eseguire la continuazione.  
  
 [!code-csharp[FromAsync#06](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#06)]
 [!code-vb[FromAsync#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#06)]  
  
### Attività FromAsync solo per il metodo End  
 Per i pochi casi in cui il metodo `Begin` richiede più di tre parametri di input o include parametri `ref` o `out`, è possibile usare gli overload `FromAsync`, ad esempio <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%600%7D%29?displayProperty=fullName>, che rappresentano solo il metodo `End`.  Questi metodi possono essere usati anche in qualsiasi scenario in cui viene passato un oggetto <xref:System.IAsyncResult> e si vuole incapsularlo in un'attività.  
  
 [!code-csharp[FromAsync#07](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#07)]
 [!code-vb[FromAsync#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#07)]  
  
### Avvio e annullamento di attività FromAsync  
 L'attività restituita da un metodo `FromAsync` ha lo stato WaitingForActivation e verrà avviata dal sistema in un determinato momento al termine della sua creazione.  Se si tenta di chiamare Start su questa attività, viene generata un'eccezione.  
  
 Non è possibile annullare un'attività `FromAsync`, perché le API di .NET Framework sottostanti non supportano l'annullamento in corso di operazioni di I\/O su file o di rete.  È possibile aggiungere la funzionalità di annullamento a un metodo che incapsula una chiamata di `FromAsync`, ma è possibile rispondere all'annullamento prima che `FromAsync` venga chiamato o dopo il suo completamento, ad esempio in un'attività di continuazione.  
  
 Alcune classi che supportano il modello EAP, ad esempio <xref:System.Net.WebClient>, supportano l'annullamento ed è possibile integrare questa funzionalità di annullamento nativa usando token di annullamento.  
  
## Esposizione di operazioni EAP complesse come attività  
 TPL non fornisce alcun metodo progettato in modo specifico per incapsulare un'operazione asincrona basata su eventi allo stesso modo in cui la famiglia di metodi `FromAsync` esegue il wrapping del modello <xref:System.IAsyncResult>.  Tuttavia, TPL fornisce la classe <xref:System.Threading.Tasks.TaskCompletionSource%601?displayProperty=fullName>, che può essere usata per rappresentare qualsiasi set arbitrario di operazioni come <xref:System.Threading.Tasks.Task%601>.  Le operazioni possono essere sincrone o asincrone di solo I\/O o di solo calcolo, o di entrambi i tipi.  
  
 L'esempio seguente mostra come usare un oggetto <xref:System.Threading.Tasks.TaskCompletionSource%601> per esporre un set di operazioni <xref:System.Net.WebClient> asincrone al codice client come <xref:System.Threading.Tasks.Task%601> di base.  Il metodo permette di immettere una matrice di URL Web e un termine o un nome da cercare e quindi restituisce il numero di volte in cui il termine di ricerca è presente in ogni sito.  
  
 [!code-csharp[FromAsync#10](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/snippet10.cs#10)]
 [!code-vb[FromAsync#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/snippet10.vb#10)]  
  
 Per un esempio più completo, che include gestione aggiuntiva delle eccezioni e mostra come chiamare il metodo dal codice client, vedere [How to: Wrap EAP Patterns in a Task](../../../docs/standard/parallel-programming/how-to-wrap-eap-patterns-in-a-task.md).  
  
 Tenere presente che qualsiasi attività creata da <xref:System.Threading.Tasks.TaskCompletionSource%601> verrà avviata da TaskCompletionSource e, di conseguenza, il codice utente non deve chiamare il metodo Start sull'attività.  
  
## Implementazione del modello APM usando attività  
 In alcuni scenari può essere opportuno esporre direttamente il modello <xref:System.IAsyncResult> usando coppie di metodi Begin\/End in un'API.  Ad esempio, si potrebbe voler mantenere la coerenza con le API esistenti o disporre di strumenti automatici che richiedono questo modello.  In questi casi, è possibile usare attività per semplificare l'implementazione interna del modello APM.  
  
 L'esempio seguente mostra come usare attività per implementare una coppia di metodi Begin\/End APM per un metodo di solo calcolo a esecuzione prolungata.  
  
 [!code-csharp[FromAsync#09](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#09)]
 [!code-vb[FromAsync#09](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#09)]  
  
## Uso del codice di esempio StreamExtensions  
 Il file Streamextensions.cs, incluso nella pagina relativa agli [esempi per la programmazione parallela con .NET Framework 4](http://go.microsoft.com/fwlink/?LinkID=165717) del sito Web MSDN, contiene diverse implementazioni di riferimento che usano oggetti Task per operazioni di I\/O su file e di rete asincrone.  
  
## Vedere anche  
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)