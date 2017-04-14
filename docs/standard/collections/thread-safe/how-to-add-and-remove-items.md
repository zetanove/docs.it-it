---
title: "Procedura: aggiungere e rimuovere elementi da un oggetto ConcurrentDictionary | Microsoft Docs"
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
  - "raccolte thread-safe, dizionario simultaneo"
ms.assetid: 81b64b95-13f7-4532-9249-ab532f629598
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: aggiungere e rimuovere elementi da un oggetto ConcurrentDictionary
In questo esempio viene illustrato come aggiungere, recuperare, aggiornare e rimuovere elementi da un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>.  Questa classe di raccolte è un'implementazione thread\-safe.  Si consiglia di utilizzarla ogni qualvolta vi è la possibilità che più thread tentino di accedere contemporaneamente agli elementi.  
  
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> fornisce diversi metodi pratici grazie ai quali non è più necessario che il codice verifichi l'esistenza di una chiave prima di tentare di aggiungere o rimuovere dati.  Nella tabella seguente vengono elencati questi metodi pratici e viene descritto quando utilizzarli.  
  
|Metodo|Utilizzare quando...|  
|------------|--------------------------|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>|Si desidera aggiungere un nuovo valore per una chiave specificata e, se la chiave già esiste, sostituirne il valore.|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>|Si desidera recuperare il valore esistente di una chiave specificata e, se la chiave non esiste, specificare una coppia chiave\/valore.|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryAdd%2A>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryGetValue%2A> , <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryUpdate%2A> , <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryRemove%2A>|Si desidera aggiungere, ottenere, aggiornare o rimuovere una coppia chiave\/valore e, se la chiave già esiste o il tentativo non riesce per qualsiasi altro motivo, eseguire un'azione alternativa.|  
  
## Esempio  
 Nell'esempio seguente vengono utilizzate due istanze di <xref:System.Threading.Tasks.Task> per aggiungere contemporaneamente alcuni elementi a un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, quindi viene restituito tutto il contenuto a riprova del fatto che gli elementi sono stati aggiunti correttamente.  Nell'esempio viene inoltre illustrato come utilizzare i metodi <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>, <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>, e <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> per aggiungere, aggiornare, e recuperare elementi dalla raccolta.  
  
 [!code-csharp[CDS#16](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/cds_dictionaryhowto.cs#16)]
 [!code-vb[CDS#16](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/cds_concdict.vb#16)]  
  
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> è pensato per scenari multithreading.  Non è necessario utilizzare blocchi nel codice per aggiungere o rimuovere elementi dalla raccolta.  Tuttavia, è sempre possibile che un thread recuperi un valore mentre un altro thread aggiorna immediatamente la raccolta assegnando alla stessa chiave un nuovo valore.  
  
 Inoltre, sebbene tutti i metodi di <xref:System.Collections.Concurrent.ConcurrentDictionary%602> siano thread\-safe, non tutti i metodi sono atomici, in particolare <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> e <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>.  Il delegato dell'utente che viene passato a questi metodi viene richiamato all'esterno del blocco interno del dizionario. In questo modo si impedisce al codice sconosciuto di bloccare tutti i thread. È possibile pertanto che si verifichi la sequenza di eventi seguente:  
  
 1\) threadA chiama <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>, non trova alcun elemento e crea un nuovo elemento in Add richiamando il delegato valueFactory.  
  
 2\) threadB chiama <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> contemporaneamente, viene richiamato il delegato valueFactory e arriva nel blocco interno prima di threadA, pertanto la nuova coppia chiave\-valore viene aggiunta al dizionario.  
  
 3\) il delegato dell'utente di threadA viene completato e il thread arriva nel blocco, ma ora rileva che l'elemento esiste già.  
  
 4\) threadA esegue una richiesta "Get" e restituisce i dati aggiunti precedentemente da threadB.  
  
 Non è pertanto garantito che i dati restituiti da <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> siano gli stessi dati creati dal delegato valueFactory del thread.  Una sequenza di eventi simile può verificarsi quando viene chiamato <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>.  
  
## Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Raccolte thread\-safe](../../../../docs/standard/collections/thread-safe/index.md)