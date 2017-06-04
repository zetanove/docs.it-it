---
title: "Installutil.exe (Installer Tool) | Microsoft Docs"
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
  - "uninstalling server resources"
  - "removing server resources"
  - "status information for installation"
  - "installation progress reports"
  - "installing server resources"
  - "Installer tool"
  - "Installutil.exe"
  - "files, Installer tool"
  - "progress information for installation"
  - "reporting installation progress"
ms.assetid: 3f9d0533-f895-4897-b4ea-528284e0241d
caps.latest.revision: 40
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 38
---
# Installutil.exe (Installer Tool)
Lo strumento Programma di installazione è un'utilità da riga di comando che consente di installare e disinstallare le risorse del server eseguendo i componenti del programma di installazione di assembly specificati.  Questo strumento funziona insieme alle classi nello spazio dei nomi <xref:System.Configuration.Install>.  
  
 Viene installato automaticamente con Visual Studio.  Per eseguire lo strumento, utilizzare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per ulteriori informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
installutil [/u[ninstall]] [options] assembly [[options] assembly] ...   
```  
  
#### Parametri  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|`assembly`|Nome file dell'assembly in cui eseguire i componenti del programma di installazione.  Omettere questo parametro se si desidera specificare il nome sicuro dell'assembly utilizzando l'opzione `/AssemblyName`.|  
  
<a name="options"></a>   
## Opzioni  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|`/h[elp]`<br /><br /> \- oppure \-<br /><br /> `/?`|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|`/help` *assembly*<br /><br /> \- oppure \-<br /><br /> `/?` *assembly*|Visualizza le opzioni aggiuntive riconosciute dai singoli programmi di installazione all'interno dell'assembly specificato, insieme alla sintassi e alle opzioni di comando di InstallUtil.exe.  Questa opzione aggiunge il testo restituito dalla proprietà <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=fullName> di ogni componente del programma di installazione al testo della Guida di InstallUtil.exe.|  
|`/AssemblyName` "*assemblyName*<br /><br /> ,Version\=*major.minor.build.revision*<br /><br /> ,Culture\=*locale*<br /><br /> ,PublicKeyToken\=*publicKeyToken*"|Specifica il nome sicuro di un assembly, che verrà registrato nella Global Assembly Cache.  Il nome dell'assembly deve essere completo, con versione, impostazioni cultura e token di chiave pubblica.  Il nome completo deve essere racchiuso tra virgolette.<br /><br /> Ad esempio, "myAssembly, Culture\=neutral, PublicKeyToken\=0038abc9deabfle5, Version\=4.0.0.0" è un nome di assembly completo.|  
|`/InstallStateDir=[` *directoryName* `]`|Specifica la directory del file con estensione InstallState contenente i dati utilizzati per la disinstallazione dell'assembly.  La directory predefinita è quella che contiene l'assembly.|  
|`/LogFile=`\[*filename*\]|Specifica il nome del file di log in cui è registrato lo stato dell'installazione.  Per impostazione predefinita, se l'opzione `/LogFile` viene omessa, viene creato un file di log denominato *assemblyname*.InstallLog.  Se *filename* viene omesso, nessun file di log verrà generato.|  
|`/LogToConsole`\={`true`&#124;`false`}|Se `true`, visualizza l'output sulla console.  Se `false` \(impostazione predefinita\), evita la visualizzazione dell'output sulla console.|  
|`/ShowCallStack`|Restituisce lo stack di chiamate al file di log se si verifica un'eccezione durante l'installazione.|  
|`/u`\[`ninstall`\]|Disinstalla gli assembly specificati.  A differenza delle altre opzioni, `/u` si applica a tutti gli assembly, indipendentemente dalla posizione dell'opzione nella riga di comando.|  
  
<a name="cmdline"></a>   
## Opzioni aggiuntive del programma di installazione  
 I singoli programmi di installazione utilizzati all'interno di un assembly sono in grado di riconoscere opzioni oltre a quelle elencate nella sezione [Opzioni](#options).  Per ulteriori informazioni su queste opzioni, eseguire InstallUtil.exe con i percorsi degli assembly sulla riga di comando con l'opzione `/?` o `/help`.  Per specificare queste opzioni, includerle nella riga di comando con le opzioni riconosciute da InstallUtil.exe.  
  
> [!NOTE]
>  Il testo della Guida sulle opzioni supportate da singoli componenti del programma di installazione viene restituito dalla proprietà <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=fullName>.  Le singole opzioni che sono state inserite nella riga di comando sono accessibili a livello di codice dalla proprietà <xref:System.Configuration.Install.Installer.Context%2A?displayProperty=fullName>.  
  
 Tutte le opzioni e i parametri della riga di comando vengono scritti nel file di log dell'installazione.  Tuttavia, se si utilizza il parametro `/Password`, che è riconosciuto da alcuni componenti del programma di installazione, le informazioni relative alla password verranno sostituite da otto asterischi \(\*\) e non verranno visualizzate nel file di log.  
  
> [!IMPORTANT]
>  In alcuni casi, i parametri passati al programma di installazione possono includere informazioni riservate o personali che, per impostazione predefinita, vengono scritte in un file di log di testo normale.  Per evitare questo comportamento, è possibile eliminare il file di log specificando `/LogFile=` \(senza l'argomento *filename*\) dopo Installutil.exe nella riga di comando.  
  
## Note  
 Le applicazioni .NET Framework sono costituite da file di programma tradizionali e risorse associate, quali code di messaggi, log eventi e contatori delle prestazioni, che è necessario creare quando l'applicazione viene distribuita.  È possibile utilizzare i componenti del programma di installazione di un assembly per creare queste risorse quando l'applicazione viene installata e rimuoverle quando l'applicazione viene disinstallata.  Installutil.exe rileva ed esegue questi componenti del programma di installazione.  
  
 È possibile specificare più assembly nella stessa riga di comando.  Qualsiasi opzione specificata prima del nome di un assembly ha effetto sull'installazione di tale assembly.  Fatta eccezione per `/u` e `/AssemblyName`, le opzioni sono cumulative ma sottoponibili a override.  In altre parole, le opzioni specificate per un assembly vengono applicate a tutti gli assembly successivi a meno che l'opzione non venga specificata con un nuovo valore.  
  
 Se si esegue Installutil.exe su un assembly senza specificare alcuna opzione, i tre file seguenti verranno inseriti nella directory dell'assembly:  
  
-   InstallUtil.InstallLog \- Contiene una descrizione generale dello stato dell'installazione.  
  
-   *assemblyname*.InstallLog \- Contiene informazioni specifiche della fase di commit del processo di installazione.  Per ulteriori informazioni sulla fase di commit, vedere il metodo <xref:System.Configuration.Install.Installer.Commit%2A>.  
  
-   *assemblyname*.InstallState \- Contiene i dati utilizzati per disinstallare l'assembly.  
  
 Installutil.exe utilizza la reflection per esaminare gli assembly specificati e individuare tutti i tipi <xref:System.Configuration.Install.Installer> il cui attributo <xref:System.ComponentModel.RunInstallerAttribute?displayProperty=fullName> è impostato su `true`.  Lo strumento esegue quindi il metodo <xref:System.Configuration.Install.Installer.Install%2A?displayProperty=fullName> o <xref:System.Configuration.Install.Installer.Uninstall%2A?displayProperty=fullName> su ciascuna istanza del tipo <xref:System.Configuration.Install.Installer>.  Installutil.exe esegue l'installazione in modo transazionale: se risulta impossibile installare uno degli assembly, viene eseguito il rollback dell'installazione di tutti gli altri assembly.  La disinstallazione non è invece transazionale.  
  
 Installutil.exe può installare o disinstallare assembly con nome sicuro, ma non assembly con firma ritardata.  
  
 A partire da .NET Framework versione 2.0, la versione a 32 bit di Common Language Runtime \(CLR\) viene fornita solo con la versione a 32 bit dello strumento Programma di installazione, mentre la versione a 64 bit di CLR viene fornita con le versioni a 32 bit e a 64 bit di questo strumento.  Se si utilizza CLR a 64 bit, occorre utilizzare lo strumento Programma di installazione a 32 bit per installare assembly a 32 bit e quello a 64 bit per installare assembly a 64 bit e MSIL \(Microsoft Intermediate Language\).  Il funzionamento delle due versioni dello strumento Programma di installazione è identico.  
  
 Non è possibile utilizzare Installutil.exe per distribuire un servizio di Windows creato utilizzando C\+\+ perché Installutil.exe non è in grado di riconoscere il codice nativo incorporato generato dal compilatore C\+\+.  Se si tenta di distribuire un servizio di Windows C\+\+ con Installutil.exe, verrà generata un'eccezione quale <xref:System.BadImageFormatException>.  Per operare con questo scenario, spostare il codice del servizio in un modulo C\+\+, quindi scrivere l'oggetto del programma di installazione in C\# o in Visual Basic.  
  
## Esempi  
 Il comando che segue visualizza una descrizione della sintassi e delle opzioni di comando per InstallUtil.exe.  
  
```  
installutil /?  
```  
  
 Il comando che segue visualizza una descrizione della sintassi e delle opzioni di comando per InstallUtil.exe.  Visualizza inoltre una descrizione e un elenco delle opzioni supportate dai componenti del programma di installazione in `myAssembly.exe` se il testo della Guida è stato assegnato alla proprietà <xref:System.Configuration.Install.Installer.HelpText%2A?displayProperty=fullName> del programma di installazione.  
  
```  
installutil /? myAssembly.exe  
```  
  
 Il comando che segue esegue i componenti del programma di installazione nell'assembly `myAssembly.exe`.  
  
```  
installutil myAssembly.exe  
```  
  
 Il comando che segue esegue i componenti del programma di installazione in un assembly utilizzando l'opzione `/AssemblyName` e un nome completo.  
  
```  
installutil /AssemblyName "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0"  
```  
  
 Il comando che segue esegue i componenti del programma di installazione in un assembly specificato in base al nome file e in un assembly specificato in base al nome sicuro.  Si noti che tutti gli assembly specificati in base al nome file devono precedere gli assembly specificati in base al nome sicuro nella riga di comando, poiché l'opzione `/AssemblyName` non può essere sottoposta a override.  
  
```  
installutil myAssembly.exe /AssemblyName "myAssembly, Culture=neutral, PublicKeyToken=0038abc9deabfle5, Version=4.0.0.0"  
```  
  
 Il comando che segue esegue i componenti del programma di disinstallazione nell'assembly `myAssembly.exe`.  
  
```  
installutil /u myAssembly.exe   
```  
  
 Il comando seguente esegue i componenti del programma di disinstallazione negli assembly `myAssembly1.exe` e `myAssembly2.exe`.  
  
```  
installutil myAssembly1.exe /u myAssembly2.exe  
```  
  
 Poiché la posizione dell'opzione `/u` nella riga di comando non è importante, questo è equivalente al comando seguente.  
  
```  
installutil /u myAssembly1.exe myAssembly2.exe  
```  
  
 Il comando che segue esegue i programmi di installazione nell'assembly `myAssembly.exe` e specifica che le informazioni sullo stato verranno scritte in `myLog.InstallLog`.  
  
```  
installutil /LogFile=myLog.InstallLog myAssembly.exe   
```  
  
 Il comando che segue esegue i programmi di installazione contenuti nell'assembly `myAssembly.exe`, specifica che le informazioni sullo stato di avanzamento devono essere scritte in `myLog.InstallLog` e utilizza l'opzione `/reg` personalizzata dei programmi di installazione per specificare che è necessario aggiornare il Registro di sistema.  
  
```  
installutil /LogFile=myLog.InstallLog /reg=true myAssembly.exe  
```  
  
 Il comando che segue esegue i programmi di installazione contenuti nell'assembly `myAssembly.exe`, utilizza l'opzione `/email` personalizzata del programma di installazione per specificare l'indirizzo di posta elettronica dell'utente ed elimina l'output al file di log.  
  
```  
installutil /LogFile= /email=admin@mycompany.com myAssembly.exe  
```  
  
 Il comando che segue scrive lo stato dell'installazione di `myAssembly.exe` in `myLog.InstallLog` e quello di `myTestAssembly.exe` in `myTestLog.InstallLog`.  
  
```  
installutil /LogFile=myLog.InstallLog myAssembly.exe /LogFile=myTestLog.InstallLog myTestAssembly.exe  
```  
  
## Vedere anche  
 <xref:System.Configuration.Install>   
 [Tools](../../../docs/framework/tools/index.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)