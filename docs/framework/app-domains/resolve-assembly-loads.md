---
title: "Risoluzione caricamenti assembly | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], risoluzione caricamenti"
  - "domini dell'applicazione, caricamento assembly"
  - "risoluzione caricamenti assembly"
  - "assembly [.NET Framework], caricamento"
  - "domini dell'applicazione, risoluzione caricamenti assembly"
ms.assetid: 5099e549-f4fd-49fb-a290-549edd456c6a
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Risoluzione caricamenti assembly
.NET Framework fornisce l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> per le applicazioni che richiedono un maggiore controllo sul caricamento dell'assembly.  Gestendo questo evento, l'applicazione è in grado di caricare un assembly nel contesto di caricamento dall'esterno dei normali percorsi di sondaggio, selezionare la versione dell'assembly da caricare, creare un assembly dinamico e restituirlo e così via.  In questo argomento vengono fornite le istruzioni per la gestione dell'evento <xref:System.AppDomain.AssemblyResolve>.  
  
> [!NOTE]
>  Per risolvere i caricamenti degli assembly nel contesto solo reflection, utilizzare invece l'evento <xref:System.AppDomain.ReflectionOnlyAssemblyResolve?displayProperty=fullName>.  
  
## Funzionamento dell'evento AssemblyResolve  
 Quando si registra un gestore per l'evento <xref:System.AppDomain.AssemblyResolve>, il gestore viene richiamato ogni volta che l'associazione di runtime a un assembly in base al nome avrà esito negativo.  Ad esempio, la chiamata ai metodi seguenti dal codice utente può causare la generazione dell'evento <xref:System.AppDomain.AssemblyResolve>:  
  
-   Un overload del metodo <xref:System.AppDomain.Load%2A?displayProperty=fullName> o un overload del metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> di cui il primo argomento è una stringa che rappresenta il nome visualizzato dell'assembly da caricare, ovvero la stringa restituita dalla proprietà <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName>.  
  
-   Un overload del metodo <xref:System.AppDomain.Load%2A?displayProperty=fullName> o un overload del metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> di cui il primo argomento è un oggetto <xref:System.Reflection.AssemblyName> che identifica l'assembly da caricare.  
  
-   Un overload del metodo <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>.  
  
-   Un overload del metodo <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=fullName> o <xref:System.AppDomain.CreateInstance%2A?displayProperty=fullName> che crea un'istanza di un oggetto in un altro dominio dell'applicazione.  
  
### Attività che il gestore eventi può eseguire  
 Il gestore dell'evento <xref:System.AppDomain.AssemblyResolve> riceve il nome visualizzato dell'assembly da caricare nella proprietà <xref:System.ResolveEventArgs.Name%2A?displayProperty=fullName>.  Se il gestore non riconosce il nome dell'assembly, restituisce null \(`Nothing` in Visual Basic, `nullptr` in Visual C\+\+\).  
  
 Se il gestore riconosce il nome dell'assembly, può caricare e restituire un assembly che soddisfi la richiesta.  Nell'elenco seguente vengono descritti alcuni scenari di esempio.  
  
-   Se il gestore conosce il percorso di una versione dell'assembly, può caricare l'assembly utilizzando il metodo <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName> o <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> e può restituire l'assembly caricato in caso di esito positivo.  
  
-   Se il gestore ha accesso a un database degli assembly archiviati come matrici di byte, può caricare una matrice di byte utilizzando uno degli overload del metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> che accetta una matrice di byte.  
  
-   Il gestore può generare un assembly dinamico e restituirlo.  
  
> [!NOTE]
>  Il gestore deve caricare l'assembly nel contesto di origine del caricamento, nel contesto di caricamento o senza contesto.  Se il gestore carica l'assembly nel contesto solo reflection utilizzando il metodo <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A?displayProperty=fullName> o <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A?displayProperty=fullName>, il tentativo di caricamento che ha generato l'evento <xref:System.AppDomain.AssemblyResolve> ha esito negativo.  
  
 Il gestore eventi deve restituire un assembly appropriato.  Il gestore può analizzare il nome visualizzato dell'assembly richiesto passando il valore della proprietà <xref:System.ResolveEventArgs.Name%2A?displayProperty=fullName> al costruttore <xref:System.Reflection.AssemblyName.%23ctor%28System.String%29>.  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], il gestore può utilizzare la proprietà <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=fullName> per determinare se la richiesta corrente è una dipendenza di un altro assembly.  Queste informazioni consentono di identificare un assembly che soddisfa la dipendenza.  
  
 Il gestore eventi può restituire una versione diversa dell'assembly anziché la versione che è stata richiesta.  
  
 Nella maggior parte dei casi, l'assembly che viene restituito dal gestore verrà visualizzato nel contesto di caricamento, indipendentemente dal contesto in cui viene caricato dal gestore.  Se, ad esempio, il gestore utilizza il metodo <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> per caricare un assembly nel contesto di origine del caricamento, l'assembly verrà visualizzato nel contesto di caricamento quando viene restituito dal gestore.  Nei seguenti casi, tuttavia, l'assembly viene visualizzato senza contesto quando viene restituito dal gestore:  
  
-   Il gestore carica un assembly senza contesto.  
  
-   La proprietà <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=fullName> non è null.  
  
-   L'assembly richiedente, ovvero l'assembly che viene restituito dalla proprietà <xref:System.ResolveEventArgs.RequestingAssembly%2A?displayProperty=fullName>, è stato caricato senza contesto.  
  
 Per ulteriori informazioni sui contesti, vedere l'overload del metodo <xref:System.Reflection.Assembly.LoadFrom%28System.String%29?displayProperty=fullName>.  
  
 È possibile caricare più versioni dello stesso assembly nello stesso dominio dell'applicazione.  Questa procedura non è consigliata poiché possono verificarsi problemi di assegnazione del tipo.  Vedere [Procedure consigliate per il caricamento di assembly](../../../docs/framework/deployment/best-practices-for-assembly-loading.md).  
  
### Attività che il gestore eventi non deve eseguire  
 La regola primaria per la gestione dell'evento <xref:System.AppDomain.AssemblyResolve> è quella di non tentare di restituire un assembly che non si riconosce.  Quando si scrive il gestore, è necessario conoscere gli assembly che possono causare la generazione dell'evento.  Il gestore deve restituire null per gli altri assembly.  
  
> [!IMPORTANT]
>  A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], l'evento <xref:System.AppDomain.AssemblyResolve> viene generato per gli assembly satellite.  Questa modifica influisce su un gestore eventi che è stato scritto per una versione precedente di .NET Framework, se il gestore tenta di risolvere tutte le richieste di caricamento dell'assembly.  I gestori eventi che ignorano gli assembly non riconoscono non sono interessati dalla modifica. Restituiscono null e vengono seguiti i normali meccanismi di fallback.  
  
 Nel caricamento di un assembly, il gestore eventi non deve utilizzare gli overload del metodo <xref:System.AppDomain.Load%2A?displayProperty=fullName> o <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> che possono causare la generazione dell'evento <xref:System.AppDomain.AssemblyResolve> in modo ricorsivo poiché può verificarsi un overflow dello stack. Vedere l'elenco fornito in precedenza in questo argomento. Ciò si verifica anche se si fornisce la gestione delle eccezioni per la richiesta di caricamento, poiché non viene generata alcuna eccezione finché non vengono restituiti tutti i gestori eventi.  Di conseguenza, il codice seguente genera un overflow dello stack se `MyAssembly` non viene trovato:  
  
 [!code-cpp[AssemblyResolveRecursive#1](../../../samples/snippets/cpp/VS_Snippets_CLR/assemblyresolverecursive/cpp/example.cpp#1)]
 [!code-csharp[AssemblyResolveRecursive#1](../../../samples/snippets/csharp/VS_Snippets_CLR/assemblyresolverecursive/cs/example.cs#1)]
 [!code-vb[AssemblyResolveRecursive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/assemblyresolverecursive/vb/example.vb#1)]  
  
## Vedere anche  
 [Procedure consigliate per il caricamento di assembly](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)   
 [Uso dei domini dell'applicazione](../../../docs/framework/app-domains/use.md)