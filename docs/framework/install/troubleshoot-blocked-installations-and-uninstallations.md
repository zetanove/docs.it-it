---
title: Risoluzione dei problemi relativi alle installazioni e disinstallazioni bloccate di .NET Framework | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework, troubleshooting blocked installations
- blocked .NET Framework installations, troubleshooting
ms.assetid: c3fdfbc1-ed99-4202-a2b0-8c4f1646385d
caps.latest.revision: 57
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: ddcefb2b35f8cbf06a3abcc16158eee850f799ff
ms.openlocfilehash: 55228928d5d3d95cf28384e5179a43bfb0f598e9
ms.contentlocale: it-it
ms.lasthandoff: 05/11/2017

---
# <a name="troubleshooting-blocked-net-framework-installations-and-uninstallations"></a>Risoluzione dei problemi relativi alle installazioni e disinstallazioni bloccate di .NET Framework
Durante l'esecuzione del [programma di installazione Web oppure offline](../../../docs/framework/install/guide-for-developers.md) di .NET Framework 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2 o 4.7, potrebbe verificarsi un problema che impedisce o blocca l'installazione di .NET Framework. Nella tabella seguente sono elencati i possibili problemi di blocco e i collegamenti a informazioni sulla risoluzione dei problemi.  
  
 In Windows 8 e versioni successive, .NET Framework è un componente del sistema operativo e non può essere disinstallato in modo indipendente. Gli aggiornamenti di .NET Framework vengono visualizzati nella scheda **Aggiornamenti installati** dell'app **Programmi e funzionalità** del Pannello di controllo. Per i sistemi operativi in cui .NET Framework non è preinstallato, .NET Framework viene visualizzato nella scheda **Disinstalla o modifica programma** (o nella scheda **Aggiungi/Rimuovi programmi**) dell'app **Programmi e funzionalità** del Pannello di controllo. Per informazioni sulle versioni di Windows in cui è preinstallato .NET Framework, vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md).  

> [!IMPORTANT]
> Dato che le versioni 4.x di .NET Framework sono aggiornamenti sul posto, è possibile installare una versione precedente di .NET Framework 4.x in un sistema in cui è già installata una versione successiva. Ad esempio, in un sistema con Windows 10 Creators Update non è possibile installare .NET Framework 4.6.2, perché .NET Framework 4.7 è preinstallato con il sistema operativo.  
  
 È possibile determinare le versioni di .NET Framework installate in un sistema. Per altre informazioni, vedere [Procedura: determinare le versioni di .NET Framework installate](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md).  
  
 In questa tabella, 4.5. *x* fa riferimento a .NET Framework 4.5 e alle relative versioni intermedie, 4.5.1, 4.5.2 e 4.6.*x* fa riferimento a .NET Framework 4.6 e alle relative versioni intermedie, 4.6.1 e 4.6.2, e 4.7 indica .NET Framework 4.7.  
  
|Messaggio di blocco|Per altre informazioni o per risolvere il problema|  
|----------------------|--------------------------------------------------|  
|La disinstallazione di Microsoft .NET Framework può compromettere il corretto funzionamento di alcune applicazioni.|In generale, non è opportuno disinstallare alcuna versione di .NET Framework dal computer, perché un'applicazione in uso potrebbe dipendere da una relativa versione specifica. Per altre informazioni, vedere [.NET Framework per utenti](../../../docs/framework/get-started/index.md#ForUsers) nella *Guida introduttiva*.|  
|.NET Framework 4.5*.x*/4.6*.x*/4.7 (ITA) o una versione successiva è già installato nel computer.|Nessuna azione necessaria.<br /><br /> Per determinare le versioni di .NET Framework installate in un sistema, vedere [Procedura: Determinare le versioni di .NET Framework installate](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md).|  
|Per .NET Framework 4.5*.x*/4.6*.x*/4.7 (*lingua*) è richiesto .NET Framework 4.5*.x*/4.6*.x*. Installare .NET Framework 4.5*.x*/4.6*.x* dall'Area download ed eseguire di nuovo l'installazione.|Prima di installare un Language Pack, è necessario installare la versione inglese della versione di .NET Framework specificata. Per altre informazioni, vedere la sezione relativa all'[installazione dei Language Pack](../../../docs/framework/install/guide-for-developers.md#to-install-language-packs) nella guida all'installazione.|  
|Non è possibile installare .NET Framework 4.5*.x*/4.6*.x*/4.7. Altre applicazioni sul computer non sono compatibili con questo programma.<br /><br /> -oppure-<br /><br /> Altre applicazioni sul computer non sono compatibili con questo programma.|La causa più probabile del messaggio è che è stata installata una versione di anteprima o RC di .NET Framework. Disinstallare la versione di anteprima o RC ed eseguire nuovamente l'installazione.|  
|.NET Framework 4.5*.x*/4.6*.x*/4.7 non può essere disinstallato usando questo pacchetto. Per disinstallare .NET Framework 4.5*.x*/4.6*.x* dal computer in uso, passare al **Pannello di controllo**, scegliere **Programmi e funzionalità**, quindi **Visualizza aggiornamenti installati**, selezionare Aggiornamento per Microsoft Windows (KB2828152) e quindi scegliere **Disinstalla**.|Tramite il pacchetto che si sta installando, non viene eseguita la disinstallazione delle versioni di anteprima o RC di .NET Framework.<br /><br /> Disinstallare la versione di anteprima o RC dal Pannello di controllo.|  
|Non è possibile disinstallare .NET Framework 4.5*.x*/4.6*.x*/4.7. Altre applicazioni del computer dipendono da questo programma.|In generale, non è opportuno disinstallare alcuna versione di .NET Framework dal computer, perché un'applicazione in uso potrebbe dipendere da una relativa versione specifica. Per altre informazioni, vedere [.NET Framework per utenti](../../../docs/framework/get-started/index.md#ForUsers) nella *Guida introduttiva*.|  
|.NET Framework 4.5*.x*/4.6*.x*/4.7 ridistribuibile non si applica a questo sistema operativo. Scaricare .NET Framework 4.5*.x*/4.6*.x* per il sistema operativo in uso dall'Area download Microsoft.|È possibile che si stia tentando di installare [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], 4.5.2, 4.6, 4.6.1, 4.6.2 o 4.7 in una piattaforma non supportata o che sia stato scelto il pacchetto di installazione che non include i componenti per tutti i sistemi operativi supportati. Eseguire nuovamente l'installazione usando il programma di installazione offline ([per 4.5.1](http://go.microsoft.com/fwlink/p/?LinkId=309493), [per 4.5.2](http://go.microsoft.com/fwlink/p/?LinkId=397706), [per 4.6](http://go.microsoft.com/fwlink/p/?LinkId=528233), [per 4.6.1](http://go.microsoft.com/fwlink/p/?LinkId=671744), per [4.6.2](http://go.microsoft.com/fwlink/p/?LinkId=780604)) oppure per [4.7](http://go.microsoft.com/fwlink/p/?LinkId=825306). Per altre informazioni, vedere la [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md) e i [requisiti di sistema](../../../docs/framework/get-started/system-requirements.md) per i sistemi operativi supportati.|  
|L'aggiornamento corrispondente KB\<*numero*> deve essere installato prima di poter installare questo prodotto.|L'installazione di .NET Framework richiede che sia installato un aggiornamento KB prima di installare .NET Framework. Installare l'aggiornamento e quindi avviare nuovamente l'installazione di .NET Framework.<br /><br /> Ad esempio, l'installazione di versioni aggiornate di .NET Framework in Windows 8.1, Windows RT 8.1 e Windows Server 2012 R2 richiede che sia installato l'aggiornamento corrispondente a [KB 2919355](https://support.microsoft.com/kb/2919355).|  
|Nel computer è attualmente in esecuzione un'installazione Server Core del sistema operativo Windows Server 2008. .NET Framework 4.5.*x* richiede una versione successiva del sistema operativo. Installare Windows Server 2008 R2 SP1 o versione successiva ed eseguire nuovamente l'installazione di .NET Framework 4.5.*x*.|[!INCLUDE[net_v451](../../../includes/net-v451-md.md)] e 4.5.2 sono supportati nel ruolo Server Core con Windows Server 2008 R2 SP1 o versioni successive. Vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md).|  
|Non si dispone dei privilegi sufficienti per completare l'operazione per tutti gli utenti del computer. Accedere come amministratore ed eseguire nuovamente il **programma di installazione**.|Per installare .NET Framework è necessario essere un amministratore del computer.|  
|Impossibile continuare l'installazione poiché un'installazione precedente richiede il riavvio del computer. Riavviare il computer ed eseguire nuovamente l'installazione.|Talvolta è necessario riavviare il computer per completare l'installazione. Seguire le istruzioni relative al riavvio del computer ed eseguire nuovamente l'installazione.<br /><br /> In rari casi, potrebbe essere richiesto di riavviare il sistema più volte se Windows rileva un certo numero di aggiornamenti mancanti ed esegue un riavvio per installare l'aggiornamento successivo in coda.|  
|Impossibile eseguire il programma di installazione di .NET Framework in modalità di compatibilità dei programmi.|Vedere la sezione [Problemi di compatibilità del programma](#compat) più avanti in questo articolo.|  
|.NET Framework 4.5*.x*/4.6*.x*/4.7 non è stato installato perché l'archivio componenti è danneggiato.|Per altre informazioni, vedere [Correggere gli errori di Windows Update utilizzando Gestione e manutenzione immagini distribuzione o lo strumento di analisi della conformità agli aggiornamenti di sistema](https://support.microsoft.com/en-us/kb/947821).|  
|Impossibile eseguire l'installazione perché nel computer non è disponibile il servizio Windows Installer.|Vedere [Messaggio di errore "Impossibile accedere al servizio Windows Installer" quando si tenta di installare un programma](http://go.microsoft.com/fwlink/p/?LinkId=248684).|  
|Nel computer non è disponibile il servizio Windows Update. L'installazione potrebbe non essere eseguita correttamente.|Il computer può essere configurato per l'utilizzo di Windows Server Update Services (WSUS) invece di Microsoft Windows Update. Per altre informazioni, vedere la sezione relativa al codice di errore 0x800F0906 in [Codici di errore quando si prova a installare .NET Framework 3.5 in Windows 8 o in Windows Server 2012](http://support.microsoft.com/kb/2734782).<br /><br /> Vedere anche [Come ottenere la versione più recente dell'agente di Windows Update per gestire gli aggiornamenti in un computer](http://go.microsoft.com/fwlink/p/?LinkId=248437) nel sito Web del supporto tecnico Microsoft.|  
|Nel computer non è disponibile il servizio di trasferimento intelligente in background. L'installazione potrebbe non essere eseguita correttamente.|Vedere [Un aggiornamento per evitare che un arresto anomalo del servizio trasferimento intelligente in background (BITS) in un computer basato su Windows Vista](http://go.microsoft.com/fwlink/p/?LinkId=248680) nel sito Web del supporto tecnico Microsoft.|  
|Il programma di installazione non viene eseguito correttamente perché Windows Update ha rilevato un errore e visualizzato il codice di errore 0x80070643 o 0x643.|Vedere [Errore di installazione dell'aggiornamento di .NET Framework: "0x80070643" o "0x643"](https://support.microsoft.com/kb/976982) nel sito Web del supporto Microsoft.|  
|.NET Framework 4.5.*.x*/4.6*.x*/4.7 è già installato in questo sistema operativo. Non è necessario installare .NET Framework 4.5*.x*/4.6*.x*/4.7 ridistribuibile.|Nessuna azione.<br /><br /> Per determinare le versioni di .NET Framework installate in un sistema, vedere [Procedura: Determinare le versioni di .NET Framework installate](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md). Per i sistemi operativi supportati, vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md).|  
|.NET Framework 4.5*.x*/4.6*.x*/4.7 non è supportato in questo sistema operativo.|Per i sistemi operativi supportati, vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md).<br /><br /> Per installazioni non riuscite di .NET Framework in Windows 7, questo messaggio indica in genere che non è installato Windows 7 SP1. Nei sistemi Windows 7, .NET Framework richiede Windows 7 SP1. Se si dispone di Windows 7 ma non è ancora stato installato il Service Pack 1, è necessario farlo prima di installare .NET Framework. Per informazioni sull'installazione di Windows 7 SP1, vedere [Installare Windows 7 Service Pack 1 (SP1)](http://windows.microsoft.com/en-us/windows7/install-windows-7-service-pack-1).|  
|Nel computer è attualmente in esecuzione un'installazione Server Core del sistema operativo Windows Server 2008. .NET Framework 4.5.*x* richiede una versione completa del sistema operativo o Server Core 2008 R2 SP1. Installare la versione completa di Windows Server 2008 SP2 o Windows Server 2008 R2 SP1 o Server Core 2008 R2 SP1 ed eseguire nuovamente l'installazione di .NET Framework 4.5.*x*.|.NET Framework è supportato nel ruolo Server Core con Windows Server 2008 R2 SP1 o versioni successive. Vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md).|  
|.NET Framework 4.5.*x* è già installato in questo sistema operativo ma è attualmente disabilitato (solo [!INCLUDE[winserver8](../../../includes/winserver8-md.md)]).|Vedere [Attivare o disattivare le funzionalità di Windows](http://go.microsoft.com/fwlink/p/?LinkId=248438) nel sito Web di Windows.|  
|Il programma di installazione richiede un computer x86. Impossibile eseguire l'installazione su computer x64 o IA64.|Vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md) in MSDN Library.|  
|Il programma di installazione richiede un computer x64 o x86. Impossibile eseguire l'installazione su computer IA64.|Vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md) in MSDN Library.|  
  
<a name="compat"></a>   
### <a name="program-compatibility-issues"></a>Problemi di compatibilità del programma  
 L'installazione di .NET Framework 4.5 o relative versioni non viene completata e restituisce l'errore 1603 o si blocca quando viene eseguita in modalità di compatibilità dei programmi Windows. **Risoluzione problemi compatibilità programmi** indica che .NET Framework potrebbe non essere stato installato correttamente e richiede di reinstallare il programma usando l'impostazione consigliata (modalità compatibilità dei programmi). La modalità di compatibilità dei programmi potrebbe anche essere impostata dalla risoluzione problemi compatibilità programmi in tentativi precedenti non superati o annullati di eseguire l'installazione di .NET Framework.  
  
 Il programma di installazione di .NET Framework non può essere eseguito in modalità di compatibilità dei programmi. Per risolvere questo problema di blocco, assicurarsi che l'impostazione della modalità di compatibilità non sia abilitata a livello di sistema nell'Editor del Registro di sistema:  
  
1.  Scegliere il pulsante **Start** e quindi scegliere **Esegui**.  
  
2.  Nella finestra di dialogo **Esegui** digitare `regedit` e quindi scegliere **OK**.  
  
3.  Nell'Editor del Registro di sistema individuare le seguenti sottochiavi:  
  
    -   HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Compatibility Assistant\Persisted  
  
    -   HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers  
  
4.  Nella colonna Nome cercare i nomi di download di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], 4.5.1, 4.5.2, 4.6, 4.6.1 o 4.6.2 , a seconda della versione che si sta installando ed eliminare queste voci. Per i nomi di download, vedere l'articolo [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md).  
  
5.  Eseguire nuovamente il programma di installazione di .NET Framework per la versione 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2 o 4.7.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md)   
 [Procedura: determinare le versioni di .NET Framework installate](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)   
 [Versioni e dipendenze](../../../docs/framework/migration-guide/versions-and-dependencies.md)
