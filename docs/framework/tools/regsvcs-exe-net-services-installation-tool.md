---
title: "Regsvcs.exe (.NET Services Installation Tool) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Regsvcs.exe"
  - ".NET Services Installation tool"
  - "loading assemblies"
  - "assemblies [.NET Framework], registering"
  - "type libraries"
  - "registering assemblies"
ms.assetid: 5220fe58-5aaf-4e8e-8bc3-b78c63025804
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Regsvcs.exe (.NET Services Installation Tool)
Lo strumento di installazione dei servizi .NET effettua le seguenti operazioni:  
  
-   Carica e registra un assembly.  
  
-   Genera, registra e installa una libreria dei tipi in un'applicazione COM\+ specificata.  
  
-   Configura i servizi aggiunti alla classe a livello di codice.  
  
 Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
regsvcs [/c | /fc | /u] [/tlb:typeLibraryFile] [/extlb] [/reconfig] [/componly] [/appname:applicationName] [/nologo] [/quiet]assemblyFile.dll   
```  
  
#### Parametri  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|*assemblyFile.dll*|File di assembly di origine.  L'assembly deve essere firmato con un nome sicuro.  Per altre informazioni, vedere [Firma di un assembly con un nome sicuro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).|  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/appdir:** *path*|Specifica la directory radice dell'applicazione.|  
|**\/appname:** *applicationName*|Specifica il nome dell'applicazione COM\+ da trovare o creare.|  
|**\/c**|Crea l'applicazione di destinazione.|  
|**\/componly**|Configura solo i componenti, ignorando metodi e interfacce.|  
|**\/exapp**|Indica allo strumento di prevedere un'applicazione esistente.|  
|**\/extlb**|Utilizza una libreria dei tipi esistente.|  
|**\/fc**|Trova o crea l'applicazione di destinazione.|  
|**\/help**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|**\/noreconfig**|Non riconfigura un'applicazione di destinazione esistente.|  
|**\/nologo**|Evita la visualizzazione del messaggio di avvio Microsoft.|  
|**\/parname:** *name*|Specifica il nome o l'ID dell'applicazione COM\+ da trovare o creare.|  
|**\/reconfig**|Riconfigura un'applicazione di destinazione esistente.  Questa è l'impostazione predefinita.|  
|**\/tlb:** *typelibraryfile*|Specifica il file della libreria dei tipi da installare.|  
|**\/u**|Disinstalla l'applicazione di destinazione.|  
|**\/quiet**|Specifica la modalità non interattiva; non visualizza il logo e i messaggi di esito positivo.|  
|**\/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
## Note  
 Regsvcs.exe richiede un file di assembly di origine specificato da *assemblyFile.dll*.  L'assembly deve essere firmato con un nome sicuro.  Per altre informazioni sulla firma con un nome sicuro, vedere [Firma di un assembly con un nome sicuro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).  I nomi dell'applicazione di destinazione e del file della libreria dei tipi sono facoltativi.  L'argomento *applicationName* può essere generato dal file di assembly di origine e, se non esiste già, viene creato.  L'argomento *typelibraryfile* può specificare il nome di una libreria dei tipi.  Se non lo si specifica, come impostazione predefinita verrà usato il nome dell'assembly.  
  
 Quando vengono registrati i metodi di un componente, lo strumento è soggetto a [richieste](http://msdn.microsoft.com/it-it/e5283e28-2366-4519-b27d-ef5c1ddc1f48) e [richieste di collegamento](../../../docs/framework/misc/link-demands.md) su questi metodi.  Poiché lo strumento viene eseguito in un ambiente completamente attendibile, molte richieste di autorizzazione vengono completate.  Regsvcs.exe non è tuttavia in grado di registrare componenti con metodi protetti da una richiesta o una richiesta di collegamento per <xref:System.Security.Permissions.StrongNameIdentityPermission> o <xref:System.Security.Permissions.PublisherIdentityPermission>.  
  
 Per usare Regsvcs.exe, è necessario disporre dei privilegi amministrativi sul computer locale.  
  
 Se durante una di queste operazioni l'esecuzione di Regsvcs.exe si interrompe, verranno visualizzati messaggi di errore pertinenti.  
  
## Esempi  
 Il comando che segue aggiunge a `myTest.dll` \(un'applicazione COM\+ esistente\) tutte le classi pubbliche contenute in `myTargetApp` e produce la libreria dei tipi `myTest.tlb`.  
  
```  
regsvcs /appname:myTargetApp myTest.dll  
```  
  
 Il comando che segue aggiunge a `myTest.dll` \(un'applicazione COM\+ esistente\) tutte le classi pubbliche contenute in `myTargetApp` e produce la libreria dei tipi `newTest.tlb`.  
  
```  
regsvcs /appname:myTargetApp /tlb:newTest.tlb myTest.dll  
```  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Procedura: firmare un assembly con un nome sicuro](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)