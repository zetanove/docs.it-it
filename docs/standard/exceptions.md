---
title: Gestione e generazione di eccezioni in .NET
description: Informazioni sull&quot;uso delle eccezioni in .NET
keywords: .NET, .NET Core
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bf116df6-0042-46bf-be13-b69864816210
translationtype: Human Translation
ms.sourcegitcommit: 9584699ad7e745ae3cb059b1bb8327301c9a3286
ms.openlocfilehash: 5271b63a47aa2fcc81cd9c8b1ffd22e618829412

---

# <a name="handling-and-throwing-exceptions-in-net"></a>Gestione e generazione di eccezioni in .NET

Le applicazioni devono essere in grado di gestire in modo coerente gli errori che si verificano durante l'esecuzione. .NET offre un modello coerente per l'invio alle applicazioni di notifiche relative agli errori: le operazioni di .NET indicano l'errore generando eccezioni.

## <a name="exceptions"></a>Eccezioni

Un'eccezione è una condizione di errore o un comportamento imprevisto riscontrato da un programma in esecuzione. Le eccezioni possono essere generate in caso di errori nel codice dell'applicazione o nel codice chiamato (ad esempio una libreria condivisa), in caso di risorse del sistema operativo non disponibili, di condizioni impreviste riscontrate dal runtime (ad esempio codice impossibile da verificare) e così via. L'applicazione è in grado di gestire alcune di queste condizioni, altre no. Sebbene sia possibile gestire gran parte delle eccezioni dell'applicazione, la maggior parte delle eccezioni di runtime risulta ingestibile.

In .NET un'eccezione è un oggetto che eredita dalla classe [System.Exception](xref:System.Exception). Le eccezioni vengono generate dalle aree di codice in cui si è verificato un problema. Ogni eccezione viene passata ai livelli superiori dello stack finché non viene gestita dall'applicazione o non si arresta il programma.

## <a name="exceptions-vs-traditional-errorhandling-methods"></a>Eccezioni e metodi tradizionali di gestione degli errori

In precedenza, il modello di gestione degli errori di un linguaggio si basava sul metodo specifico usato da tale linguaggio per rilevare gli errori e individuarne i gestori oppure sul meccanismo di gestione degli errori fornito dal sistema operativo. La modalità di gestione delle eccezioni di .NET offre i vantaggi seguenti:

- La generazione e la gestione delle eccezioni ha lo stesso funzionamento nei linguaggi di programmazione .NET.

- Senza la necessità di una sintassi di linguaggio apposita, ma con la possibilità per ciascun linguaggio di definire la propria sintassi.

- È possibile generare eccezioni anche a livello di più processi e addirittura di più computer differenti.

- È possibile aggiungere codice per la gestione delle eccezioni a un'applicazione per aumentare l'affidabilità dei programmi.

Le eccezioni presentano vantaggi rispetto ad altri metodi di notifica degli errori, quali i codici restituiti. Gli errori vengono sempre rilevati poiché se viene generata un'eccezione e l'eccezione non viene gestita, il runtime termina l'applicazione. I valori non validi non continuano a propagarsi nel sistema quando il codice non riesce a verificare la presenza di un codice di errore restituito. 

## <a name="exception-class-and-properties"></a>Classe e proprietà dell'eccezione

La classe @System.Exception è la classe di base da cui vengono ereditate le eccezioni. Ad esempio, la gerarchia della classe @System.InvalidCastException è illustrata di seguito:

```
Object
  Exception
    SystemException
       InvalidCastException
```

La classe @System.Exception include le proprietà seguenti che facilitano la comprensione di un'eccezione.

| Nome proprietà | Descrizione |
| ------------- | ----------- |
| @System.Exception.Data | @System.Collections.IDictionary contenente dati arbitrari in coppie chiave-valore. |
| @System.Exception.HelpLink | Può contenere un URL (o URN) di un file della Guida che offre informazioni dettagliate sulla causa di un'eccezione. |
| @System.Exception.InnerException | Questa proprietà può essere usata per creare e mantenere una serie di eccezioni durante la gestione delle eccezioni. È possibile usarla per creare una nuova eccezione contenente le eccezioni rilevate in precedenza. L'eccezione originale può essere acquisita dalla seconda eccezione nella proprietà @System.Exception.InnerException, consentendo al codice che gestisce la seconda eccezione di esaminare le informazioni aggiuntive. Ad esempio, si supponga di avere un metodo che riceve un argomento non formattato correttamente.  Il codice tenta di leggere l'argomento, ma viene generata un'eccezione. Il metodo rileva l'eccezione e genera un'eccezione @System.FormatException. Per migliorare la capacità del chiamante di determinare il motivo per il quale viene generata un'eccezione, è a volte utile che un metodo rilevi un'eccezione generata da una routine di supporto e quindi generi un'eccezione più indicativa dell'errore che si è verificato. Sarà possibile creare un'eccezione nuova e più significativa in cui il riferimento all'eccezione interna può essere impostato sull'eccezione originale. Questa eccezione più significativa può quindi essere inviata al chiamante. Si noti che con questa funzionalità è possibile creare una serie di eccezioni collegate che termina con l'eccezione che è stata generata per prima. |
| @System.Exception.Message | Offre informazioni dettagliate sulla causa di un'eccezione.
| @System.Exception.Source | Ottiene o imposta il nome dell'oggetto o dell'applicazione che ha generato l'errore. |
| @System.Exception.StackTrace | Contiene un'analisi dello stack che può essere usata per determinare dove si è verificato un errore. L'analisi dello stack include il nome del file di origine e il numero di riga del programma, se sono disponibili informazioni di debug. |

La maggior parte delle classi che ereditano da @System.Exception non implementa membri aggiuntivi, né offre funzionalità aggiuntive, ma si limita a ereditare da @System.Exception. Per questa ragione, le informazioni più importanti per un'eccezione si trovano nella gerarchia delle classi delle eccezioni, nel nome dell'eccezione e nelle informazioni contenute nell'eccezione.

Si consiglia di generare e rilevare solo oggetti che derivano da @System.Exception,, ma è possibile generare qualsiasi oggetto che deriva dalla classe @System.Object come eccezione. Si noti che non tutti i linguaggi supportano la generazione e il rilevamento degli oggetti che non derivano da @System.Exception.

## <a name="common-exceptions"></a>Eccezioni comuni

Nella tabella seguente sono elencate alcune eccezioni comuni con esempi di possibili cause.

| Tipo di eccezione | Tipo base | Descrizione | Esempio |
| -------------- | --------- | ----------- | ------- |
| @System.Exception | @System.Object | Classe base per tutte le eccezioni. | Nessuno (usare una classe derivata di questa eccezione). |
| @System.IndexOutOfRangeException | @System.Exception | Generata dal runtime solo quando una matrice viene indicizzata in modo non corretto. | Indicizzazione di una matrice esternamente al relativo intervallo valido: `arr[arr.Length+1]` |
| @System.NullReferenceException | @System.Exception | Generata dal runtime solo quando viene fatto riferimento a un oggetto Null. | `object o = null; o.ToString();` |
| @System.InvalidOperationException | @System.Exception | Generata dai metodi con uno stato non valido. | Chiamata di `Enumerator.GetNext()` dopo la rimozione di un elemento dalla raccolta sottostante. |
| @System.ArgumentException | @System.Exception | Classe base per tutte le eccezioni di argomento. | Nessuno (usare una classe derivata di questa eccezione). |
| @System.ArgumentNullException | @System.Exception | Generata dai metodi che non consentono un argomento Null. | `String s = null; "Calculate".IndexOf (s);` |
| @System.ArgumentOutOfRangeException | @System.Exception | Generata dai metodi che verificano se gli argomenti sono compresi in un determinato intervallo. | `String s = "string"; s.Substring(s.Length+1);` |

## <a name="how-to-use-the-trycatch-block-to-catch-exceptions"></a>Come usare il blocco try/catch per rilevare le eccezioni

Inserire le sezioni di codice che potrebbero generare eccezioni in un blocco `try` e il codice che gestisce le eccezioni in un blocco `catch`. Il blocco `catch` è una serie di istruzioni che iniziano con la parola chiave `catch`, seguita da un tipo di eccezione e un'azione da eseguire.

L'esempio di codice seguente usa un blocco `try`/`catch` per rilevare una possibile eccezione. Il metodo `Main` contiene un blocco `try` con un'istruzione @System.IO.StreamReader che apre un file di dati denominato `data.txt` e scrive una stringa del file. Il blocco `try` è seguito da un blocco `catch` che rileva qualsiasi eccezione del blocco `try`.

C#
```
using System;
using System.IO;

public class ProcessFile
{
    public static void Main()
    {
        try
        {
            StreamReader sr = File.OpenText("data.txt");
            Console.WriteLine("The first line of this file is {0}", sr.ReadLine());
            sr.Dispose();
        }
        catch (Exception e)
        {
            Console.WriteLine("An error occurred: '{0}'", e);
        }
    }
}
```

Common Language Runtime rileva le eccezioni non rilevate da un blocco catch. A seconda della configurazione del runtime, viene visualizzata una finestra di dialogo di debug, viene interrotta l'esecuzione del programma e viene visualizzata una finestra di dialogo con le informazioni sull'eccezione o viene stampato un errore in STDERR.

> [!NOTE] 
> Quasi tutte le righe di codice possono causare un'eccezione, in particolare le eccezioni che vengono generate direttamente da Common Language Runtime, come @System.OutOfMemoryException. Sebbene nella maggior parte delle applicazioni non sia necessario gestire queste eccezioni, considerare questa eventualità quando si creano librerie che devono essere usate da altri utenti. Per suggerimenti su quando impostare il codice di un blocco Try, vedere [Procedure consigliate per le eccezioni](#best-practices-for-exceptions).
 
## <a name="how-to-use-specific-exceptions-in-a-catch-block"></a>Come usare eccezioni specifiche in un blocco Catch

L'esempio di codice precedente illustra un'istruzione `catch` di base che rileva qualsiasi eccezione. In generale, tuttavia, è buona norma rilevare un tipo di eccezione specifico anziché usare un'istruzione `catch` di base.

Quando si verifica un'eccezione, l'eccezione viene passata nello stack e a ogni blocco catch viene data la possibilità di gestirla. L'ordine delle istruzioni catch è importante. Inserire i blocchi catch per il rilevamento di eccezioni specifiche prima di un blocco catch generale per il rilevamento delle eccezioni per evitare che il compilatore generi un errore. Il blocco catch appropriato viene determinato tramite la corrispondenza del tipo di eccezione al nome dell'eccezione specificato nel blocco catch. Se non è presente alcun blocco catch specifico, l'eccezione viene rilevata da un blocco catch generale, se disponibile.

Nel codice seguente viene usato un blocco `try`/`catch` per rilevare un'eccezione @System.InvalidCastException. L'esempio crea una classe denominata `Employee` con un'unica proprietà, il livello del dipendente (`Emlevel`). Il metodo `PromoteEmployee` accetta un oggetto e incrementa il livello del dipendente. Un'eccezione @System.InvalidCastException si verifica quando viene passata un'istanza di @System.DateTime al metodo `PromoteEmployee`.

C#
```
using System;

public class Employee
{
    //Create employee level property.
    public int Emlevel
    {
        get
        {
            return(emlevel);
        }
        set
        {
            emlevel = value;
        }
    }

    private int emlevel = 0;
}

public class Ex13
{
    public static void PromoteEmployee(Object emp)
    {
        //Cast object to Employee.
        Employee e = (Employee) emp;
        // Increment employee level.
        e.Emlevel = e.Emlevel + 1;
    }

    public static void Main()
    {
        try
        {
            Object o = new Employee();
            DateTime newyears = new DateTime(2001, 1, 1);
            //Promote the new employee.
            PromoteEmployee(o);
            //Promote DateTime; results in InvalidCastException as newyears is not an employee instance.
            PromoteEmployee(newyears);
        }
        catch (InvalidCastException e)
        {
            Console.WriteLine("Error passing data to PromoteEmployee method. " + e.Message);
        }
    }
}
```

## <a name="how-to-use-finally-blocks"></a>Come usare i blocchi finally

Quando si verifica un'eccezione, l'esecuzione viene arrestata e il controllo viene assegnato al gestore di eccezioni appropriato. Spesso questo significa che le righe di codice che si prevede di eseguire vengono ignorate. La pulizia di alcune risorse, ad esempio la chiusura di un file, deve essere eseguita anche se viene generata un'eccezione. A tale scopo è possibile usare un blocco `finally`. Un blocco `finally` viene sempre eseguito, indipendentemente dalla generazione di un'eccezione.

Nell'esempio di codice seguente viene usato un blocco `try`/`catch` per rilevare un'eccezione @System.ArgumentOutOfRangeException. Il metodo `Main` crea due matrici e prova a copiarle una sull'altra. L'azione genera un'eccezione @System.ArgumentOutOfRangeException e l'errore viene scritto nella console. Il blocco `finally` viene eseguito indipendentemente dal risultato dell'azione di copia.

C#
```
using System;

class ArgumentOutOfRangeExample
{
    public static void Main()
    {
        int[] array1 = {0, 0};
        int[] array2 = {0, 0};

        try
        {
            Array.Copy(array1, array2, -1);
        }
        catch (ArgumentOutOfRangeException e)
        {
            Console.WriteLine("Error: {0}", e);
        }
        finally
        {
            Console.WriteLine("This statement is always executed.");
        }
    }
}
```

## <a name="how-to-explicitly-throw-exceptions"></a>Come generare in modo esplicito le eccezioni

È possibile generare in modo esplicito un'eccezione usando l'istruzione `throw`. È anche possibile generare di nuovo un'eccezione rilevata usando l'istruzione `throw`. Si consiglia di aggiungere informazioni a un'eccezione generata di nuovo per offrire ulteriori informazioni durante il debug.

Nell'esempio di codice seguente viene usato un blocco `try`/`catch` per rilevare una possibile eccezione @System.IO.FileNotFoundException. Il blocco `try` è seguito da un blocco `catch` che rileva l'eccezione @System.IO.FileNotFoundException e scrive un messaggio nella console se il file di dati non viene trovato. L'istruzione successiva è l'istruzione `throw` che genera una nuova eccezione @System.IO.FileNotFoundException e aggiunge informazioni di testo all'eccezione.

C#
```
using System;
using System.IO;

public class ProcessFile
{
   public static void Main()
      {
      FileStream fs = null;
      try   
      {
         //Opens a text tile.
         fs = new FileStream(@"C:\temp\data.txt", FileMode.Open);
         StreamReader sr = new StreamReader(fs);
         string line;

         //A value is read from the file and output to the console.
         line = sr.ReadLine();
         Console.WriteLine(line);
      }
      catch(FileNotFoundException e)
      {
         Console.WriteLine("[Data File Missing] {0}", e);
         throw new FileNotFoundException(@"[data.txt not in c:\temp directory]",e);
      }
      finally
      {
         if (fs != null)
            fs.Dispose();
      }
   }
}
```

## <a name="how-to-create-userdefined-exceptions"></a>Come creare eccezioni definite dall'utente

.NET fornisce una gerarchia di classi di eccezione derivate in ultima istanza dalla classe di base @System.Exception. Se però nessuna delle eccezioni predefinite soddisfa le proprie esigenze, è possibile creare classi di eccezione personalizzate derivandole dalla classe @System.Exception.

Quando si creano eccezioni personalizzate, terminare il nome della classe dell'eccezione definita dall'utente con la parola "Exception" e implementare i tre costruttori comuni, come illustrato nell'esempio seguente. L'esempio definisce una nuova classe di eccezione denominata `EmployeeListNotFoundException`. La classe è derivata da @System.Exception e include tre costruttori.

C#
```
using System;

public class EmployeeListNotFoundException: Exception
{
    public EmployeeListNotFoundException()
    {
    }

    public EmployeeListNotFoundException(string message)
        : base(message)
    {
    }

    public EmployeeListNotFoundException(string message, Exception inner)
        : base(message, inner)
    {
    }
}
```

> [!NOTE]
> Nei casi in cui viene usata la comunicazione remota, è necessario assicurarsi che i metadati di tutte le eccezioni definite dall'utente siano disponibili nel server chiamato e nel client (oggetto proxy o chiamante). Per altre informazioni, vedere [Procedure consigliate per le eccezioni](#best-practices-for-exceptions).

## <a name="best-practices-for-exceptions"></a>Procedure consigliate per le eccezioni

Un'applicazione progettata correttamente gestisce eccezioni ed errori per impedire arresti anomali dell'applicazione. Questa sezione descrive le procedure consigliate per la gestione e la creazione di eccezioni.

### <a name="use-trycatchfinally-blocks"></a>Usare blocchi try/catch/finally

Usare blocchi `try`/`catch`/`finally` nel codice che può potenzialmente generare un'eccezione. 

Ordinare sempre le eccezioni in blocchi `catch` dalla più specifica alla meno specifica.

Usare un blocco `finally` per pulire le risorse, indipendentemente dalla possibilità di ripristino.

### <a name="handle-common-conditions-without-throwing-exceptions"></a>Gestire le condizioni comuni senza generare eccezioni

È consigliabile gestire le condizioni che potrebbero verificarsi ma potrebbero generare un'eccezione in modo da evitare l'eccezione. Ad esempio, se si tenta di chiudere una connessione già chiusa, si otterrà `InvalidOperationException`. Per impedire che ciò accada, usare un'istruzione `if` per verificare lo stato della connessione prima di tentare di chiuderla.

C#
```
if (conn.State != ConnectionState.Closed)
{
    conn.Close();
}
```

Se prima della chiusura non viene verificato lo stato della connessione, è possibile rilevare l'eccezione `InvalidOperationException`.

C#
```
try
{
    conn.Close();
}
catch (InvalidOperationException ex)
{
    Console.WriteLine(ex.GetType().FullName);
    Console.WriteLine(ex.Message);
}
```

Nella scelta del metodo è necessario considerare la frequenza con cui si prevede che l'evento possa verificarsi.

- Usare la gestione delle eccezioni se l'evento non si verifica molto spesso, ovvero, se l'evento è davvero eccezionale e indica un errore quale la fine imprevista di un file. Quando si utilizza la gestione delle eccezioni, una minore quantità di codice viene eseguita in condizioni normali.

- Ricercare le condizioni di errore nel codice se l'evento si verifica ripetutamente e può essere considerato parte dell'esecuzione normale. Quando si ricercano le condizioni di errore comuni, viene eseguita una minore quantità di codice poiché vengono evitate le eccezioni.

### <a name="design-classes-so-that-exceptions-can-be-avoided"></a>Progettare le classi in modo da evitare le eccezioni

Una classe può offrire metodi o proprietà che consentono di evitare di effettuare una chiamata che potrebbe generare un'eccezione. Con la classe @System.IO.FileStream, ad esempio, sono disponibili metodi che consentono di determinare se è stata raggiunta la fine del file. I metodi possono essere usati per evitare l'eccezione che verrebbe generata se si continua la lettura oltre la fine del file. L'esempio seguente illustra come continuare la lettura fino alla fine di un file senza generare un'eccezione.

C#
```
class FileRead
{
    public void ReadAll(FileStream fileToRead)
    {
        // This if statement is optional
        // as it is very unlikely that
        // the stream would ever be null.
        if (fileToRead == null)
        {
            throw new System.ArgumentNullException();
        }

        int b;

        // Set the stream position to the beginning of the file.
        fileToRead.Seek(0, SeekOrigin.Begin);

        // Read each byte to the end of the file.
        for (int i = 0; i < fileToRead.Length; i++)
        {
            b = fileToRead.ReadByte();
            Console.Write(b.ToString());
            // Or do something else with the byte.
        }
    }
}
```

Un altro metodo per evitare le eccezioni consiste nel restituire il valore Null per i casi di errore estremamente comuni anziché generare un'eccezione. Un caso di errore estremamente comune può essere considerato come un normale flusso di controllo. Restituendo Null in questi casi, si riduce l'impatto sulle prestazioni di un'applicazione.

### <a name="throw-exceptions-instead-of-returning-an-error-code"></a>Generare eccezioni anziché restituire un codice di errore

Le eccezioni garantiscono il rilevamento degli errori quando il codice chiamante non rileva un codice restituito. 

### <a name="use-the-predefined-net-exception-types"></a>Usare i tipi di eccezione .NET predefiniti

Introdurre una nuova classe di eccezioni solo quando non è possibile applicare una classe predefinita. Ad esempio:

- Generare un'eccezione @System.InvalidOperationException se un set di proprietà o una chiamata al metodo non è adatta allo stato corrente dell'oggetto.

- Generare un'eccezione @System.ArgumentException una delle classi predefinite che derivano da @System.ArgumentException se vengono passati parametri non validi.

### <a name="end-exception-class-names-with-the-word-exception"></a>Terminare i nomi delle classi di eccezioni con la parola `Exception`

Quando è necessaria un'eccezione personalizzata, assegnare un nome appropriato all'eccezione e derivarla dalla classe @System.Exception. Ad esempio:

C#
```
public class MyFileNotFoundException : Exception
{
}
```

### <a name="include-three-constructors-in-custom-exception-classes"></a>Inserire tre costruttori nelle classi di eccezioni personalizzate

Usare almeno i tre costruttori comuni quando si creano classi di eccezione personalizzate: il costruttore predefinito, un costruttore che accetta un messaggio stringa e un costruttore che accetta un messaggio stringa e un'eccezione interna.

- @System.Exception.%23ctor,, che usa valori predefiniti.

- @System.Exception.%23ctor(System.String),, che accetta un messaggio stringa.

- @System.Exception.%23ctor(System.String,System.Exception),, che accetta un messaggio stringa e un'eccezione interna.

Per un esempio, vedere [Procedura: Creare eccezioni definite dall'utente](#how-to-create-user-defined-exceptions).

### <a name="ensure-that-exception-data-is-available-when-code-executes-remotely"></a>Garantire la disponibilità dei dati dell'eccezione per il codice eseguito in modalità remota

Quando si creano eccezioni definite dall'utente, garantire che i metadati relativi alle eccezioni siano disponibili per il codice eseguito in modalità remota. 

Ad esempio, nei runtime .NET che implementano domini app, è possibile che si verifichino eccezioni nei domini app. Si supponga che il dominio app A crei il dominio app B che esegue codice che genera un'eccezione. Per rilevare e gestire correttamente l'eccezione è necessario che il dominio app A sia in grado di individuare l'assembly contenente l'eccezione generata dal dominio app B. Se il dominio app B genera un'eccezione contenuta in un assembly nella relativa base dell'applicazione ma non nella base dell'applicazione del dominio app A, il dominio app A non sarà in grado di individuare l'eccezione e Common Language Runtime genererà un'eccezione @System.IO.FileNotFoundException. Per evitare che questo si verifichi è possibile distribuire l'assembly contenente le informazioni sull'eccezione in due modi:

- Inserendo l'assembly in una base applicativa comune condivisa da entrambi i domini applicazione

    \- oppure -

- Se i domini non condividono alcuna base applicativa comune, firmando l'assembly contenente le informazioni sull'eccezione con un nome sicuro e distribuendo tale assembly nella Global Assembly Cache.

### <a name="include-a-localized-description-string-in-every-exception"></a>Includere in ciascuna eccezione una stringa descrittiva localizzata

Il messaggio di errore visualizzato all'utente è derivato dalla stringa descrittiva dell'eccezione generata, anziché dal nome della classe di eccezione.

### <a name="use-grammatically-correct-error-messages"></a>Usare messaggi di errore grammaticalmente corretti

Scrivere frasi chiare e includere la punteggiatura finale. È necessario che ogni frase della stringa descrittiva di un'eccezione termini con un punto. Ad esempio, "Overflow della tabella del log." è una stringa descrittiva corretta.

### <a name="in-custom-exceptions-provide-additional-properties-as-needed"></a>Nelle eccezioni personalizzate specificare le proprietà aggiuntive necessarie

Fornire le proprietà aggiuntive di un'eccezione (oltre alla stringa descrittiva) solo nel caso di uno scenario a livello di codice in cui è utile disporre di altre informazioni. Ad esempio, @System.IO.FileNotFoundException fornisce la proprietà @System.IO.FileNotFoundException.FileName.

### <a name="place-throw-statements-so-that-the-stack-trace-will-be-helpful"></a>Inserire istruzioni throw in modo che l'analisi dello stack risulti utile

La traccia dello stack inizia in corrispondenza dell'istruzione in cui l'eccezione viene generata e termina in corrispondenza dell'istruzione `catch` che intercetta l'eccezione.

### <a name="use-exception-builder-methods"></a>Usare metodi per la creazione di eccezioni

Una classe genera spesso la stessa eccezione da punti diversi dell'implementazione. Per evitare codice di dimensioni eccessive, utilizzare metodi di supporto che creano l'eccezione e la restituiscono. Ad esempio:

C#
```
class FileReader
{
    private string fileName;

    public FileReader(string path)
    {
        fileName = path;
    }

    public byte[] Read(int bytes)
    {
        byte[] results = FileUtils.ReadFromFile(fileName, bytes);
        if (results == null)
        {
            throw NewFileIOException();
        }
        return results;
    }

    FileReaderException NewFileIOException()
    {
        string description = "My NewFileIOException Description";

        return new FileReaderException(description);
    }
}

```

In alcuni casi è preferibile usare il costruttore dell'eccezione per compilare l'eccezione. Un esempio è una classe di eccezioni globali, ad esempio @System.ArgumentException, 

### <a name="clean-up-intermediate-results-when-throwing-an-exception"></a>Eliminare i risultati intermedi quando si genera un'eccezione

I chiamanti dovrebbero avere la garanzia che non si verifichino effetti secondari quando un'eccezione viene generata da un metodo. Ad esempio, se è presente un codice che trasferisce denaro prelevandolo da un conto e depositandolo in un altro conto e viene generata un'eccezione durante l'esecuzione del deposito, non si desidera che il prelievo rimanga attivo.

C#
```
public void TransferFunds(Account from, Account to, decimal amount)
{
    from.Withdrawal(amount);
    // If the deposit fails, the withdrawal shouldn't remain in effect. 
    to.Deposit(amount);
}
```

Un modo per gestire questa situazione consiste nel rilevare eventuali eccezioni generate dalla transazione di deposito e annullare il prelievo.

C#
```
private static void TransferFunds(Account from, Account to, decimal amount)
{
    string withdrawalTrxID = from.Withdrawal(amount);
    try
    {
        to.Deposit(amount);
    }
    catch
    {
        from.RollbackTransaction(withdrawalTrxID);
        throw
    }
}
```

Questo esempio illustra l'uso di `throw` per generare nuovamente l'eccezione originale rendendo in questo modo più semplice per i chiamanti visualizzare la causa effettiva del problema senza dover esaminare la proprietà @System.Exception.InnerException. In alternativa è possibile generare una nuova eccezione e includere l'eccezione originale come eccezione interna:

C#
```
catch (Exception ex)
{
    from.RollbackTransaction(withdrawalTrxID);
    throw new Exception("Withdrawal failed", ex);
}
```

## <a name="see-also"></a>Vedere anche

Per altre informazioni sull'uso delle eccezioni in .NET, vedere [What Every Dev needs to Know About Exceptions in the Runtime](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/exceptions.md) (Informazioni per gli sviluppatori sulle eccezioni nel runtime).



<!--HONumber=Nov16_HO3-->


