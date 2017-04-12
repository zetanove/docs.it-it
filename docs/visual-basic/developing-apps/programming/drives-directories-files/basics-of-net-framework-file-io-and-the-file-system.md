---
title: "Nozioni fondamentali sul file system e sulla funzionalità di I/O di file di .NET Framework (Visual Basic) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- file access, file I/O in Visual Basic
- file attributes, determining
- streams, fundamental operations
- file permissions
- streams
- streams, definition
ms.assetid: 49d837c0-cf28-416f-8606-4d83d7b479ef
caps.latest.revision: 30
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9623d1c3076d622d69a0f7c4e711274f6e244023
ms.lasthandoff: 03/13/2017

---
# <a name="basics-of-net-framework-file-io-and-the-file-system-visual-basic"></a>Nozioni fondamentali sul file system e sulla funzionalità di I/O di file di .NET Framework (Visual Basic)
Le classi dello spazio dei nomi <xref:System.IO> vengono usate per gestire unità, file e directory.  
  
 Lo spazio dei nomi <xref:System.IO> contiene le classi <xref:System.IO.File> e <xref:System.IO.Directory>, che offrono la funzionalità [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] che modifica file e directory. Poiché i metodi di questi oggetti sono membri statici o condivisi, è possibile usarli direttamente senza prima creare un'istanza della classe. A queste classi sono associate le classi <xref:System.IO.FileInfo> e <xref:System.IO.DirectoryInfo> che risulteranno familiari agli utenti della funzionalità `My`. Per usare queste classi è necessario specificare in modo completo i nomi oppure importare gli spazi dei nomi appropriati, includendo le istruzioni `Imports` all'inizio del codice in questione. Per altre informazioni, vedere [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
> [!NOTE]
>  Altri argomenti di questa sezione usano l'oggetto `My.Computer.FileSystem` anziché le classi `System.IO` per lavorare con unità, file e directory. L'oggetto `My.Computer.FileSystem` è destinato principalmente all'uso nei programmi [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Le classi `System.IO` sono destinate all'uso da parte di qualsiasi linguaggio che supporta il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)], tra cui [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="definition-of-a-stream"></a>Definizione di un flusso  
 Il [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] usa i flussi per supportare la lettura e scrittura su file. Un flusso è paragonabile a un set unidimensionale di dati contigui, con un inizio e una fine, e in cui il cursore indica la posizione corrente nel flusso.  
  
 ![Il cursore indica la posizione corrente nel flusso dei file.](../../../../visual-basic/developing-apps/programming/drives-directories-files/media/filestream.gif "FileStream")  
  
## <a name="stream-operations"></a>Operazioni di flusso  
 I dati contenuti nel flusso possono provenire dalla memoria, da un file o da un socket TCP/IP. Ai flussi è possibile applicare alcune operazioni fondamentali:  
  
-   Lettura. È possibile leggere da un flusso, trasferendo i dati dal flusso in una struttura di dati, ad esempio una stringa o una matrice di byte.  
  
-   **Scrittura**. È possibile scrivere in un flusso, trasferendo i dati da un'origine dati nel flusso.  
  
-   **Ricerca**. È possibile eseguire una query e modificare la propria posizione nel flusso.  
  
 Per altre informazioni, vedere [Composing Streams](https://msdn.microsoft.com/library/e4y2dch9).  
  
## <a name="types-of-streams"></a>Tipi di flussi  
 In [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)], un flusso è rappresentato dalla classe <xref:System.IO.Stream> che costituisce la classe astratta per tutti i flussi. Non è possibile creare direttamente un'istanza della classe <xref:System.IO.Stream>, ma è necessario usare una delle classi implementata dall'istanza.  
  
 Ci sono diversi tipi di flusso, ma per usare l'input/output (I/O) di file, i tipi più importanti sono la classe <xref:System.IO.FileStream>, che offre un modo di leggere e scrivere in file, e la classe <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>, che offre un modo per creare file e directory in archiviazione isolata. Altri flussi che possono essere usati quando si lavora con l'I/O su file includono:  
  
-   <xref:System.IO.BufferedStream>  
  
-   <xref:System.Security.Cryptography.CryptoStream>  
  
-   <xref:System.IO.MemoryStream>  
  
-   <xref:System.Net.Sockets.NetworkStream>.  
  
 La tabella seguente elenca le attività comunemente eseguite con un flusso:  
  
|Per|Vedere|
|---|---|   
|Leggere e scrivere in un file di dati|[Procedura: Leggere e scrivere su un file di dati appena creato](https://msdn.microsoft.com/library/36b93480.aspx)|  
|Leggere testo da un file|[Procedura: Leggere testo da un file](https://msdn.microsoft.com/library/db5x7c0d.aspx)|  
|Scrivere testo in un file|[Procedura: Scrivere un testo in un file](https://msdn.microsoft.com/library/6ka1wd3w.aspx)|  
|Leggere caratteri da una stringa|[Procedura: Leggere caratteri da una stringa](https://msdn.microsoft.com/library/9yyz8a6c.aspx)|  
|Scrivere caratteri in una stringa|[Procedura: Scrivere caratteri in una stringa](https://msdn.microsoft.com/library/z4kzt0dd.aspx)|  
|Crittografare i dati|[Crittografia di dati](https://msdn.microsoft.com/library/as0w18af.aspx)|  
|Decrittografare i dati|[Decrittografia di dati](https://msdn.microsoft.com/library/te15te69.aspx)|  
  
## <a name="file-access-and-attributes"></a>Accesso ai file e attributi  
 È possibile controllare come i file vengono creati, aperti e condivisi con le enumerazioni <xref:System.IO.FileAccess>, <xref:System.IO.FileMode> e <xref:System.IO.FileShare>, che contengono i flag usati dai costruttori della classe <xref:System.IO.FileStream>. Ad esempio, quando si apre o si crea un nuovo <xref:System.IO.FileStream>, l'enumerazione <xref:System.IO.FileMode> consente di specificare se il file viene aperto per operazioni di accodamento, se viene creato un nuovo file nel caso il file specificato non esista, se il file viene sovrascritto e così via.  
  
 L'enumerazione <xref:System.IO.FileAttributes> abilita la raccolta di informazioni specifiche del file. L'enumerazione <xref:System.IO.FileAttributes> restituisce gli attributi archiviati del file, ad esempio se è compresso, crittografato, nascosto, in sola lettura, un archivio, una directory, un file di sistema o un file temporaneo.  
  
 La tabella seguente elenca le attività che coinvolgono l'accesso ai file e gli attributi di file:  
  
|Per|Vedere|  
|---|---|
|Aprire e accodare testo in un file di log|[Procedura: Aprire e accodare un file di log](https://msdn.microsoft.com/library/3zc0w663.aspx)|  
|Determinare gli attributi di un file|<xref:System.IO.FileAttributes>|  
  
## <a name="file-permissions"></a>Autorizzazioni di file  
 Il controllo dell'accesso ai file e alle directory può essere eseguito con la classe <xref:System.Security.Permissions.FileIOPermission>. Questo può essere particolarmente importante per gli sviluppatori che lavorano con i Web Form che, per impostazione predefinita, vengono eseguiti nel contesto di un account utente locale speciale denominato ASPNET, che viene creato come parte delle installazioni di [!INCLUDE[vstecasp](../../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] e [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] . Quando una tale applicazione richiede l'accesso a una risorsa, l'account utente ASPNET dispone di autorizzazioni limitate, che potrebbero impedire all'utente di eseguire azioni quali la scrittura in un file da un'applicazione Web. Per altre informazioni, vedere [Autorizzazioni di sicurezza](http://msdn.microsoft.com/en-us/b03757b4-e926-4196-b738-3733ced2bda0) e <xref:System.Security.Permissions.FileIOPermission>.  
  
## <a name="isolated-file-storage"></a>Archiviazione di file isolati  
 Lo spazio di archiviazione isolato è un tentativo di risolvere i problemi creati durante l'uso dei file in cui l'utente o il codice non dispone delle autorizzazioni necessarie. Lo spazio di archiviazione isolato assegna a ciascun utente un raggruppamento di dati che può contenere uno o più archivi. Gli archivi possono essere isolati gli uni dagli altri per utente e per assembly. Solo l'utente e l'assembly che ha creato l'archivio può accedervi. Un archivio opera come un file system virtuale completo: all'interno di un archivio è possibile creare e modificare directory e file.  
  
 La tabella seguente elenca le attività comunemente associate all'archiviazione di file isolati.  
  
|Per|Vedere|
|---|---|  
|Creare un spazio di memorizzazione isolato|[Procedura: Recuperare archivi per lo spazio di memorizzazione isolato](https://msdn.microsoft.com/library/k48a6h13.aspx)|  
|Enumerare gli spazi di memorizzazione isolati|[Procedura: Enumerare gli archivi per lo spazio di memorizzazione isolato](https://msdn.microsoft.com/library/c3dy613a.aspx)|  
|Eliminare un spazio di memorizzazione isolato|[Procedura: Eliminare gli archivi nello spazio di memorizzazione isolato](https://msdn.microsoft.com/library/5w71t104.aspx)|  
|Creare un file o una directory in un spazio di memorizzazione isolato|[Procedura: Creare file e directory nello spazio di memorizzazione isolato](https://msdn.microsoft.com/library/6h2ws3ft.aspx)|  
|Trovare un file in un spazio di memorizzazione isolato|[Procedura: Trovare file e directory esistenti nello spazio di memorizzazione isolato](https://msdn.microsoft.com/library/zd5e2z84.aspx)|  
|Leggere o scrivere su un file in un spazio di memorizzazione isolato|[Procedura: Leggere e scrivere sui file nello spazio di memorizzazione isolato](https://msdn.microsoft.com/library/xf96a1wz.aspx)|  
|Eliminare un file o una directory in un spazio di memorizzazione isolato|[Procedura: Eliminare file e directory nello spazio di memorizzazione isolato](https://msdn.microsoft.com/library/kx3852wf.aspx)|  
  
## <a name="file-events"></a>Eventi di file  
 Il componente <xref:System.IO.FileSystemWatcher> consente di controllare le modifiche in file e directory del sistema o in ogni computer al quale si ha accesso di rete. Ad esempio, se un file viene modificato, è consigliabile inviare all'utente un avviso che la modifica ha avuto luogo. Quando vengono apportate modifiche, vengono generati uno o più eventi, che vengono archiviati in un buffer e passati al componente <xref:System.IO.FileSystemWatcher> per l'elaborazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Composizione dei flussi](https://msdn.microsoft.com/library/e4y2dch9)   
 [I/O di file e di flussi](https://msdn.microsoft.com/library/k3352a4t)   
 [I/O di file asincrono](https://msdn.microsoft.com/library/kztecsys)   
 [Classes Used in .NET Framework File I/O and the File System (Visual Basic)](../../../../visual-basic/developing-apps/programming/drives-directories-files/classes-used-in-net-framework-file-io-and-the-file-system.md) (Classi usate nel file system e nella funzionalità di I/O di file di .NET Framework (Visual Basic))
