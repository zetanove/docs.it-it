---
title: "Foreground and Background Threads | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "threading [.NET Framework], foreground"
  - "threading [.NET Framework], background"
  - "foreground threads"
  - "background threads"
ms.assetid: cfe0d632-dd35-47e0-91ad-f742a444005e
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Foreground and Background Threads
Un thread gestito può essere in background o in primo piano.  I thread in background sono identici a quelli in primo piano tranne per il fatto che i primi non mantengono attivo l'ambiente di esecuzione gestito.  Dopo che tutti i thread in primo piano sono stati interrotti in un processo gestito, in cui il file con estensione exe è un assembly gestito, tutti i thread in background vengono interrotti e viene effettuato un arresto del sistema.  
  
> [!NOTE]
>  Quando un thread in background viene interrotto dal runtime perché il processo è in fase di chiusura, nel thread non viene generata alcuna eccezione.  Tuttavia, quando i thread vengono interrotti perché il metodo <xref:System.AppDomain.Unload%2A?displayProperty=fullName> scarica il dominio applicazione, viene generata un'eccezione <xref:System.Threading.ThreadAbortException> sia nei thread in primo piano sia in quelli in background.  
  
 Utilizzare la proprietà <xref:System.Threading.Thread.IsBackground%2A?displayProperty=fullName> per determinare se un thread è in background o in primo piano oppure per cambiarne lo stato.  Un thread può essere cambiato in un thread in background in qualsiasi momento impostando la relativa proprietà <xref:System.Threading.Thread.IsBackground%2A> su `true`.  
  
> [!IMPORTANT]
>  Lo stato in primo piano o in background di un thread non influisce sull'esito di un'eccezione non gestita nel thread.  In .NET Framework versione 2.0 un'eccezione non gestita nei thread in primo piano o in background ha come risultato l'interruzione dell'applicazione.  Per informazioni, vedere [Exceptions in Managed Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md).  
  
 I thread che appartengono al pool di thread gestiti, ossia quelli con la proprietà <xref:System.Threading.Thread.IsThreadPoolThread%2A> impostata su `true`, sono thread in background.  Tutti i thread che entrano nell'ambiente di esecuzione gestito da codice non gestito vengono contrassegnati come thread in background.  Tutti i thread generati creando e avviando un nuovo oggetto <xref:System.Threading.Thread> sono thread in primo piano per impostazione predefinita.  
  
 Se si utilizza un thread per monitorare un'attività, ad esempio una connessione socket, impostare la relativa proprietà <xref:System.Threading.Thread.IsBackground%2A> su `true` per evitare che il thread impedisca l'interruzione del processo.  
  
## Vedere anche  
 <xref:System.Threading.Thread.IsBackground%2A?displayProperty=fullName>   
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadAbortException>