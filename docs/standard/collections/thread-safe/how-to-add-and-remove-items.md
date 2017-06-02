---
title: 'Procedura: aggiungere e rimuovere elementi da un oggetto ConcurrentDictionary | Documenti di Microsoft'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread-safe collections, concurrent dictionary
ms.assetid: 81b64b95-13f7-4532-9249-ab532f629598
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 9d20d75b2492c214305c07a5e19941cd91b66f67
ms.lasthandoff: 04/18/2017

---
# <a name="how-to-add-and-remove-items-from-a-concurrentdictionary"></a>Procedura: aggiungere e rimuovere elementi da un oggetto ConcurrentDictionary
In questo esempio viene illustrato come aggiungere, recuperare, aggiornare e rimuovere elementi da una classe <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>. Questa classe di raccolta è un'implementazione thread-safe. È consigliabile usarla ogni volta che più thread tentano di accedere contemporaneamente agli elementi.  
  
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> offre molti metodi pratici che consentono al codice di evitare il controllo dell'esistenza di una chiave prima di aggiungere o rimuovere dati. Nella tabella seguente vengono elencati questi metodi pratici e viene specificato quando usarli.  
  
|Metodo|Casi di uso|  
|------------|---------------|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>|Si vuole aggiungere un nuovo valore ad una chiave specificata e, se la chiave esiste già, si vuole sostituirne il valore.|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>|Si vuole recuperare il valore esistente per una chiave specificata e, se la chiave non esiste, si vuole specificare una coppia chiave/valore.|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryAdd%2A>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryGetValue%2A> , <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryUpdate%2A> , <xref:System.Collections.Concurrent.ConcurrentDictionary%602.TryRemove%2A>|Si vuole aggiungere, ottenere, aggiornare o rimuovere una coppia chiave/valore e, se la chiave esiste già o il tentativo non riesce per qualsiasi altro motivo, si vuole eseguire un'azione alternativa.|  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono usate due istanze di <xref:System.Threading.Tasks.Task> per aggiungere contemporaneamente alcuni elementi a <xref:System.Collections.Concurrent.ConcurrentDictionary%602>; quindi, viene restituito tutto il contenuto per mostrare gli elementi che sono stati aggiunti correttamente. Nell'esempio viene inoltre illustrato come usare i metodi <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>, <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> e <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> per aggiungere, aggiornare e recuperare elementi dalla raccolta.  
  
 [!code-csharp[CDS#16](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/cds_dictionaryhowto.cs#16)]
 [!code-vb[CDS#16](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/cds_concdict.vb#16)]  
  
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> è progettata per gli scenari multithreading. Non è necessario usare blocchi nel codice per aggiungere o rimuovere elementi dalla raccolta. Tuttavia, è sempre possibile per un thread recuperare un valore, e per un altro thread aggiornare immediatamente la raccolta assegnando un nuovo valore alla stessa chiave.  
  
 Inoltre, anche se tutti i metodi di <xref:System.Collections.Concurrent.ConcurrentDictionary%602> sono thread-safe, non tutti i metodi sono atomici, in particolare <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> e <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>. Il delegato utenti passato a questi metodi viene richiamato fuori dal blocco interno del dizionario. (Questa operazione viene eseguita per impedire a un codice sconosciuto di bloccare tutti i thread). Pertanto è possibile che per questa sequenza di eventi si verifichi quanto segue:  
  
 1\) threadA chiama <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A>, non trova alcun elemento e crea un nuovo elemento in Aggiungi richiamando il delegato valueFactory.  
  
 2\)threadB chiama <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> contemporaneamente, il relativo delegato valueFactory viene richiamato e arriva al blocco interno prima di threadA, pertanto la nuova coppia chiave-valore viene aggiunta al dizionario.  
  
 Il delegato utenti di 3\)threadA completa l'operazione, il thread arriva nel blocco, ma ora rileva che l'elemento esiste già  
  
 4\)threadA esegue un'operazione "Get" e restituisce i dati aggiunti precedentemente da threadB.  
  
 Non è comunque garantito che i dati restituiti da <xref:System.Collections.Concurrent.ConcurrentDictionary%602.GetOrAdd%2A> siano gli stessi dati creati dal delegato valueFactory del thread. Una sequenza di eventi analoga può verificarsi quando viene chiamato <xref:System.Collections.Concurrent.ConcurrentDictionary%602.AddOrUpdate%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Raccolte thread-safe](../../../../docs/standard/collections/thread-safe/index.md)
