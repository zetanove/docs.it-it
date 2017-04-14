---
title: "Reader-Writer Locks | Microsoft Docs"
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
  - "ReaderWriterLock class, about ReaderWriterLock class"
  - "threading [.NET Framework], ReaderWriterLock class"
ms.assetid: 8c71acf2-2c18-4f4d-8cdb-0728639265fd
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Reader-Writer Locks
La classe <xref:System.Threading.ReaderWriterLockSlim> consente a più thread di leggere contemporaneamente una risorsa, ma per scrivere nella risorsa è necessario che un thread attenda un blocco esclusivo.  
  
 All'interno dell'applicazione, è possibile utilizzare <xref:System.Threading.ReaderWriterLockSlim> per effettuare la sincronizzazione cooperativa tra i thread che accedono a una risorsa condivisa.  I blocchi vengono effettuati sullo stesso <xref:System.Threading.ReaderWriterLockSlim>.  
  
 Come con qualsiasi meccanismo di sincronizzazione di thread, è necessario assicurasi che nessun thread ignori il blocco causato da <xref:System.Threading.ReaderWriterLockSlim>.  Un modo per assicurare che questo avvenga è progettare una classe che incapsuli la risorsa condivisa.  Questa classe fornisce membri che accedono alla risorsa condivisa privata e che utilizzano un oggetto <xref:System.Threading.ReaderWriterLockSlim> privato per la sincronizzazione.  Vedere in proposito l'esempio di codice fornito per la classe <xref:System.Threading.ReaderWriterLockSlim>.  <xref:System.Threading.ReaderWriterLockSlim> è abbastanza efficiente da essere utilizzato per sincronizzare oggetti singoli.  
  
 Strutturare l'applicazione in modo da ridurre la durata delle operazioni di lettura e scrittura.  Le operazioni di scrittura lunghe influiscono direttamente sulla trasmissione di dati poiché il blocco scrittura è esclusivo.  Le operazioni di lettura lunghe bloccano i writer in attesa e, se anche un solo thread è in attesa dell'accesso in scrittura, verranno bloccati anche i thread che richiedono l'accesso in lettura.  
  
> [!NOTE]
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] presenta due blocchi reader\-writer: <xref:System.Threading.ReaderWriterLockSlim> e <xref:System.Threading.ReaderWriterLock>.  <xref:System.Threading.ReaderWriterLockSlim> è consigliato per tutti i nuovi progetti di sviluppo.  <xref:System.Threading.ReaderWriterLockSlim> è simile a <xref:System.Threading.ReaderWriterLock>, ma possiede regole semplificate per la ricorsione e per l'aggiornamento e il downgrade dello stato del blocco.  <xref:System.Threading.ReaderWriterLockSlim> evita molti casi di potenziale deadlock.  Inoltre, le prestazioni di <xref:System.Threading.ReaderWriterLockSlim> sono notevolmente migliori di <xref:System.Threading.ReaderWriterLock>.  
  
## Vedere anche  
 <xref:System.Threading.ReaderWriterLockSlim>   
 <xref:System.Threading.ReaderWriterLock>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)