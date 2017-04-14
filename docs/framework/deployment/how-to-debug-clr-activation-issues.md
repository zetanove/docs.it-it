---
title: "Procedura: debug dei problemi di attivazione CLR | Microsoft Docs"
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
  - "attivazione CLR, debug dei problemi"
ms.assetid: 4fe17546-d56e-4344-a930-6d8e4a545914
caps.latest.revision: 5
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: debug dei problemi di attivazione CLR
Se si verificano problemi nell'eseguire l'applicazione con la versione corretta di Common Language Runtime \(CLR\), è possibile visualizzare ed eseguire il debug dei registri di attivazione CLR.  Questi registri possono rivelarsi molto utili nella determinazione della causa principale di un problema di attivazione quando l'applicazione carica una versione di CLR diversa da quella prevista o non carica CLR affatto.  Di seguito [Errori di inizializzazione di .NET Framework: gestione dell'interfaccia utente](../../../docs/framework/deployment/initialization-errors-managing-the-user-experience.md) il caso in cui non viene trovato CLR per un'applicazione.  
  
 La registrazione dell'attivazione di CLR può essere abilitata a livello di sistema utilizzando una chiave del Registro di sistema HKEY\_LOCAL\_MACHINE o una variabile di ambiente di sistema.  Il log verrà generato finché la voce del Registro di sistema o la variabile di ambiente non verrà rimossa.  In alternativa, è possibile utilizzare una variabile di ambiente a livello locale o una variabile dell'utente per attivare la registrazione con ambiti e durate differenti.  
  
 I registri di attivazione CLR non devono essere confusi con i [log di associazione assembly](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md), che sono completamente diversi.  
  
## Per attivare la registrazione dell'attivazione di CLR  
  
#### Utilizzo del Registro di sistema  
  
1.  Nell'editor del Registro di sistema, passare alla cartella HKEY\_LOCAL\_MACHINE \\ SOFTWARE \\ Microsoft \\ .NETFramework \(in un computer a 32 bit\) o HKEY\_LOCAL\_MACHINE \\ SOFTWARE \\ Wow6432Node \\ Microsoft \\ .NETFramework \(in un computer a 64 bit.  
  
2.  Aggiungere un valore stringa denominato `CLRLoadLogDir`e impostarlo sul percorso completo di una directory esistente in cui si desidera archiviare i registri di attivazione CLR.  
  
 La registrazione di attivazione rimane attiva finché non verrà rimosso il valore nella stringa.  
  
#### Utilizzo di una variabile di ambiente  
  
-   Impostare la variabile di ambiente `COMPLUS_CLRLoadLogDir` con una stringa che rappresenta il percorso completo di una directory esistente in cui si desidera archiviare i registri di attivazione CLR.  
  
     Come impostare la variabile di ambiente determinate il relativo ambito:  
  
    -   Se impostata a livello di sistema, l'attività di registrazione dell'attivazione è abilitato per tutte le applicazioni .NET Framework nel computer finché non verrà rimossa la variabile di ambiente.  
  
    -   Se impostata a livello utente, la registrazione dell'attivazione è abilitata solo per l'account utente corrente.  La registrazione continua finché non viene rimossa la variabile di ambiente.  
  
    -   Se impostata dal processo, prima del caricamento di CLR, l'attività di registrazione dell'attivazione viene attivata finché non termina il processo.  
  
    -   Se impostata dal prompt dei comandi prima di eseguire un'applicazione, la registrazione dell'attivazione è abilitata per qualsiasi applicazione eseguita da quel prompt.  
  
     Ad esempio, per memorizzare l'attivazione nella directory c:\\clrloadlogs con ambito a livello di processo, aprire una finestra del prompt dei comandi e digitare il seguente codice prima di eseguire l'applicazione:  
  
    ```  
    set COMPLUS_CLRLoadLogDir=c:\clrloadlogs  
    ```  
  
## Esempio  
 I registri di attivazione di CLR forniscono una grande quantità di dati riguardanti l'attivazione di CLR e l'utilizzo delle API di hosting CLR.  La maggior parte di questi dati è utilizzato internamente da Microsoft, ma alcuni dati possono essere utili agli sviluppatori, come descritto in questo articolo.  
  
 Il log rispecchia l'ordine in cui le API di hosting di CLR sono chiamate.  Include inoltre dati utili sul set di runtime installati rilevate sul computer.  Il formato del registro stesso di attivazione CLR non viene documentato, ma può essere utilizzato dagli sviluppatori che devono risolvere problemi di attivazione CLR.  
  
> [!NOTE]
>  Non è possibile aprire il log di attivazione finchè il processo che utilizza CLR non è terminato.  
  
> [!NOTE]
>  i registri di attivazione di CLR non sono localizzati; vengono generati sempre in lingua inglese.  
  
 Nell'esempio successivo viene mostrato un log di attivazione, la maggior parte delle informazioni utili vengono evidenziate e descritte dopo il log.  
  
```  
532,205950.367,CLR Loading log for C:\Tests\myapp.exe   
532,205950.367,Log started at 4:26:12 PM on 10/6/2011   
532,205950.367,-----------------------------------   
532,205950.382,FunctionCall: _CorExeMain   
532,205950.382,FunctionCall: ClrCreateInstance, Clsid: {2EBCD49A-1B47-4A61-B13A-4A03701E594B}, Iid: {E2190695-77B2-492E-8E14-C4B3A7FDD593}   
532,205950.382,MethodCall: ICLRMetaHostPolicy::GetRequestedRuntime. Version: (null), Metahost Policy Flags: 0x168, Binary: (null), Iid: {BD39D1D2-BA2F-486A-89B0-B4B0CB466891}   
532,205950.382,Installed Runtime: v4.0.30319. VERSION_ARCHITECTURE: 0   
532,205950.382,Input values for ComputeVersionString follow this line   
532,205950.382,-----------------------------------   
532,205950.382,Default Application Name: C:\Tests\myapp.exe   
532,205950.382,IsLegacyBind is: 0   
532,205950.382,IsCapped is 0   
532,205950.382,SkuCheckFlags are 0   
532,205950.382,ShouldEmulateExeLaunch is 0   
532,205950.382,LegacyBindRequired is 0   
532,205950.382,-----------------------------------   
532,205950.382,Parsing config file: C:\Tests\myapp.exe   
532,205950.382,UseLegacyV2RuntimeActivationPolicy is set to 0   
532,205950.382,LegacyFunctionCall: GetFileVersion. Filename: C:\Tests\myapp.exe   
532,205950.382,LegacyFunctionCall: GetFileVersion. Filename: C:\Tests\myapp.exe   
532,205950.382,C:\Tests\myapp.exe was built with version: v2.0.50727   
532,205950.382,ERROR: Version v2.0.50727 is not present on the machine.   
532,205950.398,SEM_FAILCRITICALERRORS is set to 0   
532,205950.398,Launching feature-on-demand installation. CmdLine: C:\Windows\system32\fondue.exe /enable-feature:NetFx3   
532,205950.398,FunctionCall: RealDllMain. Reason: 0   
532,205950.398,FunctionCall: OnShimDllMainCalled. Reason: 0  
  
```  
  
-   **registro di caricamento di CLR** fornisce il percorso dell'eseguibile che ha iniziato il processo che ha caricato il codice gestito.  Si noti che questo potrebbe essere un host nativo.  
  
    ```  
    532,205950.367,CLR Loading log for C:\Tests\myapp.exe  
  
    ```  
  
-   **runtime installati** sono l'insieme di versioni di CLR installate nel computer, candidate per la richiesta di attivazione.  
  
    ```  
    532,205950.382,Installed Runtime: v4.0.30319. VERSION_ARCHITECTURE: 0  
  
    ```  
  
-   **compilato con la versione** è la versione di CLR utilizzata per compilare il file binario che è stato assegnato a un metodo come [ICLRMetaHostPolicy::GetRequestedRuntime](../Topic/ICLRMetaHostPolicy::GetRequestedRuntime%20Method.md).  
  
    ```  
    532,205950.382,C:\Tests\myapp.exe was built with version: v2.0.50727  
  
    ```  
  
-   **installazione di funzionalità su richiesta** si riferisce all'abilitazione di .NET Framework 3.5 in Windows 8.  Per ulteriori informazioni su questo scenario, vedere [Errori di inizializzazione di .NET Framework: gestione dell'interfaccia utente](../../../docs/framework/deployment/initialization-errors-managing-the-user-experience.md).  
  
    ```  
    532,205950.398,Launching feature-on-demand installation. CmdLine: C:\Windows\system32\fondue.exe /enable-feature:NetFx3  
  
    ```  
  
## Vedere anche  
 [Distribuzione](../../../docs/framework/deployment/net-framework-and-applications.md)   
 [Procedura: configurare un'applicazione per supportare .NET Framework 4 o 4.5](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)