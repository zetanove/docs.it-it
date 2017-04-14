---
title: "Considerazioni sulla sicurezza degli assembly | Microsoft Docs"
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
  - "assembly [.NET Framework], sicurezza"
  - "assembly [.NET Framework], firma"
  - "assembly [.NET Framework], con nome sicuro"
  - "concessione di autorizzazioni, assembly"
  - "integrità con assembly"
  - "nomi [.NET Framework], assembly"
  - "nomi [.NET Framework], nomi sicuri"
  - "autorizzazioni [.NET Framework], assembly"
  - "sicurezza [.NET Framework], assembly"
  - "signcode"
  - "firma di assembly"
  - "assembly con nome sicuro, considerazioni sulla sicurezza"
ms.assetid: 1b5439c1-f3d5-4529-bd69-01814703d067
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Considerazioni sulla sicurezza degli assembly
Quando si compila un assembly, è possibile specificare l'insieme di autorizzazioni che verranno richieste per consentirne l'esecuzione.  Se sussistano o meno le autorizzazioni per l'utilizzo di un assembly lo si evince dalle evidenze.  
  
 Le evidenze vengono utilizzate in due modi diversi:  
  
-   L'evidenza di input viene unita all'evidenza acquisita durante il caricamento per creare un set di evidenze finale utilizzato per la risoluzione dei criteri.  I metodi in cui viene utilizzata tale semantica sono **Assembly.Load**, **Assembly.LoadFrom** e **Activator.CreateInstance**.  
  
-   L'evidenza di input viene utilizzata non modificata come set di evidenze finale per la risoluzione dei criteri.  I metodi in cui viene utilizzata tale semantica sono **Assembly.Load\(byte\[\]\)** e **AppDomain.DefineDynamicAssembly\(\)**.  
  
 Autorizzazioni opzionali potranno essere concesse dai [criteri di sicurezza](../../../docs/framework/misc/code-access-security-basics.md) impostati sul computer che eseguirà l'assembly.  Se si desidera che il proprio codice gestisca tutte le possibili eccezioni di sicurezza, si può procedere in uno dei modi seguenti:  
  
-   Inserire una richiesta per tutte le autorizzazioni di cui il codice deve disporre e gestire gli errori che si verificheranno in fase di caricamento nel caso in cui le autorizzazioni non venissero riconosciute.  
  
-   Non prevedere una richiesta per le autorizzazioni eventualmente necessarie, ma limitarsi a predisporre la gestione delle eccezioni di sicurezza che si verificheranno in mancanza di tali autorizzazioni.  
  
    > [!NOTE]
    >  Quello della sicurezza è un tema complesso in cui è possibile scegliere tra molte possibili opzioni.  Per ulteriori informazioni, vedere [Concetti principali sulla sicurezza](../../../docs/standard/security/key-security-concepts.md).  
  
 In fase di caricamento, l'evidenza dell'assembly viene utilizzata come input per i criteri di sicurezza.  I criteri di sicurezza vengono stabiliti dall'azienda e dall'amministratore dei computer, così come dalle impostazioni adottate dallo stesso utente, e determinano l'insieme di autorizzazioni concesse a tutto il codice gestito che viene eseguito sul computer.  È possibile stabilire criteri di sicurezza basati sull'autore dell'assembly \(se questo dispone di una firma generata da uno strumento firma digitale\), sul sito Web e la zona \(come è definita in Internet Explorer\) da cui è stato effettuato il download dell'assembly o sul nome sicuro dell'assembly.  L'amministratore di un computer può ad esempio stabilire criteri di sicurezza che consentono a tutto il codice scaricato da un sito Web e firmato da una determinata azienda di software di accedere al database presente su un computer, ma non di scrivere sul disco rigido.  
  
## Assembly con nomi sicuri e strumenti firma digitale  
 È possibile firmare un assembly in due modi diversi ma complementari: con un nome sicuro o utilizzando [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) in .NET Framework versione 1.0 e 1.1 oppure [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md) nelle versioni successive di .NET Framework.  La firma di un assembly con un nome sicuro comporta l'aggiunta di una crittografia con chiave pubblica al file che contiene il manifesto dell'assembly.  La firma con nome sicuro garantisce l'univocità del nome, ne impedisce l'utilizzo fraudolento e fornisce un'identità al chiamante quando un riferimento viene risolto.  
  
 I nomi sicuri non garantiscono tuttavia alcun livello di attendibilità. A ciò provvedono infatti [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) e [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md).  I due strumenti firma digitale impongono all'autore di provare la propria identità a un'autorità terza per ottenere un certificato.  Il certificato viene poi incorporato nel file e può essere utilizzato da un amministratore per decidere se considerare attendibile l'autenticità del codice.  
  
 È possibile associare a un assembly il solo nome sicuro, la sola firma digitale creata mediante [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) o [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md) o entrambi.  Con i due strumenti firma digitale è possibile firmare un solo file alla volta. Nel caso di assembly su più file, si firmerà solo il file che contiene il manifesto dell'assembly.  Il nome sicuro viene memorizzato nel file che contiene il manifesto dell'assembly, mentre la firma creata mediante [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) o [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md) viene memorizzata in un'area riservata del file eseguibile portabile \(PE, Portable Executable\) che contiene il manifesto dell'assembly.  La firma di un assembly realizzata mediante [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) o [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md) può essere adottata \(con o senza un nome sicuro\) quando già si dispone di una gerarchia attendibile basata su firme generate [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) o [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md) o quando i propri criteri si avvalgono solo della chiave e non controllano la catena di attendibilità.  
  
> [!NOTE]
>  Quando a un assembly si assegna sia un nome sicuro che una firma digitale, il nome sicuro deve essere assegnato per primo.  
  
 Common Language Runtime esegue anche una verifica hash. Il manifesto dell'assembly contiene infatti un elenco di tutti i file che compongono l'assembly, comprensivo dell'hash generato per ciascun file al momento della compilazione del manifesto.  Quando si carica un file, viene calcolato il codice hash del relativo contenuto e viene eseguito un confronto con il valore hash archiviato nel manifesto.  Se i due hash non corrispondono, l'assembly non viene caricato.  
  
 Poiché nomi sicuri e firme create mediante [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) o [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md) garantiscono l'integrità, è possibile basare i criteri di sicurezza per l'accesso al codice su queste due evidenze degli assembly.  I nomi sicuri e le firme create mediante [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) o [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md) garantiscono l'integrità tramite firme digitali e certificati.  Tutte le tecnologie menzionate \(verifica hash, denominazioni sicure e firme create mediante [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db) o [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md)\) contribuiscono a garantire che l'assembly non sia stato alterato in alcun modo.  
  
## Vedere anche  
 [Assembly con nomi sicuri](../../../docs/framework/app-domains/strong-named-assemblies.md)   
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [SignTool.exe \(Sign Tool\)](../../../docs/framework/tools/signtool-exe.md)   
 [File Signing Tool \(Signcode.exe\)](http://msdn.microsoft.com/it-it/2d299154-34ea-41ba-ad12-17075bb7e1db)