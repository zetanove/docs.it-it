---
title: "Modello Dispose | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Dispose (metodo)"
  - "classe libreria linee guida di progettazione [.NET Framework], il metodo Dispose"
  - "indicazioni [.NET Framework] per la progettazione di librerie di classi, Finalize (metodo)"
  - "nome del metodo Dispose di personalizzazione"
  - "Finalize (metodo)"
ms.assetid: 31a6c13b-d6a2-492b-9a9f-e5238c983bcb
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# Modello Dispose
Tutti i programmi di acquisiscono una o più risorse di sistema, ad esempio memoria, handle del sistema o le connessioni di database, nel corso della loro esecuzione. Gli sviluppatori devono prestare molta attenzione quando si utilizzano tali risorse di sistema, poiché deve essere liberate dopo l'acquisizione e utilizzati.  
  
 CLR fornisce il supporto per la gestione automatica della memoria. Gestione della memoria \(memoria allocata tramite l'operatore c\# `new`\) non deve essere rilasciato in modo esplicito. Viene rilasciata automaticamente dal garbage collector \(GC\). Ciò consente agli sviluppatori di attività difficile e noioso del rilascio di memoria ed è stato uno dei motivi principali per la produttività senza precedenti offerto da .NET Framework.  
  
 Sfortunatamente, della memoria gestita è solo uno dei molti tipi di risorse di sistema. Risorse diverse dalla memoria gestita ancora devono essere rilasciate in modo esplicito e vengono definite come risorse non gestite. Il GC non è stato progettato per gestire tali risorse non gestite, il che significa che la responsabilità della gestione delle risorse non gestite si trovi nelle mani degli sviluppatori.  
  
 CLR fornisce un supporto di rilasciare risorse non gestite.<xref:System.Object?displayProperty=fullName> dichiara un metodo virtuale <xref:System.Object.Finalize%2A> \(chiamato anche il finalizzatore\) che viene chiamato dal GC prima che la memoria dell'oggetto venga recuperata tramite il catalogo globale e può essere sottoposto a override per rilasciare risorse non gestite. Tipi che eseguono l'override del finalizzatore vengono definiti come tipi di finalizzazione.  
  
 Sebbene i finalizzatori sono efficaci in alcuni scenari di pulizia, presentano due svantaggi significativi:  
  
-   Il finalizzatore viene richiamato quando il Garbage Collector rileva che un oggetto è idoneo per la raccolta. Ciò accade in un determinato periodo di tempo dopo che la risorsa non è più necessaria. Il ritardo tra quando lo sviluppatore può o si desidera rilasciare la risorsa e il tempo quando la risorsa viene effettivamente rilasciata dal finalizzatore può essere inaccettabile in programmi che acquisiscono molte risorse limitate \(risorse che possono essere facilmente esaurite\) o nei casi in cui le risorse sono i costi di mantenere in uso \(ad esempio, i buffer di grandi quantità di memoria non gestito\).  
  
-   Quando CLR deve chiamare un finalizzatore, è necessario posticipare raccolta della memoria dell'oggetto fino al successivo round di garbage collection \(i finalizzatori vengano eseguiti tra raccolte\). Ciò significa che la memoria dell'oggetto \(e tutti gli oggetti cui a che fa riferimento\) non verranno rilasciati per un periodo di tempo più lungo.  
  
 Pertanto, affidarsi esclusivamente i finalizzatori potrebbe non essere appropriato in molti scenari, quando è importante recuperare le risorse non gestite al più presto, quando si gestiscono le risorse o in altamente efficiente scenari in cui il GC aggiunto overhead della finalizzazione non è accettabile.  
  
 Il Framework fornisce il <xref:System.IDisposable?displayProperty=fullName> interfaccia che deve essere implementato per fornire allo sviluppatore di rilasciare risorse non gestite, non appena non sono necessari in modo manuale. Fornisce inoltre il <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> metodo che può indicare il catalogo globale che un oggetto è stato eliminato manualmente e non deve essere finalizzato più, nel qual caso la memoria dell'oggetto possa essere recuperata in precedenza. I tipi che implementano il `IDisposable` interfaccia sono detti tipi disposable.  
  
 Il modello Dispose è destinato per standardizzare l'utilizzo e l'implementazione di finalizzatori e `IDisposable` interfaccia.  
  
 La motivazione principale per il modello è quello di ridurre la complessità dell'implementazione del <xref:System.Object.Finalize%2A> e <xref:System.IDisposable.Dispose%2A> metodi. La complessità deriva dal fatto che i metodi condividono alcuni ma non tutti i percorsi di codice \(le differenze sono descritte più avanti in questo capitolo\). Inoltre, esistono motivi storici per alcuni elementi del modello correlato all'evoluzione del supporto delle lingue per la gestione delle risorse deterministica.  
  
 **✓ si** implementare il modello Dispose base su tipi contenente le istanze di tipi disposable. Vedere il [base modello Dispose](#basic_pattern) per ulteriori informazioni sul modello di base.  
  
 Se un tipo è responsabile per la durata di altri oggetti disposable, gli sviluppatori devono un modo per eliminare tali risorse, troppo. Usa il contenitore `Dispose` metodo è un modo pratico per ottenere questo risultato.  
  
 **✓ si** implementare il modello Dispose base e fornire un finalizzatore tipi che contiene risorse che devono essere liberate in modo esplicito e che non dispongono di finalizzatori.  
  
 Ad esempio, il modello deve essere implementato sui tipi di archiviazione di buffer di memoria non gestita. Il [tipi finalizzabili](#finalizable_types) sezione vengono illustrate le linee guida relative all'implementazione di finalizzatori.  
  
 **✓ PROVARE** che implementa il modello Dispose base nelle classi che stessi non contenere le risorse non gestite o oggetti disposable, ma sono soggetti a sottotipi di.  
  
 Un ottimo esempio di questo è il <xref:System.IO.Stream?displayProperty=fullName> \(classe\). Sebbene sia una classe base astratta che non contiene tutte le risorse, eseguire la maggior parte delle sue sottoclassi e per questo motivo, implementa questo modello.  
  
<a name="basic_pattern"></a>   
## Modello Dispose base  
 L'implementazione di base del modello comporta l'implementazione di `System.IDisposable` interfaccia e la dichiarazione il `Dispose(bool)` metodo che implementa la logica di pulizia risorse tutti per essere condivisi tra il `Dispose` metodo e il finalizzatore facoltativo.  
  
 Nell'esempio seguente viene illustrata un'implementazione semplice del modello di base:  
  
```  
public class DisposableResourceHolder : IDisposable {  
  
    private SafeHandle resource; // handle to a resource  
  
    public DisposableResourceHolder(){  
        this.resource = ... // allocates the resource  
    }  
  
    public void Dispose(){  
        Dispose(true);  
        GC.SuppressFinalize(this);  
    }  
  
    protected virtual void Dispose(bool disposing){  
        if (disposing){  
            if (resource!= null) resource.Dispose();  
        }  
    }  
}  
```  
  
 Il parametro Boolean `disposing` indica se è stato richiamato il metodo di `IDisposable.Dispose` implementazione o dal finalizzatore. Il `Dispose(bool)` implementazione deve controllare il parametro prima dell'accesso ad altri oggetti di riferimento \(ad esempio, il campo delle risorse nell'esempio precedente\). Tali oggetti è possibile accedere solo quando viene chiamato il metodo dal `IDisposable.Dispose` implementazione \(quando il `disposing` parametro è uguale a true\). Se il metodo viene richiamato dal finalizzatore \(`disposing` è false\), altri oggetti non possono accedervi. Il motivo è che gli oggetti vengono finalizzati in un ordine prevedibile e pertanto esse, o una delle relative dipendenze, potrebbe essere già stata finalizzata.  
  
 Inoltre, questa sezione si applica alle classi con una base che non implementano il modello Dispose. Se sta ereditando da una classe che implementa già il modello, è sufficiente eseguire l'override di `Dispose(bool)` metodo per fornire la logica di pulizia di risorse aggiuntivi.  
  
 **✓ si** dichiarare un valore void virtuale protetto `Dispose(bool disposing)` correlato metodo centralizzare tutta la logica per rilasciare risorse non gestite.  
  
 In questo metodo deve verificarsi tutti pulitura delle risorse. Il metodo viene chiamato dal finalizzatore entrambi e `IDisposable.Dispose` metodo. Il parametro sarà false se viene richiamata dall'interno un finalizzatore. E deve essere utilizzato per verificare il codice in esecuzione durante la finalizzazione non accede ad altri oggetti finalizzabili. Dettagli di implementazione i finalizzatori sono descritti nella sezione successiva.  
  
```  
protected virtual void Dispose(bool disposing){  
    if (disposing){  
        if (resource!= null) resource.Dispose();  
    }  
}  
```  
  
 **✓ si** implementare il `IDisposable` interfaccia chiamando semplicemente `Dispose(true)` seguito da `GC.SuppressFinalize(this)`.  
  
 La chiamata a `SuppressFinalize` dovrebbe verificarsi solo se `Dispose(true)` viene eseguita correttamente.  
  
```  
public void Dispose(){  
    Dispose(true);  
    GC.SuppressFinalize(this);  
}  
```  
  
 **X non** apportare senza parametri `Dispose` metodo virtuale.  
  
 Il `Dispose(bool)` metodo è quello che deve essere sottoposto a override dalle sottoclassi.  
  
```  
// bad design  
public class DisposableResourceHolder : IDisposable {  
    public virtual void Dispose(){ ... }  
    protected virtual void Dispose(bool disposing){ ... }  
}  
  
// good design  
public class DisposableResourceHolder : IDisposable {  
    public void Dispose(){ ... }  
    protected virtual void Dispose(bool disposing){ ... }  
}  
```  
  
 **X non** alcun overload di dichiarare il `Dispose` metodo diverso da `Dispose()` e `Dispose(bool)`.  
  
 `Dispose` deve essere considerata una parola riservata per codificare questo modello e per impedire confusione tra i responsabili dell'implementazione, utenti e i compilatori. Alcuni linguaggi è potrebbero scegliere di implementare automaticamente questo modello su determinati tipi.  
  
 **✓ si** consentono di `Dispose(bool)` metodo da chiamare più volte. Il metodo è possibile scegliere di non eseguire alcuna operazione dopo la prima chiamata.  
  
```  
public class DisposableResourceHolder : IDisposable {  
  
    bool disposed = false;  
  
    protected virtual void Dispose(bool disposing){  
        if(disposed) return;  
        // cleanup  
        ...  
        disposed = true;  
    }  
}  
```  
  
 **X evitare** generare un'eccezione dall'interno `Dispose(bool)` solo in situazioni critiche in cui il processo che lo contiene è stato danneggiato \(perdite, lo stato condiviso non coerente, ecc.\).  
  
 Gli utenti si aspettano che una chiamata a `Dispose` non genererà un'eccezione.  
  
 Se `Dispose` potrebbe generare un'eccezione, non verrà eseguita la logica di pulizia ulteriore blocco finally. Per risolvere il problema, l'utente deve eseguire il wrapping di ogni chiamata a `Dispose` \(entro il blocco finally\!\) in un blocco try, con la conseguente ai gestori di pulizia molto complessi. Se l'esecuzione di un `Dispose(bool disposing)` \(metodo\), non genera un'eccezione se l'eliminazione è false. In questo modo terminerà il processo se l'esecuzione all'interno di un contesto finalizzatore.  
  
 **✓ si** generano un <xref:System.ObjectDisposedException> da qualsiasi membro non può essere utilizzati dopo aver eliminato l'oggetto di.  
  
```  
public class DisposableResourceHolder : IDisposable {  
    bool disposed = false;  
    SafeHandle resource; // handle to a resource  
  
    public void DoSomething(){  
           if(disposed) throw new ObjectDisposedException(...);  
        // now call some native methods using the resource   
            ...  
    }  
    protected virtual void Dispose(bool disposing){  
        if(disposed) return;  
        // cleanup  
        ...  
        disposed = true;  
    }  
}  
```  
  
 **✓ PROVARE** offrendo metodo `Close()`, oltre al `Dispose()`, se chiudere è terminologia standard utilizzata nell'area.  
  
 In tal caso, è importante eseguire il `Close` identico all'implementazione `Dispose` e si consiglia di implementare il `IDisposable.Dispose` metodo in modo esplicito.  
  
```  
public class Stream : IDisposable {  
    IDisposable.Dispose(){  
        Close();  
    }  
    public void Close(){  
        Dispose(true);  
        GC.SuppressFinalize(this);  
    }  
}  
```  
  
<a name="finalizable_types"></a>   
## Tipi di finalizzazione  
 Finalizzazione tipi sono tipi che estendono il modello Dispose base eseguendo l'override del finalizzatore e fornire il percorso di codice di finalizzazione nel `Dispose(bool)` metodo.  
  
 I finalizzatori sono notoriamente difficili da implementare correttamente, principalmente perché non è possibile apportare alcuni presupposti sullo stato del sistema \(in genere validi\) durante la loro esecuzione. Le seguenti linee guida dovrebbero essere preso in un'attenta valutazione.  
  
 Si noti che alcune linee guida si applicano non solo al `Finalize` metodo, tuttavia, per qualsiasi codice chiamato da un finalizzatore. Nel caso il metodo Dispose modello di base definiti in precedenza, questo significa logica che viene eseguita all'interno di `Dispose(bool disposing)` quando il `disposing` parametro è impostato su false.  
  
 Se la classe di base già è finalizzabile e implementa il modello Dispose base, è consigliabile non eseguire l'override `Finalize` nuovamente. È invece sufficiente eseguire l'override di `Dispose(bool)` metodo per fornire la logica di pulizia di risorse aggiuntivi.  
  
 Il codice seguente viene illustrato un esempio di un tipo finalizzabile:  
  
```  
public class ComplexResourceHolder : IDisposable {  
  
    private IntPtr buffer; // unmanaged memory buffer  
    private SafeHandle resource; // disposable handle to a resource  
  
    public ComplexResourceHolder(){  
        this.buffer = ... // allocates memory  
        this.resource = ... // allocates the resource  
    }  
  
    protected virtual void Dispose(bool disposing){  
            ReleaseBuffer(buffer); // release unmanaged memory  
        if (disposing){ // release other disposable objects  
            if (resource!= null) resource.Dispose();  
        }  
    }  
  
    ~ ComplexResourceHolder(){  
        Dispose(false);  
    }  
  
    public void Dispose(){  
        Dispose(true);  
        GC.SuppressFinalize(this);  
    }  
}  
```  
  
 **X evitare** esecuzione finalizzabili tipi.  
  
 Valutare con attenzione tutti i casi in cui si ritiene che è necessario un finalizzatore. Esiste un reale costi associati alle istanze con i finalizzatori, dal punto di vista della complessità codice sia le prestazioni. Preferire l'utilizzo di wrapper di risorse, ad esempio <xref:System.Runtime.InteropServices.SafeHandle> per incapsulare le risorse non gestite, laddove possibile, nel qual caso un finalizzatore diventa non necessario perché il wrapper è responsabile della pulizia di risorse.  
  
 **X non** rendere finalizzabile tipi di valore.  
  
 Solo i tipi di riferimento ottengano effettivamente finalizzati da CLR, e pertanto verrà ignorato qualsiasi tentativo di inserire un finalizzatore per un tipo di valore. I compilatori c\# e C\+\+ applica questa regola.  
  
 **✓ si** rendere finalizzabile un tipo se il tipo è responsabile del rilascio di una risorsa non gestita che non dispone di un proprio finalizzatore.  
  
 Quando si implementa il finalizzatore, è sufficiente chiamare `Dispose(false)` e inserire logica di pulizia tutte le risorse all'interno di `Dispose(bool disposing)` metodo.  
  
```  
public class ComplexResourceHolder : IDisposable {  
  
    ~ ComplexResourceHolder(){  
        Dispose(false);  
    }  
  
    protected virtual void Dispose(bool disposing){  
        ...  
    }  
}  
```  
  
 **✓ si** implementare il modello Dispose base su ogni tipo di finalizzazione.  
  
 In questo modo gli utenti del tipo di un mezzo per eseguire in modo esplicito la pulitura deterministica delle stesse risorse di cui è responsabile il finalizzatore.  
  
 **X non** accedere agli oggetti finalizzabili nel percorso del codice finalizzatore in quanto vi è rischio significativo che essi saranno sia già stati completati.  
  
 Ad esempio, un oggetto finalizzabile oggetto che presenta un riferimento a un altro oggetto finalizzabile B in modo affidabile non può utilizzare B nel finalizzatore, o viceversa. I finalizzatori vengono chiamati in ordine casuale \(una garanzia di ordinamento debole per la finalizzazione critica\).  
  
 Inoltre, tenere presente che gli oggetti archiviati in variabili statiche vengono raccolti in determinati momenti durante uno scaricamento del dominio applicazione o l'uscita dal processo. L'accesso a una variabile statica che fa riferimento a un oggetto finalizzabile \(o chiamare un metodo statico che potrebbe utilizzare i valori archiviati in variabili statiche\) potrebbe non essere sicuro se <xref:System.Environment.HasShutdownStarted%2A?displayProperty=fullName> restituisce true.  
  
 **✓ si** rendere la `Finalize` metodo protetto.  
  
 Gli sviluppatori c\#, C\+\+ e Visual Basic.NET non è necessario preoccuparsi di ciò, perché i compilatori consentono di applicare questa linea guida.  
  
 **X non** escape consentire eccezioni dalla logica del finalizzatore, ad eccezione di errori di sistema critici.  
  
 Se viene generata un'eccezione da un finalizzatore, Common Language Runtime verrà arrestato l'intero processo \(a partire da .NET Framework versione 2.0\), impedire che altri finalizzatori risorse rilasciato in modo controllato e l'esecuzione.  
  
 **✓ PROVARE** creazione e utilizzo di un oggetto finalizzabile critico \(un tipo con una gerarchia dei tipi contenente <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject>\) per le situazioni in cui un finalizzatore assolutamente necessario eseguire anche in caso di dominio dell'applicazione forzata viene scaricata e interruzioni di thread.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>   
 <xref:System.Object.Finalize%2A?displayProperty=fullName>   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Modelli di progettazione comuni](../../../docs/standard/design-guidelines/common-design-patterns.md)   
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)