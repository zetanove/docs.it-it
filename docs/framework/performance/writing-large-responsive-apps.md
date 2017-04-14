---
title: "Scrittura di app grandi e reattive in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 123457ac-4223-4273-bb58-3bc0e4957e9d
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
caps.handback.revision: 23
---
# Scrittura di app grandi e reattive in .NET Framework
Questo articolo include suggerimenti per il miglioramento delle prestazioni delle app .NET Framework di grandi dimensioni o di app che elaborano una quantità elevata di dati, ad esempio file o database.  Questi suggerimenti derivano dalla riscrittura di compilatori C\# e Visual Basic nel codice gestito e l'articolo include diversi esempi concreti tratti dal compilatore C\#.  
  
 Grazie a .NET Framework è possibile ottenere una produttività elevata per la creazione di app.  Linguaggi avanzati e sicuri e una vasta raccolta di librerie rendono molto efficace la creazione delle app.  La produttività elevata comporta tuttavia alcune conseguenze.  È consigliabile usare tutte le funzionalità di .NET Framework, ma occorre ottimizzare le prestazioni del codice in caso di necessità.  
  
## Applicabilità delle prestazioni del nuovo compilatore all'app  
 Il team responsabile del progetto .NET Compiler Platform \("Roslyn"\) ha riscritto i compilatori C\# e Visual Basic nel codice gestito, per offrire nuove API per la modellazione e l'analisi di codice, la creazione di strumenti e l'abilitazione di esperienze più avanzate e sensibili al codice in Visual Studio.  La riscrittura dei compilatori e la creazione di esperienze di Visual Studio nei nuovi compilatori hanno permesso di ottenere approfondimenti utili sulle prestazioni, applicabili a qualsiasi app .NET Framework di grandi dimensioni o a qualsiasi app che elabora quantità elevate di dati.  Per avvalersi degli approfondimenti e degli esempi tratti dal compilatore C\#, non sono necessarie conoscenze specifiche sui compilatori.  
  
 Visual Studio usa le API dei compilatori per creare tutte le funzionalità IntelliSense amate dagli utenti, ad esempio la colorazione di identificatori e parole chiave, elenchi di completamento della sintassi, zigzag per gli errori, suggerimenti relativi ai parametri, problemi relativi al codice e azioni per il codice.  Visual Studio offre questo supporto mentre gli sviluppatori digitano e modificano il codice e Visual Studio deve essere sempre in grado di rispondere mentre il compilatore modella in modo continuativo il codice modificato dagli sviluppatori.  
  
 Quando gli utenti finali interagiscono con l'app, si aspettano che sia reattiva.  La digitazione o la gestione dei comandi non devono essere mai bloccate.  Le informazioni di supporto devono essere visualizzate rapidamente o scomparire se l'utente continua a digitare.  L'app deve evitare di bloccare il thread dell'interfaccia utente con calcoli di lunga durata, che potrebbero dare l'impressione di lentezza dell'app.  
  
 Per altre informazioni sui nuovi compilatori, vedere il sito Web relativo al [progetto open source .NET Compiler Platform \("Roslyn"\)](http://roslyn.codeplex.com/).  
  
## Considerazioni essenziali  
 Quando si ottimizzano le prestazioni e si creano app .NET Framework reattive, occorre prestare attenzione alle considerazioni seguenti.  
  
### Considerazione 1: Non eseguire prematuramente l'ottimizzazione  
 La scrittura di codice più complesso del necessario comporta costi di gestione, debug e ottimizzazione.  I programmatori esperti sono in grado di risolvere problemi di codifica e di scrivere codice più efficiente in modo intuitivo.  A volte, però, ottimizzano il codice con troppo anticipo.  Ad esempio, usano una tabella hash quando sarebbe sufficiente una semplice matrice o usano una procedura complessa per la memorizzazione nella cache, che può provocare la perdita di memoria, invece di ricalcolare semplicemente i valori.  Anche se si è programmatori esperti, è consigliabile eseguire test relativi alle prestazioni e analizzare il codice in caso di problemi.  
  
### Considerazione 2: Solo le misurazioni assicurano la precisione  
 I profili e le misurazioni sono attendibili.  I profili indicano se la CPU è caricata completamente o se si è verificato un blocco di I\/O del disco.  Specificano inoltre il tipo e la quantità di memoria allocata e se la CPU dedica molto tempo a [Garbage Collection](../../../docs/standard/garbage-collection/index.md) \(GC\).  
  
 È consigliabile definire obiettivi per le prestazioni relative a esperienze utente o scenari chiave dell'app e scrivere test per la misurazione delle prestazioni.  Esaminare i test che rilevano errori applicando un metodo scientifico: usare i profili come indicazione, definire ipotesi sulla natura del problema e testare le ipotesi tramite un esperimento o una modifica del codice.  Stabilire misure di base per le prestazioni nel tempo grazie a testing regolare, in modo da potere isolare le modifiche che provocano una regressione nelle prestazioni.  Un approccio rigoroso alle operazioni relative alle prestazioni permette di evitare di perdere tempo con aggiornamenti di codice superflui.  
  
### Considerazione 3: La qualità degli strumenti è essenziale  
 Gli strumenti efficaci permettono di individuare rapidamente i problemi principali a livello di prestazioni \(CPU, memoria o disco\) e semplificano l'individuazione del codice che provoca tali colli di bottiglia.  Microsoft offre diversi strumenti relativi alle prestazioni, ad esempio [Profiler di Visual Studio](../Topic/Beginners%20Guide%20to%20Performance%20Profiling.md), [Windows Phone Analysis Tool](http://msdn.microsoft.com/it-it/e67e3199-ea43-4d14-ab7e-f7f19266253f) e [PerfView](http://www.microsoft.com/download/details.aspx?id=28567).  
  
 PerfView è uno strumento gratuito e straordinariamente efficace che permette di concentrarsi sui problemi essenziali, ad esempio I\/O del disco, eventi GC e memoria.  È possibile acquisire eventi [Event Tracing for Windows](../../../docs/framework/wcf/samples/etw-tracing.md) \(ETW\) relativi alle prestazioni e visualizzarli con facilità in base a singole app, singoli stack e informazioni di thread.  PerfView mostra la quantità e il tipo di memoria allocata dall'app e le quantità di memoria allocate da quali funzioni o stack di chiamata.  Per informazioni dettagliate, vedere gli argomenti, le demo e i video di supporto inclusi con lo strumento, ad esempio le [esercitazioni relative a PerfView](http://channel9.msdn.com/Series/PerfView-Tutorial) su Channel 9.  
  
### Considerazione 4: Le allocazioni sono importantissime  
 Si potrebbe pensare che la creazione di un'app .NET Framework reattiva dipenda completamente dagli algoritmi, ad esempio dall'uso dell'ordinamento rapido invece dell'ordinamento a bolle, ma non è così.  Il fattore principale nella creazione di un'app reattiva è costituito dall'allocazione della memoria, in particolare se le dimensioni dell'app sono molto elevate o se l'app elabora quantità elevate di dati.  
  
 Quasi tutte le operazioni relative alla creazione di esperienze IDE reattive con le API del nuovo compilatore comportano il tentativo di evitare allocazioni e la gestione delle strategie per la memorizzazione nella cache.  Le tracce di PerfView mostrano che le prestazioni dei nuovi compilatori C\# e Visual Basic è associato raramente alla CPU.  I compilatori possono essere associati a I\/O durante la lettura di centinaia di migliaia o di milioni di righe di codice, la lettura di metadati o l'emissione di codice generato.  I ritardi dei thread dell'interfaccia utente sono quasi sempre dovuti a operazioni di Garbage Collection.  Le operazioni di Garbage Collection di .NET Framework sono ottimizzate al massimo per le prestazioni e sono eseguite nella maggior parte dei casi simultaneamente all'esecuzione del codice dell'app.  Una singola allocazione, tuttavia, può attivare una raccolta [gen2](../../../docs/standard/garbage-collection/fundamentals.md) dispendiosa, arrestando tutti i thread.  
  
## Allocazioni comuni ed esempi  
 Le espressioni di esempio in questa sezione includono allocazioni nascoste apparentemente di piccole dimensioni.  Se tuttavia un'app di grandi dimensioni esegue le espressioni per un numero sufficiente di volte, è possibile che ciò generi centinaia di megabyte o addirittura gigabyte di allocazioni.  Ad esempio, test di un minuto che simulano la digitazione nell'editor da parte di uno sviluppatore hanno provocato l'allocazione di gigabyte di memoria e hanno portato il team responsabile delle prestazioni a esaminare a fondo gli scenari relativi alla digitazione.  
  
### Conversione boxing  
 La [conversione boxing](../Topic/Boxing%20and%20Unboxing%20\(C%23%20Programming%20Guide\).md) si verifica quando si esegue il wrapping in un oggetto di tipi di valori che normalmente si trovano nello stack o in strutture di dati,  ovvero quando si alloca un oggetto per l'inclusione dei dati e quindi si restituisce un puntatore a quell'oggetto.  La conversione boxing dei valori è a volte eseguita in .NET Framework a causa della firma di un metodo o del tipo di posizione di archiviazione.  Il wrapping di un tipo di valore in un oggetto provoca l'allocazione di memoria.  Molte operazioni di conversione boxing possono comportare megabyte o gigabyte di allocazioni nell'app e quindi l'app provocherà più operazioni di Garbage Collection.  I compilatori di linguaggi e .NET Framework evitano la conversione boxing quando possibile, ma a volte questa conversione si verifica in modo imprevisto.  
  
 Per verificare la conversione boxing in PerfView, aprire una traccia ed esaminare gli stack di allocazione heap corrispondenti al nome di processo dell'app. Occorre ricordare che PerfView crea report relativi a tutti i processi.  Se alle allocazioni sono associati tipi quali <xref:System.Int32?displayProperty=fullName> e <xref:System.Char?displayProperty=fullName>, si sta eseguendo la conversione boxing dei tipi di valore.  Se si sceglie uno di questi tipi, saranno visualizzati gli stack e le funzioni in cui ne è eseguita la conversione boxing.  
  
 **Esempio 1: metodi di stringa e argomenti di tipo valore**  
  
 Questo codice di esempio illustra la conversione boxing potenzialmente superflua ed eccessiva:  
  
```csharp  
public class Logger  
{  
    public static void WriteLine(string s) { /*...*/ }  
}  
  
public class BoxingExample  
{  
    public void Log(int id, int size)  
    {  
        var s = string.Format("{0}:{1}", id, size);  
        Logger.WriteLine(s);  
    }  
}  
  
```  
  
 Il codice fornisce funzionalità di registrazione, in modo che un'app possa chiamare spesso la funzione `Log`, anche milioni di volte.  Il problema consiste nel fatto che la chiamata a `string.Format` provoca l'overload di <xref:System.String.Format%28System.String%2CSystem.Object%2CSystem.Object%29>.  
  
 L'overload richiede a .NET Framework di eseguire la conversione boxing dei valori `int` in oggetti per passarli alla chiamata del metodo.  Una soluzione parziale consiste nel chiamare `id.ToString()` e `size.ToString()` e passare tutte le stringe \(ovvero gli oggetti\) alla chiamata `string.Format`.  La chiamata a `ToString()` permette di allocare una stringa, ma l'allocazione sarà comunque eseguita in `string.Format`.  
  
 È possibile che si pensi che questa chiamata di base a `string.Format` sia solo una concatenazione di stringhe e che quindi si scriva invece il codice seguente:  
  
```csharp  
var s = id.ToString() + ':' + size.ToString();  
```  
  
 Questa riga di codice, tuttavia, introduce un'allocazione di tipo boxing, poiché si ottiene <xref:System.String.Concat%28System.Object%2CSystem.Object%2CSystem.Object%29> come risultato della compilazione.  È necessario che .NET Framework esegua la conversione boxing del valore letterale di carattere per richiamare `Concat`  
  
 **Correzione per l'esempio 1**  
  
 La correzione completa è molto semplice.  È sufficiente sostituire il valore letterale di carattere con il valore letterale di stringa, che non provoca conversione boxing poiché le stringhe sono già oggetti:  
  
```csharp  
var s = id.ToString() + ":" + size.ToString();  
  
```  
  
 **Esempio 2: Conversione boxing delle enumerazioni**  
  
 Questo esempio è responsabile di una quantità elevata di allocazioni nei nuovi compilatori C\# e Visual Basic a causa dell'uso frequente di tipi di enumerazione, in particolare nelle operazioni di ricerca nel dizionario.  
  
```csharp  
public enum Color  
{  
    Red, Green, Blue  
}  
  
public class BoxingExample  
{  
    private string name;  
    private Color color;  
    public override int GetHashCode()  
    {  
        return name.GetHashCode() ^ color.GetHashCode();  
    }  
}  
  
```  
  
 Questo problema è molto complesso.  PerfView lo segnalerebbe come conversione boxing di <xref:System.Enum.GetHashCode>, poiché il metodo esegue la conversione boxing della rappresentazione sottostante del tipo di enumerazione, per fini di implementazione.  Se si esamina attentamente in PerfView, è possibile notare due allocazioni di tipo boxing per ogni chiamata a <xref:System.Enum.GetHashCode>.  Il compilatore ne inserisce una e .NET Framework inserisce l'altra.  
  
 **Correzione per l'esempio 2**  
  
 È possibile evitare con facilità entrambe le allocazioni tramite esecuzione di cast sulla rappresentazione sottostante prima di chiamare <xref:System.Enum.GetHashCode>:  
  
```csharp  
((int)color).GetHashCode()  
  
```  
  
 Un'altra causa comune della conversione boxing sui tipi di enumerazione è costituita dal metodo <xref:System.Enum.HasFlag%28System.Enum%29?displayProperty=fullName>.  È necessario eseguire la conversione boxing dell'argomento passato a <xref:System.Enum.HasFlag%28System.Enum%29>.  Nella maggior parte dei casi, la sostituzione di chiamate a <xref:System.Enum.HasFlag%28System.Enum%29?displayProperty=fullName> con un test bit per bit risulta più semplice e non comporta la creazione di allocazioni.  
  
 Occorre ricordare la prima considerazione sulle prestazioni, ovvero non ottimizzare con troppo anticipo, e non iniziare a riscrivere in questo modo tutto il codice.  È necessario essere consapevoli dei costi relativi alla conversione boxing, ma cambiare il codice solo dopo la profilatura dell'app e l'individuazione delle aree sensibili.  
  
### Stringhe  
 Le modifiche alle stringhe sono una delle cause principali delle allocazioni e spesso sono visualizzate nelle prime cinque allocazioni in PerfView.  I programmi usano le stringhe per serializzazione, JSON e API REST.  È possibile usare le stringhe come costanti a livello di codice per l'ineroperabilità con i sistemi quando non è possibile usare i tipi di enumerazione.  Quando la profilatura mostra che le stringhe influiscono notevolmente sulle prestazioni, cercare chiamate a metodi <xref:System.String> quali <xref:System.String.Format%2A>, <xref:System.String.Concat%2A>, <xref:System.String.Split%2A>, <xref:System.String.Join%2A>, <xref:System.String.Substring%2A> e così via.  L'uso di <xref:System.Text.StringBuilder> per evitare i costi di creazione di una stringa da molti pezzi è utile, ma anche l'allocazione dell'oggetto <xref:System.Text.StringBuilder> potrebbe trasformarsi in un collo di bottiglia da gestire.  
  
 **Esempio 3: Operazioni su stringhe**  
  
 Il compilatore C\# include il codice seguente per la scrittura del testo di un commento di un documento XML formattato:  
  
```csharp  
public void WriteFormattedDocComment(string text)  
{  
    string[] lines = text.Split(new[] { "\r\n", "\r", "\n" },  
                                StringSplitOptions.None);  
    int numLines = lines.Length;  
    bool skipSpace = true;  
    if (lines[0].TrimStart().StartsWith("///"))  
    {  
        for (int i = 0; i < numLines; i++)  
        {  
            string trimmed = lines[i].TrimStart();  
            if (trimmed.Length < 4 || !char.IsWhiteSpace(trimmed[3]))  
            {  
                skipSpace = false;  
                break;  
            }  
        }  
        int substringStart = skipSpace ? 4 : 3;  
        for (int i = 0; i < numLines; i++)  
            WriteLine(lines[i].TrimStart().Substring(substringStart));  
    }  
    else { /* ... */ }  
  
```  
  
 Come si può notare, nel codice sono eseguite molte modifiche sulle stringhe.  Il codice usa i metodi della libreria per suddividere le righe in stringhe separate, ritagliare lo spazio vuoto, verificare se l'argomento `text` è un commento di documentazione XML ed estrarre sottostringhe dalle righe.  
  
 Nella prima riga in `WriteFormattedDocComment` la chiamata `text.Split` esegue l'allocazione di una nuova matrice di tre elementi come argomento a ogni chiamata.  Il compilatore deve emettere ogni volta codice per allocare questa matrice.  Il compilatore infatti non è in grado di sapere se <xref:System.String.Split%2A> archivia la matrice in una posizione in cui potrebbe essere modificata da altro codice, influendo così su chiamate successive a `WriteFormattedDocComment`.  La chiamata a <xref:System.String.Split%2A> esegue anche l'allocazione di una stringa per ogni riga in `text` ed esegue l'allocazione di memoria aggiuntiva per eseguire l'operazione.  
  
 `WriteFormattedDocComment` include tre chiamate al metodo <xref:System.String.TrimStart%2A>.  Due cicli interni duplicano le operazioni e le allocazioni.  Per complicare ulteriormente la situazione, la chiamata al metodo <xref:System.String.TrimStart%2A> senza argomenti comporta l'allocazione di una matrice vuota \(per il parametro `params`\), oltre al risultato della stringa.  
  
 È infine presente una chiamata al metodo <xref:System.String.Substring%2A>, che in genere esegue l'allocazione di una nuova stringa.  
  
 **Correzione per l'esempio 3**  
  
 A differenza degli esempi precedenti, queste allocazioni non possono essere corrette da piccole modifiche.  È necessario esaminare il problema nel suo complesso e scegliere un approccio diverso.  Come si può notare, ad esempio, l'argomento per `WriteFormattedDocComment()` è una stringa che include tutte le informazioni necessarie per il metodo. Il codice può quindi eseguire più indicizzazioni invece di allocare molte stringhe parziali.  
  
 Il team responsabile delle prestazioni del compilatore ha affrontato tutte queste allocazioni con codice analogo al seguente:  
  
```csharp  
private int IndexOfFirstNonWhiteSpaceChar(string text, int start) {  
    while (start < text.Length && char.IsWhiteSpace(text[start])) start++;  
    return start;  
}  
  
private bool TrimmedStringStartsWith(string text, int start, string prefix) {  
    start = IndexOfFirstNonWhiteSpaceChar(text, start);  
    int len = text.Length - start;  
    if (len < prefix.Length) return false;  
    for (int i = 0; i < len; i++)  
    {  
        if (prefix[i] != text[start + i]) return false;  
    }  
    return true;  
}  
  
// etc...  
  
```  
  
 La prima versione di `WriteFormattedDocComment()` esegue l'allocazione di una matrice, alcune sottostringhe e una sottostringa ritagliata, insieme a una matrice di `params` vuota.  Rileva inoltre eventuali `“///”`.  Il codice rivisto usa solo l'indicizzazione e non esegue alcuna allocazione.  Rileva il primo carattere diverso da uno spazio vuoto, quindi controlla carattere per carattere per verificare se la stringa inizia con `“///”`.  Il nuovo codice usa `IndexOfFirstNonWhiteSpaceChar` invece di <xref:System.String.TrimStart%2A> per restituire il primo indice \(dopo un indice iniziale specificato\) in corrispondenza della posizione in cui si trova un carattere diverso da uno spazio vuoto.  La correzione non è completa, ma è semplice intuire come applicare correzioni simili per ottenere una soluzione completa.  Applicando questo approccio a tutto il codice sarà possibile rimuovere tutte le allocazioni in `WriteFormattedDocComment()`.  
  
 **Esempio 4: StringBuilder**  
  
 Questo esempio usa un oggetto <xref:System.Text.StringBuilder>.  La funzione seguente genera un nome completo del tipo per tipi generici:  
  
```csharp  
public class Example  
{  
    // Constructs a name like "SomeType<T1, T2, T3>"  
    public string GenerateFullTypeName(string name, int arity)  
    {  
        StringBuilder sb = new StringBuilder();  
  
        sb.Append(name);  
        if (arity != 0)  
        {  
            sb.Append("<");  
            for (int i = 1; i < arity; i++)  
            {  
                sb.Append("T"); sb.Append(i.ToString()); sb.Append(", ");  
            }  
            sb.Append("T"); sb.Append(i.ToString()); sb.Append(">");  
        }  
  
        return sb.ToString();  
    }  
}  
  
```  
  
 Occorre esaminare attentamente la riga che crea una nuova istanza di <xref:System.Text.StringBuilder>.  Il codice provoca allocazioni per `sb.ToString()` e allocazioni interne nell'implementazione di <xref:System.Text.StringBuilder>, ma non è possibile controllare queste allocazioni se si vuole ottenere il risultato della stringa.  
  
 **Correzione per l'esempio 4**  
  
 Per correggere l'allocazione dell'oggetto `StringBuilder`, memorizzare l'oggetto nella cache.  La memorizzazione nella cache anche di una singola istanza che potrebbe essere eliminata può migliorare in modo significativo le prestazioni.  Questa è la nuova implementazione della funzione, in cui si omette tutto il codice tranne le prime e le ultime righe:  
  
```csharp  
// Constructs a name like "MyType<T1, T2, T3>"  
public string GenerateFullTypeName(string name, int arity)  
{  
    StringBuilder sb = AcquireBuilder();  
    /* Use sb as before */  
    return GetStringAndReleaseBuilder(sb);  
}  
  
```  
  
 Gli elementi essenziali sono le nuove funzioni `AcquireBuilder()` e `GetStringAndReleaseBuilder()`:  
  
```csharp  
[ThreadStatic]  
private static StringBuilder cachedStringBuilder;  
  
private static StringBuilder AcquireBuilder()  
{  
    StringBuilder result = cachedStringBuilder;  
    if (result == null)  
    {  
        return new StringBuilder();  
    }  
    result.Clear();  
    cachedStringBuilder = null;  
    return result;  
}  
  
private static string GetStringAndReleaseBuilder(StringBuilder sb)  
{  
    string result = sb.ToString();  
    cachedStringBuilder = sb;  
    return result;  
}  
  
```  
  
 Poiché i nuovi compilatori usano il threading, queste implementazioni usano un campo statico a livello di thread \(attributo <xref:System.ThreadStaticAttribute>\) per la memorizzazione nella cache di <xref:System.Text.StringBuilder> ed è probabilmente possibile evitare la dichiarazione di `ThreadStatic`.  Il campo statico a livello di thread include un valore univoco per ogni thread che esegue il codice.  
  
 `AcquireBuilder()` restituisce l'istanza di <xref:System.Text.StringBuilder> memorizzata nella cache, se presente, dopo averla pulita e dopo avere impostato il campo o la cache su Null.  In caso contrario, `AcquireBuilder()` crea una nuova istanza e la restituisce, lasciando il campo o la cache impostati su Null.  
  
 Al termine delle operazioni con <xref:System.Text.StringBuilder> , è possibile chiamare `GetStringAndReleaseBuilder()` per ottenere il risultato della stringa, ad eccezione dell'istanza di <xref:System.Text.StringBuilder> nel campo o nella cache, e quindi restituire il risultato.  È possibile che il codice sia immesso di nuovo per l'esecuzione e che siano creati più oggetti <xref:System.Text.StringBuilder>, anche se ciò si verifica raramente.  Il codice salva solo l'ultima istanza rilasciata di <xref:System.Text.StringBuilder> per un uso successivo.  Questa semplice strategia per la memorizzazione nella cache riduce in modo significativo le allocazioni nei nuovi compilatori.  Parti di .NET Framework e MSBuild \([MSBuild1](../Topic/MSBuild1.md)\) usano una tecnica simile per migliorare le prestazioni.  
  
 Questa semplice strategia per la memorizzazione nella cache rispetta le indicazioni per una progettazione ottimale della cache, poiché prevede un limite per le dimensioni.  La quantità di codice, tuttavia, è superiore rispetto all'originale e ciò comporta maggiori costi di gestione.  È consigliabile adottare la strategia per la memorizzazione nella cache solo se si sono verificati problemi di prestazioni e se PerfView ha mostrato che le allocazioni di <xref:System.Text.StringBuilder> contribuiscono in modo significativo a questi problemi.  
  
### LINQ ed espressioni lambda  
 L'uso di espressioni LINQ \(Language Integrated Query\) e lambda è un ottimo esempio di uso di funzionalità produttive che potrebbe essere necessario riscrivere in seguito se l'impatto del codice sulle prestazioni risulta significativo.  
  
 **Esempio 5: Espressioni lambda, List\<T\> e IEnumerable\<T\>**  
  
 Questo esempio usa [codice di tipo LINQ e funzionale](http://blogs.msdn.com/b/charlie/archive/2007/01/26/anders-hejlsberg-on-linq-and-functional-programming.aspx) per individuare un simbolo nel modello del compilatore, a partire da una stringa nome:  
  
```csharp  
class Symbol {  
    public string Name { get; private set; }  
    /*...*/  
}  
  
class Compiler {  
    private List<Symbol> symbols;  
    public Symbol FindMatchingSymbol(string name)  
    {  
        return symbols.FirstOrDefault(s => s.Name == name);  
    }  
}  
  
```  
  
 Il nuovo compilatore e le esperienze IDE basate sul compilatore chiamano molto spesso `FindMatchingSymbol()` e questa singola riga di codice della funzione include alcune allocazioni nascoste.  Per esaminare queste allocazioni, suddividere prima di tutto la singola riga di codice della funzione in due righe:  
  
```csharp  
Func<Symbol, bool> predicate = s => s.Name == name;  
     return symbols.FirstOrDefault(predicate);  
  
```  
  
 Nella prima riga l'[espressione lambda](../Topic/Lambda%20Expressions%20\(C%23%20Programming%20Guide\).md) `s => s.Name == name` [si chiude sulla](http://blogs.msdn.com/b/ericlippert/archive/2003/09/17/53028.aspx) variabile locale `name`.  Ciò significa che, oltre ad allocare un oggetto per il [delegato](../Topic/delegate%20\(C%23%20Reference\).md) incluso in `predicate`, il codice esegue l'allocazione di una classe statica in cui includere l'ambiente che acquisisce il valore di `name`.  Il compilatore genera codice analogo al seguente:  
  
```csharp  
// Compiler-generated class to hold environment state for lambda  
private class Lambda1Environment  
{  
    public string capturedName;  
    public bool Evaluate(Symbol s)  
    {  
        return s.Name == this.capturedName;  
    }  
}  
  
// Expanded Func<Symbol, bool> predicate = s => s.Name == name;  
Lambda1Environment l = new Lambda1Environment() { capturedName = name };  
var predicate = new Func<Symbol, bool>(l.Evaluate);  
  
```  
  
 Le due allocazioni di `new`, una per la classe di ambiente e una per il delegato, sono ora esplicite.  
  
 Esaminare ora la chiamata a `FirstOrDefault`.  Anche questo metodo di estensione nel tipo <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> comporta un'allocazione.  Poiché `FirstOrDefault` accetta un oggetto <xref:System.Collections.Generic.IEnumerable%601> come primo argomento, è possibile espandere la chiamata al codice seguente \(semplificato leggermente per questo esempio\):  
  
```csharp  
// Expanded return symbols.FirstOrDefault(predicate) ...  
     IEnumerable<Symbol> enumerable = symbols;  
     IEnumerator<Symbol> enumerator = enumerable.GetEnumerator();  
     while(enumerator.MoveNext())  
     {  
         if (predicate(enumerator.Current))  
             return enumerator.Current;  
     }  
     return default(Symbol);  
  
```  
  
 Il tipo della variabile `symbols` è <xref:System.Collections.Generic.List%601>.  Il tipo della raccolta <xref:System.Collections.Generic.List%601> implementa <xref:System.Collections.Generic.IEnumerable%601> e definisce in modo intelligente un enumeratore \(interfaccia <xref:System.Collections.Generic.IEnumerator%601>\) implementato da <xref:System.Collections.Generic.List%601> con un `struct`.  L'uso di una struttura invece di una classe significa che in genere si evitano allocazioni heap e ciò può influire sulle prestazioni delle operazioni di Garbage Collection.  Gli enumeratori sono in genere usati con il ciclo `foreach` del linguaggio, che usa la struttura dell'enumeratore restituita allo stack di chiamate.  L'incremento del puntatore dello stack di chiamate per un oggetto non influisce sulle operazioni di Garbage Collection in modo analogo all'allocazione heap.  
  
 Nel caso della chiamata `FirstOrDefault` espansa, il codice deve chiamare `GetEnumerator()` su un oggetto <xref:System.Collections.Generic.IEnumerable%601>.  L'assegnazione di `symbols` alla variabile `enumerable` di tipo `IEnumerable<Symbol>` comporta la perdita dell'informazione che indica che l'oggetto effettivo è un <xref:System.Collections.Generic.List%601>.  Ciò significa che quando il codice recupera l'enumeratore con `enumerable.GetEnumerator()`, .NET Framework deve eseguire la conversione boxing della struttura restituita per assegnarla alla variabile `enumerator`.  
  
 **Correzione per l'esempio 5**  
  
 La correzione consiste nel riscrivere `FindMatchingSymbol` come indicato di seguito, sostituendo la singola riga di codice corrispondente con sei righe di codice che risultano comunque concise, facili da leggere, comprendere e gestire:  
  
```csharp  
public Symbol FindMatchingSymbol(string name)  
    {  
        foreach (Symbol s in symbols)  
        {  
            if (s.Name == name)  
                return s;  
        }  
        return null;  
    }  
  
```  
  
 Il codice non usa metodi di estensione LINQ, espressioni lambda o enumeratori e non comporta allocazioni.  L'assenza di allocazioni è dovuta al fatto che il compilatore è in grado di verificare che la raccolta `symbols` e un <xref:System.Collections.Generic.List%601> e può associare l'enumeratore esistente \(una struttura\) a una variabile locale con il tipo corretto per evitare la conversione boxing.  La versione originale di questa funzione è un esempio ottimale delle capacità espressive di C\# e della produttività di .NET Framework.  La nuova versione, più efficiente, mantiene queste qualità senza aggiungere codice complesso da gestire.  
  
### Memorizzazione del metodo async nella cache  
 L'esempio seguente mostra un problema comune che si verifica quando si tenta di usare i risultati memorizzati nella cache in un metodo [async](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  
  
 **Esempio 6: Memorizzazione di metodi async nella cache**  
  
 Le funzionalità IDE di Visual Studio basate sui nuovi compilatori C\# e Visual Basic recuperano spesso alberi della sintassi e i compilatori usano il metodo async durante il recupero per mantenere la reattività di Visual Studio.  Ecco la prima versione del codice che si potrebbe scrivere per ottenere un albero della sintassi:  
  
```csharp  
class SyntaxTree { /*...*/ }  
  
class Parser { /*...*/  
    public SyntaxTree Syntax { get; }  
    public Task ParseSourceCode() { /*...*/ }  
}  
  
class Compilation { /*...*/  
    public async Task<SyntaxTree> GetSyntaxTreeAsync()  
    {  
        var parser = new Parser(); // allocation  
        await parser.ParseSourceCode(); // expensive  
        return parser.Syntax;  
    }  
}  
  
```  
  
 Come si può notare, la chiamata a `GetSyntaxTreeAsync()` crea un'istanza di `Parser`, analizza il codice e quindi restituisce un oggetto <xref:System.Threading.Tasks.Task>, `Task<SyntaxTree>`.  La parte dispendiosa consiste nell'allocazione dell'istanza di `Parser` e nell'analisi del codice.  Questa funzione restituisce un <xref:System.Threading.Tasks.Task>, in modo che i chiamanti possano attendere il completamento del processo di analisi e liberare il thread dell'interfaccia utente in modo che possa rispondere all'input utente.  
  
 È possibile che alcune funzionalità di Visual Studio tentino di ottenere lo stesso albero della sintassi. La scrittura del codice seguente permette quindi di memorizzare nella cache il risultato dell'analisi, per risparmiare tempo e allocazioni.  Questo codice comporta tuttavia un'allocazione:  
  
```csharp  
class Compilation { /*...*/  
  
    private SyntaxTree cachedResult;  
  
    public async Task<SyntaxTree> GetSyntaxTreeAsync()  
    {  
        if (this.cachedResult == null)  
        {  
            var parser = new Parser(); // allocation  
            await parser.ParseSourceCode(); // expensive  
            this.cachedResult = parser.Syntax;  
        }  
        return this.cachedResult;  
    }  
}  
  
```  
  
 Il nuovo codice con memorizzazione nella cache include un campo `SyntaxTree` con nome `cachedResult`.  Quando questo campo è Null, `GetSyntaxTreeAsync()` esegue le operazioni e salva il risultato nella cache.  `GetSyntaxTreeAsync()` restituisce l'oggetto `SyntaxTree`.  Se però è disponibile una funzione di tipo `async` `Task<SyntaxTree>` e si restituisce un valore di tipo `SyntaxTree`, il compilatore emette codice per allocare un oggetto Task in cui includere il risultato, usando `Task<SyntaxTree>.FromResult()`.  L'oggetto Task è contrassegnato come completato e il risultato è immediatamente disponibile.  Nel codice per i nuovi compilatori gli oggetti <xref:System.Threading.Tasks.Task> già completati erano così frequenti che la correzione di queste allocazioni ha permesso un notevole miglioramento della reattività.  
  
 **Correzione per l'esempio 6**  
  
 Per rimuovere l'allocazione <xref:System.Threading.Tasks.Task> completata, è possibile memorizzare nella cache l'oggetto Task con il risultato completato:  
  
```csharp  
class Compilation { /*...*/  
  
    private Task<SyntaxTree> cachedResult;  
  
    public Task<SyntaxTree> GetSyntaxTreeAsync()  
    {  
        return this.cachedResult ??   
               (this.cachedResult = GetSyntaxTreeUncachedAsync());  
    }  
  
    private async Task<SyntaxTree> GetSyntaxTreeUncachedAsync()  
    {  
        var parser = new Parser(); // allocation  
        await parser.ParseSourceCode(); // expensive  
        return parser.Syntax;  
    }  
}  
  
```  
  
 Questo codice modifica il tipo di `cachedResult` in `Task<SyntaxTree>` e usa una funzione `async` dell'helper che include il codice originale da `GetSyntaxTreeAsync()`.  `GetSyntaxTreeAsync()` usa ora l'[operatore Null\-coalescing](../Topic/??%20Operator%20\(C%23%20Reference\).md) per restituire `cachedResult` nel caso in cui sia Null.  Se `cachedResult` è Null, `GetSyntaxTreeAsync()` chiama `GetSyntaxTreeUncachedAsync()` e memorizza il risultato nella cache.  Si noti che `GetSyntaxTreeAsync()` non attende la chiamata a `GetSyntaxTreeUncachedAsync()`, come farebbe normalmente il codice.  Se non si attende, quando `GetSyntaxTreeUncachedAsync()` restituisce l'oggetto <xref:System.Threading.Tasks.Task> corrispondente, `GetSyntaxTreeAsync()` restituisce immediatamente l'oggetto <xref:System.Threading.Tasks.Task>.  Il risultato memorizzato nella cache è ora un oggetto <xref:System.Threading.Tasks.Task> e non sono quindi presenti allocazioni per la restituzione del risultato memorizzato nella cache.  
  
### Considerazioni aggiuntive  
 Di seguito sono riportate altre considerazioni sui potenziali problemi relativi ad app di grandi dimensioni o app che elaborano quantità elevate di dati.  
  
 **Dizionari**  
  
 I dizionari sono usati ampliamente in molti programmi e, benché siano molto comodi e intrinsecamente efficienti,  sono tuttavia usati spesso in modo non appropriato.  L'analisi eseguita in Visual Studio e nei nuovi compilatori mostra che molti dizionari includono un solo elemento o sono vuoti.  Un <xref:System.Collections.Generic.Dictionary%602> vuoto include dieci campi e occupa 48 byte sull'heap in una macchina x86.  I dizionari sono molto utili se si necessita di una struttura di dati di mapping o associativa con ricerca continua.  Se sono presenti solo pochi elementi, tuttavia, l'uso del dizionario comporta lo spreco di una grande quantità di spazio.  In alternativa, è ad esempio possibile eseguire in modo iterativo una ricerca in un oggetto `List<KeyValuePair\<K,V>>`, con velocità analoga.  Se si usa un dizionario solo per il caricamento di dati e la lettura dei dati, uno schema molto comune, l'uso di una matrice ordinata con una ricerca di tipo N\(log\(N\)\) potrebbe offrire velocità analoghe, in base al numero di elementi usati.  
  
 **Confronto tra classi e  strutture**  
  
 In un certo senso, le classi e le strutture comportano un compromesso classico tra spazio e tempo per l'ottimizzazione delle app.  Le classi comportano 12 byte di sovraccarico in una macchina x86, anche se non includono campi, ma il passaggio di classi è poco dispendioso, poiché per fare riferimento a un'istanza di classe è necessario solo un puntatore.  Le strutture non comportano allocazioni heap se non sono sottoposte a conversione boxing, ma quando si passano strutture di grandi dimensioni come argomenti di funzione o valori restituiti, la copia atomica di tutti i membri di dati delle strutture richiede tempo della CPU.  Occorre prestare attenzione alle chiamate ripetute alle proprietà che restituiscono strutture e memorizzare nella cache il valore della proprietà in una variabile locale per evitare la copia eccessiva di dati.  
  
 **Cache**  
  
 Una soluzione comune per ottimizzare le prestazioni consiste nel memorizzare i risultati nella cache.  Una cache senza limiti di dimensione o senza criteri di eliminazione può tuttavia provocare perdita di memoria.  Quando si elaborano quantità elevate di dati, se le cache trattengono una quantità elevata di memoria, è possibile che le operazioni di Garbage Collection annullino i vantaggi delle ricerche memorizzate nella cache.  
  
 In questo articolo è stato illustrato come individuare i sintomi relativi a colli di bottiglia delle prestazioni che possono influire sulla reattività dell'app, in particolare per sistemi di grandi dimensioni o sistemi che elaborano quantità elevate di dati.  Le cause più comuni includono la conversione boxing, le modifiche alle stringhe, le espressioni LINQ e lambda, la memorizzazione di metodi async nella cache, la memorizzazione nella cache senza limiti di dimensione o criteri di eliminazione, l'uso non appropriato di dizionari e il passaggio di strutture.  Occorre tenere presenti le quattro considerazioni per l'ottimizzazione delle app:  
  
-   Non eseguire prematuramente l'ottimizzazione: è consigliabile essere produttivi e ottimizzare l'app quando si individuano problemi.  
  
-   I profili sono attendibili: solo le misurazioni assicurano la precisione.  
  
-   La qualità degli strumenti è essenziale: scaricare PerfView e provare a usarlo.  
  
-   Le allocazioni sono importantissime: il team responsabile della piattaforma del compilatore si è impegnato principalmente nel migliorare le prestazioni dei nuovi compilatori da questo punto di vista.  
  
## Vedere anche  
 [Video di presentazione di questo argomento](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B333)   
 [Guida per principianti alla profilatura delle prestazioni](../Topic/Beginners%20Guide%20to%20Performance%20Profiling.md)   
 [Performance](../../../docs/framework/performance/index.md)   
 [Suggerimenti relativi alle prestazioni di .NET](http://msdn.microsoft.com/library/ms973839.aspx)   
 [Windows Phone Performance Analysis Tool](http://msdn.microsoft.com/magazine/hh781024.aspx)   
 [Individuazione dei colli di bottiglia delle applicazioni con Visual Studio Profiler](http://msdn.microsoft.com/magazine/cc337887.aspx)   
 [Esercitazioni relative a PerfView su Channel 9](http://channel9.msdn.com/Series/PerfView-Tutorial)   
 [Suggerimenti avanzati sulle prestazioni](http://curah.microsoft.com/4604/improving-your-net-apps-startup-performance)   
 [Progetto open source .NET Compiler Platform \("Roslyn"\)](http://roslyn.codeplex.com/)