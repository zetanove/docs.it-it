---
title: "Procedura dettagliata: individuazione della posizione di inserimento delle informazioni con My.Application.Log (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "oggetto My.Log, percorso di output"
  - "output, percorso del log applicazione"
  - "oggetto My.Application.Log, percorso di output"
  - "log eventi, determinazione del percorso di output"
  - "log eventi applicazioni, percorso di output"
  - "applicazioni [Visual Basic], percorso di output"
ms.assetid: 5b70143a-7741-45f2-ae1d-03324a3a4189
caps.latest.revision: 24
caps.handback.revision: 24
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura dettagliata: individuazione della posizione di inserimento delle informazioni con My.Application.Log (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'oggetto `My.Application.Log` può scrivere le informazioni in diversi listener di log. I listener di log sono configurati dal file di configurazione del computer ed è possibile eseguirne l'override con il file di configurazione di un'applicazione. Questo argomento descrive le impostazioni predefinite e illustra come determinare le impostazioni dell'applicazione.  
  
 Per altre informazioni sui percorsi di output predefiniti, vedere [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md).  
  
### Per determinare i listener per My.Application.Log  
  
1.  Individuare il file di configurazione dell'assembly. Se si sta sviluppando l'assembly, è possibile accedere al file app.config in [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] da **Esplora soluzioni**. In caso contrario, il nome del file di configurazione sarà il nome dell'assembly seguito da ".config" e si troverà nella stessa directory dell'assembly.  
  
    > [!NOTE]
    >  Non tutti gli assembly hanno un file di configurazione.  
  
     Il file di configurazione è un file XML.  
  
2.  Individuare la sezione `<listeners>` all'interno della sezione `<source>` con l'attributo `name` "DefaultSource" che si trova nella sezione `<sources>`. La sezione `<sources>` si trova nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>`.  
  
     Se queste sezioni non esistono, è possibile configurare i listener di log `My.Application.Log` nel file di configurazione del computer. I passaggi seguenti descrivono come determinare ciò che viene definito dal file di configurazione del computer:  
  
    1.  Individuare il file machine.config del computer. Il file si trova in genere nella directory *SystemRoot\\Microsoft.NET\\Framework\\frameworkVersion\\CONFIG*, dove `SystemRoot` è la directory del sistema operativo e `frameworkVersion` è la versione di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
         È possibile eseguire l'override delle impostazioni del file machine.config con il file di configurazione di un'applicazione.  
  
         Se gli elementi facoltativi seguenti non esistono, è possibile crearli.  
  
    2.  Individuare la sezione `<listeners>` all'interno della sezione `<source>` con l'attributo `name` "DefaultSource" che si trova nella sezione `<sources>` all'interno della sezione `<system.diagnostics>` nella sezione di primo livello `<configuration>`.  
  
         Se queste sezioni non esistono, `My.Application.Log` conterrà solo i listener di log predefiniti.  
  
3.  Individuare gli elementi \<`add>` nella sezione \<`listeners>`.  
  
     Questi elementi consentono di aggiungere i listener di log denominati all'origine `My.Application.Log`.  
  
4.  Individuare gli elementi `<add>` con i nomi dei listener di log nella sezione `<sharedListeners>` all'interno della sezione `<system.diagnostics>` nella sezione di primo livello `<configuration>`.  
  
5.  Per molti tipi di listener condivisi, i dati di inizializzazione del listener includono una descrizione della posizione in cui il listener indirizza i dati:  
  
    -   Il listener <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName> scrive le informazioni in un log file, come descritto nell'introduzione.  
  
    -   Il listener <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName> scrive le informazioni nel log eventi del computer specificato dal parametro `initializeData`. Per visualizzare un log eventi, è possibile usare **Esplora server** o **Visualizzatore eventi di Windows**. Per altre informazioni, vedere [ETW Events in the .NET Framework](../Topic/ETW%20Events%20in%20the%20.NET%20Framework.md).  
  
    -   I listener <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName> e <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName> scrivono le informazioni nel file specificato nel parametro `initializeData`.  
  
    -   Il listener <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName> scrive le informazioni nella console della riga di comando.  
  
    -   Per sapere dove gli altri tipi di listener di log scrivono le informazioni, consultare la documentazione relativa al tipo di listener desiderato.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:System.Diagnostics.DefaultTraceListener>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 <xref:System.Diagnostics.DelimitedListTraceListener>   
 <xref:System.Diagnostics.XmlWriterTraceListener>   
 <xref:System.Diagnostics.ConsoleTraceListener>   
 <xref:System.Diagnostics>   
 [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [How to: Log Exceptions](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [Procedura: scrivere messaggi di log](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [Procedura dettagliata: modifica della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)   
 [ETW Events in the .NET Framework](../Topic/ETW%20Events%20in%20the%20.NET%20Framework.md)   
 [Troubleshooting: Log Listeners](../../../../visual-basic/developing-apps/programming/log-info/troubleshooting-log-listeners.md)