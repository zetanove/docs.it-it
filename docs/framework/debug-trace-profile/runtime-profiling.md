---
title: "Profilatura runtime | Microsoft Docs"
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
  - "contatori delle prestazioni"
  - "Common Language Runtime, profilatura"
  - "Perfmon.exe"
  - "Monitor di sistema"
  - "profilatura"
  - "runtime, profilatura"
  - "applicazioni di profilatura"
  - "Console prestazioni"
ms.assetid: ccd68284-f3a8-47b8-bc3f-92e5fe3a1640
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 22
---
# Profilatura runtime
La profilatura è un metodo di raccolta dei dati sulle prestazioni in qualsiasi scenario di sviluppo o distribuzione. Questa sezione è destinata agli sviluppatori e agli amministratori di sistema che vogliono raccogliere le informazioni sulle prestazioni delle applicazioni.  
  
## Rilevamento delle prestazioni con Performance Monitor \(Perfmon.exe\)  
 Performance Monitor è lo strumento più facile da usare per la profilatura dell'applicazione [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Performance Monitor rappresenta graficamente i dati trovati nei contatori delle prestazioni di .NET Framework installati con Common Language Runtime e [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]. Questi contatori possono essere usati per monitorare una serie di attività, dalla gestione della memoria alle prestazioni del compilatore JIT. Forniscono informazioni sulle risorse usate dall'applicazione, che indirettamente misurano le prestazioni dell'applicazione. Usare questi contatori per comprendere il funzionamento interno dell'applicazione.  
  
#### Per eseguire Perfmon.exe in Windows Vista e versioni successive  
  
1.  Al prompt dei comandi digitare **perfmon**. Viene visualizzata la console di **Performance Monitor**.  
  
2.  Nella cartella **Strumenti di monitoraggio** fare clic su **Performance Monitor**.  
  
3.  Nella barra degli strumenti di Performance Monitor fare clic sull'icona **Aggiungi** \(il segno di addizione\), se presente. Se non è presente, fare clic con il pulsante destro del mouse nella finestra di monitoraggio e selezionare l'opzione **Aggiungi contatori**.  
  
     Viene aperta la finestra di dialogo **Aggiungi contatori**. La casella di riepilogo **Contatori disponibili** visualizza gli oggetti prestazione disponibili. Esistono diversi oggetti predefiniti per le applicazioni .NET Framework, inclusi quelli per la gestione della memoria \(**Memoria CLR .NET**\), per l'interoperabilità \(**Interoperabilità CLR .NET**\), per la gestione delle eccezioni \(**Eccezioni CLR .NET**\) e per il multithreading \(**LocksAndThreads CLR .NET**\). Ogni oggetto prestazione include diversi contatori delle prestazioni singoli. Per un elenco dei contatori delle prestazioni disponibili in Performance Monitor, vedere [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md).  
  
4.  Selezionare la casella di controllo accanto al nome di un oggetto prestazione per visualizzare l'elenco dei singoli contatori delle prestazioni che supporta.  
  
5.  Fare clic sul contatore delle prestazioni da visualizzare:  
  
6.  Nella casella di riepilogo **Istanze dell'oggetto selezionato** fare clic su **\<Tutte le istanze\>** per specificare che si desidera controllare il contatore di prestazioni per Common Language Runtime globalmente, cioè a livello di sistema.  
  
     \-oppure\-  
  
     Nella casella di riepilogo **Istanze dell'oggetto selezionato** fare clic su un nome dell'applicazione per monitorare il relativo contatore delle prestazioni.  
  
     Per differenziare più versioni di runtime o per evitare ambiguità tra più applicazioni con lo stesso nome, è necessario modificare anche una chiave del Registro di sistema. Per altre informazioni, vedere [Performance Counters and In\-Process Side\-By\-Side Applications](../../../docs/framework/debug-trace-profile/performance-counters-and-in-process-side-by-side-applications.md).  
  
> [!NOTE]
>  Quando vengono installati nuovi contatori delle prestazioni mentre è in esecuzione la console prestazioni, arrestare e riavviare la console per rendere visibili i nuovi contatori.  
  
 Per profilare un assembly esistente in un'area o in una condivisione remota, assicurarsi che l'assembly remoto sia totalmente attendibile nel computer che esegue i contatori delle prestazioni. Se l'assembly non ha l'attendibilità totale, i contatori delle prestazioni non funzioneranno. Per informazioni sulla concessione dell'attendibilità alle diverse aree, vedere [Caspol.exe \(Code Access Security Policy Tool\)](../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md).  
  
> [!NOTE]
>  Nei sistemi in cui è installato [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], Performance Monitor potrebbe non visualizzare i dati per i contatori delle prestazioni in alcune categorie, ad esempio **Dati CLR .NET** e **Rete CLR .NET**, per le applicazioni sviluppate con [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)]. In questo caso, è possibile configurare Performance Monitor per visualizzare questi dati aggiungendo l'elemento [\<forcePerformanceCounterUniqueSharedMemoryReads\>](../../../docs/framework/configure-apps/file-schema/runtime/forceperformancecounteruniquesharedmemoryreads-element.md) al file di configurazione dell'applicazione.  
  
## Lettura e creazione di contatori delle prestazioni a livello di codice  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornisce le classi che è possibile usare per accedere a livello di codice alle stesse informazioni sulle prestazioni disponibili nella console prestazioni. È anche possibile usare queste classi per creare contatori delle prestazioni personalizzati. La tabella seguente descrive alcune classi di monitoraggio delle prestazioni disponibili in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
|Classe|Descrizione|  
|------------|-----------------|  
|<xref:System.Diagnostics.PerformanceCounter?displayProperty=fullName>|Rappresenta un componente del contatore delle prestazioni di Windows NT. Usare questa classe per leggere i contatori predefiniti o personalizzati esistenti e pubblicare i dati sulle prestazioni \(scrittura\) nei contatori personalizzati.|  
|<xref:System.Diagnostics.PerformanceCounterCategory?displayProperty=fullName>|Fornisce diversi metodi per interagire con i contatori e le categorie di contatori del computer.|  
|<xref:System.Diagnostics.PerformanceCounterInstaller?displayProperty=fullName>|Specifica un programma di installazione per il componente `PerformanceCounter`.|  
|<xref:System.Diagnostics.PerformanceCounterType?displayProperty=fullName>|Specifica la formula per calcolare il metodo `NextValue` per `PerformanceCounter`.|  
  
## Vedere anche  
 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)