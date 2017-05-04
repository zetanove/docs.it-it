---
title: I/O di file e di flussi | Documenti di Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IO namespace
- files, I/O
- System.IO namespace
- I/O [.NET Framework]
- streams, I/O
- data streams, I/O
ms.assetid: 4f4a33a9-66b7-4cd7-a285-4ad3e4276cd2
caps.latest.revision: 33
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 1fabc43044b6e0fa765a7c2f225add8b7eb923f5
ms.openlocfilehash: 1d0c203313b33aeba26aded268467b1a1b181118
ms.lasthandoff: 05/02/2017

---
# <a name="file-and-stream-io"></a>I/O di file e di flussi
I/O (input/output) di file e di flussi fa riferimento al trasferimento di dati da o verso un supporto di archiviazione. In .NET Framework gli spazi dei nomi [System.IO](http://go.microsoft.com/fwlink/?LinkId=231142) contengono i tipi che consentono la lettura e la scrittura, sia in modo sincrono che in modo asincrono, su flussi di dati e file. Questi spazi dei nomi contengono anche i tipi che eseguono la compressione e la decompressione dei file e i tipi che consentono la comunicazione tra le pipe e le porte seriali.  
  
 Un file è una raccolta ordinata e denominata di byte con archivio permanente. Quando si lavora con i file, si usano i percorsi di directory, l'archiviazione su disco e i nomi di file e directory. Al contrario, un flusso è una sequenza di byte che è possibile usare per leggere e scrivere in un archivio di backup, che può essere uno fra vari supporti di archiviazione (ad esempio, dischi o memoria). Così come esistono vari archivi di backup che non siano dischi, sono disponibili diversi tipi di flussi che non siano flussi di file, ad esempio la rete, la memoria e i flussi delle pipe.  
  
## <a name="files-and-directories"></a>File e directory  
 È possibile usare i tipi nello spazio dei nomi <xref:System.IO?displayProperty=fullName> per interagire con i file e le directory. Ad esempio, è possibile ottenere e impostare le proprietà dei file e delle directory e recuperare le raccolte di file e directory in base ai criteri di ricerca.  
  
 Di seguito sono riportate alcune classi di file e directory comunemente usate:  
  
-   <xref:System.IO.File>: fornisce metodi statici per creare, copiare, eliminare, spostare e aprire file; inoltre facilita la creazione di un oggetto <xref:System.IO.FileStream>.  
  
-   <xref:System.IO.FileInfo>: fornisce metodi di istanza per creare, copiare, eliminare, spostare e aprire file; inoltre facilita la creazione di un oggetto <xref:System.IO.FileStream>.  
  
-   <xref:System.IO.Directory>: fornisce metodi statici per creare, spostare ed enumerare directory e sottodirectory.  
  
-   <xref:System.IO.DirectoryInfo>: fornisce metodi di istanza per creare, spostare ed enumerare directory e sottodirectory.  
  
-   <xref:System.IO.Path>: fornisce metodi e proprietà che consentono di elaborare le stringhe di directory indipendentemente dalla piattaforma.  
  
 Oltre a usare queste classi, gli utenti di Visual Basic possono usare i metodi e le proprietà forniti dalla classe <xref:Microsoft.VisualBasic.FileIO.FileSystem?displayProperty=fullName> per l'I/O di file.  
  
 Vedere [Procedura: copiare le directory](../../../docs/standard/io/how-to-copy-directories.md), [Procedura: creare una visualizzazione directory](http://msdn.microsoft.com/en-us/4d2772b1-b991-4532-a8a6-6ef733277e69) e [Procedura: enumerare directory e file](../../../docs/standard/io/how-to-enumerate-directories-and-files.md).  
  
## <a name="streams"></a>Flussi  
 La classe di base astratta <xref:System.IO.Stream> supporta la lettura e la scrittura di byte. Tutte le classi che rappresentano flussi ereditano dalla classe <xref:System.IO.Stream>. La classe <xref:System.IO.Stream> e le relative classi derivate forniscono una rappresentazione comune degli archivi e delle origini dati, separando così il programmatore dai dettagli specifici del sistema operativo e dei dispositivi sottostanti.  
  
 I flussi implicano tre operazioni fondamentali:  
  
-   Lettura: trasferimento di dati da un flusso a una struttura di dati, quale una matrice di byte.  
  
-   Scrittura: trasferimento di dati da un'origine dati a un flusso.  
  
-   Ricerca: interrogazione di un flusso e modifica della posizione corrente al suo interno.  
  
 A seconda dell'origine dati o dell'archivio sottostante, è possibile che un flusso supportino queste funzionalità solo in parte. Ad esempio, la classe <xref:System.IO.Pipes.PipeStream> non supporta la ricerca. Le proprietà di un flusso <xref:System.IO.Stream.CanRead%2A>, <xref:System.IO.Stream.CanWrite%2A> e <xref:System.IO.Stream.CanSeek%2A> specificano le operazioni supportate dal flusso.  
  
 Di seguito sono riportate alcune classi di flusso comunemente usate:  
  
-   <xref:System.IO.FileStream>: per la lettura e la scrittura in un file.  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>: per la lettura e la scrittura in un file nello spazio di memorizzazione isolato.  
  
-   <xref:System.IO.MemoryStream>: per la lettura e la scrittura in memoria come l'archivio di backup.  
  
-   <xref:System.IO.BufferedStream>: per migliorare le prestazioni delle operazioni di lettura e scrittura.  
  
-   <xref:System.Net.Sockets.NetworkStream>: per la lettura e la scrittura sui socket di rete.  
  
-   <xref:System.IO.Pipes.PipeStream>: per la lettura e la scrittura su pipe unnamed e named.  
  
-   <xref:System.Security.Cryptography.CryptoStream>: per collegare i flussi di dati alle trasformazioni crittografiche.  
  
 Per un esempio relativo all'uso dei flussi in modo asincrono, vedere [I/O di file asincrono](../../../docs/standard/io/asynchronous-file-i-o.md).  
  
## <a name="readers-and-writers"></a>Reader e writer  
 Lo spazio dei nomi <xref:System.IO?displayProperty=fullName> fornisce anche i tipi per leggere caratteri codificati dai flussi e per scriverli nei flussi. In genere i flussi sono progettati per l'input e l'output di byte. I tipi reader e writer gestiscono la conversione dei caratteri codificati in byte e viceversa, in modo che il flusso possa completare l'operazione. Ogni classe reader e writer è associata a un flusso, che può essere recuperato tramite la proprietà `BaseStream` della classe.  
  
 Di seguito sono riportate alcune classi comunemente usate di reader e writer:  
  
-   <xref:System.IO.BinaryReader> e <xref:System.IO.BinaryWriter>: per la lettura e scrittura di tipi di dati primitivi come valori binari.  
  
-   <xref:System.IO.StreamReader> e <xref:System.IO.StreamWriter>: per la lettura e la scrittura di caratteri usando un valore di codifica per la conversione dei caratteri in byte e viceversa.  
  
-   <xref:System.IO.StringReader> e <xref:System.IO.StringWriter>: per la lettura e scrittura di caratteri nelle stringhe e dalle stringhe.  
  
-   <xref:System.IO.TextReader> e <xref:System.IO.TextWriter: fungono da classi di base astratte per gli altri reader e writer che leggono e scrivono caratteri e stringhe, ma non dati binari.  
  
 Vedere [Procedura: leggere testo da un file](../../../docs/standard/io/how-to-read-text-from-a-file.md), [Procedura: scrivere un testo in un file](../../../docs/standard/io/how-to-write-text-to-a-file.md), [Procedura: leggere caratteri da una stringa](../../../docs/standard/io/how-to-read-characters-from-a-string.md) e [Procedura: scrivere caratteri in una stringa](../../../docs/standard/io/how-to-write-characters-to-a-string.md).  
  
## <a name="asynchronous-io-operations"></a>Operazioni di I/O asincrone  
 La lettura o la scrittura di grandi quantità di dati può portare ad un elevato consumo di risorse. È necessario eseguire queste attività in modo asincrono se l'applicazione deve mantenersi reattiva verso utente. Usando operazioni di I/O sincrone, il thread di interfaccia utente rimane bloccato fino a quando l'operazione, che richiede un elevato utilizzo di risorse, non sarà completata.  Usare le operazioni di I/O asincrono quando si sviluppano applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], per non dare l'impressione che l'applicazione abbia arrestato l'esecuzione.  
  
 I membri asincroni contengono `Async` nei loro nomi, ad esempio i metodi <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.FlushAsync%2A>,  <xref:System.IO.Stream.ReadAsync%2A> e <xref:System.IO.Stream.WriteAsync%2A>. È possibile usare questi metodi tramite le parole chiave `async` e `await`.  
  
 Per altre informazioni, vedere [I/O di file asincrono](../../../docs/standard/io/asynchronous-file-i-o.md).  
  
## <a name="compression"></a>Compressione  
 Per compressione si intende il processo di riduzione della dimensione di un file per l'archiviazione. La decompressione è il processo di estrazione del contenuto di un file compresso in modo che sia in un formato utilizzabile. Lo spazio dei nomi <xref:System.IO.Compression?displayProperty=fullName> contiene tipi per comprimere e decomprimere file e flussi.  
  
 Le classi seguenti vengono spesso usate quando si comprimono e si decomprimono i file e i flussi:  
  
-   <xref:System.IO.Compression.ZipArchive>: per creare e recuperare voci nell'archivio zip.  
  
-   <xref:System.IO.Compression.ZipArchiveEntry>: per rappresentare un file compresso.  
  
-   <xref:System.IO.Compression.ZipFile>: per creare, estrarre e aprire un pacchetto compresso.  
  
-   <xref:System.IO.Compression.ZipFileExtensions>: per creare ed estrarre voci in un pacchetto compresso.  
  
-   <xref:System.IO.Compression.DeflateStream>: per comprimere e decomprimere i flussi utilizzando l'algoritmo Deflate.  
  
-   <xref:System.IO.Compression.GZipStream>: per comprimere e decomprimere i flussi nel formato di dati gzip.  
  
 Vedere [Procedura: comprimere ed estrarre file](../../../docs/standard/io/how-to-compress-and-extract-files.md).  
  
## <a name="isolated-storage"></a>Spazio di memorizzazione isolato  
 L'archiviazione isolata è un meccanismo di archiviazione dati che offre isolamento e sicurezza definendo modi standardizzati di associare il codice ai dati salvati. L'archiviazione offre un file system virtuale che è isolato dall'utente, dall'assembly ed eventualmente dal dominio. Lo spazio di memorizzazione isolato è particolarmente utile quando l'applicazione non dispone delle autorizzazioni di accesso ai file dell'utente. È possibile salvare le impostazioni o i file per l'applicazione in modo tale che vengano controllati dai criteri di sicurezza del computer.  
  
 Lo spazio di memorizzazione isolato non è disponibile per le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]; usare invece le classi di dati nello spazio dei nomi [Windows.Storage](http://msdn.microsoft.com/library/windows/apps/windows.storage.aspx). Per altre informazioni, vedere [Dati dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=229175) nel Centro per sviluppatori Windows.  
  
 Le classi seguenti vengono spesso usate nell'implementazione dello spazio di memorizzazione isolato:  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorage>: fornisce la classe di base per le implementazioni dello spazio di memorizzazione isolato.  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile>: fornisce un'area di memorizzazione isolata che contiene file e directory.  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>: espone un file all'interno dello spazio di memorizzazione isolato.  
  
 Vedere [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md).  
  
## <a name="io-operations-in-windows-store-apps"></a>Operazioni di I/O nelle applicazioni Windows Store  
 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] contiene molti tipi per leggere e scrivere su flussi; tuttavia, questo set non include tutti i tipi di I/O di .NET Framework.  
  
 Alcune differenze importanti da tenere presente quando si usano le operazioni di I/O nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]:  
  
-   I tipi legati specificatamente alle operazioni del file, quali <xref:System.IO.File>, <xref:System.IO.FileInfo>, <xref:System.IO.Directory> and <xref:System.IO.DirectoryInfo>, non sono inclusi in [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]. Usare invece i tipi nello spazio dei nomi [Windows.Storage](http://msdn.microsoft.com/library/windows/apps/windows.storage.aspx) di [!INCLUDE[wrt](../../../includes/wrt-md.md)], ad esempio [StorageFile](http://msdn.microsoft.com/library/windows/apps/windows.storage.storagefile.aspx) e [StorageFolder](http://msdn.microsoft.com/library/windows/apps/windows.storage.storagefolder.aspx).  
  
-   Lo spazio di memorizzazione isolato non è disponibile; usare invece i [dati dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=229175).  
  
-   Usare metodi asincroni, ad esempio <xref:System.IO.Stream.ReadAsync%2A> e <xref:System.IO.Stream.WriteAsync%2A>, per evitare il blocco del thread UI.  
  
-   I tipi di compressione basati sul percorso <xref:System.IO.Compression.ZipFile> e <xref:System.IO.Compression.ZipFileExtensions> non sono disponibili. Usare invece i tipi nello spazio dei nomi [Windows.Storage.Compression](http://msdn.microsoft.com/library/windows/apps/windows.storage.compression.aspx).  
  
 Se necessario è possibile passare da flussi di .NET Framework a flussi di Windows Runtime e viceversa. Per altre informazioni, vedere [Procedura: eseguire la conversione tra flussi di .NET Framework e flussi di Windows Runtime](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md) o [System.IO.WindowsRuntimeStreamExtensions](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.aspx). <!--zz TODO: <xref:System.IO.WindowsRuntimeStreamExtensions>--> 
  
 Per altre informazioni sulle operazioni di I/O in un'applicazione [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], vedere [Guida rapida: Lettura e scrittura di un file](http://go.microsoft.com/fwlink/p/?LinkId=243072) nel Windows Dev Center.  
  
## <a name="io-and-security"></a>I/O e sicurezza  
 Quando si usano le classi nello spazio dei nomi <xref:System.IO?displayProperty=fullName>, è necessario soddisfare i requisiti di sicurezza del sistema operativo, ad esempio gli elenchi di controllo di accesso (ACL), che controllano l'accesso ai file e alle directory. Questo requisito si affianca agli altri requisiti <xref:System.Security.Permissions.FileIOPermission>. Gli elenchi di controllo dell'accesso (ACL) possono essere gestiti a livello di codice. Per altre informazioni, vedere [Procedura: aggiungere o rimuovere voci dell'elenco di controllo di accesso (ACL)](../../../docs/standard/io/how-to-add-or-remove-access-control-list-entries.md).  
  
 I criteri di sicurezza predefiniti impediscono alle applicazioni Internet o Intranet di accedere ai file nel computer dell'utente. Pertanto, nello scrivere codice che verrà scaricato da Internet o Intranet, non usare classi I/O che richiedono un percorso a un file fisico. In alternativa, usare lo [spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md) per le applicazioni .NET Framework tradizionali o [dati dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=229175) per le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
 Un controllo di sicurezza viene eseguito solo quando il flusso viene costruito. Di conseguenza, non aprire un flusso per poi passarlo a codice o domini di applicazione meno attendibili.  
  
## <a name="related-topics"></a>Argomenti correlati  
  
-   [Attività di I/O comuni](../../../docs/standard/io/common-i-o-tasks.md)  
  
 Fornisce un elenco delle attività I/O associate ai file, alle directory e ai flussi, e i collegamenti al contenuto rilevante e ad esempi relativi a ogni attività.  
  
-   [I/O di file asincrono](../../../docs/standard/io/asynchronous-file-i-o.md)  
  
 Vengono descritti il funzionamento di base dell'I/O asincrono e i relativi vantaggi in termini di prestazioni.  
  
-   [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)  
  
 Viene descritto un meccanismo di archiviazione dei dati che fornisce isolamento e sicurezza tramite la definizione di modi standardizzati di associare il codice ai dati salvati.  
  
-   [Pipe](../../../docs/standard/io/pipe-operations.md)  
  
 Vengono descritte le operazioni di pipe named e unnamed in .NET Framework.  
  
-   [File mappati alla memoria](../../../docs/standard/io/memory-mapped-files.md)  
  
 Vengono descritti i file mappati alla memoria, che includono il contenuto dei file su disco nella memoria virtuale. È possibile usare file mappati alla memoria per modificare file molto grandi e per creare memoria condivisa per la comunicazione interprocesso.

