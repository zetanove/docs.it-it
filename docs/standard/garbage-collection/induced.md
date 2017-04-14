---
title: "Raccolte indotte | Microsoft Docs"
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
  - "Garbage Collection, forzata"
ms.assetid: 019008fe-4708-4e65-bebf-04fd9941e149
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Raccolte indotte
Nella maggior parte dei casi, il Garbage Collector può determinare il momento migliore per eseguire una raccolta, ed è consigliabile lasciare che venga eseguito in modo indipendente.  Possono verificarsi casi meno comuni in cui sia possibile che l'esecuzione di un Garbage Collection imposto migliori le prestazioni dell'applicazione.  In tali casi, è possibile forzare un Garbage Collection mediante il metodo <xref:System.GC.Collect%2A?displayProperty=fullName>.  
  
 Utilizzare il metodo <xref:System.GC.Collect%2A?displayProperty=fullName> quando si verifica una riduzione significativa della quantità di memoria utilizzata in un determinato punto del codice dell'applicazione.  Se viene ad esempio utilizzata una finestra di dialogo complessa con molti controlli, la chiamata al metodo <xref:System.GC.Collect%2A> in seguito alla chiusura della finestra di dialogo determina un miglioramento delle prestazioni dell'applicazione recuperando immediatamente memoria utilizzata nella casella di dialogo.  Assicurarsi che il Garbage Collection non venga indotto troppo frequentemente dalla propria applicazione: il tentativo di recupero di oggetti in tempi non ottimali da parte del Garbage Collector può causare una riduzione delle prestazioni.  È possibile specificare un valore di enumerazione <xref:System.GCCollectionMode?displayProperty=fullName> nel metodo <xref:System.GC.Collect%2A> per eseguire la raccolta solo quando è produttivo, come descritto nella sezione successiva.  
  
## Modalità di GC \(Garbage Collection\)  
 È possibile utilizzare uno degli overload del metodo <xref:System.GC.Collect%2A?displayProperty=fullName> che include un valore <xref:System.GCCollectionMode> per specificare il comportamento di una raccolta imposta, come illustrato di seguito.  
  
|Valore `GCCollectionMode`|Descrizione|  
|-------------------------------|-----------------|  
|<xref:System.GCCollectionMode>|Utilizza l'impostazione di Garbage Collection predefinita per la versione in esecuzione di .NET Framework.|  
|<xref:System.GCCollectionMode>|Forza il Garbage Collection affinché venga eseguito immediatamente.  Questo sistema equivale a chiamare l'overload <xref:System.GC.Collect?displayProperty=fullName>.  Restituisce una raccolta di blocco completa di tutte le generazioni.<br /><br /> È inoltre possibile comprimere heap di oggetti grandi impostando la proprietà <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=fullName> su <xref:System.Runtime.GCLargeObjectHeapCompactionMode?displayProperty=fullName> prima di imporre un'operazione completa di Garbage Collection bloccante.|  
|<xref:System.GCCollectionMode>|Consente al Garbage Collector di determinare il momento migliore per recuperare oggetti.<br /><br /> Se il Garbage Collector determina che non sia sufficientemente produttivo eseguire il Garbage Collection, non verranno recuperati oggetti.|  
  
## Raccolte in background o di blocco  
 È possibile chiamare l'overload del metodo <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29?displayProperty=fullName> per specificare se una raccolta indotta è bloccante o meno.  Il tipo di raccolta eseguita dipende da una combinazione dei parametri `mode` e `blocking` del metodo.  `mode` è un numero dell'enumerazione <xref:System.GCCollectionMode> e `blocking` è un valore <xref:System.Boolean>.  Nella tabella seguente viene riepilogata l'interazione degli argomenti `mode` e `blocking`.  
  
|`mode`|`blocking` \= `true`|`blocking` \= `false`|  
|------------|--------------------------|---------------------------|  
|<xref:System.GCCollectionMode> o <xref:System.GCCollectionMode>|Una raccolta di blocco viene eseguita il prima possibile.  Se è in corso una raccolta in background e la generazione è 0 o 1, il metodo <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> attiva immediatamente una raccolta di blocco e viene restituito quando la raccolta viene completata.  Se è in corso una raccolta in background e il parametro `generation` è 2, il metodo attende fino a quando la raccolta in background non viene completata, attiva una raccolta di blocco di generazione 2, quindi viene restituito.|Una raccolta viene eseguita il prima possibile.  Il metodo <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> richiede una raccolta in background, ma non è garantito; a seconda delle circostanze, una raccolta di blocco può ancora essere eseguita.  Se è già in corso una raccolta in background, il metodo viene restituito immediatamente.|  
|<xref:System.GCCollectionMode>|Una raccolta di blocco può essere eseguita a seconda dello stato del Garbage Collector e del parametro `generation`.  Garbage Collector tenta di fornire prestazioni ottimali.|Una raccolta può essere eseguita a seconda dello stato del Garbage Collector.  Il metodo <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%29> richiede una raccolta in background, ma non è garantito; a seconda delle circostanze, una raccolta di blocco può ancora essere eseguita.  Garbage Collector tenta di fornire prestazioni ottimali.  Se è già in corso una raccolta in background, il metodo viene restituito immediatamente.|  
  
## Vedere anche  
 [Latency Modes](../../../docs/standard/garbage-collection/latency.md)   
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)