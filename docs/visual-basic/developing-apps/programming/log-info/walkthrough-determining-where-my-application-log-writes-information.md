---
title: Individuazione della posizione di inserimento delle informazioni con My.Application.Log (Visual Basic) | Microsoft Docs
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
- My.Log object, output location
- output, application log location
- My.Application.Log object, outpout location
- event logs, determining output location
- application event logs, output location
- applications [Visual Basic], output location
ms.assetid: 5b70143a-7741-45f2-ae1d-03324a3a4189
caps.latest.revision: 24
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
ms.openlocfilehash: 3ef53fb9439159c94bb3894c233977088edc8872
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-determining-where-myapplicationlog-writes-information-visual-basic"></a>Procedura dettagliata: individuazione della posizione di inserimento delle informazioni con My.Application.Log (Visual Basic)
L'oggetto `My.Application.Log` può scrivere le informazioni in diversi listener di log. I listener di log sono configurati dal file di configurazione del computer ed è possibile eseguirne l'override con il file di configurazione di un'applicazione. Questo argomento descrive le impostazioni predefinite e illustra come determinare le impostazioni dell'applicazione.  
  
 Per altre informazioni sui percorsi di output predefiniti, vedere [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md).  
  
### <a name="to-determine-the-listeners-for-myapplicationlog"></a>Per determinare i listener per My.Application.Log  
  
1.  Individuare il file di configurazione dell'assembly. Se si sta sviluppando l'assembly, è possibile accedere al file app.config in [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] da **Esplora soluzioni**. In caso contrario, il nome del file di configurazione sarà il nome dell'assembly seguito da ".config" e si troverà nella stessa directory dell'assembly.  
  
    > [!NOTE]
    >  Non tutti gli assembly hanno un file di configurazione.  
  
     Il file di configurazione è un file XML.  
  
2.  Individuare la sezione `<listeners>` all'interno della sezione `<source>` con l'attributo `name` "DefaultSource" che si trova nella sezione `<sources>` . La sezione `<sources>` si trova nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .  
  
     Se queste sezioni non esistono, è possibile configurare i listener di log `My.Application.Log` nel file di configurazione del computer. I passaggi seguenti descrivono come determinare ciò che viene definito dal file di configurazione del computer:  
  
    1.  Individuare il file machine.config del computer. Il file si trova in genere nella directory *SystemRoot\Microsoft.NET\Framework\frameworkVersion\CONFIG*, dove `SystemRoot` è la directory del sistema operativo e `frameworkVersion` è la versione di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
         È possibile eseguire l'override delle impostazioni del file machine.config con il file di configurazione di un'applicazione.  
  
         Se gli elementi facoltativi seguenti non esistono, è possibile crearli.  
  
    2.  Individuare la sezione `<listeners>` all'interno della sezione `<source>` con l'attributo `name` "DefaultSource" che si trova nella sezione `<sources>` all'interno della sezione `<system.diagnostics>` nella sezione di primo livello `<configuration>` .  
  
         Se queste sezioni non esistono, `My.Application.Log` conterrà solo i listener di log predefiniti.  
  
3.  Individuare gli elementi <`add>` nella sezione <`listeners>`.  
  
     Questi elementi consentono di aggiungere i listener di log denominati all'origine `My.Application.Log` .  
  
4.  Individuare gli elementi `<add>` con i nomi dei listener di log nella sezione `<sharedListeners>` all'interno della sezione `<system.diagnostics>` nella sezione di primo livello `<configuration>` .  
  
5.  Per molti tipi di listener condivisi, i dati di inizializzazione del listener includono una descrizione della posizione in cui il listener indirizza i dati:  
  
    -   Un listener <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=fullName> scrive in un log file, come descritto nell'introduzione.  
  
    -   Un listener <xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName> scrive informazioni nel registro eventi del computer specificato dal parametro `initializeData`. Per visualizzare un log eventi, è possibile usare **Esplora server** o **Visualizzatore eventi di Windows**. Per altre informazioni, vedere l'articolo relativo agli [eventi ETW in .NET Framework](http://msdn.microsoft.com/library/d186276f-6afb-4dfd-bf3c-4251edc2c299).  
  
    -   I listener <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName> e <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName> scrivono nel file specificato nel parametro `initializeData`.  
  
    -   Un listener <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName> scrive nella console della riga di comando.  
  
    -   Per sapere dove gli altri tipi di listener di log scrivono le informazioni, consultare la documentazione relativa al tipo di listener desiderato.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 <xref:System.Diagnostics.DefaultTraceListener>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 <xref:System.Diagnostics.DelimitedListTraceListener>   
 <xref:System.Diagnostics.XmlWriterTraceListener>   
 <xref:System.Diagnostics.ConsoleTraceListener>   
 <xref:System.Diagnostics>   
 [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [Procedura: Registrare eccezioni](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)   
 [Procedura: Scrivere messaggi di log](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)   
 [Procedura dettagliata: Modifica della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)   
 [ETW Events in the .NET Framework](http://msdn.microsoft.com/library/d186276f-6afb-4dfd-bf3c-4251edc2c299)  (Eventi ETW in .NET Framework)  
 [Risoluzione dei problemi: Listener di log](../../../../visual-basic/developing-apps/programming/log-info/troubleshooting-log-listeners.md)
