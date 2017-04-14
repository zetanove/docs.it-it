---
title: "Attached and Detached Child Tasks | Microsoft Docs"
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
  - "tasks, child tasks"
ms.assetid: c95788bf-90a6-4e96-b7bc-58e36a228cc5
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Attached and Detached Child Tasks
Un'*attività figlio* \(o *attività annidata*\) è un'istanza <xref:System.Threading.Tasks.Task?displayProperty=fullName> creata nel delegato dell'utente di un'altra attività, noto come *attività padre*.  Un'attività figlio può essere scollegata o collegata.  Un'*attività figlio scollegata* è un'attività eseguita indipendentemente dall'attività padre.  Un'*attività figlio collegata* è un'attività annidata creata con l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> alla quale l'attività padre non impedisce il collegamento in modo esplicito o per impostazione predefinita.  Un'attività può creare un numero qualsiasi di attività figlio collegate e scollegate, limitato solo dalle risorse di sistema.  
  
 La tabella seguente elenca le differenze di base tra i due tipi di attività figlio.  
  
|Categoria|Attività figlio scollegate|Attività figlio collegate|  
|---------------|--------------------------------|-------------------------------|  
|L'attività padre attende il completamento delle attività figlio.|No|Sì|  
|L'attività padre propaga le eccezioni generate dalle attività figlio.|No|Sì|  
|Lo stato dell'attività padre dipende dallo stato dell'attività figlio.|No|Sì|  
  
 Nella maggior parte degli scenari, è consigliabile usare l'attività figlio scollegata perché le relazioni con altre attività risultano meno complesse.  Per questo motivo le attività create all'interno delle attività padre sono di tipo scollegato per impostazione predefinita ed è necessario specificare esplicitamente l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> per creare un'attività figlio collegata.  
  
## Attività figlio scollegate  
 Anche se un'attività figlio viene creata da un'attività padre, per impostazione predefinita è indipendente dell'attività padre.  Nell'esempio seguente, un'attività padre crea un'attività figlio semplice.  Se si esegue più volte il codice di esempio, è possibile notare che l'output dell'esempio è diverso da quello indicato e potrebbe cambiare ogni volta che si esegue il codice.  Il motivo è che l'attività padre e le attività figlio sono eseguite in modo indipendente; l'attività figlio è di tipo scollegato.  Nell'esempio si attende solo il completamento dell'attività padre, mentre l'attività figlio potrebbe non essere eseguita o completata prima del termine dell'applicazione console.  
  
 [!code-csharp[TPL_ChildTasks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/nested1.cs#1)]
 [!code-vb[TPL_ChildTasks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/nested1.vb#1)]  
  
 Se l'attività figlio è rappresentata da un oggetto <xref:System.Threading.Tasks.Task%601> anziché da un oggetto <xref:System.Threading.Tasks.Task>, è possibile assicurarsi che l'attività padre attenda il completamento dell'attività figlio accedendo alla proprietà <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=fullName> dell'attività figlio anche è di tipo scollegato.  La proprietà <xref:System.Threading.Tasks.Task%601.Result%2A> viene bloccata fino al completamento dell'attività, come mostrato nell'esempio seguente.  
  
 [!code-csharp[TPL_ChildTasks#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/childtasks.cs#4)]
 [!code-vb[TPL_ChildTasks#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/tpl_childtasks.vb#4)]  
  
## Attività figlio collegate  
 A differenza delle attività figlio scollegate, le attività figlio collegate sono strettamente sincronizzate con l'attività padre.  È possibile modificare il tipo dell'attività figlio da scollegato a collegato usando l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> nell'istruzione di creazione dell'attività, come mostrato nell'esempio seguente.  In questo codice, l'attività figlio collegata viene completata prima dell'attività padre.  Di conseguenza, l'output dell'esempio è lo stesso per ogni esecuzione del codice.  
  
 [!code-csharp[TPL_ChildTasks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1.cs#2)]
 [!code-vb[TPL_ChildTasks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1.vb#2)]  
  
 Per creare grafici strettamente sincronizzati di operazioni asincrone, è possibile usare le attività figlio collegate.  
  
 Tuttavia, un'attività figlio può collegarsi all'attività padre solo se quest'ultimo consente le attività figlio collegate.  Le attività padre possono impedire in modo esplicito il collegamento di attività figlio specificando l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> nel costruttore della classe dell'attività padre o il metodo <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=fullName>.  Le attività padre possono impedire in modo implicito il collegamento di attività figlio se sono state create chiamando il metodo <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName>.  Questa condizione è illustrata nell'esempio seguente.  L'esempio è uguale a quello precedente, ma in questo caso l'attività padre viene creata chiamando il metodo <xref:System.Threading.Tasks.Task.Run%28System.Action%29?displayProperty=fullName> anziché il metodo <xref:System.Threading.Tasks.TaskFactory.StartNew%28System.Action%29?displayProperty=fullName>.  Poiché l'attività figlio non è in grado di collegarsi all'attività padre, l'output dell'esempio è imprevedibile.  Poiché le opzioni di creazione dell'attività predefinite per gli overload <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=fullName> includono <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName>, questo esempio è funzionalmente equivalente al primo esempio nella sezione "Attività figlio scollegate".  
  
 [!code-csharp[TPL_ChildTasks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_childtasks/cs/child1a.cs#3)]
 [!code-vb[TPL_ChildTasks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_childtasks/vb/child1a.vb#3)]  
  
## Eccezioni nelle attività figlio  
 Se un'attività figlio scollegata genera un'eccezione, l'eccezione deve essere osservata o gestita direttamente nell'attività padre come accade nel caso di qualsiasi attività non annidata.  Se un'attività figlio collegata genera un'eccezione, l'eccezione viene propagata automaticamente all'attività padre e al thread che rimane in attesa o tenta di accedere alla proprietà <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=fullName> dell'attività.  Quindi, usando le attività figlio collegate è possibile gestire tutte le eccezioni in un solo punto della chiamata a <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName> nel thread chiamante.  Per altre informazioni, vedere [Gestione delle eccezioni](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md).  
  
## Annullamento e attività figlio  
 L'annullamento delle attività è cooperativo,  ossia, per essere annullabile, ogni attività figlio collegata o scollegata deve monitorare lo stato del token di annullamento.  Per annullare un'attività padre e le relative attività figlio usando un'unica richiesta, è necessario passare lo stesso token come argomento a tutte le attività e fornire la logica di risposta alla richiesta in ogni attività.  Per altre informazioni, vedere [Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md) e [How to: Cancel a Task and Its Children](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md).  
  
### Annullamento dell'attività padre  
 Se un'attività padre annulla se stessa prima dell'avvio dell'attività figlio, quest'ultima non viene avviata.  Se un'attività padre annulla se stessa dopo l'avvio dell'attività figlio, quest'ultima viene completata a meno che non abbia una propria logica di annullamento.  Per altre informazioni, vedere [Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md).  
  
### Annullamento di un'attività figlio scollegata  
 Se un'attività figlio scollegata annulla se stessa usando lo stesso token passato all'attività padre e quest'ultima non attende l'attività figlio, non viene propagata alcuna eccezione poiché l'eccezione viene considerata come un annullamento cooperativo sicuro.  Questo comportamento è uguale a quello di qualsiasi attività di primo livello.  
  
### Annullamento di un'attività figlio collegata  
 Quando un'attività figlio collegata annulla se stessa usando lo stesso token passato all'attività padre, <xref:System.Threading.Tasks.TaskCanceledException> viene propagato al thread di unione all'interno di <xref:System.AggregateException>.  È necessario attendere l'attività padre in modo che sia possibile gestire tutte le eccezioni sicure oltre a tutte le eccezioni di errore propagate tramite un grafico di attività figlio collegate.  
  
 Per altre informazioni, vedere [Gestione delle eccezioni](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md).  
  
## Impedire il collegamento di un'attività figlio all'attività padre  
 Un'eccezione non gestita generata da un'attività figlio viene propagata all'attività padre.  È possibile usare questo comportamento per osservare tutte le eccezioni dell'attività figlio da un'attività radice invece di passare per un albero di attività.  Tuttavia, la propagazione delle eccezioni può essere problematica quando un'attività padre non prevede un allegato da altro codice.  Si consideri ad esempio un'applicazione che chiama un componente della libreria di terze parti da un oggetto <xref:System.Threading.Tasks.Task>.  Se il componente della libreria di terze parti crea anche un oggetto <xref:System.Threading.Tasks.Task> e specifica <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> per collegarlo all'attività padre, le eventuali eccezioni non gestite che si verificano nell'attività figlio vengono propagate all'attività padre.  Questo potrebbe causare un comportamento imprevisto nell'applicazione principale.  
  
 Per impedire il collegamento di un'attività figlio all'attività padre, specificare l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> quando si crea l'attività padre <xref:System.Threading.Tasks.Task> o l'oggetto <xref:System.Threading.Tasks.Task%601>.  Quando un'attività tenta di connettersi all'attività padre che specifica l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName>, l'attività figlio non riuscirà a collegarsi a un'attività padre e verrà eseguita come se l'opzione <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> non fosse stata specificata.  
  
 Se l'attività figlio non viene completata in modo tempestivo, è anche possibile impedirne il collegamento all'attività padre.  Poiché un'attività padre non viene completata fino al completamento di tutte le attività figlio, un'attività figlio a esecuzione prolungata può influire negativamente sulle prestazioni dell'applicazione.  Per un esempio in cui viene spiegato come migliorare le prestazioni dell'applicazione impedendo il collegamento di un'attività all'attività padre, vedere [How to: Prevent a Child Task from Attaching to its Parent](../../../docs/standard/parallel-programming/how-to-prevent-a-child-task-from-attaching-to-its-parent.md).  
  
## Vedere anche  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)