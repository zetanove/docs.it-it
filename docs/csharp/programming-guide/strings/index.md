---
title: Stringhe (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, strings
- strings [C#]
ms.assetid: 21580405-cb25-4541-89d5-037846a38b07
caps.latest.revision: 41
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: 5ec9d6aebcb38e89aa21b86cbd005c594bf756e6
ms.lasthandoff: 03/31/2017

---
# <a name="strings-c-programming-guide"></a>Stringhe (Guida per programmatori C#)
Una stringa è un oggetto di tipo <xref:System.String> il cui valore è testo. Internamente, il testo viene archiviato come una raccolta di sola lettura sequenziale di oggetti <xref:System.Char>. Le stringhe C# non presentano un carattere di terminazione null alla fine, pertanto una stringa C# può contenere qualsiasi numero di caratteri null incorporati ('\0'). La proprietà <xref:System.String.Length%2A> di una stringa rappresenta il numero di oggetti `Char` in essa contenuti e non il numero di caratteri Unicode. Per accedere ai singoli punti di codice Unicode in una stringa, usare l'oggetto <xref:System.Globalization.StringInfo>.  
  
## <a name="string-vs-systemstring"></a>string e System.String  
 In C#, la parola chiave `string` è un alias per <xref:System.String>. `String` e `string` sono pertanto equivalenti ed è possibile usare la convenzione di denominazione che si preferisce. La classe `String` fornisce molti metodi per creare, modificare e confrontare stringhe in modo sicuro. Inoltre, il linguaggio C# esegue l'overload di alcuni operatori per semplificare le operazioni comuni sulle stringhe. Per altre informazioni sull'uso della parola chiave, vedere [string](../../../csharp/language-reference/keywords/string.md). Per altre informazioni sul tipo e i relativi metodi, vedere <xref:System.String>.  
  
## <a name="declaring-and-initializing-strings"></a>Dichiarazione e inizializzazione di stringhe  
 È possibile dichiarare e inizializzare stringhe in vari modi, come mostrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStrings#1](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_1.cs)]  
  
 Si noti che l'operatore [new](../../../csharp/language-reference/keywords/new-operator.md) non viene usato per creare un oggetto stringa tranne nel caso in cui la stringa viene inizializzata con una matrice di caratteri.  
  
 Inizializzare una stringa con il valore costante <xref:System.String.Empty> per creare un nuovo oggetto <xref:System.String> la cui stringa è di lunghezza zero. La rappresentazione del valore letterale stringa di una stringa di lunghezza zero è "". Inizializzando le stringhe con il valore <xref:System.String.Empty> anziché [null](../../../csharp/language-reference/keywords/null.md), è possibile ridurre le possibilità di <xref:System.NullReferenceException>. Usare il metodo <xref:System.String.IsNullOrEmpty%28System.String%29> statico per verificare il valore di una stringa prima di tentare di accedervi.  
  
## <a name="immutability-of-string-objects"></a>Immutabilità degli oggetti stringa  
 Gli oggetti stringa sono *immutabili*, ovvero non possono essere modificati una volta creati. Tutti i metodi <xref:System.String> e gli operatori C# che sembrano modificare una stringa, in realtà restituiscono i risultati in un nuovo oggetto stringa. Nell'esempio seguente, quando il contenuto di `s1` e `s2` viene concatenato per formare un'unica stringa, le due stringhe originali restano immutate. L'operatore `+=` crea una nuova stringa che contiene il contenuto delle due stringhe combinato. Il nuovo oggetto viene assegnato alla variabile `s1` e l'oggetto originale assegnato a `s1` viene rilasciato per l'operazione di Garbage Collection perché nessun'altra variabile contiene un riferimento a tale oggetto.  
  
 [!code-cs[csProgGuideStrings#2](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_2.cs)]  
  
 Dato che una "modifica" della stringa è in effetti la creazione di una nuova stringa, è necessario prestare attenzione quando si creano riferimenti alle stringhe. Se si crea un riferimento a una stringa e quindi si "modifica" la stringa originale, il riferimento continuerà a puntare all'oggetto originale anziché al nuovo oggetto creato quando la stringa è stata modificata. Il codice seguente illustra questo comportamento:  
  
 [!code-cs[csProgGuideStrings#25](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_3.cs)]  
  
 Per altre informazioni su come creare nuove stringhe basate su modifiche quali operazioni di ricerca e sostituzione sulla stringa originale, vedere [Procedura: modificare il contenuto delle stringhe](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md).  
  
## <a name="regular-and-verbatim-string-literals"></a>Valori letterali stringa normali e verbatim  
 Usare valori letterali stringa normali quando è necessario incorporare caratteri di escape forniti da C#, come mostrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideStrings#3](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_4.cs)]  
  
 Usare stringhe verbatim per praticità e migliore leggibilità quando il testo della stringa contiene barre rovesciate, ad esempio nei percorsi di file. Dato che le stringhe verbatim mantengono i caratteri di nuova riga come parte del testo della stringa, possono essere usate per inizializzare stringhe su più righe. Usare virgolette doppie per incorporare una virgoletta in una stringa verbatim. L'esempio seguente mostra alcuni usi comuni delle stringhe verbatim:  
  
 [!code-cs[csProgGuideStrings#4](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_5.cs)]  
  
## <a name="string-escape-sequences"></a>Sequenze di escape delle stringhe  
  
|Sequenza di escape|Nome carattere|Codifica Unicode|  
|---------------------|--------------------|----------------------|  
|\\'|Virgoletta singola|0x0027|  
|\\"|Virgoletta doppia|0x0022|  
|\\\|Barra rovesciata|0x005C|  
|\0|Null|0x0000|  
|\a|Avviso|0x0007|  
|\b|Backspace|0x0008|  
|\f|Avanzamento carta|0x000C|  
|\n|Nuova riga|0x000A|  
|\r|Ritorno a capo|0x000D|  
|\t|Tabulazione orizzontale|0x0009|  
|\U|Sequenza di escape Unicode per le coppie di surrogati|\Unnnnnnnn|  
|\u|Sequenza di escape Unicode|\u0041 = "A"|  
|\v|Tabulazione verticale|0x000B|  
|\x|Sequenza di escape Unicode simile a "\u", ma con lunghezza variabile|\x0041 = "A"|  
  
> [!NOTE]
>  In fase di compilazione, le stringhe verbatim vengono convertite in stringhe normali con tutte le stesse sequenze di escape. Pertanto, se si visualizza una stringa verbatim nella finestra Espressioni di controllo del debugger, si vedranno i caratteri di escape aggiunti dal compilatore e non la versione verbatim del codice sorgente. Ad esempio, la stringa verbatim @"C:\file.txt" verrà visualizzata nella finestra Espressioni di controllo come "C:\\\file.txt".  
  
## <a name="format-strings"></a>Stringhe di formato  
 Una stringa di formato è una stringa il cui contenuto può essere determinato dinamicamente in fase di esecuzione. Si crea una stringa di formato tramite il metodo <xref:System.String.Format%2A> statico e incorporando in parentesi graffe i segnaposto che verranno sostituiti da altri valori in fase di esecuzione. L'esempio seguente usa una stringa di formato per restituire il risultato di ogni iterazione di un ciclo:  
  
 [!code-cs[csProgGuideStrings#26](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_6.cs)]  
  
 Un overload del metodo <xref:System.Console.WriteLine%2A> accetta una stringa di formato come parametro. Pertanto, è possibile incorporare solo un valore letterale stringa di formato senza una chiamata esplicita al metodo. Tuttavia, se si usa il metodo <xref:System.Diagnostics.Trace.WriteLine%2A> per visualizzare l'output di debug nella finestra **Output** di Visual Studio, si deve chiamare in modo esplicito il metodo <xref:System.String.Format%2A> perché <xref:System.Diagnostics.Trace.WriteLine%2A> accetta solo una stringa e non una stringa di formato. Per altre informazioni sulle stringhe di formato, vedere [Formattazione di tipi](../../../standard/base-types/formatting-types.md).  
  
## <a name="substrings"></a>Sottostringhe  
 Una sottostringa è qualsiasi sequenza di caratteri contenuta in una stringa. Usare il metodo <xref:System.String.Substring%2A> per creare una nuova stringa da una parte della stringa originale. È possibile cercare una o più occorrenze di una sottostringa tramite il metodo <xref:System.String.IndexOf%2A>. Usare il metodo <xref:System.String.Replace%2A> per sostituire tutte le occorrenze di una sottostringa specificata con una nuova stringa. Come il metodo <xref:System.String.Substring%2A>, <xref:System.String.Replace%2A> restituisce in realtà una nuova stringa e non modifica la stringa originale. Per altre informazioni, vedere [Procedura: eseguire la ricerca di stringhe tramite metodi stringa](../../../csharp/programming-guide/strings/how-to-search-strings-using-string-methods.md) e [Procedura: modificare il contenuto delle stringhe](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md).  
  
 [!code-cs[csProgGuideStrings#7](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_7.cs)]  
  
## <a name="accessing-individual-characters"></a>Accesso a caratteri singoli  
 È possibile utilizzare la notazione di matrice con un valore di indice per ottenere l'accesso in sola lettura a singoli caratteri, come nell'esempio seguente:  
  
 [!code-cs[csProgGuideStrings#9](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_8.cs)]  
  
 Se i metodi <xref:System.String> non forniscono la funzionalità richiesta per modificare singoli caratteri in una stringa, è possibile usare un oggetto <xref:System.Text.StringBuilder> per modificare i singoli caratteri "sul posto", quindi creare una nuova stringa per archiviare i risultati tramite i metodi <xref:System.Text.StringBuilder>. Nell'esempio seguente presupporre che sia necessario modificare la stringa originale in un modo specifico e archiviare quindi i risultati per uso futuro:  
  
 [!code-cs[csProgGuideStrings#8](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_9.cs)]  
  
## <a name="null-strings-and-empty-strings"></a>Stringhe null e stringhe vuote  
 Una stringa vuota è un'istanza di un oggetto <xref:System.String?displayProperty=fullName> che contiene zero caratteri. Le stringhe vuote sono utilizzate di frequente in diversi scenari di programmazione per rappresentare un campo di testo vuoto. È possibile chiamare metodi in stringhe vuote perché sono oggetti <xref:System.String?displayProperty=fullName> validi. Le stringhe vuote vengono inizializzate come indicato di seguito:  
  
```  
string s = String.Empty;  
```  
  
 Al contrario, una stringa null non fa riferimento a un'istanza di un oggetto <xref:System.String?displayProperty=fullName> ed eventuali tentativi di chiamata di un metodo su una stringa null restituiscono un'eccezione <xref:System.NullReferenceException>. È tuttavia possibile usare stringhe null nelle operazioni di concatenazione e confronto con altre stringhe. Gli esempi seguenti illustrano alcuni casi in cui un riferimento a una stringa null causa o meno la generazione di un'eccezione:  
  
 [!code-cs[csProgGuideStrings#27](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_10.cs)]  
  
## <a name="using-stringbuilder-for-fast-string-creation"></a>Uso di StringBuilder per la creazione veloce di stringhe  
 Le operazioni sulle stringhe in .NET sono altamente ottimizzate e nella maggior parte dei casi non influiscono sulle prestazioni in modo significativo. Tuttavia, in alcuni scenari, ad esempio cicli rigidi eseguiti molte centinaia o migliaia di volte, le operazioni sulle stringhe possono incidere sulle prestazioni. La classe <xref:System.Text.StringBuilder> crea un buffer di stringhe che offre prestazioni migliori se il programma esegue numerose modifiche di stringhe. La stringa <xref:System.Text.StringBuilder> consente anche di riassegnare singoli caratteri, un'operazione non supportata dal tipo di dati string incorporato. Questo codice, ad esempio, consente di modificare il contenuto di una stringa senza crearne una nuova:  
  
 [!code-cs[csProgGuideStrings#20](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_11.cs)]  
  
 In questo esempio viene usato un oggetto <xref:System.Text.StringBuilder> per creare una stringa da un set di tipi numerici:  
  
 [!code-cs[csProgGuideStrings#15](../../../csharp/programming-guide/strings/codesnippet/CSharp/index_12.cs)]  
  
## <a name="strings-extension-methods-and-linq"></a>Stringhe, metodi di estensione e LINQ  
 Poiché il tipo <xref:System.String> implementa <xref:System.Collections.Generic.IEnumerable%601>, è possibile usare i metodi di estensione definiti nella classe <xref:System.Linq.Enumerable> sulle stringhe. Per evitare confusioni a livello visivo, questi metodi sono esclusi da IntelliSense per il tipo <xref:System.String>, ma sono comunque disponibili. È anche possibile usare le espressioni di query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] sulle stringhe. Per altre informazioni, vedere [LINQ e stringhe](../../../csharp/programming-guide/concepts/linq/linq-and-strings.md).  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Procedura: Modificare il contenuto delle stringhe](../../../csharp/programming-guide/strings/how-to-modify-string-contents.md)|Esempio di codice che illustra come modificare il contenuto delle stringhe.|  
|[Procedura: Concatenare più stringhe](../../../csharp/programming-guide/strings/how-to-concatenate-multiple-strings.md)|Viene illustrato come usare l'operatore `+` e la classe `Stringbuilder` per unire stringhe in fase di compilazione e fase di esecuzione.|  
|[Procedura: Confrontare stringhe](../../../csharp/programming-guide/strings/how-to-compare-strings.md)|Viene illustrato come eseguire confronti ordinali di stringhe.|  
|[Procedura: Analizzare le stringhe con String.Split ](../../../csharp/programming-guide/strings/how-to-parse-strings-using-string-split.md)|Esempio di codice che illustra come usare il metodo `String.Split` per analizzare le stringhe.|  
|[Procedura: Eseguire la ricerca di stringhe usando metodi stringa](../../../csharp/programming-guide/strings/how-to-search-strings-using-string-methods.md)|Viene spiegato come usare metodi specifici per la ricerca di stringhe.|  
|[Procedura: Eseguire la ricerca di stringhe usando espressioni regolari](../../../csharp/programming-guide/strings/how-to-search-strings-using-regular-expressions.md)|Viene spiegato come usare le espressioni regolari per la ricerca di stringhe.|  
|[Procedura: Determinare se una stringa rappresenta un valore numerico](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)|Viene illustrato come analizzare in modo sicuro una stringa per verificare se ha un valore numerico valido.|  
|[Procedura: Convertire una stringa in un oggetto DateTime](../../../csharp/programming-guide/strings/how-to-convert-a-string-to-a-datetime.md)|Viene illustrato come convertire una stringa come "24/01/2008" in un oggetto <xref:System.DateTime?displayProperty=fullName>.|  
|[Operazioni di base su stringhe](https://msdn.microsoft.com/library/a292he7t)|Collegamenti agli argomenti che usano <xref:System.String?displayProperty=fullName> e <xref:System.Text.StringBuilder?displayProperty=fullName> per eseguire operazioni di base sulle stringhe.|  
|[Analisi di stringhe](https://msdn.microsoft.com/library/b4w53z0y)|Viene descritto come inserire caratteri o spazi vuoti in una stringa.|  
|[Confronto di stringhe](https://msdn.microsoft.com/library/fbh501kz)|Informazioni su come confrontare le stringhe ed esempi in C# e Visual Basic.|  
|[Uso della classe StringBuilder](../../../standard/base-types/stringbuilder.md)|Viene descritto come creare e modificare oggetti stringa dinamici tramite la classe <xref:System.Text.StringBuilder>.|  
|[LINQ e stringhe](../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)|Informazioni su come eseguire varie operazioni sulle stringhe tramite query LINQ.|  
|[Guida per programmatori C#](../../../csharp/programming-guide/index.md)|Collegamenti ad argomenti che spiegano i costrutti di programmazione in C#.|  

