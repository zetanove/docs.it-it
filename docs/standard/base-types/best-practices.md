---
title: "Procedure consigliate per le espressioni regolari in .NET Framework | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, procedure consigliate"
  - "espressioni regolari, procedure consigliate"
ms.assetid: 618e5afb-3a97-440d-831a-70e4c526a51c
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedure consigliate per le espressioni regolari in .NET Framework
Il motore delle espressioni regolari in .NET Framework è uno strumento potente e completo che consente di elaborare il testo in base alle corrispondenze dei modelli anziché in base al confronto e alla corrispondenza con il testo letterale.  Nella maggior parte dei casi, la corrispondenza dei modelli viene applicata in modo rapido ed efficiente.  In alcuni casi, tuttavia, il motore delle espressioni regolari può risultare molto lento.  In casi estremi, può anche sembrare che il motore non risponda durante l'elaborazione di un input relativamente piccolo per ore o perfino giorni.  
  
 In questo argomento vengono illustrate alcune procedure consigliate che possono essere adottate dagli sviluppatori per ottenere prestazioni ottimali con le espressioni regolari.  Include le sezioni seguenti:  
  
-   [Esaminare l'origine di input](#InputSource)  
  
-   [Gestire la creazione di istanze degli oggetti in modo appropriato](#ObjectInstantiation)  
  
-   [Assumere il controllo del backtracking](#Backtracking)  
  
-   [Utilizzare valori di timeout](#Timeouts)  
  
-   [Eseguire l'acquisizione solo quando necessario](#Capture)  
  
-   [Argomenti correlati](#RelatedTopics)  
  
<a name="InputSource"></a>   
## Esaminare l'origine di input  
 In generale, le espressioni regolari possono accettare due tipi di input: vincolato o non vincolato.  Per input vincolato si intende un testo che proviene da un'origine conosciuta o affidabile e segue un formato predefinito.  Per input non vincolato si intende un testo che proviene da un'origine non inaffidabile, ad esempio un utente Web, e non può seguire un formato predefinito o previsto.  
  
 I modelli di espressione regolare vengono scritti in genere in modo da corrispondere all'input valido,  ovvero gli sviluppatori esaminano il testo per il quale desiderano trovare una corrispondenza e scrivono quindi un modello di espressione regolare a esso corrispondente.  Gli sviluppatori determinano infine se questo modello richiede una correzione o un'ulteriore elaborazione testandolo con più elementi di input validi.  Se il modello corrisponde a tutti gli input considerati validi, viene dichiarato pronto per la produzione e può essere incluso in un'applicazione rilasciata.  In tal modo, un modello di espressione regolare viene considerato appropriato per la corrispondenza con un input vincolato.  Tuttavia, non verrà considerato appropriato per la corrispondenza con un input non vincolato.  
  
 Per corrispondere a un input non vincolato, un'espressione regolare deve potere gestire efficientemente tre tipi di testo:  
  
-   Testo che corrisponde al modello di espressione regolare.  
  
-   Testo che non corrisponde al modello di espressione regolare.  
  
-   Testo che corrisponde quasi al modello di espressione regolare.  
  
 L'ultimo tipo di testo è particolarmente problematico per un'espressione regolare scritta per gestire l'input vincolato.  Se tale espressione regolare si basa anche sul [backtracking](../../../docs/standard/base-types/backtracking-in-regular-expressions.md) esteso, il motore delle espressioni regolari può richiedere una quantità eccessiva di tempo, in alcuni casi molte ore o giorni, per l'elaborazione di un testo apparentemente irrilevante.  
  
> [!WARNING]
>  Nell'esempio seguente viene utilizzata un'espressione regolare soggetta a un backtracking eccessivo e che con tutta probabilità rifiuta indirizzi di posta elettronica validi.  Non utilizzarla in una routine di convalida di posta elettronica.  Per un'espressione regolare che convalida gli indirizzi di posta elettronica, vedere [Procedura: Verificare che le stringhe siano in formato di posta elettronica valido](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md).  
  
 Si consideri, ad esempio, un'espressione regolare comunemente utilizzata ma estremamente problematica per la convalida dell'alias di un indirizzo di posta elettronica.  L'espressione regolare `^[0-9A-Z]([-.\w]*[0-9A-Z])*$` viene scritta per elaborare gli indirizzi di posta elettronica ritenuti validi, composti da un carattere alfanumerico seguito da zero o più caratteri che possono essere alfanumerici, punti o trattini.  L'espressione regolare deve terminare con un carattere alfanumerico.  Tuttavia, come illustrato nell'esempio seguente, sebbene questa espressione regolare gestisca facilmente l'input valido, le prestazioni risulteranno molto inefficienti quando viene elaborato un input quasi valido.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/design2.cs#1)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/design2.vb#1)]  
  
 Come illustrato nell'output dell'esempio, il motore delle espressioni regolari elabora l'alias di posta elettronica valido nello stesso intervallo di tempo indipendentemente dalla lunghezza.  D'altra parte, quando l'indirizzo di posta elettronica quasi valido ha più di cinque caratteri, il tempo di elaborazione raddoppia approssimativamente per ogni carattere aggiuntivo nella stringa.  Ciò significa che l'elaborazione di una stringa di 28 caratteri quasi valida richiederebbe più di un'ora e l'elaborazione di una stringa di 33 caratteri quasi valida richiederebbe quasi un giorno.  
  
 Poiché questa espressione regolare è stata sviluppata considerando unicamente la corrispondenza con il formato di input, l'input che non corrisponde al modello non viene preso in considerazione.  Di conseguenza, è possibile consentire a un input non vincolato che corrisponde quasi al modello di espressione regolare di ridurre significativamente le prestazioni.  
  
 Per risolvere tale problema, è possibile effettuare le operazioni seguenti:  
  
-   Durante lo sviluppo di un modello, è consigliabile considerare il modo in cui il backtracking potrebbe influire sulle prestazioni del motore delle espressioni regolari, soprattutto se l'espressione regolare è progettata per elaborare un input non vincolato.  Per ulteriori informazioni, vedere la sezione [Assumere il controllo del backtracking](#Backtracking) di questo argomento.  
  
-   Testare in modo approfondito l'espressione regolare utilizzando un input non valido e quasi valido nonché un input valido.  Per generare casualmente input for un'espressione regolare specifica, è possibile usare [Rex](http://go.microsoft.com/fwlink/?LinkId=210756), uno strumento di analisi delle espressioni regolari di Microsoft Research.  
  
 [Torna all'inizio](#top)  
  
<a name="ObjectInstantiation"></a>   
## Gestire la creazione di istanze degli oggetti in modo appropriato  
 Il modello a oggetti delle espressioni regolari di .NET Framework è basato sulla classe <xref:System.Text.RegularExpressions.Regex?displayProperty=fullName>, che rappresenta il motore delle espressioni regolari.  Il fattore principale che spesso influisce sulle prestazioni delle espressioni regolari è il modo in cui viene utilizzato il motore <xref:System.Text.RegularExpressions.Regex>.  Per definire un'espressione regolare è necessario associare il motore delle espressioni regolari a un modello di espressione regolare.  Tale processo di associazione, indipendentemente dal fatto che comporti la creazione di un'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> passando al relativo costruttore un modello di espressione regolare o la chiamata a un metodo statico passando il modello di espressione regolare con una stringa da analizzare, è necessariamente dispendioso.  
  
> [!NOTE]
>  Per informazioni più dettagliate sull'impatto che può avere l'uso delle espressioni regolari interpretate e compilate sulle prestazioni, vedere [Ottimizzazione delle prestazioni delle espressioni regolari, parte II: controllo del backtracking](http://go.microsoft.com/fwlink/?LinkId=211566) nel blog del team BCL.  
  
 È possibile associare il motore delle espressioni regolari a un modello di espressione regolare specifico e quindi utilizzare il motore per trovare una corrispondenza con il testo in diversi modi:  
  
-   È possibile chiamare un metodo statico di corrispondenza dei modelli, ad esempio <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%29?displayProperty=fullName>.  Non è richiesta la creazione di un'istanza di un oggetto di espressione regolare.  
  
-   È possibile creare un'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> e chiamare un metodo di corrispondenza dei modelli dell'istanza di un'espressione regolare interpretata.  È il metodo predefinito per associare il motore delle espressioni regolari a un modello di espressione regolare.  Viene utilizzato quando l'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> viene creata senza un argomento `options` che include il flag <xref:System.Text.RegularExpressions.RegexOptions>.  
  
-   È possibile creare un'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> e chiamare un metodo di corrispondenza dei modelli dell'istanza di un'espressione regolare compilata.  Gli oggetti di espressioni regolari rappresentano i modelli compilati quando l'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> viene creata con un argomento `options` che include il flag <xref:System.Text.RegularExpressions.RegexOptions>.  
  
-   È possibile creare un oggetto <xref:System.Text.RegularExpressions.Regex> specifico strettamente associato a un modello di espressione regolare specifico, compilarlo e salvarlo in un assembly autonomo.  A tale scopo, è possibile chiamare il metodo <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=fullName>.  
  
 La modalità utilizzata per chiamare i metodi di corrispondenza delle espressioni regolari può avere un impatto notevole sull'applicazione.  Nelle sezioni seguenti viene illustrato quando utilizzare le chiamate al metodo statico, le espressioni regolari interpretate e le espressioni regolari compilate per migliorare le prestazioni dell'applicazione.  
  
> [!IMPORTANT]
>  Il formato della chiamata al metodo \(statico, interpretato, compilato\) influisce sulle prestazioni se la stessa espressione regolare viene utilizzata più volte nelle chiamate al metodo oppure se in un'applicazione vengono utilizzati spesso gli oggetti di espressione regolare.  
  
### Espressioni regolari statiche  
 I metodi con espressioni regolari statiche sono consigliati come alternativa alla creazione ripetuta di un'istanza di un oggetto di espressione regolare con la stessa espressione regolare.  A differenza dei modelli di espressione regolare utilizzati dagli oggetti di espressione regolare, i codici operativi o il linguaggio MSIL \(Microsoft Intermediate Language\) compilato dei modelli utilizzati nelle chiamate al metodo di istanza vengono memorizzati nella cache interna dal motore delle espressioni regolari.  
  
 Ad esempio, un gestore eventi chiama frequentemente un altro metodo per convalidare l'input dell'utente.  Tale situazione viene riportata nel codice seguente, in cui l'evento <xref:System.Windows.Forms.Button> di un controllo <xref:System.Windows.Forms.Control.Click> viene utilizzato per chiamare un metodo denominato `IsValidCurrency`, che controlla se l'utente ha immesso un simbolo di valuta seguito da almeno una cifra decimale.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/static1.cs#2)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/static1.vb#2)]  
  
 Nell'esempio seguente viene illustrata un'implementazione molto inefficiente del metodo `IsValidCurrency`.  Si noti che ogni chiamata al metodo crea una nuova istanza dell'oggetto <xref:System.Text.RegularExpressions.Regex> con lo stesso modello.  Di conseguenza, il modello di espressione regolare deve essere ricompilato ogni volta che viene chiamato il metodo.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/static1.cs#3)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/static1.vb#3)]  
  
 È consigliabile sostituire questo codice inefficiente con una chiamata al metodo statico <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=fullName>.  In tal modo si evita di dover creare un'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> ogni volta che si desidera chiamare un metodo di corrispondenza dei modelli e si consente al motore delle espressioni regolari di recuperare una versione compilata dell'espressione regolare dalla cache.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/static2.cs#4)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/static2.vb#4)]  
  
 Per impostazione predefinita, nella cache vengono memorizzati gli ultimi 15 modelli di espressione regolare statica utilizzati più di recente.  Per le applicazioni che richiedono un numero maggiore di espressioni regolari statiche memorizzate nella cache, la dimensione della cache può essere modificata impostando la proprietà <xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=fullName>.  
  
 L'espressione regolare `\p{Sc}+\s*\d+` usata in questo esempio verifica che la stringa di input sia costituita da un simbolo di valuta e da almeno una cifra decimale.  Il modello viene definito come illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\p{Sc}+`|Trova la corrispondenza di uno o più caratteri nella categoria Unicode Symbol, Currency.|  
|`\s*`|Trovare la corrispondenza di zero o più spazi vuoti.|  
|`\d+`|Trova la corrispondenza con una o più cifre decimali.|  
  
<a name="Interpreted"></a>   
### Espressioni regolari interpretate edEspressioni regolari compilate  
 I modelli di espressione regolare che non sono associati al motore delle espressioni mediante l'opzione <xref:System.Text.RegularExpressions.RegexOptions> vengono interpretati.  Quando viene creata un'istanza di un oggetto di espressione regolare, il motore delle espressioni regolari converte l'espressione regolare in un set di codici operativi.  Quando viene chiamato un metodo di istanza, i codici operativi vengono convertiti in MSIL ed eseguiti dal compilatore JIT.  Analogamente, quando viene chiamato un metodo con espressioni regolari statiche e l'espressione regolare non è presente nella cache, il motore delle espressioni regolari converte l'espressione regolare in un set di codici operativi che memorizza nella cache.  Converte quindi i codici operativi in MSIL in modo tale che possano essere eseguiti dal compilatore JIT.  Le espressioni regolari interpretate consentono di ridurre il tempo di avvio ma implicano tempi di esecuzione più lenti.  Per questo motivo, risultano particolarmente adatte quando l'espressione regolare viene utilizzata in un numero limitato di chiamate al metodo o se il numero esatto di chiamate ai metodi delle espressioni regolari è sconosciuto ma si prevede che sia esiguo.  Man mano che aumenta il numero di chiamate al metodo, il miglioramento delle prestazioni rispetto alla riduzione del tempo di avvio viene superato dalla minore velocità di esecuzione.  
  
 I modelli di espressione regolare che sono associati al motore delle espressioni regolari mediante l'opzione <xref:System.Text.RegularExpressions.RegexOptions> vengono compilati.  Ciò significa che quando viene creata un'istanza di un oggetto di espressione regolare o quando viene chiamato un metodo con espressioni regolari statiche e l'espressione regolare non è presente nella cache, il motore delle espressioni regolari converte l'espressione regolare in un set intermedio di codici operativi, il quale viene quindi convertito in MSIL.  Il codice MSIL viene eseguito dal compilatore JIT non appena viene chiamato un metodo.  A differenza delle espressioni regolari interpretate, le espressioni regolari compilate aumentano il tempo di avvio eseguendo i singoli metodi di corrispondenza dei modelli più velocemente.  Di conseguenza, il vantaggio in termini di prestazioni che risulta dalla compilazione dell'espressione regolare aumenta proporzionalmente al numero di metodi dell'espressione regolare chiamati.  
  
 Riepilogando, è consigliabile utilizzare le espressioni regolari interpretate quando i metodi dell'espressione regolare vengono chiamati raramente con un'espressione regolare specifica  e le espressioni regolari compilate quando i metodi dell'espressione regolare vengono chiamati frequentemente con un'espressione regolare specifica.  È difficile determinare la soglia esatta oltre la quale la minore velocità di esecuzione delle espressioni regolari interpretate supera i vantaggi offerti dalla riduzione del tempo di avvio o la soglia oltre la quale la riduzione del tempo di avvio delle espressioni regolari compilate supera i vantaggi offerti dalla maggiore velocità di esecuzione.  Dipende da vari fattori, tra cui la complessità dell'espressione regolare e i dati specifici che vengono elaborati.  Per determinare se le espressioni regolari interpretate o compilate offrono le migliori prestazioni per lo scenario specifico dell'applicazione, è possibile utilizzare la classe <xref:System.Diagnostics.Stopwatch> per confrontare i rispettivi tempi di esecuzione.  
  
 Nell'esempio seguente vengono confrontate le prestazioni delle espressioni regolari compilate e interpretate durante la lettura delle prime dieci frasi e durante la lettura di tutte le frasi del testo di *The Financier* di Theodore Dreiser.  Come illustrato nell'output dell'esempio, quando vengono effettuate solo dieci chiamate ai metodi di corrispondenza delle espressioni regolari, un'espressione regolare interpretata offre prestazioni migliori rispetto a un'espressione regolare compilata.  Tuttavia, un'espressione regolare compilata offre prestazioni migliori quando viene effettuato un numero di chiamate maggiore, in questo caso oltre 13.000.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/compare1.cs#5)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/compare1.vb#5)]  
  
 Il criterio di espressione regolare usato nell'esempio, `\b(\w+((\r?\n)|,?\s))*\w+[.?:;!]`, è definito nel modo illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`\w+`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
|`(\r?  \n)&#124;,?  \s)`|Trova la corrispondenza di uno o nessun ritorno a capo seguito da un carattere di nuova riga o di una o nessuna virgola seguita da uno spazio vuoto.|  
|`(\w+((\r?  \n)&#124;,?  \s))*`|Trova la corrispondenza di zero o più occorrenze di uno o più caratteri alfanumerici seguiti da uno o nessun ritorno a capo e un carattere di nuova riga o da una o nessuna virgola seguita da uno spazio vuoto.|  
|`\w+`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
|`[.?:;!]`|Trova la corrispondenza di un punto, un punto interrogativo, due punti, un punto e virgola o un punto esclamativo.|  
  
### Compilazione delle espressioni regolari in un assembly  
 .NET Framework consente inoltre di creare un assembly che contiene le espressioni regolari compilate.  In questo modo il calo di prestazioni della compilazione delle espressioni regolari viene spostato dalla fase di esecuzione alla fase di progettazione.  Vengono tuttavia richieste alcune operazioni aggiuntive: è necessario definire in anticipo le espressioni regolari e compilarle in un assembly.  Il compilatore può quindi fare riferimento all'assembly durante la compilazione del codice sorgente che utilizza le espressioni regolari dell'assembly.  Ogni espressione regolare compilata inclusa nell'assembly viene rappresentata da una classe derivata da <xref:System.Text.RegularExpressions.Regex>.  
  
 Per compilare le espressioni regolari in un assembly, è necessario chiamare il metodo [Regex.CompileToAssembly\(RegexCompilationInfo\<xref:System.Text.RegularExpressions.Regex.CompileToAssembly%28System.Text.RegularExpressions.RegexCompilationInfo%5B%5D%2CSystem.Reflection.AssemblyName%29?displayProperty=fullName> e passare una matrice di oggetti <xref:System.Text.RegularExpressions.RegexCompilationInfo> che rappresentano le espressioni regolari da compilare e un oggetto <xref:System.Reflection.AssemblyName> che contiene le informazioni sull'assembly da creare.  
  
 È consigliabile compilare le espressioni regolari in un assembly nelle situazioni seguenti:  
  
-   Se si è uno sviluppatore di componenti e si desidera creare una libreria di espressioni regolari riutilizzabili.  
  
-   Se si prevede di chiamare i metodi di corrispondenza dei modelli delle espressioni regolari un numero indeterminato di volte, da una o due volte a migliaia o decine di migliaia di volte.  A differenza delle espressioni regolari compilate o interpretate, le espressioni regolari compilate in assembly separati offrono prestazioni coerenti indipendentemente dal numero di chiamate al metodo.  
  
 Se si utilizzano le espressioni regolari compilate per ottimizzare le prestazioni, è consigliabile non utilizzare la reflection per creare l'assembly, caricare il motore delle espressioni regolari ed eseguire i metodi di corrispondenza dei modelli.  A tale scopo occorre evitare di compilare i modelli di espressione regolare in modo dinamico e occorre specificare le opzioni di corrispondenza dei modelli, ad esempio la corrispondenza dei modelli senza distinzione tra maiuscole e minuscole, al momento della creazione dell'assembly.  È inoltre necessario separare il codice mediante cui viene creato l'assembly dal codice che utilizza l'espressione regolare.  
  
 Nell'esempio seguente viene illustrato come creare un assembly contenente un'espressione regolare compilata.  Viene creato un assembly denominato `RegexLib.dll` con una singola classe di espressioni regolari, `SentencePattern`, che contiene il criterio di espressione regolare per la corrispondenza delle frasi usato nella sezione [Espressioni regolari interpretate ed espressioni regolari compilate](#Interpreted).  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/compile1.cs#6)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/compile1.vb#6)]  
  
 Quando l'esempio viene compilato in un eseguibile ed eseguito, viene creato un assembly denominato `RegexLib.dll`.  L'espressione regolare viene rappresentata da una classe denominata `Utilities.RegularExpressions.SentencePattern` derivata da <xref:System.Text.RegularExpressions.Regex>.  Nell'esempio seguente viene quindi usata l'espressione regolare compilata per estrarre le frasi dal testo di *The Financier* di Theodore Dreiser.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/compile2.cs#7)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/compile2.vb#7)]  
  
 [Torna all'inizio](#top)  
  
<a name="Backtracking"></a>   
## Assumere il controllo del backtracking  
 In genere, il motore delle espressioni regolari utilizza la progressione lineare per spostarsi in una stringa di input e confrontarla con un modello di espressione regolare.  Tuttavia, quando in un modello di espressione regolare vengono utilizzati quantificatori indeterminati come `*`, `+` e `?`, il motore delle espressioni regolari può tralasciare una parte delle corrispondenze parziali corrette e tornare a uno stato salvato in precedenza per cercare una corrispondenza corretta per l'intero modello.  Questo processo è noto come backtracking.  
  
> [!NOTE]
>  Per altre informazioni sul backtracking, vedere [Dettagli sul comportamento delle espressioni regolari](../../../docs/standard/base-types/details-of-regular-expression-behavior.md) e [Backtracking](../../../docs/standard/base-types/backtracking-in-regular-expressions.md).  Per informazioni più dettagliate sul backtracking, vedere [Ottimizzazione delle prestazioni delle espressioni regolari, parte II: controllo del backtracking](http://go.microsoft.com/fwlink/?LinkId=211567) sul blog del team BCL.  
  
 Il supporto del backtracking fornisce alle espressioni regolari potenza e flessibilità.  Inoltre la responsabilità del controllo del funzionamento del motore delle espressioni regolari viene affidata agli sviluppatori delle espressioni regolari.  Poiché spesso gli sviluppatori non sono consapevoli di questa responsabilità, un utilizzo improprio del backtracking o un utilizzo eccessivo del backtracking rappresenta spesso la causa principale della riduzione delle prestazioni delle espressioni regolari.  Nello scenario peggiore, il tempo di esecuzione può raddoppiarsi per ogni carattere aggiuntivo nella stringa di input.  Utilizzando infatti il backtracking in modo eccessivo, è facile creare l'equivalente a livello di codice di un ciclo infinito se l'input corrisponde quasi al modello di espressione regolare. Il motore delle espressioni regolari può richiedere ore o persino giorni per l'elaborazione di una stringa di input relativamente breve.  
  
 L'utilizzo del backtracking comporta spesso una riduzione delle prestazioni delle applicazioni sebbene il backtracking non sia essenziale per una corrispondenza.  Ad esempio, l'espressione regolare `\b\p{Lu}\w*\b` cerca una corrispondenza di tutte le parole che iniziano con un carattere maiuscolo, come illustrato nella tabella seguente.  
  
|||  
|-|-|  
|Modello|Descrizione|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`\p{Lu}`|Trova la corrispondenza di un carattere maiuscolo.|  
|`\w*`|Trova la corrispondenza di zero o più caratteri alfanumerici.|  
|`\b`|Termina la corrispondenza sul confine di parola.|  
  
 Poiché un confine di parola non è uguale a un carattere alfanumerico né è un subset di tali caratteri, non è possibile che il motore delle espressioni regolari attraversi un confine di parola quando viene trovata una corrispondenza con i caratteri alfanumerici.  Ciò significa che per questa espressione regolare, il backtracking non potrà mai contribuire alla riuscita dell'operazione ma potrà solo ridurre le prestazioni poiché il motore delle espressioni regolari deve salvare lo stato per ogni corrispondenza preliminare corretta di un carattere alfanumerico.  
  
 Se si determina che il backtracking non è necessario, è possibile disabilitarlo utilizzando l'elemento del linguaggio `(?>``subexpression``)`.  Nell'esempio seguente viene analizzata una stringa di input utilizzando due espressioni regolari.  La prima, `\b\p{Lu}\w*\b`, si basa sul backtracking.  La seconda, `\b\p{Lu}(?>\w*)\b`, disabilita il backtracking.  Come illustrato nell'output dell'esempio, entrambe producono lo stesso risultato.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/backtrack2.cs#10)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/backtrack2.vb#10)]  
  
 In molti casi, il backtracking è essenziale per la corrispondenza di un modello di espressione regolare con il testo di input.  Tuttavia, un utilizzo eccessivo del backtracking può ridurre notevolmente le prestazioni e dare l'impressione che un'applicazione non risponda.  In particolare, tale situazione si verifica quando vengono annidati i quantificatori e il testo che corrisponde alla sottoespressione esterna è un subset del testo che corrisponde alla sottoespressione interna.  
  
> [!WARNING]
>  Oltre a evitare un eccessivo utilizzo del backtracking, è necessario utilizzare la funzionalità di timeout per assicurarsi che l'eccessivo backtracking non comprometta troppo le prestazioni dell'espressione regolare.  Per ulteriori informazioni, vedere la sezione [Utilizzare valori di timeout](#Timeouts).  
  
 Ad esempio, il criterio di espressione regolare `^[0-9A-Z]([-.\w]*[0-9A-Z])*\$$` viene usato per trovare la corrispondenza con un numero parte costituito da almeno un carattere alfanumerico.  Tutti i caratteri aggiuntivi possono essere costituiti da un carattere alfanumerico, un trattino, un carattere di sottolineatura o un punto, sebbene l'ultimo carattere debba essere alfanumerico.  Il numero parte termina con il simbolo del dollaro.  In alcuni casi, il criterio di espressione regolare può presentare prestazioni estremamente insufficienti perché vengono annidati i quantificatori e perché la sottoespressione `[0-9A-Z]` è un subset della sottoespressione `[-.\w]*`.  
  
 In questi casi, è possibile ottimizzare le prestazioni dell'espressione regolare rimuovendo i quantificatori annidati e sostituendo la sottoespressione esterna con un'asserzione lookahead o lookbehind di larghezza zero.  Le asserzioni lookahead e lookbehind sono ancoraggi; non spostano il puntatore nella stringa di input, ma eseguono il lookahead e lookbehind per verificare se è stata soddisfatta una condizione specificata.  Ad esempio, l'espressione regolare del numero parte può essere riscritta come `^[0-9A-Z][-.\w]*(?<=[0-9A-Z])\$$`.  Tale modello di espressione regolare viene definito come illustrato nella tabella seguente.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`^`|Inizia la corrispondenza all'inizio della stringa di input.|  
|`[0-9A-Z]`|Trova la corrispondenza di un carattere alfanumerico.  Il numero parte deve essere costituito da almeno uno di questi caratteri.|  
|`[-.  \w]*`|Trova la corrispondenza di zero o più occorrenze di un carattere alfanumerico, un trattino o un punto.|  
|`\$`|Trova la corrispondenza di un simbolo del dollaro.|  
|`(?<=[0-9A-Z])`|Esegue il lookahead del simbolo del dollaro finale per verificare che il carattere precedente sia alfanumerico.|  
|`$`|Termina la ricerca della corrispondenza alla fine della stringa di input.|  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'espressione regolare per trovare la corrispondenza con una matrice contenente i numeri parte possibili.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/backtrack4.cs#11)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/backtrack4.vb#11)]  
  
 Il linguaggio delle espressioni regolari in .NET Framework include i seguenti elementi che è possibile utilizzare per eliminare i quantificatori annidati.  Per altre informazioni, vedere [Costrutti di raggruppamento](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
|Elemento di linguaggio|Descrizione|  
|----------------------------|-----------------|  
|`(?=` `subexpression` `)`|Asserzione lookahead positiva di larghezza zero.  Lookahead della posizione corrente per determinare se `subexpression` corrisponde alla stringa di input.|  
|`(?!` `subexpression` `)`|Asserzione lookahead negativa di larghezza zero.  Lookahead della posizione corrente per determinare se `subexpression` non corrisponde alla stringa di input.|  
|`(?<=` `subexpression` `)`|Lookbehind positivo di larghezza zero.  Lookbehind della posizione corrente per determinare se `subexpression` corrisponde alla stringa di input.|  
|`(?<!` `subexpression` `)`|Lookbehind negativo di larghezza zero.  Lookbehind della posizione corrente per determinare se `subexpression` non corrisponde alla stringa di input.|  
  
 [Torna all'inizio](#top)  
  
<a name="Timeouts"></a>   
## Utilizzare valori di timeout  
 Se le espressioni regolari elaborano l'input che corrisponde quasi al modello dell'espressione regolare, possono spesso basarsi su un backtracking eccessivo, con un impatto notevole sulle prestazioni.  Oltre a considerare attentamente l'utilizzo del backtracking e a testare l'espressione regolare rispetto all'input maggiormente corrispondente, è necessario impostare sempre un valore di timeout per assicurarsi che l'impatto di un eventuale backtracking eccessivo sia contenuto.  
  
 L'intervallo di timeout dell'espressione regolare definisce il periodo di tempo durante il quale il motore delle espressioni regolari cercherà una singola corrispondenza prima del timeout.  L'intervallo di timeout predefinito è <xref:System.Text.RegularExpressions.Regex.InfiniteMatchTimeout?displayProperty=fullName> che significa che l'espressione regolare non scadrà.  È possibile eseguire l'override di questo valore e definire un intervallo di timeout come segue:  
  
-   Specificando un valore di timeout quando si crea un'istanza di un oggetto <xref:System.Text.RegularExpressions.Regex> chiamando il costruttore <xref:System.Text.RegularExpressions.Regex.%23ctor%28System.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=fullName>.  
  
-   Chiamando un metodo statico di corrispondenza dei modelli, come <xref:System.Text.RegularExpressions.Regex.Match%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=fullName> o <xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%2CSystem.TimeSpan%29?displayProperty=fullName>, che include un parametro `matchTimeout`.  
  
-   Per le espressioni regolari compilate che vengono create chiamando il metodo <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=fullName>, chiamando il costruttore con un parametro di tipo <xref:System.TimeSpan>.  
  
 Se è stato definito un intervallo di timeout e non viene trovata alcuna corrispondenza alla fine di questo intervallo, il metodo dell'espressione regolare genera un'eccezione <xref:System.Text.RegularExpressions.RegexMatchTimeoutException>.  Nel gestore eccezioni, è possibile continuare a cercare la corrispondenza con un intervallo di timeout più lungo, abbandonare il tentativo di ricerca supponendo che non esista alcuna corrispondenza oppure abbandonare il tentativo di ricerca e registrare le informazioni sull'eccezione per un'analisi futura.  
  
 Nell'esempio seguente viene definito un metodo `GetWordData` che crea un'istanza di un'espressione regolare con un intervallo di timeout di 350 millisecondi per calcolare il numero di parole e il numero medio di caratteri di una parola in un documento di testo.  Se l'operazione di ricerca della corrispondenza scade, l'intervallo di timeout viene aumentato di 350 millisecondi e viene nuovamente creata un'istanza dell'oggetto <xref:System.Text.RegularExpressions.Regex>.  Se il nuovo intervallo di timeout supera 1 secondo, il metodo genera nuovamente l'eccezione al chiamante.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/timeout1.cs#12)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/timeout1.vb#12)]  
  
 [Torna all'inizio](#top)  
  
<a name="Capture"></a>   
## Eseguire l'acquisizione solo quando necessario  
 Le espressioni regolari in .NET Framework supportano diversi costrutti di raggruppamento, che consentono di raggruppare un modello di espressione regolare in una o più sottoespressioni.  I costrutti di raggruppamento più comunemente usati nel linguaggio delle espressioni regolari di .NET Framework sono `(`*sottoespressione*`)`, che definisce un gruppo di acquisizione numerato, e `(?<`*nome*`>`*sottoespressione*`)`, che definisce un gruppo di acquisizione denominato.  I costrutti di raggruppamento sono indispensabili per la creazione di backreference e per la definizione di una sottoespressione a cui viene applicato un quantificatore.  
  
 Tuttavia, l'utilizzo di questi elementi del linguaggio ha un costo.  Comportano il popolamento dell'oggetto <xref:System.Text.RegularExpressions.GroupCollection> restituito dalla proprietà <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=fullName> con le acquisizioni non denominate o denominate più recenti e se un singolo costrutto di raggruppamento ha acquisito più sottostringhe nella stringa di input comportano anche il popolamento dell'oggetto <xref:System.Text.RegularExpressions.CaptureCollection> restituito dalla proprietà <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=fullName> di un gruppo di acquisizione specifico con più oggetti <xref:System.Text.RegularExpressions.Capture>.  
  
 I costrutti di raggruppamento spesso vengono utilizzati solo in un'espressione regolare in modo tale che sia possibile applicarvi i quantificatori e che i gruppi acquisiti da queste sottoespressioni non vengano utilizzati successivamente.  Ad esempio, l'espressione regolare `\b(\w+[;,]?\s?)+[.?!]` è progettata per acquisire un'intera frase.  Nella tabella seguente vengono descritti gli elementi del linguaggio di tale modello di espressione regolare e il relativo effetto sulle raccolte <xref:System.Text.RegularExpressions.Match> e <xref:System.Text.RegularExpressions.Match.Groups%2A?displayProperty=fullName> dell'oggetto <xref:System.Text.RegularExpressions.Group.Captures%2A?displayProperty=fullName>.  
  
|Modello|Descrizione|  
|-------------|-----------------|  
|`\b`|Inizia la corrispondenza sul confine di parola.|  
|`\w+`|Trova la corrispondenza di uno o più caratteri alfanumerici.|  
|`[;,]?`|Trova la corrispondenza di una o nessuna virgola oppure di uno o nessun punto e virgola.|  
|`\s?`|Trova la corrispondenza di uno o nessuno spazio vuoto.|  
|`(\w+[;,]?  \s?)+`|Trova la corrispondenza di una o più occorrenze di uno o più caratteri alfanumerici seguiti da una virgola o un punto e virgola facoltativo seguito da uno spazio vuoto facoltativo.  Questo modello definisce il primo gruppo di acquisizione, necessario affinché la combinazione di più caratteri alfanumerici, ovvero una parola, seguiti da un simbolo di punteggiatura facoltativo venga ripetuta finché il motore delle espressioni regolari non raggiunge la fine di una frase.|  
|`[.?!]`|Trova la corrispondenza di un punto, un punto interrogativo o un punto esclamativo.|  
  
 Come illustrato nell'esempio seguente, quando viene trovata una corrispondenza, entrambi gli oggetti <xref:System.Text.RegularExpressions.GroupCollection> e <xref:System.Text.RegularExpressions.CaptureCollection> vengono popolati con le acquisizioni della corrispondenza.  In questo caso, è presente il gruppo di acquisizione `(\w+[;,]?\s?)` in modo tale che sia possibile applicarvi il quantificatore `+` consentendo al criterio di espressione regolare di trovare la corrispondenza con ogni parola di una frase.  In caso contrario, verrebbe trovata la corrispondenza con l'ultima parola di una frase.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/group1.cs#8)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/group1.vb#8)]  
  
 Quando le sottoespressioni vengono utilizzate solo per applicarvi i quantificatori e non è necessario il testo acquisito, è consigliabile disabilitare le acquisizioni del gruppo.  Ad esempio, l'elemento del linguaggio `(?:``subexpression``)` impedisce al gruppo al quale viene applicato di acquisire le sottostringhe corrispondenti.  Nell'esempio seguente il criterio di espressione regolare dell'esempio precedente viene modificato in `\b(?:\w+[;,]?\s?)+[.?!]`.  Come illustrato nell'output, il motore delle espressioni regolari non popolerà le raccolte <xref:System.Text.RegularExpressions.GroupCollection> e <xref:System.Text.RegularExpressions.CaptureCollection>.  
  
 [!code-csharp[Conceptual.RegularExpressions.BestPractices#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/cs/group2.cs#9)]
 [!code-vb[Conceptual.RegularExpressions.BestPractices#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.bestpractices/vb/group2.vb#9)]  
  
 È possibile disabilitare le acquisizioni in uno dei modi seguenti:  
  
-   Utilizzare l'elemento del linguaggio `(?:``subexpression``)`.  Questo elemento impedisce l'acquisizione delle sottostringhe corrispondenti nel gruppo a cui viene applicato.  Non disabilita le acquisizioni delle sottostringhe in tutti i gruppi annidati.  
  
-   Usare l'opzione <xref:System.Text.RegularExpressions.RegexOptions>.  Disabilita tutte le acquisizioni non denominate o implicite nel modello di espressione regolare.  Quando si utilizza questa opzione, è possibile acquisire solo le sottostringhe che corrispondono ai gruppi denominati definiti con l'elemento del linguaggio `(?<``name``>``subexpression``)`.  Il flag <xref:System.Text.RegularExpressions.RegexOptions> può essere passato al parametro `options` del costruttore della classe <xref:System.Text.RegularExpressions.Regex> o al parametro `options` di un metodo <xref:System.Text.RegularExpressions.Regex> statico corrispondente.  
  
-   Utilizzare l'opzione `n` nell'elemento del linguaggio `(?imnsx)`.  Questa opzione disabilita tutte le acquisizioni non denominate o implicite dal punto nel modello di espressione regolare in corrispondenza del quale viene visualizzato l'elemento.  Le acquisizioni vengono disabilitate fino alla fine del modello o finché l'opzione `(-n)` non abilita le acquisizioni non denominate o implicite.  Per altre informazioni, vedere [Costrutti vari](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md).  
  
-   Usare l'opzione `n` nell'elemento del linguaggio `(?imnsx:``subexpression``)`.  Questa opzione disabilita tutte le acquisizioni non denominate o implicite in `subexpression`.  Vengono inoltre disabilitate tutte le acquisizioni dai gruppi di acquisizione annidati non denominati o impliciti.  
  
 [Torna all'inizio](#top)  
  
<a name="RelatedTopics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Dettagli sul comportamento delle espressioni regolari](../../../docs/standard/base-types/details-of-regular-expression-behavior.md)|Viene esaminata l'implementazione del motore delle espressioni regolari in .NET Framework.  L'argomento è incentrato sulla flessibilità delle espressioni regolari e sulla responsabilità dello sviluppatore al fine di garantire un funzionamento efficace e affidabile del motore delle espressioni regolari.|  
|[Backtracking](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)|Viene illustrato il backtracking e il modo in cui influisce sulle prestazioni delle espressioni regolari e vengono esaminati gli elementi del linguaggio che forniscono le alternative al backtracking.|  
|[Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)|Vengono illustrati gli elementi del linguaggio delle espressioni regolari in .NET Framework e vengono forniti i collegamenti alla documentazione dettagliata per ogni elemento del linguaggio.|