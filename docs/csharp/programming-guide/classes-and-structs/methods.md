---
title: "Metodi (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, metodi"
  - "metodi [C#]"
ms.assetid: cc738f07-e8cd-4683-9585-9f40c0667c37
caps.latest.revision: 41
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 41
---
# Metodi (Guida per programmatori C#)
Un metodo è un blocco di codice che contiene una serie di istruzioni. Un programma fa in modo che le istruzioni vengano eseguite chiamando il metodo e specificando gli argomenti del metodo obbligatori. In C\#, ogni istruzione eseguita viene attuata nel contesto di un metodo. Il metodo principale è il punto di ingresso per ogni applicazione C\# e viene chiamato da Common Language Runtime \(CLR\) quando viene avviato il programma.  
  
> [!NOTE]
>  In questo argomento vengono descritti i metodi denominati. Per informazioni sulle funzioni anonime, vedere [Funzioni anonime](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## Firme del metodo  
 I metodi vengono dichiarati in una [classe](../../../csharp/language-reference/keywords/class.md) o in una [struct](../../../csharp/language-reference/keywords/struct.md) specificando il livello di accesso, ad esempio `public` o `private`, i modificatori facoltativi, ad esempio `abstract` o `sealed`, il valore restituito, il nome del metodo e i parametri del metodo. Queste parti costituiscono la firma del metodo.  
  
> [!NOTE]
>  Un tipo restituito di un metodo non fa parte della firma del metodo in caso di overload dei metodi. Fa tuttavia parte della firma del metodo quando si determina la compatibilità tra un delegato e il metodo a cui fa riferimento.  
  
 I parametri del metodo vengono racchiusi tra parentesi e separati da virgole. Le parentesi vuote indicano che il metodo non richiede parametri. Questa classe contiene tre metodi:  
  
 [!code-cs[csProgGuideObjects#40](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_1.cs)]  
  
## Accesso ai metodi  
 Chiamare un metodo su un oggetto è come accedere a un campo. Dopo il nome dell'oggetto aggiungere un punto, il nome del metodo e le parentesi. Gli argomenti vengono elencati tra parentesi e separati da virgole. I metodi della classe `Motorcycle` possono quindi essere chiamati come nell'esempio seguente:  
  
 [!code-cs[csProgGuideObjects#41](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_2.cs)]  
  
## Parametri di metodo e argomenti  
 La definizione del metodo specifica i nomi e i tipi di tutti i parametri obbligatori. Quando il codice chiamante chiama il metodo, fornisce valori concreti, detti argomenti, per ogni parametro. Gli argomenti devono essere compatibili con il tipo di parametro, ma il nome dell'argomento \(se esistente\) usato nel codice chiamante non deve essere lo stesso del parametro denominato definito nel metodo. Ad esempio:  
  
 [!code-cs[csProgGuideObjects#74](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_3.cs)]  
  
## Passaggio per riferimento e passaggio per valore  
 Per impostazione predefinita, quando un tipo valore viene passato a un metodo, viene passata una copia anziché l'oggetto stesso. Di conseguenza, le modifiche all'argomento non hanno effetto sulla copia dell'originale nel metodo chiamante. È possibile passare un tipo valore per riferimento usando la parola chiave ref. Per altre informazioni, vedere [Passaggio di parametri di tipi di valore](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md). Per un elenco dei tipi predefiniti, vedere [Tabella dei tipi di valore](../../../csharp/language-reference/keywords/value-types-table.md).  
  
 Quando viene passato un oggetto di un tipo riferimento a un metodo, viene passato un riferimento all'oggetto, ovvero, il metodo riceve un argomento che indica la posizione dell'oggetto, ma non l'oggetto stesso. Se si modifica un membro dell'oggetto usando questo riferimento, la modifica si riflette nell'argomento nel metodo chiamante, anche se si passa l'oggetto per valore.  
  
 Per creare un tipo riferimento, usare la parola chiave `class`, come mostra l'esempio seguente.  
  
 [!code-cs[csProgGuideObjects#42](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_4.cs)]  
  
 Se ora si passa un oggetto basato su questo tipo a un metodo, viene passato un riferimento all'oggetto. Il seguente esempio passa un oggetto di tipo `SampleRefType` al metodo `ModifyObject`.  
  
 [!code-cs[csProgGuideObjects#75](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_5.cs)]  
  
 L'esempio è sostanzialmente uguale al precedente in quanto passa un argomento per valore a un metodo, ma, essendo usato un tipo riferimento, il risultato è diverso. La modifica apportata in `ModifyObject` al campo `value` del parametro, `obj`, cambia anche il campo `value` dell'argomento, `rt`, nel metodo `TestRefType`. Il metodo `TestRefType` visualizza 33 come output.  
  
 Per altre informazioni su come passare i tipi riferimento per riferimento e per valore, vedere [Passaggio di parametri di tipi di riferimento](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md) e [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md).  
  
## Valori restituiti  
 I metodi possono restituire un valore al chiamante. Se il tipo restituito, il tipo elencato prima del nome del metodo, non è `void`, il metodo può restituire il valore usando la parola chiave `return`. Un'istruzione con la parola chiave `return` seguita da un valore corrispondente al tipo restituito restituirà tale valore al chiamante del metodo. La parola chiave `return` interrompe anche l'esecuzione del metodo. Se il tipo restituito è `void`, un'istruzione `return` senza un valore è tuttavia utile per interrompere l'esecuzione del metodo. Senza la parola chiave `return`, l'esecuzione del metodo verrà interrotta quando verrà raggiunta la fine del blocco di codice. Per usare la parola chiave `return` per restituire un valore, sono obbligatori metodi con un tipo restituito non void. Ad esempio, questi due metodi usano la parola chiave `return` per restituire numeri interi:  
  
 [!code-cs[csProgGuideObjects#44](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_6.cs)]  
  
 Per usare un valore restituito da un metodo, il metodo chiamante può usare la chiamata al metodo stessa ovunque è sufficiente un valore dello stesso tipo. È inoltre possibile assegnare il valore restituito a una variabile. I due esempi seguenti di codice ottengono lo stesso risultato:  
  
 [!code-cs[csProgGuideObjects#45](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_7.cs)]  
  
 [!code-cs[csProgGuideObjects#46](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/methods_8.cs)]  
  
 L'uso di una variabile locale, in questo caso `result`, per archiviare un valore è facoltativo. Potrebbe migliorare la leggibilità del codice o potrebbe essere necessario se si desidera archiviare il valore originale dell'argomento per l'intero ambito del metodo.  
  
 Non è necessario restituire una matrice multidimensionale da un metodo, M, che modifica il contenuto della matrice, se la funzione chiamante ha passato la matrice a M. Si può restituire la matrice risultante da M per un flusso di valori corretto o funzionale, ma non è necessario.  Il motivo per cui non è necessario restituire la matrice modificata è che C\# passa tutti i tipi riferimento per valore e il valore di un riferimento della matrice è il puntatore alla matrice. Nel metodo M, eventuali modifiche apportate al contenuto della matrice sono osservabili da qualsiasi codice che presenti un riferimento alla matrice, come illustrato nell'esempio seguente.  
  
```c#  
static void Main(string[] args) { int[,] matrix = new int[2, 2]; FillMatrix(matrix); // matrix is now full of -1 } public static void FillMatrix(int[,] matrix) { for (int i = 0; i < matrix.GetLength(0); i++) { for (int j = 0; j < matrix.GetLength(1); j++) { matrix[i, j] = -1; } } }  
  
```  
  
 Per altre informazioni, vedere [return](../../../csharp/language-reference/keywords/return.md).  
  
## Metodi asincroni  
 Tramite la funzionalità async, è possibile richiamare i metodi asincroni senza usare callback espliciti o suddividere manualmente il codice in più metodi o espressioni lambda. La funzionalità async è stata introdotta in [!INCLUDE[vs_dev11_long](../../../csharp/includes/vs-dev11-long-md.md)].  
  
 Se si contrassegna un metodo con il modificatore [async](../../../csharp/language-reference/keywords/async.md), è possibile usare l'operatore [await](../../../csharp/language-reference/keywords/await.md) nel metodo. Quando il controllo raggiunge un'espressione await nel metodo asincrono, il controllo torna al chiamante e l'avanzamento nel metodo viene sospeso fino al completamento dell'attività attesa. Una volta completata l'attività, l'esecuzione del metodo può riprendere.  
  
> [!NOTE]
>  Un metodo async viene restituito al chiamante quando rileva il primo oggetto atteso che non è ancora completo o raggiunge la fine del metodo async, qualunque si verifichi prima.  
  
 Un metodo asincrono può avere un tipo restituito <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task> o void. Il tipo restituito void viene usato principalmente per definire i gestori eventi, dove un tipo restituito void è necessario. Un metodo asincrono che restituisce void non può essere atteso e il chiamante di un metodo che restituisce void non può intercettare eccezioni generate dal metodo.  
  
 Nel seguente esempio, `DelayAsync` è un metodo asincrono con un tipo restituito <xref:System.Threading.Tasks.Task%601>.`DelayAsync` ha un'istruzione `return` che restituisce un numero intero. La dichiarazione del metodo di `DelayAsync` deve quindi avere un tipo restituito `Task<int>`. Poiché il tipo restituito è `Task<int>`, la valutazione dell'espressione `await` in `DoSomethingAsync` genera un numero intero come illustra l'istruzione seguente: `int result = await delayTask`.  
  
 Il metodo `startButton_Click` è un esempio di un metodo asincrono con un tipo restituito void. Poiché `DoSomethingAsync` è un metodo asincrono, l'attività per la chiamata a `DoSomethingAsync` deve essere attesa, come mostra l'istruzione seguente: `await DoSomethingAsync();`. Il metodo `startButton_Click` deve essere definito con il modificatore `async` perché il metodo ha un'espressione `await`.  
  
 [!code-cs[csAsyncMethod#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/asyncmethodcs/mainwindow.xaml.cs#2)]  
  
 Un metodo asincrono non può dichiarare parametri [ref](../../../csharp/language-reference/keywords/ref.md) o [out](../../../csharp/language-reference/keywords/out.md), ma può chiamare metodi che hanno tali parametri.  
  
 Per altre informazioni sui metodi asincroni, vedere [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md), [Flusso di controllo in programmi asincroni](../Topic/Control%20Flow%20in%20Async%20Programs%20\(C%23%20and%20Visual%20Basic\).md) e [Tipi restituiti asincroni](../Topic/Async%20Return%20Types%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Definizioni di espressioni corpo  
 È comune disporre di definizioni di metodo che semplicemente restituiscono subito il risultato di un'espressione o che includono una singola istruzione come corpo del metodo.  Esiste una sintassi breve per definire tali metodi usando `=>`:  
  
```c#  
public Point Move(int dx, int dy) => new Point(x + dx, y + dy); public void Print() => Console.WriteLine(First + " " + Last); // Works with operators, properties, and indexers too. public static Complex operator +(Complex a, Complex b) => a.Add(b); public string Name => First + " " + Last; public Customer this[long id] => store.LookupCustomer(id);  
```  
  
 Se il metodo restituisce `void` o è un metodo asincrono, il corpo del metodo deve essere un'espressione di istruzione \(come per le espressioni lambda\).  Per le proprietà e gli indicizzatori, devono essere di sola lettura e non è necessario usare la parola chiave della funzione di accesso `get`.  
  
## Iteratori  
 Un iteratore esegue un'iterazione personalizzata su una raccolta, ad esempio un elenco o una matrice. Un iteratore usa l'istruzione [yield return](../../../csharp/language-reference/keywords/yield.md) per restituire un elemento per volta. Quando viene raggiunta un'istruzione [yield return](../../../csharp/language-reference/keywords/yield.md), la posizione corrente nel codice viene memorizzata. L'esecuzione viene riavviata a partire da quella posizione la volta successiva che viene chiamato l'iteratore.  
  
 Per chiamare un iteratore dal codice client, usare un'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md).  
  
 Il tipo restituito di un iteratore può essere <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator> o <xref:System.Collections.Generic.IEnumerator%601>.  
  
 Per altre informazioni, vedere [Iteratori](../Topic/Iterators%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)   
 [params](../../../csharp/language-reference/keywords/params.md)   
 [return](../../../csharp/language-reference/keywords/return.md)   
 [out](../../../csharp/language-reference/keywords/out.md)   
 [ref](../../../csharp/language-reference/keywords/ref.md)   
 [Passaggio di parametri](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)