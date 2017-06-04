---
title: "Suggerimenti per le eccezioni | Microsoft Docs"
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
  - "eccezioni, procedure ottimali"
ms.assetid: f06da765-235b-427a-bfb6-47cd219af539
caps.latest.revision: 28
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 28
---
# Suggerimenti per le eccezioni
Un'applicazione progettata correttamente gestisce eccezioni ed errori per impedire arresti anomali dell'applicazione.  In questo articolo vengono descritte le procedure consigliate per la gestione e la creazione di eccezioni.  
  
## Gestione delle eccezioni  
 Nell'elenco seguente vengono fornite indicazioni generali sulla gestione delle eccezioni nell'applicazione.  
  
-   Usare il codice di gestione delle eccezioni \(blocchi `try`\/`catch`\) in modo appropriato.  È inoltre possibile controllare a livello di codice una condizione che è probabile si verifichi senza ricorrere alla gestione delle eccezioni.  
  
     **Controlli a livello di codice**.  Nell'esempio seguente viene utilizzata un'istruzione `if` per controllare se una connessione è chiusa.  In caso contrario, nell'esempio viene chiusa la connessione anziché generare un'eccezione.  
  
     [!code-cpp[Conceptual.Exception.Handling#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#2)]
     [!code-csharp[Conceptual.Exception.Handling#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#2)]
     [!code-vb[Conceptual.Exception.Handling#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#2)]  
  
     **Gestione delle eccezioni**.  Nell'esempio seguente viene utilizzato un blocco `try`\/`catch` per verificare la connessione e generare un'eccezione se la connessione non è chiusa.  
  
     [!code-cpp[Conceptual.Exception.Handling#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#3)]
     [!code-csharp[Conceptual.Exception.Handling#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#3)]
     [!code-vb[Conceptual.Exception.Handling#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#3)]  
  
     Nella scelta del metodo è necessario considerare la frequenza con cui si prevede che l'evento possa verificarsi.  
  
    -   Usare la gestione delle eccezioni se l'evento non si verifica molto spesso, ovvero, se l'evento è davvero eccezionale e indica un errore quale la fine imprevista di un file.  Quando si utilizza la gestione delle eccezioni, una minore quantità di codice viene eseguita in condizioni normali.  
  
    -   Usare il metodo a livello di codice per verificare la presenza di errori se l'evento si verifica ripetutamente e può essere considerato parte dell'esecuzione normale.  Quando si effettua il controllo degli errori a livello di codice, viene eseguita una maggiore quantità di codice se si verifica un'eccezione.  
  
-   Usare i blocchi `try`\/`catch` intorno al codice che potrebbe potenzialmente generare un'eccezione e usare un blocco `finally` per eseguire la pulizia delle risorse, se necessario.  In questo modo l'istruzione `try` genera l'eccezione, l'istruzione `catch` la gestisce e l'istruzione `finally` chiude o dealloca le risorse a prescindere che l'eccezione venga generata o meno.  
  
-   Ordinare sempre le eccezioni in blocchi `catch` dalla più specifica alla meno specifica.  In questo modo l'eccezione specifica viene gestita prima di essere passata a un blocco `catch` più generico.  
  
## Creazione e generazione di eccezioni  
 Nell'elenco seguente sono riportate le linee guida per creare eccezioni personalizzate e quando devono essere generate.  Per informazioni dettagliate, vedere [Linee guida di progettazione per le eccezioni](../../../docs/standard/design-guidelines/exceptions.md).  
  
-   Progettare le classi in modo che non venga mai generata un'eccezione nell'utilizzo normale.  Con la classe <xref:System.IO.FileStream>, ad esempio, sono disponibili metodi che consentono di determinare se è stata raggiunta la fine del file.  Questo consente di evitare l'eccezione che verrebbe generata se si continua la lettura oltre il termine del file.  Nell'esempio che segue viene illustrato come terminare la lettura in corrispondenza della fine del file.  
  
     [!code-cpp[Conceptual.Exception.Handling#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#5)]
     [!code-csharp[Conceptual.Exception.Handling#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#5)]
     [!code-vb[Conceptual.Exception.Handling#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#5)]  
  
-   Generare eccezioni anziché restituire un codice di errore o HRESULT.  
  
-   Restituire il valore Null per i casi di errore estremamente comuni anziché generare un'eccezione.  Un caso di errore estremamente comune può essere considerato come un normale flusso di controllo.  Restituendo Null in questi casi, si riduce l'impatto sulle prestazioni di un'applicazione.  
  
-   Nella maggior parte dei casi usare i tipi di eccezione .NET Framework.  Introdurre una nuova classe di eccezioni solo quando non è possibile applicare una classe predefinita.  
  
-   Generare un'eccezione <xref:System.InvalidOperationException> se un set di proprietà o una chiamata al metodo non è adatta allo stato corrente dell'oggetto.  
  
-   Generare un'eccezione <xref:System.ArgumentException> o una classe derivata da <xref:System.ArgumentException> se vengono passati parametri non validi.  
  
-   Per la maggior parte delle applicazioni, derivare le eccezioni personalizzate dalla classe <xref:System.Exception>.  La derivazione dalla classe <xref:System.ApplicationException> non aggiunge valore significativo.  
  
-   Terminare i nomi delle classi di eccezioni con la parola "Exception".  Ad esempio:  
  
     [!code-cpp[Conceptual.Exception.Handling#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#4)]
     [!code-csharp[Conceptual.Exception.Handling#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#4)]
     [!code-vb[Conceptual.Exception.Handling#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#4)]  
  
-   In C\# e C\+\+, utilizzare almeno i tre costruttori comuni quando si creano classi di eccezione personalizzate: il costruttore predefinito, un costruttore che accetta un messaggio stringa e un costruttore che accetta un messaggio stringa e un'eccezione interna.  Per un esempio, vedere [Procedura: creare eccezioni definite dall'utente](../../../docs/standard/exceptions/how-to-create-user-defined-exceptions.md).  
  
    1.  <xref:System.Exception.%23ctor>, che utilizza valori predefiniti.  
  
    2.  <xref:System.Exception.%23ctor%28System.String%29>, che accetta un messaggio stringa.  
  
    3.  <xref:System.Exception.%23ctor%28System.String%2CSystem.Exception%29>, che accetta un messaggio stringa e un'eccezione interna.  
  
-   Quando si creano eccezioni definite dall'utente, è necessario garantire che i metadati relativi alle eccezioni siano disponibili per il codice eseguito in posizione remota, incluso il caso di eccezioni che si verificano a livello di più domini applicazione.  Si supponga ad esempio che nel dominio applicazione A venga creato il dominio applicazione B, nel quale viene eseguito codice che genera un'eccezione.  Per rilevare e gestire correttamente l'eccezione, il dominio applicazione A deve essere in grado di individuare l'assembly contenente l'eccezione generata dal dominio applicazione B.  Se il dominio applicazione B genera un'eccezione contenuta in un assembly nella base dell'applicazione di tale dominio, ma non nella base dell'applicazione del dominio applicazione A, quest'ultimo non sarà in grado di individuare l'eccezione e Common Language Runtime genererà un'eccezione <xref:System.IO.FileNotFoundException>.  Per evitare che questo si verifichi è possibile distribuire l'assembly contenente le informazioni sull'eccezione in due modi:  
  
    -   Inserendo l'assembly in una base applicativa comune condivisa da entrambi i domini applicazione  
  
         \-oppure\-  
  
    -   Se i domini non condividono alcuna base applicativa comune, firmando l'assembly contenente le informazioni sull'eccezione con un nome sicuro e distribuendo tale assembly nella Global Assembly Cache.  
  
-   Includere in ciascuna eccezione una stringa descrittiva localizzata.  Il messaggio di errore visualizzato all'utente viene tratto dalla stringa descrittiva dell'eccezione generata, anziché dalla classe di eccezione.  
  
-   Usare messaggi di errore corretti dal punto di vista grammaticale, inclusa la punteggiatura finale.  È necessario che ogni frase della stringa descrittiva di un'eccezione termini con un punto.  Ad esempio, "Overflow della tabella di log." è una stringa descrittiva appropriata.  
  
-   Fornire proprietà <xref:System.Exception> per l'accesso a livello di codice.  Fornire le proprietà aggiuntive di un'eccezione \(oltre alla stringa descrittiva\) solo nel caso di uno scenario a livello di codice in cui è utile disporre di altre informazioni.  Ad esempio, <xref:System.IO.FileNotFoundException> fornisce la proprietà <xref:System.IO.FileNotFoundException.FileName%2A>.  
  
-   La traccia dello stack inizia in corrispondenza dell'istruzione in cui l'eccezione viene generata e termina in corrispondenza dell'istruzione `catch` che intercetta l'eccezione.  Tenere presente questo fatto quando si decide in che punto inserire un'istruzione `throw`.  
  
-   Usare metodi per la creazione di eccezioni.  Una classe genera spesso la stessa eccezione da punti diversi dell'implementazione.  Per evitare codice di dimensioni eccessive, utilizzare metodi di supporto che creano l'eccezione e la restituiscono.  Ad esempio:  
  
     [!code-cpp[Conceptual.Exception.Handling#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.exception.handling/cpp/source.cpp#6)]
     [!code-csharp[Conceptual.Exception.Handling#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.exception.handling/cs/source.cs#6)]
     [!code-vb[Conceptual.Exception.Handling#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.exception.handling/vb/source.vb#6)]  
  
     In alternativa, utilizzare il costruttore dell'eccezione per compilare l'eccezione.  Questo è opportuno soprattutto per le classi di eccezione globali, ad esempio <xref:System.ArgumentException>.  
  
-   Eliminare i risultati intermedi quando si genera un'eccezione.  I chiamanti dovrebbero avere la garanzia che non si verifichino effetti secondari quando un'eccezione viene generata da un metodo.  
  
## Vedere anche  
 [Eccezioni](../../../docs/standard/exceptions/index.md)