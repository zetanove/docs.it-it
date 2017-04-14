---
title: "Stati degli oggetti e rilevamento delle modifiche | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7a808b00-9c3c-479a-aa94-717280fefd71
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Stati degli oggetti e rilevamento delle modifiche
Agli oggetti [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è sempre associato uno *stato*.  Ad esempio, quando in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene creato un nuovo oggetto, lo stato dell'oggetto è `Unchanged`.  Un nuovo oggetto creato dall'utente è sconosciuto all'oggetto <xref:System.Data.Linq.DataContext> e si trova nello stato `Untracked`.  Dopo la corretta esecuzione di <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, tutti gli oggetti riconosciuti da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sono nello stato `Unchanged`.  La sola eccezione è rappresentata dagli oggetti eliminati dal database che sono nello stato `Deleted` e di conseguenza inutilizzabili in quell'istanza di <xref:System.Data.Linq.DataContext>.  
  
## Stati degli oggetti  
 Nella tabella riportata di seguito sono elencati gli stati possibili per gli oggetti [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
|Stato|Descrizione|  
|-----------|-----------------|  
|`Untracked`|Un oggetto non registrato da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Di seguito vengono forniti alcuni esempi:<br /><br /> -   Un oggetto per cui non è stata eseguita una query tramite l'istanza corrente di <xref:System.Data.Linq.DataContext>. Ad esempio, un oggetto appena creato.<br />-   Un oggetto creato tramite deserializzazione<br />-   Un oggetto per cui è stata eseguita una query tramite una diversa istanza di <xref:System.Data.Linq.DataContext>.|  
|`Unchanged`|Un oggetto recuperato usando l'istanza corrente di <xref:System.Data.Linq.DataContext> e che non risulta modificato da quando è stato creato.|  
|`PossiblyModified`|Un oggetto *associato* a un'istanza di <xref:System.Data.Linq.DataContext>.  Per altre informazioni, vedere [Recupero dei dati e operazioni CUD in applicazioni a più livelli \(LINQ to SQL\)](../../../../../../docs/framework/data/adonet/sql/linq/data-retrieval-and-cud-operations-in-n-tier-applications.md).|  
|`ToBeInserted`|Un oggetto non recuperato usando l'istanza corrente di <xref:System.Data.Linq.DataContext>.  In questo caso viene eseguita un'operazione `INSERT` in un database durante l'esecuzione di <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.|  
|`ToBeUpdated`|Un oggetto che risulta modificato da quando è stato recuperato.  In questo caso viene eseguita un'operazione `UPDATE` in un database durante l'esecuzione di <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.|  
|`ToBeDeleted`|Un oggetto contrassegnato per l'eliminazione, che causa un'operazione `DELETE` in un database durante l'esecuzione di <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.|  
|`Deleted`|Un oggetto eliminato nel database.  Questo stato è finale e non consente transizioni aggiuntive.|  
  
## Inserimento di oggetti  
 È possibile richiedere `Inserts` usando <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> in modo esplicito.  In alternativa, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è possibile dedurre l'oggetto `Inserts` mediante la ricerca di oggetti collegati a uno degli oggetti conosciuti che devono essere aggiornati.  Ad esempio, se si aggiunge un oggetto `Untracked` a un oggetto <xref:System.Data.Linq.EntitySet%601> o si imposta un oggetto <xref:System.Data.Linq.EntityRef%601> su un oggetto `Untracked`, si rende raggiungibile l'oggetto `Untracked` mediante gli oggetti rilevati nel grafico.  Durante l'elaborazione dell'oggetto <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono attraversati gli oggetti rilevati e individuato qualsiasi oggetto persistente raggiungibile di cui non è stata tenuta traccia.  Tali oggetti sono candidati per l'inserimento nel database.  
  
 Per le classi in una gerarchia di ereditarietà, <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>\(`o`\) imposta inoltre il valore del membro definito come *discriminatore* in modo che corrisponda al tipo dell'oggetto `o`.  Qualora un tipo dovesse corrispondere al valore discriminante predefinito, questa azione causerà la sovrascrittura del valore discriminante con il valore predefinito.  Per altre informazioni, vedere [Supporto dell'ereditarietà](../../../../../../docs/framework/data/adonet/sql/linq/inheritance-support.md).  
  
> [!IMPORTANT]
>  Un oggetto aggiunto a un oggetto `Table` non si trova nella cache delle identità,  che riflette solo gli oggetti recuperati dal database.  Dopo una chiamata a <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>, l'entità aggiunta non viene visualizzata nelle query eseguite sul database finché non si completerà <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  
  
## Eliminazione di oggetti  
 Per contrassegnare per l'eliminazione un oggetto `o` rilevato, chiamare <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>\(o\) sull'oggetto <xref:System.Data.Linq.Table%601> appropriato.  In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] la rimozione di un oggetto da un oggetto <xref:System.Data.Linq.EntitySet%601> viene considerata come un'operazione di aggiornamento e il valore della chiave esterna corrispondente viene impostato su Null.  La destinazione dell'operazione \(`o`\) non viene eliminata dalla relativa tabella.  Ad esempio, `cust.Orders.DeleteOnSubmit(ord)` indica un aggiornamento in cui la relazione tra `cust` e `ord` viene interrotta mediante l'impostazione della chiave esterna `ord.CustomerID` su null.  Non causa l'eliminazione della riga che corrisponde a `ord`.  
  
 Quando un oggetto viene eliminato \(<xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>\) dalla relativa tabella, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene eseguita l'elaborazione seguente:  
  
-   Quando si chiama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, per quell'oggetto viene eseguita un'operazione `DELETE`.  
  
-   La rimozione non viene propagata agli oggetti correlati, indipendentemente dallo stato di caricamento.  In particolare, gli oggetti correlati non vengono caricati per aggiornare la proprietà della relazione.  
  
-   Dopo la corretta esecuzione di <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, gli oggetti vengono impostati sullo stato `Deleted`.  Di conseguenza non sarà possibile usare l'oggetto o il relativo `id` in un'istanza di <xref:System.Data.Linq.DataContext>.  La cache interna gestita da un'istanza di <xref:System.Data.Linq.DataContext> non elimina gli oggetti recuperati o aggiunti come nuovi, anche dopo che sono stati eliminati nel database.  
  
 È possibile chiamare <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> solo su un oggetto registrato da <xref:System.Data.Linq.DataContext>.  Per un oggetto `Untracked` è necessario chiamare <xref:System.Data.Linq.Table%601.Attach%2A> prima di <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>.  Chiamando <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> su un oggetto`Untracked`, verrà generata un'eccezione.  
  
> [!NOTE]
>  La rimozione di un oggetto da una tabella indica a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] di generare un comando SQL `DELETE` corrispondente al momento dell'esecuzione dell'oggetto <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  Questa azione non rimuove l'oggetto dalla cache, né propaga l'eliminazione agli oggetti correlati.  
>   
>  Per recuperare l'`id` di un oggetto eliminato, usare una nuova istanza di <xref:System.Data.Linq.DataContext>.  Per la pulizia degli oggetti correlati è possibile usare la funzionalità del database per la *propagazione in cascata di un'eliminazione* oppure eliminare manualmente gli oggetti correlati.  
>   
>  Non è necessario, a differenza del database, eliminare gli oggetti correlati in un ordine particolare.  
  
## Aggiornamento di oggetti  
 È possibile rilevare l'esecuzione di `Updates` osservando le notifiche delle modifiche,  che vengono fornite tramite l'evento <xref:System.ComponentModel.INotifyPropertyChanging.PropertyChanging> nei metodi per l'impostazione delle proprietà.  Quando [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] riceve una notifica della prima modifica a un oggetto, crea una copia dell'oggetto e lo considera candidato per la generazione di un'istruzione `Update`.  
  
 Per gli oggetti che non implementano l'oggetto <xref:System.ComponentModel.INotifyPropertyChanging>, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene mantenuta una copia dei valori degli oggetti quando sono stati materializzati per la prima volta.  Quando si chiama l'oggetto <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono confrontati i valori originali e correnti per stabilire se l'oggetto è stato modificato.  
  
 Per gli aggiornamenti delle relazioni, il riferimento dal figlio al padre, ovvero il riferimento che corrisponde alla chiave esterna, viene considerato autorevole.  Il riferimento nella direzione inversa, ovvero da padre a figlio, è facoltativo.  Le classi di relazione \(<xref:System.Data.Linq.EntitySet%601> e <xref:System.Data.Linq.EntityRef%601>\) assicurano che i riferimenti bidirezionali siano coerenti per le relazioni uno\-a\-molti e uno\-a\-uno.  Se il modello a oggetti non usa <xref:System.Data.Linq.EntitySet%601> o <xref:System.Data.Linq.EntityRef%601> e se è presente il riferimento inverso, sarà necessario mantenerlo coerente con il riferimento in avanti quando viene aggiornata la relazione.  
  
 Se si aggiornano sia il riferimento obbligatorio che la chiave esterna corrispondente, è necessario assicurarsi che corrispondano.  Se non sono entrambi sincronizzati quando si chiama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, verrà generata un'eccezione <xref:System.InvalidOperationException>.  Anche se le modifiche dei valori della chiave esterna sono sufficienti per interessare un aggiornamento della riga sottostante, è necessario modificare il riferimento per mantenere la connettività dell'oggetto grafico e la coerenza bidirezionale delle relazioni.  
  
## Vedere anche  
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [Operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/insert-update-and-delete-operations.md)