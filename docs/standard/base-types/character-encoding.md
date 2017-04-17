---
title: "Codifica di caratteri in .NET Framework | Microsoft Docs"
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
  - "codifica, scelta"
  - "codifica, strategia di fallback"
  - "codifica, informazioni"
ms.assetid: bf6d9823-4c2d-48af-b280-919c5af66ae9
caps.latest.revision: 33
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 33
---
# Codifica di caratteri in .NET Framework
I caratteri sono entità astratte rappresentabili in molti modi. La codifica dei caratteri è un sistema che abbina ogni carattere di un set di caratteri supportato a un valore che lo rappresenta. Il codice Morse, ad esempio, è una codifica dei caratteri che abbina ogni carattere dell'alfabeto romano a una serie di punti e linee utilizzabili per la trasmissione su linee telegrafiche. La codifica dei caratteri per i computer abbina ogni carattere di un set di caratteri supportato a un valore numerico che lo rappresenta. La codifica dei caratteri presenta due componenti distinti:  
  
-   Un codificatore, che converte una sequenza di caratteri in una sequenza di valori numerici \(byte\).  
  
-   Un decodificatore, che converte una sequenza di byte in una sequenza di caratteri.  
  
 La codifica dei caratteri descrive le regole in base alle quali operano un codificatore e un decodificatore. Ad esempio, la classe <xref:System.Text.UTF8Encoding> descrive le regole per la codifica e la decodifica con Unicode Transformation Format a 8 bit \(UTF\-8\), che usa da uno a quattro byte per rappresentare un singolo carattere Unicode. La codifica e la decodifica possono includere anche la convalida. Ad esempio, la classe <xref:System.Text.UnicodeEncoding> controlla tutti i surrogati per assicurarsi che costituiscano coppie di surrogati valide. Una coppia di surrogati è costituita da un carattere con un punto di codice compreso tra U\+D800 e U\+DBFF seguito da un carattere con un punto di codice compreso tra U\+DC00 e U\+DFFF.  Una strategia di fallback determina come un codificatore gestisce i caratteri non validi o come un decodificatore gestisce i byte non validi.  
  
> [!WARNING]
>  Le classi Encoding di .NET Framework consentono di archiviare e convertire i dati di tipo carattere. Non devono essere usate per archiviare i dati binari in formato stringa. In base alla codifica usata, la conversione dei dati binari in formato stringa con le classi Encoding può introdurre un comportamento imprevisto e generare dati non accurati o danneggiati. Per convertire i dati binari in un formato stringa, usare il metodo <xref:System.Convert.ToBase64String%2A?displayProperty=fullName>.  
  
 .NET Framework usa la codifica UTF\-16 \(rappresentata dalla classe <xref:System.Text.UnicodeEncoding>\) per rappresentare i caratteri e le stringhe. Le applicazioni destinate a Common Language Runtime usano codificatori per eseguire il mapping di rappresentazioni di caratteri Unicode supportate da Common Language Runtime ad altri schemi di codifica. Usano i decodificatori per eseguire il mapping di caratteri da codifiche non Unicode a Unicode.  
  
 Questo argomento include le sezioni seguenti:  
  
-   [Codifiche in .NET Framework](../../../docs/standard/base-types/character-encoding.md#Encodings)  
  
-   [Selezione di una classe Encoding](../../../docs/standard/base-types/character-encoding.md#Selecting)  
  
-   [Uso di un oggetto di codifica](../../../docs/standard/base-types/character-encoding.md#Using)  
  
-   [Scelta di una strategia di fallback](../../../docs/standard/base-types/character-encoding.md#FallbackStrategy)  
  
-   [Implementazione di una strategia di fallback personalizzata](../../../docs/standard/base-types/character-encoding.md#Custom)  
  
<a name="Encodings"></a>   
## Codifiche in .NET Framework  
 Tutte le classi Encoding dei caratteri in .NET Framework ereditano dalla classe <xref:System.Text.Encoding?displayProperty=fullName>, una classe astratta che definisce la funzionalità comune a tutte le codifiche dei caratteri. Per accedere ai singoli oggetti di codifica implementati in .NET Framework, eseguire le operazioni seguenti:  
  
-   Usare le proprietà statiche della classe <xref:System.Text.Encoding>, che restituiscono oggetti che rappresentano le codifiche dei caratteri standard disponibili in .NET Framework \(ASCII, UTF\-7, UTF\-8, UTF\-16 e UTF\-32\). Ad esempio, la proprietà <xref:System.Text.Encoding.Unicode%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Text.UnicodeEncoding>. Ogni oggetto usa il fallback di sostituzione per gestire le stringhe che non può codificare e i byte che non può decodificare. Per altre informazioni, vedere la sezione [Fallback di sostituzione](../../../docs/standard/base-types/character-encoding.md#Replacement).  
  
-   Chiamare il costruttore di classe della codifica. In questo modo è possibile creare istanze di oggetti per le codifiche ASCII, UTF\-7, UTF\-8, UTF\-16 e UTF\-32. Per impostazione predefinita, ogni oggetto usa il fallback di sostituzione per gestire le stringhe che non può codificare e i byte che non può decodificare, ma è possibile specificare che invece deve essere generata un'eccezione. Per altre informazioni, vedere le sezioni [Fallback di sostituzione](../../../docs/standard/base-types/character-encoding.md#Replacement) e [Fallback di eccezione](../../../docs/standard/base-types/character-encoding.md#Exception).  
  
-   Chiamare il costruttore <xref:System.Text.Encoding.%23ctor%28System.Int32%29?displayProperty=fullName> e passargli un Integer che rappresenta la codifica. Gli oggetti di codifica standard usano il fallback di sostituzione e gli oggetti di codifica della tabella codici e Double Byte Character Set \(DBCS\) usano il fallback con mapping più appropriato per gestire le stringhe che non possono codificare e i byte che non possono decodificare. Per altre informazioni, vedere la sezione [Fallback con mapping più appropriato](../../../docs/standard/base-types/character-encoding.md#BestFit).  
  
-   Chiamare il metodo <xref:System.Text.Encoding.GetEncoding%2A?displayProperty=fullName>, che restituisce qualsiasi codifica standard, della tabella codici o DBCS disponibile in .NET Framework. Gli overload consentono di specificare un oggetto di fallback sia per il codificatore che per il decodificatore.  
  
> [!NOTE]
>  Lo standard Unicode assegna un punto di codice \(un numero\) e un nome a ciascun carattere in ogni script supportato. Ad esempio, il carattere "A" è rappresentato dal punto di codice U\+0041 e dal nome "LATIN CAPITAL LETTER A". Le codifiche Unicode Transformation Format \(UTF\) definiscono i modi per codificare quel punto di codice in una sequenza di uno o più byte. Uno schema di codifica Unicode semplifica lo sviluppo di applicazioni internazionali, perché consente di rappresentare in una sola codifica i caratteri di qualsiasi set di caratteri. Gli sviluppatori di applicazioni non devono più tenere traccia dello schema di codifica usato per produrre i caratteri per una lingua o un sistema di scrittura specifico e i dati possono essere condivisi tra i sistemi a livello internazionale senza essere danneggiati.  
>   
>  .NET Framework supporta tre codifiche definite dallo standard Unicode: UTF\-8, UTF\-16 e UTF\-32. Per altre informazioni, vedere lo standard Unicode nella [home page di Unicode](http://go.microsoft.com/fwlink/?LinkId=37123).  
  
 È possibile recuperare informazioni su tutte le codifiche disponibili in .NET Framework chiamando il metodo <xref:System.Text.Encoding.GetEncodings%2A?displayProperty=fullName>. .NET Framework supporta i sistemi di codifica dei caratteri elencati nella tabella seguente.  
  
|Codifica|Classe|Descrizione|Vantaggi\/Svantaggi|  
|--------------|------------|-----------------|-------------------------|  
|non|<xref:System.Text.ASCIIEncoding>|Codifica un intervallo limitato di caratteri usando i sette bit più bassi di un byte.|Poiché questa codifica supporta solo i valori dei caratteri compresi tra U\+0000 e U\+007F, nella maggior parte dei casi non è adatta per le applicazioni internazionalizzate.|  
|UTF\-7|<xref:System.Text.UTF7Encoding>|Rappresenta i caratteri come sequenze di caratteri ASCII a 7 bit. I caratteri Unicode non ASCII sono rappresentati da una sequenza di escape di caratteri ASCII.|UTF\-7 supporta protocolli di newsgroup e di posta elettronica. UTF\-7 non è tuttavia particolarmente sicura o affidabile. In alcuni casi, la modifica di un bit può alterare radicalmente l'interpretazione di un'intera stringa UTF\-7. In altri casi, stringhe UTF\-7 diverse possono codificare lo stesso testo. Per le sequenze che includono caratteri non ASCII, UTF\-7 richiede più spazio di UTF\-8 e la codifica\/decodifica è più lenta. Di conseguenza, è consigliabile usare UTF\-8 anziché UTF\-7, se possibile.|  
|UTF\-8|<xref:System.Text.UTF8Encoding>|Rappresenta ogni punto di codice Unicode come sequenza che include da uno a quattro byte.|UTF\-8 supporta dimensioni dati a 8 bit e funziona bene con molti sistemi operativi esistenti. Per l'intervallo di caratteri ASCII, UTF\-8 è identica alla codifica ASCII e consente un più ampio set di caratteri. Tuttavia, per gli script in cinese\-giapponese\-coreano \(CJK\), UTF\-8 può richiedere tre byte per ogni carattere e potrebbe generare dimensioni dati maggiori di UTF\-16. Si noti che a volte la quantità di dati ASCII, ad esempio di tag HTML, giustifica l'aumento delle dimensioni per la gamma CJK.|  
|UTF\-16|<xref:System.Text.UnicodeEncoding>|Rappresenta ogni punto di codice Unicode come sequenza di uno o due Integer a 16 bit. I caratteri Unicode più comuni richiedono un solo punto di codice UTF\-16, anche se i caratteri supplementari Unicode \(U\+10000 e successivi\) richiedono due punti di codice surrogati UTF\-16. Sono supportati sia ordini dei byte little\-endian che big\-endian.|La codifica UTF\-16 viene usata da Common Language Runtime per rappresentare i valori <xref:System.Char> e <xref:System.String> e dal sistema operativo Windows per rappresentare i valori `WCHAR`.|  
|UTF\-32|<xref:System.Text.UTF32Encoding>|Rappresenta ogni punto di codice Unicode come Integer a 32 bit. Sono supportati sia ordini dei byte little\-endian che big\-endian.|La codifica UTF\-32 viene usata quando le applicazioni vogliono evitare il comportamento dei punti di codice surrogati della codifica UTF\-16 in sistemi operativi per cui lo spazio codificato è estremamente importante. I singoli glifi visualizzati su uno schermo possono comunque essere codificati con più di un carattere UTF\-32.|  
|Codifiche ANSI\/ISO||Forniscono il supporto per un'ampia gamma di tabelle codici. Nei sistemi operativi Windows, le tabelle codici vengono usate per supportare una lingua specifica o un gruppo di lingue. Per una tabella che elenca le tabelle codici supportate da .NET Framework, vedere la classe <xref:System.Text.Encoding>. È possibile recuperare un oggetto di codifica per una particolare tabella codici chiamando il metodo <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=fullName>.|Una tabella codici contiene 256 punti di codice ed è in base zero. Nella maggior parte delle tabelle codici, i punti di codice da 0 a 127 rappresentano il set di caratteri ASCII e i punti di codice da 128 a 255 sono molto diversi da una tabella codici all'altra. Ad esempio, la tabella codici 1252 fornisce i caratteri per i sistemi di scrittura in caratteri latini, tra cui inglese, tedesco e francese. Gli ultimi 128 punti di codice nella tabella codici 1252 contengono i caratteri accentati. La tabella codici 1253 fornisce i codici carattere necessari nel sistema di scrittura in caratteri greci. Gli ultimi 128 punti di codice nella tabella codici 1253 contengono i caratteri greci. Di conseguenza, un'applicazione che si basa su tabelle codici ANSI non può archiviare il greco e il tedesco nello stesso flusso di testo, a meno che non includa un identificatore indicante la tabella codici a cui si fa riferimento.|  
|Codifiche Double Byte Character Set \(DBCS\)||Supportano lingue, quali cinese, giapponese e coreano, che contengono più di 256 caratteri. In un set DBCS, una coppia di punti di codice \(un byte doppio\) rappresenta ogni carattere. La proprietà <xref:System.Text.Encoding.IsSingleByte%2A?displayProperty=fullName> restituisce `false` per le codifiche DBCS. È possibile recuperare un oggetto di codifica per un particolare DBCS chiamando il metodo <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=fullName>.|In un set DBCS, una coppia di punti di codice \(un byte doppio\) rappresenta ogni carattere. Quando un'applicazione gestisce dati DBCS, il primo byte di un carattere DBCS \(il byte di apertura\) viene elaborato in combinazione con il byte di chiusura che lo segue immediatamente. Poiché una singola coppia di punti di codice a doppio byte può rappresentare caratteri diversi a seconda della tabella codici, questo schema non consente la combinazione di due lingue, quali giapponese e cinese, nello stesso flusso di dati.|  
  
 Queste codifiche consentono di lavorare con i caratteri Unicode e con le codifiche più comunemente usate nelle applicazioni legacy. Inoltre, è possibile creare una codifica personalizzata definendo una classe che deriva da <xref:System.Text.Encoding> ed eseguendo l'override dei relativi membri.  
  
### Note sulla piattaforma: [!INCLUDE[net_core](../../../includes/net-core-md.md)]  
 Per impostazione predefinita, [!INCLUDE[net_core](../../../includes/net-core-md.md)] non rende disponibili le codifiche delle tabelle codici diverse dalla tabella codice 28591 e le codifiche Unicode, ad esempio UTF\-8 e UTF\-16. Tuttavia, è possibile aggiungere all'app le codifiche delle tabelle codici presenti nelle app di Windows standard destinate a .NET Framework. Per informazioni complete, vedere l'argomento <xref:System.Text.CodePagesEncodingProvider>.  
  
<a name="Selecting"></a>   
## Selezione di una classe Encoding  
 Se è possibile scegliere la codifica che verrà usata dall'applicazione, è opportuno usare una codifica Unicode, preferibilmente <xref:System.Text.UTF8Encoding> o <xref:System.Text.UnicodeEncoding>. .NET Framework supporta anche una terza codifica Unicode, <xref:System.Text.UTF32Encoding>.  
  
 Se si prevede di usare una codifica ASCII \(<xref:System.Text.ASCIIEncoding>\), scegliere invece <xref:System.Text.UTF8Encoding>. Le due codifiche sono identiche per il set di caratteri ASCII, ma <xref:System.Text.UTF8Encoding> offre i vantaggi seguenti:  
  
-   Può rappresentare ogni carattere Unicode, mentre <xref:System.Text.ASCIIEncoding> supporta solo i valori dei caratteri Unicode valori compresi tra U\+0000 e U\+007F.  
  
-   Fornisce il rilevamento errori e una migliore sicurezza.  
  
-   È stata ottimizzata per essere il più veloce possibile e dovrebbe essere più veloce di qualsiasi altra codifica. Anche per il contenuto interamente ASCII, le operazioni eseguite con <xref:System.Text.UTF8Encoding> sono più veloci delle operazioni eseguite con <xref:System.Text.ASCIIEncoding>.  
  
 È consigliabile usare <xref:System.Text.ASCIIEncoding> solo per le applicazioni legacy. Tuttavia, anche per le applicazioni legacy, <xref:System.Text.UTF8Encoding> potrebbe essere una scelta migliore per i motivi seguenti \(presupponendo le impostazioni predefinite\):  
  
-   Se l'applicazione include contenuto non esclusivamente ASCII e lo codifica con <xref:System.Text.ASCIIEncoding>, ogni carattere non ASCII viene codificato come punto interrogativo \(?\). Se l'applicazione quindi decodifica questi dati, le informazioni vengono perse.  
  
-   Se l'applicazione include contenuto non esclusivamente ASCII e lo codifica con <xref:System.Text.UTF8Encoding>, il risultato appare incomprensibile se interpretato come ASCII. Tuttavia, se l'applicazione usa poi un decodificatore UTF\-8 per decodificare questi dati, i dati eseguono correttamente un round trip.  
  
 In un'applicazione Web, i caratteri inviati al client in risposta a una richiesta Web dovrebbero rispecchiare la codifica usata nel client. Nella maggior parte dei casi, è opportuno impostare la proprietà <xref:System.Web.HttpResponse.ContentEncoding%2A?displayProperty=fullName> sul valore restituito dalla proprietà <xref:System.Web.HttpRequest.ContentEncoding%2A?displayProperty=fullName> per visualizzare il testo nella codifica prevista dall'utente.  
  
<a name="Using"></a>   
## Uso di un oggetto di codifica  
 Un codificatore converte una stringa di caratteri \(per lo più caratteri Unicode\) nell'equivalente numerico \(byte\). Ad esempio, è possibile usare un codificatore ASCII per convertire i caratteri Unicode in ASCII e poterli visualizzare nella console. Per eseguire la conversione, si chiama il metodo <xref:System.Text.Encoding.GetBytes%2A?displayProperty=fullName>. Per determinare il numero di byte necessari per archiviare i caratteri codificati prima di eseguire la codifica, è possibile chiamare il metodo <xref:System.Text.Encoding.GetByteCount%2A>.  
  
 L'esempio seguente usa una singola matrice di byte per codificare le stringhe in due operazioni distinte. Gestisce un indice che indica la posizione iniziale nella matrice di byte per il set successivo di byte con codifica ASCII. Chiama il metodo <xref:System.Text.ASCIIEncoding.GetByteCount%28System.String%29?displayProperty=fullName> per assicurarsi che la matrice di byte sia grande abbastanza da contenere la stringa codificata. Chiama quindi il metodo [ASCIIEncoding.GetBytes\(String, Int32, Int32, Byte\<xref:System.Text.ASCIIEncoding.GetBytes%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Byte%5B%5D%2CSystem.Int32%29?displayProperty=fullName> per codificare i caratteri nella stringa.  
  
 [!code-csharp[Conceptual.Encoding#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getbytes1.cs#8)]
 [!code-vb[Conceptual.Encoding#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getbytes1.vb#8)]  
  
 Un decodificatore converte una matrice di byte che rispecchia una particolare codifica dei caratteri in un set di caratteri, in una matrice di caratteri o in una stringa. Per decodificare una matrice di byte in una matrice di caratteri, si chiama il metodo <xref:System.Text.Encoding.GetChars%2A?displayProperty=fullName>. Per decodificare una matrice di byte in una stringa, si chiama il metodo <xref:System.Text.Encoding.GetString%2A>. Per determinare il numero di caratteri necessari per archiviare i byte decodificati prima di eseguire la decodifica, è possibile chiamare il metodo <xref:System.Text.Encoding.GetCharCount%2A>.  
  
 L'esempio seguente codifica tre stringhe e quindi le decodifica in una singola matrice di caratteri. Gestisce un indice che indica la posizione iniziale nella matrice di caratteri per il set successivo di caratteri decodificati. Chiama il metodo <xref:System.Text.ASCIIEncoding.GetCharCount%2A> per assicurarsi che la matrice di caratteri sia grande abbastanza da contenere tutti i caratteri decodificati. Chiama quindi il metodo [ASCIIEncoding.GetChars\(Byte\[\], Int32, Int32, Char\<xref:System.Text.ASCIIEncoding.GetChars%28System.Byte%5B%5D%2CSystem.Int32%2CSystem.Int32%2CSystem.Char%5B%5D%2CSystem.Int32%29?displayProperty=fullName> per decodificare la matrice di byte.  
  
 [!code-csharp[Conceptual.Encoding#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/getchars1.cs#9)]
 [!code-vb[Conceptual.Encoding#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/getchars1.vb#9)]  
  
 I metodi di codifica e di decodifica di una classe derivata da <xref:System.Text.Encoding> sono progettati per funzionare su un set completo di dati, ovvero tutti i dati da codificare o decodificare vengono forniti in una singola chiamata al metodo. In alcuni casi, tuttavia, i dati sono disponibili in un flusso e i dati da codificare o decodificare potrebbero essere disponibili solo in operazioni di lettura distinte. Ciò richiede che l'operazione di codifica o decodifica ricordi qualsiasi stato salvato dalla chiamata precedente. I metodi delle classi derivate da <xref:System.Text.Encoder> e <xref:System.Text.Decoder> possono gestire le operazioni di codifica e decodifica di operazioni che comprendono più chiamate ai metodi.  
  
 Un oggetto <xref:System.Text.Encoder> per una particolare codifica è disponibile nella proprietà <xref:System.Text.Encoding.GetEncoder%2A?displayProperty=fullName> di tale codifica. Un oggetto <xref:System.Text.Decoder> per una particolare codifica è disponibile nella proprietà <xref:System.Text.Encoding.GetDecoder%2A?displayProperty=fullName> di tale codifica. Per le operazioni di decodifica, tenere presente che le classi derivate da <xref:System.Text.Decoder> includono un metodo <xref:System.Text.Decoder.GetChars%2A?displayProperty=fullName>, ma non dispongono di un metodo corrispondente a <xref:System.Text.Encoding.GetString%2A?displayProperty=fullName>.  
  
 L'esempio seguente illustra la differenza tra l'uso dei metodi <xref:System.Text.Encoding.GetChars%2A?displayProperty=fullName> e <xref:System.Text.Decoder.GetChars%2A?displayProperty=fullName> per la decodifica di una matrice di byte Unicode. L'esempio codifica in un file una stringa che contiene alcuni caratteri Unicode e quindi usa i due metodi di decodifica per decodificarli dieci byte alla volta. Una coppia di surrogati presente nel decimo e nell'undicesimo byte viene decodificata in chiamate ai metodi distinte. Come mostra l'output, il metodo <xref:System.Text.Encoding.GetChars%2A?displayProperty=fullName> non è in grado di decodificare correttamente i byte e li sostituisce invece con U\+FFFD \(REPLACEMENT CHARACTER\). D'altra parte, il <xref:System.Text.Decoder.GetChars%2A?displayProperty=fullName> metodo è in grado di decodificare correttamente la matrice di byte per ottenere la stringa originale.  
  
 [!code-csharp[Conceptual.Encoding#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/stream1.cs#10)]
 [!code-vb[Conceptual.Encoding#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/stream1.vb#10)]  
  
<a name="FallbackStrategy"></a>   
## Scelta di una strategia di fallback  
 Quando un metodo tenta di codificare o decodificare un carattere, ma non esiste alcun mapping, deve implementare una strategia di fallback che determina come gestire il mapping non riuscito. Esistono tre tipi di strategie di fallback:  
  
-   Fallback con mapping più appropriato  
  
-   Fallback di sostituzione  
  
-   Fallback di eccezione  
  
> [!IMPORTANT]
>  I problemi più comuni nelle operazioni di codifica si verificano quando non è possibile eseguire il mapping di un carattere Unicode a una particolare codifica della tabella codici. I problemi più comuni nelle operazioni di decodifica si verificano quando sequenze di byte non valide non possono essere convertite in caratteri Unicode validi. Per questi motivi, è opportuno conoscere la strategia di fallback usata da un oggetto di codifica specifico. Quando è possibile, è consigliabile specificare la strategia di fallback usata da un oggetto di codifica quando si crea un'istanza dell'oggetto.  
  
<a name="BestFit"></a>   
### Fallback con mapping più appropriato  
 Quando un carattere non ha una corrispondenza esatta nella codifica di destinazione, il codificatore può provare a eseguirne il mapping a un carattere simile. Il fallback con mapping più appropriato è principalmente un problema di codifica più che di decodifica. Esistono pochissime tabelle codici contenenti caratteri di cui non è possibile eseguire correttamente il mapping a Unicode. Il fallback con mapping più appropriato è quello predefinito per le codifiche della tabella codici e Double Byte Character Set recuperate dagli overload <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=fullName> e <xref:System.Text.Encoding.GetEncoding%28System.String%29?displayProperty=fullName>.  
  
> [!NOTE]
>  In teoria, le classi Encoding Unicode fornite in .NET Framework \(<xref:System.Text.UTF8Encoding>, <xref:System.Text.UnicodeEncoding> e <xref:System.Text.UTF32Encoding>\) supportano ogni carattere di ogni set di caratteri e quindi possono essere usate per eliminare i problemi di fallback con mapping più appropriato.  
  
 Le strategie di fallback con mapping più appropriato sono diverse a seconda delle tabelle codici e non sono documentate in dettaglio. Ad esempio, per alcune tabelle codici, dei caratteri latini a larghezza intera viene eseguito il mapping ai caratteri latini a metà larghezza più comuni. Per altre tabelle codici, questo mapping non viene eseguito. Anche se si adotta una strategia aggressiva basata sul mapping più appropriato, per alcuni caratteri in alcune codifiche non è concepibile un mapping appropriato. Ad esempio, per un ideogramma cinese non esistono mapping ragionevoli alla tabella codici 1252. In questo caso, viene usata una stringa di sostituzione. Per impostazione predefinita, questa stringa è semplicemente un punto interrogativo \(QUESTION MARK, U\+003F\).  
  
 L'esempio seguente usa la tabella codici 1252 \(la tabella codici di Windows per le lingue dell'Europa occidentale\) per illustrare il mapping più appropriato e i relativi svantaggi. Viene usato il metodo <xref:System.Text.Encoding.GetEncoding%28System.Int32%29?displayProperty=fullName> per recuperare un oggetto di codifica per la tabella codici 1252. Per impostazione predefinita, usa il mapping più appropriato per i caratteri Unicode che non supporta. L'esempio crea un'istanza di una stringa che contiene tre caratteri non ASCII, CIRCLED LATIN CAPITAL LETTER S \(U\+24C8\), SUPERSCRIPT FIVE \(U\+2075\) e INFINITY \(U\+221E\), separati da spazi. Come mostra l'output del seguente esempio, quando la stringa viene codificata, i tre caratteri originali diversi dallo spazio vengono sostituiti da QUESTION MARK \(U\+003F\), DIGIT FIVE \(U\+0035\) e DIGIT EIGHT \(U\+0038\). DIGIT EIGHT è una sostituzione del tutto inadeguata per il carattere INFINITY non supportato e QUESTION MARK indica che non è disponibile alcun mapping per il carattere originale.  
  
 [!code-csharp[Conceptual.Encoding#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1.cs#1)]
 [!code-vb[Conceptual.Encoding#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1.vb#1)]  
  
 Il mapping più appropriato è il comportamento predefinito per un oggetto <xref:System.Text.Encoding> che codifica i dati Unicode come dati della tabella codici. Esistono applicazioni legacy che si basano su questo comportamento. Tuttavia, per motivi di sicurezza, per la maggior parte delle nuove applicazioni si dovrebbe evitare il comportamento basato sul mapping più appropriato. Ad esempio, le applicazioni non dovrebbero inserire un nome di dominio tramite una codifica con mapping più appropriato.  
  
> [!NOTE]
>  Si può anche implementare un mapping basato sul fallback più appropriato personalizzato per una codifica. Per altre informazioni, vedere la sezione [Implementazione di una strategia di fallback personalizzata](../../../docs/standard/base-types/character-encoding.md#Custom).  
  
 Se il fallback con mapping più appropriato è quello predefinito per un oggetto di codifica, è possibile scegliere un'altra strategia di fallback quando si recupera un oggetto <xref:System.Text.Encoding> chiamando l'overload <xref:System.Text.Encoding.GetEncoding%28System.Int32%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=fullName> o <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=fullName>. La sezione seguente include un esempio che sostituisce con un asterisco \(\*\) ogni carattere di cui non è possibile eseguire il mapping alla tabella codici 1252.  
  
 [!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
 [!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]  
  
<a name="Replacement"></a>   
### Fallback di sostituzione  
 Quando un carattere non ha una corrispondenza esatta nello schema di destinazione e non esiste un carattere appropriato a cui eseguirne il mapping, l'applicazione può specificare una carattere o una stringa di sostituzione. È il comportamento predefinito del decodificatore Unicode, che sostituisce con REPLACEMENT\_CHARACTER \(U\+FFFD\) le sequenze a due byte che non può decodificare. È anche il comportamento predefinito della classe <xref:System.Text.ASCIIEncoding>, che sostituisce ogni carattere che non può codificare o decodificare con un punto interrogativo. Il seguente esempio illustra la sostituzione dei caratteri della stringa Unicode dell'esempio precedente. Come mostra l'output, ogni carattere che non può essere decodificato con un byte ASCII viene sostituito da 0x3F, ovvero dal codice ASCII per il punto interrogativo.  
  
 [!code-csharp[Conceptual.Encoding#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/replacementascii.cs#2)]
 [!code-vb[Conceptual.Encoding#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/replacementascii.vb#2)]  
  
 .NET Framework include le classi <xref:System.Text.EncoderReplacementFallback> e <xref:System.Text.DecoderReplacementFallback>, che usano una stringa di sostituzione se non è possibile eseguire il mapping esatto di un carattere in un'operazione di codifica o decodifica. Per impostazione predefinita, questa stringa di sostituzione è un punto interrogativo, ma è possibile chiamare un overload del costruttore di classe per scegliere un'altra stringa. In genere, la stringa di sostituzione è costituita da un solo carattere, anche se questo non è un requisito. L'esempio seguente modifica il comportamento del codificatore della tabella codici 1252 creando un'istanza dell'oggetto <xref:System.Text.EncoderReplacementFallback> che usa un asterisco \(\*\) come stringa di sostituzione.  
  
 [!code-csharp[Conceptual.Encoding#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/bestfit1a.cs#3)]
 [!code-vb[Conceptual.Encoding#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/bestfit1a.vb#3)]  
  
> [!NOTE]
>  Si può anche implementare una classe di sostituzione per una codifica. Per altre informazioni, vedere la sezione [Implementazione di una strategia di fallback personalizzata](../../../docs/standard/base-types/character-encoding.md#Custom).  
  
 Oltre a QUESTION MARK \(U\+003F\), anche il carattere Unicode REPLACEMENT CHARACTER \(U\+FFFD\) viene di solito usato come stringa di sostituzione, in particolare quando si decodificano sequenze di byte che non possono essere convertite in caratteri Unicode. Tuttavia è possibile scegliere qualsiasi stringa di sostituzione, che potrà contenere più caratteri.  
  
<a name="Exception"></a>   
### Fallback di eccezione  
 Invece di fornire un fallback con mapping più appropriato o una stringa di sostituzione, un codificatore può generare un'eccezione <xref:System.Text.EncoderFallbackException> se non può codificare un set di caratteri, mentre un decodificatore può generare un'eccezione <xref:System.Text.DecoderFallbackException> se non può decodificare una matrice di byte. Per generare un'eccezione durante le operazioni di codifica e decodifica, si passa rispettivamente un oggetto <xref:System.Text.EncoderExceptionFallback> e un oggetto <xref:System.Text.DecoderExceptionFallback> al metodo <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=fullName>. L'esempio seguente illustra il fallback di eccezione con la classe <xref:System.Text.ASCIIEncoding>.  
  
 [!code-csharp[Conceptual.Encoding#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/exceptionascii.cs#4)]
 [!code-vb[Conceptual.Encoding#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/exceptionascii.vb#4)]  
  
> [!NOTE]
>  Si può anche implementare un gestore di eccezioni personalizzato per un'operazione di codifica. Per altre informazioni, vedere la sezione [Implementazione di una strategia di fallback personalizzata](../../../docs/standard/base-types/character-encoding.md#Custom).  
  
 Gli oggetti <xref:System.Text.EncoderFallbackException> e <xref:System.Text.DecoderFallbackException> forniscono le seguenti informazioni sulla condizione che ha causato l'eccezione:  
  
-   L'oggetto <xref:System.Text.EncoderFallbackException> include un metodo <xref:System.Text.EncoderFallbackException.IsUnknownSurrogate%2A>, indicante se il carattere o i caratteri che non possono essere codificati rappresentano una coppia di surrogati sconosciuti \(in questo caso, il metodo restituisce `true`\) o un solo carattere sconosciuto \(in questo caso, il metodo restituisce `false`\). I caratteri della coppia di surrogati sono disponibili nelle proprietà <xref:System.Text.EncoderFallbackException.CharUnknownHigh%2A?displayProperty=fullName> e <xref:System.Text.EncoderFallbackException.CharUnknownLow%2A?displayProperty=fullName>. Il singolo carattere sconosciuto è disponibile nella proprietà <xref:System.Text.EncoderFallbackException.CharUnknown%2A?displayProperty=fullName>. La proprietà <xref:System.Text.EncoderFallbackException.Index%2A?displayProperty=fullName> indica la posizione nella stringa in cui è stato trovato il primo carattere che non è stato possibile codificare.  
  
-   L'oggetto <xref:System.Text.DecoderFallbackException> include una proprietà <xref:System.Text.DecoderFallbackException.BytesUnknown%2A> che restituisce una matrice di byte che non è possibile decodificare. La proprietà <xref:System.Text.DecoderFallbackException.Index%2A?displayProperty=fullName> indica la posizione iniziale dei byte sconosciuti.  
  
 Anche se gli oggetti <xref:System.Text.EncoderFallbackException> e <xref:System.Text.DecoderFallbackException> forniscono informazioni diagnostiche adeguate sull'eccezione, tuttavia non forniscono accesso al buffer di codifica o di decodifica. Quindi non consentono di sostituire o correggere i dati non validi nel metodo di codifica o di decodifica.  
  
<a name="Custom"></a>   
## Implementazione di una strategia di fallback personalizzata  
 Oltre al mapping più appropriato che viene implementato internamente dalle tabelle codici, .NET Framework include le seguenti classi per implementare una strategia di fallback:  
  
-   Usare <xref:System.Text.EncoderReplacementFallback> e <xref:System.Text.EncoderReplacementFallbackBuffer> per sostituire i caratteri nelle operazioni di codifica.  
  
-   Usare <xref:System.Text.DecoderReplacementFallback> e <xref:System.Text.DecoderReplacementFallbackBuffer> per sostituire i caratteri nelle operazioni di decodifica.  
  
-   Usare <xref:System.Text.EncoderExceptionFallback> e <xref:System.Text.EncoderExceptionFallbackBuffer> per generare un'eccezione <xref:System.Text.EncoderFallbackException> quando un carattere non può essere codificato.  
  
-   Usare <xref:System.Text.DecoderExceptionFallback> e <xref:System.Text.DecoderExceptionFallbackBuffer> per generare un'eccezione <xref:System.Text.DecoderFallbackException> quando un carattere non può essere decodificato.  
  
 Inoltre, è possibile implementare una soluzione personalizzata che usa il fallback con mapping più appropriato, il fallback di sostituzione o il fallback di eccezione, attenendosi alla procedura seguente:  
  
1.  Derivare una classe da <xref:System.Text.EncoderFallback> per le operazioni di codifica e da <xref:System.Text.DecoderFallback> per le operazioni di decodifica.  
  
2.  Derivare una classe da <xref:System.Text.EncoderFallbackBuffer> per le operazioni di codifica e da <xref:System.Text.DecoderFallbackBuffer> per le operazioni di decodifica.  
  
3.  Per il fallback di eccezione, se le classi predefinite <xref:System.Text.EncoderFallbackException> e <xref:System.Text.DecoderFallbackException> non rispondono alle esigenze specifiche, derivare una classe da un oggetto eccezione, ad esempio <xref:System.Exception> o <xref:System.ArgumentException>.  
  
### Derivazione da EncoderFallback o DecoderFallback  
 Per implementare una soluzione di fallback personalizzata, è necessario creare una classe che eredita da <xref:System.Text.EncoderFallback> per le operazioni di codifica e da <xref:System.Text.DecoderFallback> per le operazioni di decodifica. Le istanze di queste classi vengono passate al metodo <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=fullName> e fungono da intermediario tra la classe Encoding e l'implementazione del fallback.  
  
 Quando si crea una soluzione di fallback personalizzata per un codificatore o un decodificatore, è necessario implementare i membri seguenti:  
  
-   La proprietà <xref:System.Text.EncoderFallback.MaxCharCount%2A?displayProperty=fullName> o <xref:System.Text.DecoderFallback.MaxCharCount%2A?displayProperty=fullName>, che restituisce il numero massimo possibile di caratteri che il fallback con mapping più appropriato, di sostituzione o di eccezione può restituire per sostituire un singolo carattere. Per un fallback di eccezione personalizzata, il valore è zero.  
  
-   Il metodo <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=fullName> o <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=fullName>, che restituisce l'implementazione personalizzata di <xref:System.Text.EncoderFallbackBuffer> o <xref:System.Text.DecoderFallbackBuffer>. Il metodo viene chiamato dal codificatore quando rileva il primo carattere che non può codificare correttamente oppure dal decodificatore quando rileva il primo byte che non può decodificare correttamente.  
  
### Derivazione da EncoderFallbackBuffer o DecoderFallbackBuffer  
 Per implementare una soluzione di fallback personalizzata, è necessario creare anche una classe che eredita da <xref:System.Text.EncoderFallbackBuffer> per le operazioni di codifica e da <xref:System.Text.DecoderFallbackBuffer> per le operazioni di decodifica. Le istanze di queste classi vengono restituite dal metodo <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A> delle classi <xref:System.Text.EncoderFallback> e <xref:System.Text.DecoderFallback>. Il metodo <xref:System.Text.EncoderFallback.CreateFallbackBuffer%2A?displayProperty=fullName> viene chiamato dal codificatore quando rileva il primo carattere che non può codificare, mentre il metodo <xref:System.Text.DecoderFallback.CreateFallbackBuffer%2A?displayProperty=fullName> viene chiamato dal decodificatore quando rileva uno o più byte che non può decodificare. Le classi <xref:System.Text.EncoderFallbackBuffer> e <xref:System.Text.DecoderFallbackBuffer> forniscono l'implementazione del fallback. Ogni istanza rappresenta un buffer contenente i caratteri di fallback che sostituiranno il carattere che non può essere codificato o la sequenza di byte che non può essere decodificata.  
  
 Quando si crea una soluzione di fallback personalizzata per un codificatore o un decodificatore, è necessario implementare i membri seguenti:  
  
-   Il metodo <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=fullName> o <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=fullName>.<xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=fullName> viene chiamato dal codificatore per fornire al buffer di fallback informazioni sul carattere che non può codificare. Poiché il carattere da codificare può essere una coppia di surrogati, questo metodo viene sottoposto a overload. A un overload vengono passati il carattere da codificare e l'indice nella stringa. Al secondo overload vengono passati il surrogato alto e quello basso insieme all'indice nella stringa. Il metodo <xref:System.Text.DecoderFallbackBuffer.Fallback%2A?displayProperty=fullName> viene chiamato dal decodificatore per fornire al buffer di fallback informazioni sui byte che non può decodificare. A questo metodo viene passata una matrice di byte che non può decodificare, insieme all'indice del primo byte. Il metodo di fallback dovrebbe restituire `true` se il buffer di fallback può fornire uno o più caratteri di sostituzione o con mapping più appropriato. In caso contrario, dovrebbe restituire `false`. Per un fallback di eccezione, il metodo di fallback dovrebbe generare un'eccezione.  
  
-   Il metodo <xref:System.Text.EncoderFallbackBuffer.GetNextChar%2A?displayProperty=fullName> o <xref:System.Text.DecoderFallbackBuffer.GetNextChar%2A?displayProperty=fullName>, che viene chiamato ripetutamente dal codificatore o dal decodificatore per ottenere il carattere successivo dal buffer di fallback. Quando sono stati restituiti tutti i caratteri di fallback, il metodo dovrebbe restituire U\+0000.  
  
-   La proprietà <xref:System.Text.EncoderFallbackBuffer.Remaining%2A?displayProperty=fullName> o <xref:System.Text.DecoderFallbackBuffer.Remaining%2A?displayProperty=fullName>, che restituisce il numero di caratteri rimanenti nel buffer di fallback.  
  
-   Il metodo <xref:System.Text.EncoderFallbackBuffer.MovePrevious%2A?displayProperty=fullName> o <xref:System.Text.DecoderFallbackBuffer.MovePrevious%2A?displayProperty=fullName>, che sposta la posizione corrente nel buffer del fallback al carattere precedente.  
  
-   Il metodo <xref:System.Text.EncoderFallbackBuffer.Reset%2A?displayProperty=fullName> o <xref:System.Text.DecoderFallbackBuffer.Reset%2A?displayProperty=fullName>, che reinizializza il buffer di fallback.  
  
 Se l'implementazione del fallback è un fallback con mapping più appropriato o un fallback di sostituzione, le classi derivate da <xref:System.Text.EncoderFallbackBuffer> e <xref:System.Text.DecoderFallbackBuffer> gestisco anche due campi di istanza privati: il numero esatto di caratteri nel buffer e l'indice del carattere successivo nel buffer da restituire.  
  
### Esempio di EncoderFallback  
 In un esempio precedente è stato usato il fallback di sostituzione per sostituire con un asterisco \(\*\) i caratteri Unicode non corrispondenti a caratteri ASCII. L'esempio seguente usa un'implementazione del fallback con mapping più appropriato personalizzato invece di fornire un mapping migliore dei caratteri non ASCII.  
  
 Il codice seguente definisce una classe denominata `CustomMapper` che deriva da <xref:System.Text.EncoderFallback> per gestire il mapping più appropriato dei caratteri non ASCII. Il metodo `CreateFallbackBuffer` restituisce un oggetto `CustomMapperFallbackBuffer` oggetto che fornisce l'implementazione di <xref:System.Text.EncoderFallbackBuffer>. La classe `CustomMapper` usa un oggetto <xref:System.Collections.Generic.Dictionary%602> per archiviare i mapping dei caratteri Unicode non supportati \(valore chiave\) e i corrispondenti caratteri a 8 bit \(archiviati in due byte consecutivi in un Integer a 64 bit\). Per rendere questo mapping disponibile al buffer di fallback, l'istanza di `CustomMapper` viene passata come parametro al costruttore di classe `CustomMapperFallbackBuffer`. Poiché il mapping di più lungo è la stringa "INF" per il carattere Unicode U\+221E, la proprietà `MaxCharCount` restituisce 3.  
  
 [!code-csharp[Conceptual.Encoding#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#5)]
 [!code-vb[Conceptual.Encoding#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#5)]  
  
 Il codice seguente definisce la classe `CustomMapperFallbackBuffer`, derivata da <xref:System.Text.EncoderFallbackBuffer>. Il dizionario contenente i mapping più appropriati e definito nell'istanza di `CustomMapper` è disponibile nel costruttore di classe. Il metodo `Fallback` restituisce `true` se uno dei caratteri Unicode che il codificatore ASCII non può codificare è definito nel dizionario dei mapping. In caso contrario, restituisce `false`. Per ogni fallback, la variabile privata `count` indica il numero di caratteri ancora da restituire e la variabile privata `index` indica la posizione nel buffer della stringa, `charsToReturn`, del carattere successivo da restituire.  
  
 [!code-csharp[Conceptual.Encoding#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#6)]
 [!code-vb[Conceptual.Encoding#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#6)]  
  
 Il codice seguente crea quindi un'istanza dell'oggetto `CustomMapper` e ne passa un'istanza al metodo <xref:System.Text.Encoding.GetEncoding%28System.String%2CSystem.Text.EncoderFallback%2CSystem.Text.DecoderFallback%29?displayProperty=fullName>. L'output indica che l'implementazione del fallback con mapping più appropriato gestisce correttamente i tre caratteri non ASCII nella stringa originale.  
  
 [!code-csharp[Conceptual.Encoding#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.encoding/cs/custom1.cs#7)]
 [!code-vb[Conceptual.Encoding#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.encoding/vb/custom1.vb#7)]  
  
## Vedere anche  
 <xref:System.Text.Encoder>   
 <xref:System.Text.Decoder>   
 <xref:System.Text.DecoderFallback>   
 <xref:System.Text.Encoding>   
 <xref:System.Text.EncoderFallback>   
 [Globalizzazione e localizzazione](../../../ml/index.xml)