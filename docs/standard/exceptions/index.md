---
title: "Gestione e generazione di eccezioni | Microsoft Docs"
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
  - "Common Language Runtime, eccezioni"
  - "errori [.NET Framework], eccezioni"
  - "eccezioni [.NET Framework]"
  - "eccezioni [.NET Framework], gestione"
  - "eccezioni [.NET Framework], generazione"
  - "filtro di eccezioni"
  - "runtime, eccezioni"
ms.assetid: f99a1d29-a2a8-47af-9707-9909f9010735
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# Gestione e generazione di eccezioni
<a name="top"></a> Le applicazioni devono essere in grado di gestire in modo coerente gli errori che si verificano durante l'esecuzione. Common Language Runtime fornisce un modello per notificare gli errori alle applicazioni in modo uniforme. In tutte le operazioni di .NET Framework gli errori vengono indicati mediante la generazione di eccezioni.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Eccezioni in .NET Framework](#exceptions_in_the_net_framework)  
  
-   [Confronto tra eccezioni e metodi di gestione degli errori tradizionali](#exceptions_vs_traditional_errorhandling_methods)  
  
-   [Modalità di gestione delle eccezioni del runtime](#how_the_runtime_manages_exceptions)  
  
-   [Filtro delle eccezioni del runtime](#filtering_runtime_exceptions)  
  
-   [Argomenti correlati](#related_topics)  
  
-   [Riferimento](#reference)  
  
<a name="exceptions_in_the_net_framework"></a>   
## Eccezioni in .NET Framework  
 Un'eccezione è una condizione di errore o un comportamento imprevisto riscontrato da un programma in esecuzione. Le eccezioni possono essere generate in caso di errori nel codice dell'applicazione o nel codice chiamato \(ad esempio una libreria condivisa\), in caso di risorse del sistema operativo non disponibili, di condizioni impreviste riscontrate da Common Language Runtime \(ad esempio codice impossibile da verificare\) e così via. L'applicazione è in grado di gestire alcune di queste condizioni, altre no. Sebbene sia possibile gestire gran parte delle eccezioni dell'applicazione, la maggior parte delle eccezioni di runtime risulta ingestibile.  
  
 In .NET Framework, un'eccezione è un oggetto che eredita dalla classe <xref:System.Exception?displayProperty=fullName>. Le eccezioni vengono generate dalle aree di codice in cui si è verificato un problema. Ogni eccezione viene passata ai livelli superiori dello stack finché non viene gestita dall'applicazione o non si arresta il programma.  
  
 [Torna all'inizio](#top)  
  
<a name="exceptions_vs_traditional_errorhandling_methods"></a>   
## Confronto tra eccezioni e metodi di gestione degli errori tradizionali  
 In precedenza, il modello di gestione degli errori di un linguaggio si basava sul metodo specifico usato da tale linguaggio per rilevare gli errori e individuarne i gestori oppure sul meccanismo di gestione degli errori fornito dal sistema operativo. Nel runtime la gestione delle eccezioni viene implementata con le seguenti modalità:  
  
-   Indipendentemente dal linguaggio in cui vengono generate o gestite le singole eccezioni.  
  
-   Senza la necessità di una sintassi di linguaggio apposita, ma con la possibilità per ciascun linguaggio di definire la propria sintassi.  
  
-   Con la possibilità di generare eccezioni anche a livello di più processi e addirittura di più computer differenti.  
  
 Le eccezioni presentano vari vantaggi rispetto ad altri metodi di notifica degli errori, quali i codici restituiti. Gli errori vengono sempre rilevati. I valori non validi non continuano a propagarsi nel sistema. Non è necessario controllare i codici restituiti. È possibile aggiungere con facilità codice per la gestione delle eccezioni per aumentare l'affidabilità dei programmi. La gestione delle eccezioni nel runtime, infine, è più rapida rispetto alla gestione degli errori di C\+\+ per Windows.  
  
 Dal momento che i thread di esecuzione riguardano normalmente blocchi di codice gestiti e non gestiti, il runtime può generare o rilevare eccezioni sia nel codice gestito che nel codice non gestito. Nel codice non gestito possono essere incluse sia eccezioni SEH C\+\+ che HRESULT basati su COM.  
  
<a name="how_the_runtime_manages_exceptions"></a>   
## Modalità di gestione delle eccezioni del runtime  
 Il runtime usa un modello di gestione delle eccezioni basato su oggetti eccezione e blocchi di codice protetti. Quando si verifica un'eccezione viene creato un oggetto <xref:System.Exception> per rappresentarla.  
  
 Il runtime crea, per ciascun eseguibile, una tabella contenente informazioni sulle eccezioni. A ogni metodo dell'eseguibile è associata, nella tabella delle informazioni sulle eccezioni, una matrice di informazioni sulla gestione delle eccezioni, che può essere vuota. Ogni voce della matrice descrive un blocco di codice protetto, eventuali filtri di eccezioni associati a tale codice nonché eventuali gestori di eccezioni \(istruzioni `catch`\). Questa tabella delle eccezioni è estremamente efficiente e, finché non si verifica alcuna eccezione, non compromette in alcun modo le prestazioni, né in termini di tempo del processore né in termini di utilizzo della memoria. Le risorse vengono usate solo quando ha luogo un'eccezione.  
  
 La tabella di informazioni sulle eccezioni rappresenta quattro tipi di gestori di eccezioni per blocchi protetti:  
  
-   Un gestore `finally` che viene eseguito a ogni uscita dal blocco, indipendentemente dal fatto che si verifichi per un normale flusso di controllo o in seguito a un'eccezione non gestita.  
  
-   Un gestore fault che viene eseguito se si verifica un'eccezione, ma non al completamento del normale flusso del controllo.  
  
-   Un gestore filtrato in base al tipo che gestisce tutte le eccezioni di una classe specificata o delle relative classi derivate.  
  
-   Un gestore filtrato dall'utente che esegue codice specificato dall'utente per determinare se l'eccezione debba essere gestita dal gestore associato o passata al blocco protetto successivo.  
  
 In ciascun linguaggio questi gestori di eccezioni vengono implementati in base alle specifiche in esso definite. Visual Basic, ad esempio, consente di accedere al gestore filtrato dall'utente tramite un confronto tra variabili \(usando la parola chiave `When`\) nell'istruzione `catch`; C\#, per contro, non implementa il gestore filtrato dall'utente.  
  
 Quando si verifica un'eccezione, il runtime avvia un processo suddiviso in due fasi:  
  
1.  Il runtime cerca nella matrice il primo blocco protetto che risponde alle seguenti caratteristiche:  
  
    -   Protegge un'area che include l'istruzione attualmente in esecuzione.  
  
    -   Contiene un gestore di eccezioni oppure un filtro che gestisce l'eccezione.  
  
2.  Se è presente un blocco che soddisfa queste condizioni, il runtime crea un oggetto <xref:System.Exception> che descrive l'eccezione. Il runtime esegue quindi tutte le istruzioni `finally` o fault tra l'istruzione in cui si è verificata l'eccezione e l'istruzione che gestisce tale eccezione. L'ordine dei gestori di eccezioni è importante, dal momento che il gestore più interno viene valutato per primo. Si noti inoltre che i gestori di eccezioni possono accedere alle variabili locali e alla memoria locale della routine che intercetta l'eccezione, ma vanno persi gli eventuali valori intermedi presenti al momento della generazione dell'eccezione.  
  
     Se nel metodo corrente non è presente alcun blocco che soddisfa le condizioni indicate, il runtime esegue la ricerca in ciascun chiamante del metodo corrente, risalendo via via, in questo modo, i vari livelli dello stack. Se anche la ricerca effettuata tra i chiamanti ha esito negativo, il runtime consentirà al debugger di accedere all'eccezione. Se il debugger non è associabile all'eccezione, il runtime genererà l'evento <xref:System.AppDomain.UnhandledException?displayProperty=fullName>. Se non è presente alcun listener per l'evento, il runtime eseguirà il dump dell'analisi dello stack e terminerà l'applicazione.  
  
 [Torna all'inizio](#top)  
  
<a name="filtering_runtime_exceptions"></a>   
## Filtro delle eccezioni del runtime  
 È possibile filtrare le eccezioni intercettate e gestite in base al tipo o ad altri criteri definiti dall'utente.  
  
 I gestori filtrati in base al tipo gestiscono un tipo particolare di eccezione o le classi da esso derivate. L'esempio seguente illustra un gestore filtrato in base al tipo progettato per rilevare un'eccezione specifica, in questo caso <xref:System.IO.FileNotFoundException>.  
  
 [!code-cpp[CatchException#5](../../../samples/snippets/cpp/VS_Snippets_CLR/CatchException/CPP/catchexception3.cpp#5)]
 [!code-csharp[CatchException#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CatchException/CS/catchexception3.cs#5)]
 [!code-vb[CatchException#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CatchException/VB/catchexception3.vb#5)]  
  
 I gestori di eccezioni filtrati dall'utente intercettano e gestiscono le eccezioni in base a requisiti definiti dall'utente per le singole eccezioni. Per altre informazioni su questo tipo di filtro delle eccezioni, vedere [Uso di eccezioni specifiche in un blocco catch](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md).  
  
 [Torna all'inizio](#top)  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Classe e proprietà dell'eccezione](../../../docs/standard/exceptions/exception-class-and-properties.md)|Descrive gli elementi di un oggetto eccezione.|  
|[Gerarchia delle eccezioni](../../../docs/standard/exceptions/exception-hierarchy.md)|Descrive le eccezioni da cui deriva la maggior parte delle eccezioni.|  
|[Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)|Illustra come gestire le eccezioni tramite istruzioni catch, throw e finally.|  
|[Suggerimenti per le eccezioni](../../../docs/standard/exceptions/best-practices-for-exceptions.md)|Descrive alcuni metodi che è consigliabile adottare per la gestione delle eccezioni.|  
|[Gestione di eccezioni per interoperabilità COM](../../../docs/standard/exceptions/handling-com-interop-exceptions.md)|Descrive come gestire le eccezioni generate e intercettate in codice non gestito.|  
|[How to: Map HRESULTs and Exceptions](../../../docs/framework/interop/how-to-map-hresults-and-exceptions.md)|Descrive il mapping delle eccezioni tra codice gestito e non gestito.|  
  
<a name="reference"></a>   
## Riferimento  
 <xref:System.Exception?displayProperty=fullName>  
  
 <xref:System.ApplicationException?displayProperty=fullName>  
  
 <xref:System.SystemException?displayProperty=fullName>