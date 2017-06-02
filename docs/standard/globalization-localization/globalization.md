---
title: "Globalizzazione | Microsoft Docs"
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
  - "globalizzazione [.NET Framework], informazioni sulla globalizzazione"
  - "applicazioni globali, globalizzazione"
  - "applicazioni internazionali [.NET Framework], globalizzazione"
  - "applicazioni internazionalizzate, globalizzazione"
  - "sviluppo di applicazioni [.NET Framework], globalizzazione"
  - "impostazioni cultura, globalizzazione"
ms.assetid: 4e919934-6b19-42f2-b770-275a4fae87c9
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Globalizzazione
La globalizzazione comporta la progettazione e lo sviluppo di un'app internazionalizzata che supporti interfacce localizzate e dati locali per utenti in più impostazioni cultura. Prima di iniziare la fase di progettazione, è necessario determinare quali impostazioni cultura verranno supportate dall'app. Sebbene un'app sia destinata per impostazione predefinita a singole impostazioni cultura o a una singola area, è possibile progettarla e scriverla in modo che possa essere facilmente estesa agli utenti di altre impostazioni cultura o aree.  
  
 Gli sviluppatori partono sempre da supposizione su interfacce utente e dati che sono relativi alle impostazioni cultura. Ad esempio, per uno sviluppatore di lingua inglese negli Stati Uniti, la serializzazione di data e ora sotto forma di stringa nel formato `MM/dd/yyyy hh:mm:ss` sembra perfettamente ragionevole. Tuttavia, la deserializzazione di questa stringa in un sistema con impostazioni cultura diverse potrebbe generare un'eccezione <xref:System.FormatException> o dati non accurati. La globalizzazione consente di identificare queste supposizioni relative alle impostazioni cultura e di garantire che non influiscano sulla progettazione o sul codice dell'app.  
  
 Nelle sezioni seguenti vengono descritti alcuni dei principali aspetti da considerare e le procedure consigliate da seguire quando si gestiscono stringhe, valori di data e ora e valori numerici in un'app globalizzata.  
  
-   [Gestione delle stringhe](../../../docs/standard/globalization-localization/globalization.md#HandlingStrings)  
  
    -   [Utilizzare Unicode internamente](../../../docs/standard/globalization-localization/globalization.md#Strings_Unicode)  
  
    -   [Utilizzare file di risorse](../../../docs/standard/globalization-localization/globalization.md#Strings_Resources)  
  
    -   [Ricerca e confronto delle stringhe](../../../docs/standard/globalization-localization/globalization.md#Strings_Searching)  
  
    -   [Test dell'uguaglianza delle stringhe](../../../docs/standard/globalization-localization/globalization.md#Strings_Equality)  
  
    -   [Ordinamento delle stringhe](../../../docs/standard/globalization-localization/globalization.md#Strings_Ordering)  
  
    -   [Evitare la concatenazione di stringhe](../../../docs/standard/globalization-localization/globalization.md#Strings_Concat)  
  
-   [Gestione di date e ore](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes)  
  
    -   [Salvare in modo permanente date e ore](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_Persist)  
  
    -   [Visualizzazione di date e ore](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_Display)  
  
    -   [Presenza di fuso orario e serializzazione](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_TimeZones)  
  
    -   [Eseguire l'aritmetica di data e ora](../../../docs/standard/globalization-localization/globalization.md#DatesAndTimes_Arithmetic)  
  
-   [Gestione dei valori numerici](../../../docs/standard/globalization-localization/globalization.md#Numbers)  
  
    -   [Visualizzazione di valori numerici](../../../docs/standard/globalization-localization/globalization.md#Numbers_Display)  
  
    -   [Salvare in modo permanente i valori numerici](../../../docs/standard/globalization-localization/globalization.md#Numbers_Persist)  
  
-   [Utilizzo di impostazioni specifiche delle impostazioni cultura](../../../docs/standard/globalization-localization/globalization.md#Cultures)  
  
<a name="HandlingStrings"></a>   
## Gestione delle stringhe  
 La gestione di caratteri e stringhe è un elemento cruciale nella globalizzazione, in quanto le impostazioni cultura o area possono usare caratteri e set di caratteri diversi e ordinarli in modo diverso. Questa sezione include suggerimenti per l'uso delle stringhe nelle app globalizzate.  
  
<a name="Strings_Unicode"></a>   
### Utilizzare Unicode internamente  
 Per impostazione predefinita, .NET Framework usa stringhe Unicode. Una stringa Unicode è costituita da zero, da uno o più oggetti <xref:System.Char>, ognuno dei quali rappresenta un'unità di codice UTF\-16. Esiste una rappresentazione in formato Unicode di quasi tutti i caratteri inclusi nei set di caratteri usati nel mondo.  
  
 In molti sistemi operativi e applicazioni, incluso il sistema operativo Windows, è possibile usare anche tabelle codici per rappresentare i set di caratteri. Le tabelle codici in genere contengono i valori ASCII standard compresi tra 0x00 e 0x7F ed eseguono il mapping degli altri caratteri ai valori rimanenti compresi tra 0x80 e 0xFF. L'interpretazione dei valori da 0x80 a 0xFF dipende dalla tabella codici specifica. Per questo motivo, se possibile, è consigliabile evitare l'uso di tabelle codici in un'app globalizzata.  
  
 Nell'esempio seguente vengono illustrati i rischi di interpretazione dei dati della tabella codici quando la tabella codici predefinita in un sistema è diversa dalla tabella codici in cui i sono stati salvati i dati. Per simulare questo scenario, l'esempio specifica in modo esplicito tabelle codici diverse. Innanzitutto, nell'esempio viene definita una matrice costituita dai caratteri maiuscoli dell'alfabeto greco. I caratteri vengono codificati in una matrice di byte usando la tabella codici 737 \(nota anche come Greco MS\-DOS\) e la matrice di byte viene salvata in un file. Se viene recuperato il file e viene decodificata la relativa matrice di byte tramite la tabella codici 737, vengono ripristinati i caratteri originali. Tuttavia, se viene recuperato il file e viene decodificata la relativa matrice di byte usando la tabella codici 1252 \(o Windows\-1252, che rappresenta i caratteri nell'alfabeto latino\), i caratteri originali vengono persi.  
  
 [!code-csharp[Conceptual.Globalization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/codepages1.cs#1)]
 [!code-vb[Conceptual.Globalization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/codepages1.vb#1)]  
  
 L'uso di Unicode assicura che le stesse unità di codice eseguono sempre il mapping agli stessi caratteri e che gli stessi caratteri eseguono sempre il mapping alle stesse matrici di byte.  
  
<a name="Strings_Resources"></a>   
### Utilizzare file di risorse  
 Anche se si sviluppa un'app destinata a singole impostazioni cultura o aree, è necessario usare file di risorse per archiviare le stringhe e altre risorse visualizzate nell'interfaccia utente. Si raccomanda di non aggiungerli mai direttamente al codice. L'uso di file di risorse presenta una serie di vantaggi:  
  
-   Tutte le stringhe si trovano in un'unica posizione. Non è necessario eseguire la ricerca in tutto il codice di origine per identificare le stringhe da modificare per una lingua o impostazioni cultura specifiche.  
  
-   Non è necessario duplicare le stringhe. Gli sviluppatori che non usano file di risorse spesso definiscono la stessa stringa in più file di codice sorgente. Questa duplicazione aumenta la probabilità che una o più istanze possano essere ignorate quando viene modificata una stringa.  
  
-   È possibile includere risorse non di tipo stringa, ad esempio immagini o dati binari, nel file di risorse anziché archiviarle in un file autonomo separato, per poterle recuperare facilmente.  
  
 L'uso di file di risorse presenta vantaggi specifici se si crea un'app localizzata. Quando si distribuiscono le risorse in assembly satellite, Common Language Runtime seleziona automaticamente una risorsa di impostazioni cultura appropriata basata sulle impostazioni cultura dell'interfaccia utente corrente come specificato dalla proprietà <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>. Purché venga definita una risorsa specifica delle impostazioni cultura adatta e si crei correttamente un'istanza di un oggetto <xref:System.Resources.ResourceManager> o si usi una classe di risorse fortemente tipizzata, il runtime gestisce i dettagli relativi al recupero delle risorse appropriate.  
  
 Per altre informazioni sulla creazione di file di risorse, vedere [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md). Per informazioni sulla creazione e distribuzione di assembly satellite, vedere [Creazione di assembly satellite](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md) e [Creazione del pacchetto e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  
  
<a name="Strings_Searching"></a>   
### Ricerca e confronto delle stringhe  
 Quando possibile, si raccomanda di gestire le stringhe come unità intere, anziché come serie di caratteri singoli. Ciò è particolarmente importante quando si ordinano o cercano le sottostringhe, per impedire problemi associati all'analisi dei caratteri combinati.  
  
> [!TIP]
>  È possibile usare la classe <xref:System.Globalization.StringInfo> per gestire gli elementi di testo anziché i singoli caratteri in una stringa.  
  
 Nelle ricerche e nei confronti di stringhe, un errore comune consiste nel gestire la stringa come una raccolta di caratteri, ognuno dei quali è rappresentato da un oggetto <xref:System.Char>. Infatti, un singolo carattere può essere costituito da uno, due o più oggetti <xref:System.Char>. Caratteri di questo tipo vengono trovati più frequentemente nelle stringhe delle impostazioni cultura i cui alfabeti sono costituiti da caratteri esterni all'intervallo di caratteri latini di base Unicode \(da U\+0021 a U\+007E\). Nell'esempio seguente si tenta di trovare l'indice del carattere LETTERA LATINA A MAIUSCOLA CON accento GRAVE \(U\+00C0\) in una stringa. Tuttavia, questo carattere può essere rappresentato in due modi diversi: come singola unità di codice \(U\+00C0\) o come carattere composito \(due unità di codice: U\+0021 e U\+007E\). In questo caso, il carattere è rappresentato nell'istanza della stringa da due oggetti <xref:System.Char>, U\+0021 e U\+007E. Il codice di esempio chiama gli overload <xref:System.String.IndexOf%28System.Char%29?displayProperty=fullName> e <xref:System.String.IndexOf%28System.String%29?displayProperty=fullName> per trovare la posizione del carattere incluso nell'istanza della stringa, ma questi restituiscono risultati diversi. La prima chiamata al metodo dispone di un argomento <xref:System.Char>; esegue un confronto ordinale e pertanto non può trovare una corrispondenza. La seconda chiamata dispone di un argomento <xref:System.String>; esegue un confronto dipendente dalle impostazioni cultura e pertanto trova una corrispondenza.  
  
 [!code-csharp[Conceptual.Globalization#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/search1.cs#18)]
 [!code-vb[Conceptual.Globalization#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/search1.vb#18)]  
  
 È possibile evitare parte dell'ambiguità di questo esempio \(chiamate a due overload simili di un metodo che restituisce risultati diversi\) chiamando un overload che include un parametro <xref:System.StringComparison>, ad esempio il metodo <xref:System.String.IndexOf%28System.String%2CSystem.StringComparison%29?displayProperty=fullName> o <xref:System.String.LastIndexOf%28System.String%2CSystem.StringComparison%29?displayProperty=fullName>.  
  
 Tuttavia, le ricerche non sono sempre dipendenti dalle impostazioni cultura. Se lo scopo della ricerca è prendere una decisione relativa alla sicurezza oppure consentire o impedire l'accesso ad alcune risorse, il confronto deve essere ordinale, come descritto nella sezione successiva.  
  
<a name="Strings_Equality"></a>   
### Test dell'uguaglianza delle stringhe  
 Se si vuole verificare l'uguaglianza di due stringhe anziché determinare la relativa modalità di confronto nell'ordinamento, usare il metodo <xref:System.String.Equals%2A?displayProperty=fullName> anziché un metodo di confronto di stringhe, quale <xref:System.String.Compare%2A?displayProperty=fullName> o <xref:System.Globalization.CompareInfo.Compare%2A?displayProperty=fullName>.  
  
 I confronti di uguaglianza in genere vengono eseguiti i per accedere ad alcune risorse in modo condizionale. Ad esempio, è possibile eseguire un confronto di uguaglianza per verificare una password o l'esistenza di un file. Confronti non linguistici di questo tipo devono essere ordinali anziché dipendenti dalle impostazioni cultura. In genere, è consigliabile chiamare il metodo <xref:System.String.Equals%28System.String%2CSystem.StringComparison%29?displayProperty=fullName> dell'istanza o il metodo <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=fullName> statico con un valore <xref:System.StringComparison?displayProperty=fullName> per stringhe quali le password e un valore <xref:System.StringComparison?displayProperty=fullName> per stringhe quali i nomi file o gli URI.  
  
 I confronti di uguaglianza talvolta comportano ricerche o confronti delle sottostringhe anziché chiamate al metodo <xref:System.String.Equals%2A?displayProperty=fullName>. In alcuni casi, si potrebbe usare la ricerca di una sottostringa per determinare se la sottostringa è uguale a un'altra stringa. Se lo scopo di questo confronto non è linguistico, anche la ricerca deve essere ordinale anziché dipendente dalle impostazioni cultura.  
  
 Nell'esempio seguente viene illustrato il rischio di una ricerca dipendente dalle impostazioni cultura su dati non linguistici. Il metodo `AccessesFileSystem` è progettato per impedire l'accesso al file system agli URI che iniziano con la sottostringa "FILE". A tale scopo, esegue un confronto dipendente dalle impostazioni cultura, con distinzione tra maiuscole e minuscole, dell'inizio dell'URI con la stringa "FILE". Poiché un'URI che accede al file system può iniziare con "FILE:" o "file:", il presupposto implicito è che la "i" \(U\+0069\) è sempre l'equivalente minuscolo di "I" \(U\+0049\). Tuttavia, in turco e in azero, la versione maiuscola di "i" è "İ" \(U\+0130\). A causa di questa discrepanza, il confronto dipendente dalle impostazioni cultura consente l'accesso al file system anche se non dovesse essere consentito.  
  
 [!code-csharp[Conceptual.Globalization#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/equals1.cs#12)]
 [!code-vb[Conceptual.Globalization#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/equals1.vb#12)]  
  
 È possibile evitare questo problema eseguendo un confronto ordinale che ignora le maiuscole e minuscole, come illustrato nell'esempio di seguito.  
  
 [!code-csharp[Conceptual.Globalization#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/equals2.cs#13)]
 [!code-vb[Conceptual.Globalization#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/equals2.vb#13)]  
  
<a name="Strings_Ordering"></a>   
### Ordinamento delle stringhe  
 In genere, le stringhe ordinate da visualizzare nell'interfaccia utente devono essere ordinate in base alle impostazioni cultura. Nella maggior parte dei casi, questi confronti di stringhe vengono gestiti in modo implicito da .NET Framework quando si chiama un metodo che ordina stringhe, ad esempio <xref:System.Array.Sort%2A?displayProperty=fullName> o <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=fullName>. Per impostazione predefinita, le stringhe vengono ordinate usando le convenzioni di ordinamento delle impostazioni cultura correnti. Nell'esempio seguente viene illustrata la differenza quando viene ordinata una matrice di stringhe usando le convenzioni delle impostazioni cultura inglese \(Stati Uniti\) e le impostazioni cultura svedese \(Svezia\).  
  
 [!code-csharp[Conceptual.Globalization#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/sort1.cs#14)]
 [!code-vb[Conceptual.Globalization#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/sort1.vb#14)]  
  
 Il confronto di stringhe dipendenti dalle impostazioni cultura viene definito dall'oggetto <xref:System.Globalization.CompareInfo>, restituito dalla proprietà <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=fullName> delle singole impostazioni cultura. I confronti di stringhe dipendenti dalle impostazioni cultura che usano gli overload del metodo <xref:System.String.Compare%2A?displayProperty=fullName> usano anche l'oggetto <xref:System.Globalization.CompareInfo>.  
  
 .NET Framework usa tabelle per eseguire ordinamenti dipendenti dalle impostazioni cultura sui dati di tipo stringa. Il contenuto delle tabelle, che contengono dati sui fattori di ordinamento e sulla normalizzazione delle stringhe, è determinato dalla versione standard Unicode implementata da una determinata versione di .NET Framework. Nella tabella riportata di seguito sono elencate le versioni di Unicode implementate dalle versioni specifiche di .NET Framework. Si noti che l'elenco delle versioni supportate da Unicode si applica soltanto al confronto dei caratteri e all'ordinamento alfabetico; non si applica alla classificazione di caratteri Unicode in base alla categoria. Per altre informazioni, vedere la sezione "Stringhe e standard Unicode" nell'articolo <xref:System.String>.  
  
|Versione di .NET Framework|Sistema operativo|Versione Unicode|  
|--------------------------------|-----------------------|----------------------|  
|.NET Framework 2.0|Tutti i sistemi operativi|Unicode 4.1|  
|.NET Framework 3.0|Tutti i sistemi operativi|Unicode 4.1|  
|.NET Framework 3.5|Tutti i sistemi operativi|Unicode 4.1|  
|.NET Framework 4|Tutti i sistemi operativi|Unicode 5.0|  
|.NET Framework 4.5|[!INCLUDE[win7](../../../includes/win7-md.md)]|Unicode 5.0|  
|.NET Framework 4.5|[!INCLUDE[win8](../../../includes/win8-md.md)]|Unicode 6.0|  
  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] il confronto e l'ordinamento di stringhe dipendono dal sistema operativo.[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] in esecuzione su [!INCLUDE[win7](../../../includes/win7-md.md)] recupera i dati dalle rispettive tabelle che implementano il formato Unicode 5.0.[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] in esecuzione su [!INCLUDE[win8](../../../includes/win8-md.md)] recupera i dati dalle tabelle del sistema operativo che implementano il formato Unicode 6.0. Se si serializzano i dati ordinati dipendenti dalle impostazioni cultura, è possibile usare la classe <xref:System.Globalization.SortVersion> per determinare se i dati serializzati devono essere ordinati in modo che siano coerenti con .NET Framework e con l'ordinamento del sistema operativo. Per un esempio, vedere l'argomento relativo alla classe <xref:System.Globalization.SortVersion>.  
  
 Se l'app esegue ordinamenti estesi specifici delle impostazioni cultura di dati stringa, è possibile usare la classe <xref:System.Globalization.SortKey> per confrontare le stringhe. Una chiave di ordinamento riflette i fattori di ordinamento specifici alle impostazioni cultura, inclusi i caratteri alfabetici, i caratteri maiuscoli e minuscoli e i segni diacritici di una determinata stringa. Poiché i confronti che usano le chiavi di ordinamento sono binari, risultano più veloci dei confronti che usano un oggetto <xref:System.Globalization.CompareInfo> in modo implicito o esplicito. Si deve creare una chiave di ordinamento specifico delle impostazioni cultura per una determinata stringa passando la stringa al metodo <xref:System.Globalization.CompareInfo.GetSortKey%2A?displayProperty=fullName>.  
  
 L'esempio seguente è simile all'esempio precedente. Tuttavia, anziché chiamare il metodo <xref:System.Array.Sort%28System.Array%29?displayProperty=fullName>, che chiama in modo implicito il metodo <xref:System.Globalization.CompareInfo.Compare%2A?displayProperty=fullName>, viene definita un'implementazione <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> che confronta le chiavi di ordinamento di cui viene creata un'istanza e vengono passate al metodo [Array.Sort\<T\>\(T\<xref:System.Array.Sort%60%601%28%60%600%5B%5D%2CSystem.Collections.Generic.IComparer%7B%60%600%7D%29?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.Globalization#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/sortkey1.cs#15)]
 [!code-vb[Conceptual.Globalization#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/sortkey1.vb#15)]  
  
<a name="Strings_Concat"></a>   
### Evitare la concatenazione di stringhe  
 Se possibile, evitare l'uso di stringhe composite che vengono compilate in fase di esecuzione da frasi concatenate. Le stringhe composite sono difficili da localizzare, in quanto richiedono spesso un ordine grammaticale nel linguaggio originale dell'app che non è applicabile ad altre lingue localizzate.  
  
<a name="DatesAndTimes"></a>   
## Gestione di date e ore  
 La modalità di gestione dei valori di data e ora dipende se vengono visualizzati nell'interfaccia utente o resi persistenti. In questa sezione vengono esaminati entrambi gli usi. Viene inoltre descritto come gestire le differenze di fuso orario e le operazioni aritmetiche quando si usano date e ore.  
  
<a name="DatesAndTimes_Display"></a>   
### Visualizzazione di date e ore  
 In genere, quando le date e le ore sono visualizzate nell'interfaccia utente, è consigliabile usare le convenzioni di formattazione delle impostazioni cultura dell'utente, definite dalla proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e dall'oggetto <xref:System.Globalization.DateTimeFormatInfo> restituito dalla proprietà `CultureInfo.CurrentCulture.DateTimeFormat`. Le convenzioni di formattazione delle impostazioni cultura correnti vengono automaticamente usate quando si formatta una data tramite uno di questi metodi:  
  
-   Il metodo <xref:System.DateTime.ToString?displayProperty=fullName> senza parametri  
  
-   Il metodo <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName>, che include una stringa di formato  
  
-   Il metodo <xref:System.DateTimeOffset.ToString?displayProperty=fullName> senza parametri  
  
-   Il metodo <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName>, che include una stringa di formato  
  
-   La funzionalità di [formattazione composita](../../../docs/standard/base-types/composite-formatting.md), quando viene usata con le date  
  
 Nell'esempio seguente vengono visualizzati due volte i dati di tramonto e di alba dell'11 ottobre 2012. Innanzitutto vengono impostate le impostazioni cultura correnti su Croato \(Croazia\) e, successivamente, su Inglese \(Gran Bretagna\). In entrambi i casi, le date e le ore verranno visualizzate nel formato appropriato per le impostazioni cultura specifiche.  
  
 [!code-csharp[Conceptual.Globalization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates1.cs#2)]
 [!code-vb[Conceptual.Globalization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates1.vb#2)]  
  
<a name="DatesAndTimes_Persist"></a>   
### Salvare in modo permanente date e ore  
 È consigliabile non salvare in modo permanente i valori di data e ora in un formato che può variare in base alle impostazioni cultura. Si tratta di un errore di programmazione comune che restituisce dati danneggiati o eccezione di runtime. L'esempio seguente serializza due date, 9 gennaio 2013 e 18 agosto 2013, come stringhe usando le convenzioni di formattazione delle impostazioni cultura inglese \(Stati Uniti\). I dati recuperati e analizzati mediante le convenzioni delle impostazioni cultura inglese \(Stati Uniti\) vengono ripristinati correttamente. Tuttavia, quando viene recuperata e analizzata tramite le convenzioni delle impostazioni cultura inglese \(Regno Unito\), la prima data viene interpretata in modo errato come 1° settembre e la seconda non viene analizzata perché il calendario gregoriano non dispone di un diciottesimo mese.  
  
 [!code-csharp[Conceptual.Globalization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates2.cs#3)]
 [!code-vb[Conceptual.Globalization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates2.vb#3)]  
  
 È possibile evitare questo problema in tre modi:  
  
-   Serializzare la data e l'ora in formato binario anziché come stringa.  
  
-   Salvare e analizzare la rappresentazione della stringa di data e ora usando una stringa di formato personalizzato uguale, indipendentemente dalle impostazioni cultura dell'utente.  
  
-   Salvare la stringa usando le convenzioni di formattazione della cultura invariabile.  
  
 L'ultimo approccio viene illustrato nell'esempio seguente. Vengono usate le convenzioni di formattazione della cultura invariabile restituita dalla proprietà statica <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.Globalization#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates3.cs#4)]
 [!code-vb[Conceptual.Globalization#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates3.vb#4)]  
  
<a name="DatesAndTimes_TimeZones"></a>   
### Presenza di fuso orario e serializzazione  
 Un valore di data e ora può avere più interpretazioni, a partire da un'ora generale \(Gli archivi vengono aperti il 2 gennaio 2013 alle 9:00\) a un momento specifico \("Data di nascita: 2 gennaio 2013 6.32.00"\). Quando un valore di ora rappresenta un momento specifico e si ripristina da un valore serializzato, è necessario assicurarsi che rappresenti lo stesso momento indipendentemente dalla posizione geografica o dal fuso orario dell'utente.  
  
 L'esempio seguente illustra questo problema. Viene salvato un singolo valore locale di data e ora come stringa in tre [formati standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md) \("G" per ora estesa e data generale, "S" per data\/ora ordinabile e "O" per data\/ora roundtrip\), nonché in formato binario.  
  
 [!code-csharp[Conceptual.Globalization#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates4.cs#10)]
 [!code-vb[Conceptual.Globalization#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates4.vb#10)]  
  
 Quando i dati vengono ripristinati in un sistema con lo stesso fuso orario del sistema su cui sono stati serializzati, i valori di data e ora deserializzati riflettono accuratamente il valore originale, come mostra l'output:  
  
```  
  
'3/30/2013 6:00:00 PM' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00.0000000-07:00' --> 3/30/2013 6:00:00 PM Local  
  
3/30/2013 6:00:00 PM Local  
  
```  
  
 Tuttavia, se si ripristinano i dati in un sistema con un fuso orario diverso, solo il valore di data e orario formattato con la stringa di formato standard "O" \(roundtrip\) conserva le informazioni sul fuso orario e pertanto rappresenta lo stesso istante di tempo. Di seguito è riportato l'output quando i dati relativi a data e ora vengono ripristinati in un sistema con fuso orario standard dell'Europa occidentale:  
  
```  
  
'3/30/2013 6:00:00 PM' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00' --> 3/30/2013 6:00:00 PM Unspecified  
'2013-03-30T18:00:00.0000000-07:00' --> 3/31/2013 3:00:00 AM Local  
  
3/30/2013 6:00:00 PM Local  
  
```  
  
 Per riflettere in modo preciso un valore di data e ora che rappresenta un singolo momento di tempo indipendentemente dal fuso orario del sistema in cui i dati sono deserializzati, è possibile eseguire una delle seguenti operazioni:  
  
-   Salvare il valore come stringa usando la stringa di formato standard \(round trip\) "O". Quindi deserializzarlo nel sistema di destinazione.  
  
-   Convertirlo in UTC e salvarlo come stringa usando la stringa di formato standard "R" \(RFC1123\). Quindi deserializzarlo nel sistema di destinazione e convertirlo in un'ora locale.  
  
-   Convertirlo in UTC e salvarlo come stringa usando la stringa di formato standard "U" \(ordinabile universale\). Quindi deserializzarlo nel sistema di destinazione e convertirlo in un'ora locale.  
  
-   Convertirlo in UTC e salvarlo in formato binario. Quindi deserializzarlo nel sistema di destinazione e convertirlo in un'ora locale.  
  
 Ogni tecnica viene illustrata nell'esempio riportato di seguito.  
  
 [!code-csharp[Conceptual.Globalization#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates8.cs#11)]
 [!code-vb[Conceptual.Globalization#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates8.vb#11)]  
  
 Quando i dati vengono serializzati in un sistema nel fuso orario del Pacifico e deserializzati in un sistema nel fuso orario dell'Europa occidentale, l'esempio visualizza il seguente output:  
  
```  
  
'2013-03-30T18:00:00.0000000-07:00' --> 3/31/2013 3:00:00 AM Local  
'Sun, 31 Mar 2013 01:00:00 GMT' --> 3/31/2013 3:00:00 AM Local  
'2013-03-31 01:00:00Z' --> 3/31/2013 3:00:00 AM Local  
  
3/31/2013 3:00:00 AM Local  
  
```  
  
 Per altre informazioni, vedere [Conversione degli orari tra fusi orari](../../../docs/standard/datetime/converting-between-time-zones.md).  
  
<a name="DatesAndTimes_Arithmetic"></a>   
### Eseguire l'aritmetica di data e ora  
 Entrambi i tipi <xref:System.DateTime> e <xref:System.DateTimeOffset> supportano le operazioni aritmetiche. È possibile calcolare la differenza tra due valori di data, oppure aggiungere o sottrarre intervalli di tempo particolari a o da un valore di data. Tuttavia, nelle operazioni aritmetiche sui valori di data e ora non vengono presi in considerazione i fusi orari e le relative norme di regolazione. Per questo motivo, le operazioni aritmetiche con date e ore sui valori che rappresentano determinati momenti possono restituire risultati imprecisi.  
  
 Ad esempio, la transizione dall'ora solare Pacifico all'ora legale Pacifico si verifica la seconda domenica di marzo, cioè il 10 marzo per l'anno 2013. Come illustrato nell'esempio seguente, se si calcola la data e l'ora, vale a dire 48 ore dopo le 10.30 del 9 marzo 2013 in un sistema con ora solare Pacifico \(Stati Uniti\), il risultato, 10.30 dell'11 marzo 2013, non tiene conto della regolazione dell'ora.  
  
 [!code-csharp[Conceptual.Globalization#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates5.cs#8)]
 [!code-vb[Conceptual.Globalization#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates5.vb#8)]  
  
 Per assicurarsi che un'operazione aritmetica sui valori di data e ora produca risultati accurati, attenersi alla seguente procedura:  
  
1.  Convertire l'ora nel fuso orario di origine in ora UTC.  
  
2.  Eseguire l'operazione aritmetica.  
  
3.  Se il risultato è un valore di data e ora, convertirlo dall'ora UTC all'ora del fuso orario di origine.  
  
 L'esempio seguente è simile a quello precedente, con la differenza che segue questi tre passaggi correttamente per aggiungere 48 ore alle 10.30 del 9 marzo 2013.  
  
 [!code-csharp[Conceptual.Globalization#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates6.cs#9)]
 [!code-vb[Conceptual.Globalization#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates6.vb#9)]  
  
 Per altre informazioni, vedere [Esecuzione di operazioni aritmetiche con date e ore](../../../docs/standard/datetime/performing-arithmetic-operations.md).  
  
### Utilizzo dei nomi dipendenti delle impostazioni cultura per gli elementi di dati  
 È possibile che l'app debba visualizzare il nome del mese o il giorno della settimana. A tale scopo, il codice come il seguente è comune.  
  
 [!code-csharp[Conceptual.Globalization#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/monthname1.cs#19)]
 [!code-vb[Conceptual.Globalization#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/monthname1.vb#19)]  
  
 Tuttavia, tramite il codice vengono restituiti sempre i nomi dei giorni della settimana in inglese. Il codice che estrae il nome del mese è spesso più flessibile. Spesso si presuppone un calendario di dodici mesi con i nomi dei mesi in una lingua specifica.  
  
 Usando le [stringhe di formato di data e ora personalizzate](../../../docs/standard/base-types/custom-date-and-time-format-strings.md) o le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo>, è facile estrarre le stringhe che riflettono i nomi dei giorni della settimana o dei mesi nelle impostazioni cultura dell'utente, come illustrato nell'esempio seguente. Vengono impostate le impostazioni cultura correnti su Francese \(Francia\) e vengono visualizzati il nome del giorno della settimana e il nome del mese per il 1° luglio 2013.  
  
 [!code-csharp[Conceptual.Globalization#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/monthname2.cs#20)]
 [!code-vb[Conceptual.Globalization#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/monthname2.vb#20)]  
  
<a name="Numbers"></a>   
## Gestione dei valori numerici  
 La gestione di numeri dipende se vengono visualizzati nell'interfaccia utente o resi persistenti. In questa sezione vengono esaminati entrambi gli usi.  
  
> [!NOTE]
>  Nelle operazioni di analisi e formattazione, .NET Framework riconosce solo i caratteri latini di base da 0 a 9 \(da U\+0030 a U\+0039\) come cifre numeriche.  
  
<a name="Numbers_Display"></a>   
### Visualizzazione di valori numerici  
 In genere, quando i numeri sono visualizzati nell'interfaccia utente, è consigliabile usare le convenzioni di formattazione delle impostazioni cultura dell'utente, definite nella proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e dall'oggetto <xref:System.Globalization.NumberFormatInfo> restituito dalla proprietà `CultureInfo.CurrentCulture.NumberFormat`. Le convenzioni di formattazione delle impostazioni cultura correnti vengono automaticamente usate quando si formatta una data tramite uno dei seguenti metodi:  
  
-   Il metodo `ToString` senza parametri di qualsiasi tipo numerico  
  
-   Il metodo `ToString(String)` di qualsiasi tipo numerico, che include una stringa di formato come argomento  
  
-   La funzionalità di [formattazione composita](../../../docs/standard/base-types/composite-formatting.md), quando viene usata con valori numerici  
  
 L'esempio seguente consente di visualizzare la temperatura mensile media di Parigi, Francia. Innanzitutto vengono impostate le impostazioni cultura correnti su Francese \(Francia\) prima di visualizzare i dati e, successivamente, vengono impostate su Inglese \(Stati Uniti\). In ogni caso, le temperature e i nomi dei mesi verranno visualizzati nel formato appropriato per le impostazioni cultura in questione. Si noti che nelle due impostazioni cultura vengono usati separatori decimali diversi per il valore della temperatura. Si noti inoltre che in questo esempio viene usata la stringa di formato di data e ora personalizzata "MMMM" per visualizzare il nome completo dei mesi e che viene allocata la quantità di spazio appropriata per il nome del mese nella stringa di risultato determinando la lunghezza del nome del mese più lungo nella matrice <xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.Globalization#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers1.cs#5)]
 [!code-vb[Conceptual.Globalization#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers1.vb#5)]  
  
<a name="Numbers_Persist"></a>   
### Salvare in modo permanente i valori numerici  
 È consigliabile non salvare in maniera permanente i dati numerici in un formato specifico delle impostazioni cultura. Si tratta di un errore di programmazione comune che restituisce dati danneggiati o eccezione di runtime. L'esempio seguente genera dieci numeri a virgola mobile casuali e li serializza come stringhe usando le convenzioni di formattazione delle impostazioni cultura della lingua inglese \(Stati Uniti\). I dati recuperati e analizzati mediante le convenzioni delle impostazioni cultura inglese \(Stati Uniti\) vengono ripristinati correttamente. Tuttavia, quando vengono recuperati e analizzati usando le convenzioni delle impostazioni cultura Francese \(Francia\), nessuno dei numeri può essere analizzato in quanto vengono usati separatori decimali diversi nelle impostazioni cultura.  
  
 [!code-csharp[Conceptual.Globalization#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers2.cs#6)]
 [!code-vb[Conceptual.Globalization#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers2.vb#6)]  
  
 Per evitare questo problema, usare una delle seguenti tecniche:  
  
-   Salvare e analizzare la rappresentazione di stringa del numero usando una stringa di formato personalizzata uguale indipendentemente dalle impostazioni cultura dell'utente.  
  
-   Salvare il numero come stringa usando le convenzioni di formattazione della lingua inglese restituita dalla proprietà <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  
  
-   Serializzare il numero in formato di file binario anziché in formato stringa.  
  
 L'ultimo approccio viene illustrato nell'esempio seguente. Viene serializzata la matrice di valori <xref:System.Double> e, successivamente, i valori in questione vengono deserializzati e visualizzati usando le convenzioni di formattazione delle impostazioni cultura inglese \(Stati Uniti\) e francese \(Francia\).  
  
 [!code-csharp[Conceptual.Globalization#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers3.cs#7)]
 [!code-vb[Conceptual.Globalization#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers3.vb#7)]  
  
 La serializzazione dei valori di valuta è un caso speciale. Poiché un valore di valuta dipende dall'unità di valuta in cui viene espresso, non è opportuno considerarlo un valore numerico indipendente. Tuttavia, se si salva un valore di valuta come stringa formattata in cui è incluso un simbolo di valuta, non è possibile deserializzarlo in un sistema in cui le impostazioni cultura predefinite usano un simbolo di valuta diverso, come illustrato nell'esempio di seguito.  
  
 [!code-csharp[Conceptual.Globalization#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/currency1.cs#16)]
 [!code-vb[Conceptual.Globalization#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/currency1.vb#16)]  
  
 In alternativa, serializzare il valore numerico con alcune informazioni relative alle impostazioni cultura, ad esempio il nome delle impostazioni cultura, in modo che il valore e il relativo simbolo di valuta possano essere deserializzati indipendentemente dalle impostazioni cultura correnti. Nell'esempio seguente viene definita una struttura `CurrencyValue` con due membri: il valore <xref:System.Decimal> e il nome delle impostazioni cultura a cui appartiene il valore.  
  
 [!code-csharp[Conceptual.Globalization#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/currency2.cs#17)]
 [!code-vb[Conceptual.Globalization#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/currency2.vb#17)]  
  
<a name="Cultures"></a>   
## Utilizzo di impostazioni specifiche delle impostazioni cultura  
 In .NET Framework la classe <xref:System.Globalization.CultureInfo> rappresenta particolari impostazioni cultura o area. Alcune proprietà restituiscono oggetti che includono informazioni specifiche su alcuni aspetti delle impostazioni cultura:  
  
-   La proprietà <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Globalization.CompareInfo> che contiene informazioni relative a come le impostazioni cultura confrontano e ordinano le stringhe.  
  
-   La proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Globalization.DateTimeFormatInfo> che contiene informazioni sulle impostazioni cultura specifiche usate per la formattazione dei dati di data e ora.  
  
-   La proprietà <xref:System.Globalization.CultureInfo.NumberFormat%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Globalization.NumberFormatInfo> che contiene informazioni sulle impostazioni cultura specifiche usate per la formattazione dei dati numerici.  
  
-   La proprietà <xref:System.Globalization.CultureInfo.TextInfo%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Globalization.TextInfo> che contiene informazioni sul sistema di scrittura di una cultura.  
  
 In genere, non fare supposizioni sui valori della proprietà <xref:System.Globalization.CultureInfo> specifiche e sui relativi oggetti correlati. Considerare invece i dati specifici delle impostazioni cultura come elementi soggetti a modifiche, per questi motivi:  
  
-   I singoli valori di proprietà sono soggetti a modifiche e revisioni nel tempo, poiché i dati vengono corretti, si rendono disponibili dati migliori o si apportano modifiche di convenzioni specifiche delle impostazioni cultura.  
  
-   I singoli valori di proprietà possono variare tra le diverse versioni di .NET Framework o del sistema operativo.  
  
-   .NET Framework supporta impostazioni cultura sostitutive. Ciò consente di definire nuove impostazioni cultura personalizzate che completano le impostazioni cultura standard esistenti o li sostituiscono completamente.  
  
-   L'utente può personalizzare le impostazioni specifiche di una cultura usando l'app **Area e lingua** nel Pannello di controllo. Quando viene creata un'istanza di un oggetto <xref:System.Globalization.CultureInfo>, è possibile determinare se rifletta le personalizzazioni dell'utente chiamando il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName>. In genere, per le app degli utenti finali, è necessario rispettare le preferenze dell'utente in modo da offrirgli i dati in un formato che l'utente si aspetta.  
  
## Vedere anche  
 [Globalizzazione e localizzazione](../../../docs/standard/globalization-localization/index.md)   
 [Procedure consigliate per l'utilizzo di stringhe](../../../docs/standard/base-types/best-practices-strings.md)