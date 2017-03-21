---
title: Applicazioni multithreading (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 02b0444b-2e68-4f2c-bc28-28c046004017
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5bde7f49a2f2bc8a2e6c1eeab3722428b8a37a95
ms.lasthandoff: 03/13/2017

---
# <a name="multithreaded-applications-visual-basic"></a>Applicazioni multithreading (Visual Basic)
Con Visual Basic, è possibile scrivere applicazioni che eseguono più attività contemporaneamente. Attività con la possibilità di compromettere altre attività possono eseguire sui thread separati, un processo noto come *multithreading* o *libero threading*.  
  
 Le applicazioni che utilizzano il multithread sono più reattive all'input dell'utente, in quanto l'interfaccia utente rimane attiva durante l'esecuzione di attività intensiva sul thread diversi. Il multithreading è utile anche quando si creano applicazioni scalabili, in quanto è possibile aggiungere thread man mano che aumenta il carico di lavoro.  
  
## <a name="creating-and-using-threads"></a>Creazione e utilizzo di thread  
 Se è necessario un maggiore controllo sul comportamento dei thread dell'applicazione, è possibile gestire i thread. Tuttavia, tenere presente che la scrittura di applicazioni multithread complesse può essere difficile: l'applicazione potrebbe smettere di rispondere o si verifichino errori temporanei causati da condizioni di competizione. Per ulteriori informazioni, vedere [componenti Thread-Safe](http://msdn.microsoft.com/library/4f7c7377-a782-4bd0-aaa3-9db8c12945ee).  
  
 Per creare un nuovo thread dichiarando una variabile di tipo <xref:System.Threading.Thread>e chiama il costruttore, fornendo il nome della procedura o del metodo che si desidera eseguire sul nuovo thread.</xref:System.Threading.Thread> Nel codice seguente ne viene illustrato un esempio.  
  
```vb  
Dim newThread As New System.Threading.Thread(AddressOf AMethod)  
```  
  
### <a name="starting-and-stopping-threads"></a>Avvio e arresto di thread  
 Per avviare l'esecuzione di un nuovo thread, utilizzare il <xref:System.Threading.Thread.Start%2A>(metodo), come illustrato nel codice seguente.</xref:System.Threading.Thread.Start%2A>  
  
```vb  
newThread.Start()  
```  
  
 Per interrompere l'esecuzione di un thread, utilizzare il <xref:System.Threading.Thread.Abort%2A>(metodo), come illustrato nel codice seguente.</xref:System.Threading.Thread.Abort%2A>  
  
```vb  
newThread.Abort()  
```  
  
 Oltre all'avvio e arresto di thread, è anche possibile sospendere i thread chiamando il <xref:System.Threading.Thread.Sleep%2A>o <xref:System.Threading.Thread.Suspend%2A>(metodo), riprendere un thread sospeso utilizzando il <xref:System.Threading.Thread.Resume%2A>(metodo) e l'eliminazione di un thread utilizzando il <xref:System.Threading.Thread.Abort%2A>metodo</xref:System.Threading.Thread.Abort%2A> </xref:System.Threading.Thread.Resume%2A> </xref:System.Threading.Thread.Suspend%2A> </xref:System.Threading.Thread.Sleep%2A>  
  
### <a name="thread-methods"></a>Metodi di thread  
 Nella tabella seguente vengono illustrati alcuni dei metodi che è possibile utilizzare per controllare i singoli thread.  
  
|Metodo|Azione|  
|------------|------------|  
|<xref:System.Threading.Thread.Start%2A></xref:System.Threading.Thread.Start%2A>|Consente di avviare l'esecuzione di un thread.|  
|<xref:System.Threading.Thread.Sleep%2A></xref:System.Threading.Thread.Sleep%2A>|Sospende un thread per un determinato periodo.|  
|<xref:System.Threading.Thread.Suspend%2A></xref:System.Threading.Thread.Suspend%2A>|Sospende un thread quando raggiunge un punto sicuro.|  
|<xref:System.Threading.Thread.Abort%2A></xref:System.Threading.Thread.Abort%2A>|Interrompe un thread quando raggiunge un punto sicuro.|  
|<xref:System.Threading.Thread.Resume%2A></xref:System.Threading.Thread.Resume%2A>|Riavvia un thread in sospeso|  
|<xref:System.Threading.Thread.Join%2A></xref:System.Threading.Thread.Join%2A>|Determina che il thread corrente attendere un altro thread di completamento. Se utilizzato con un valore di timeout, questo metodo restituisce `True` se il thread viene completato nel tempo allocato.|  
  
### <a name="safe-points"></a>Punti sicuri  
 La maggior parte di questi metodi sono di chiara interpretazione, ma il concetto di *punti sicuri* potrebbe essere nuovo per l'utente. Si tratta di posizioni nel codice in cui è sicura per common language runtime per eseguire automatica *operazione di garbage collection*, il processo di rilasciare variabili inutilizzate e il recupero della memoria. Quando si chiama il <xref:System.Threading.Thread.Abort%2A>o <xref:System.Threading.Thread.Suspend%2A>Analizza il codice e determina la posizione di un percorso appropriato per il thread arrestare l'esecuzione di un thread, common language runtime.</xref:System.Threading.Thread.Suspend%2A> </xref:System.Threading.Thread.Abort%2A>  
  
### <a name="thread-properties"></a>Proprietà thread  
 Thread contiene inoltre diverse proprietà utili, come illustrato nella tabella riportata di seguito:  
  
|Proprietà|Valore|  
|--------------|-----------|  
|<xref:System.Threading.Thread.IsAlive%2A></xref:System.Threading.Thread.IsAlive%2A>|Contiene il valore `True` se il thread è attivo.|  
|<xref:System.Threading.Thread.IsBackground%2A></xref:System.Threading.Thread.IsBackground%2A>|Ottiene o imposta un valore booleano che indica se un thread è o deve essere un thread in background. I thread in background sono simili ai thread in primo piano, ma un thread in background non impedisce un processo di arresto. Al termine di tutti i thread in foreground che appartengono a un processo, common language runtime termina il processo chiamando il <xref:System.Threading.Thread.Abort%2A>metodo thread in background che ancora attivi.</xref:System.Threading.Thread.Abort%2A>|  
|<xref:System.Threading.Thread.Name%2A></xref:System.Threading.Thread.Name%2A>|Ottiene o imposta il nome di un thread. Molto spesso utilizzati per individuare i singoli thread quando esegue il debug.|  
|<xref:System.Threading.Thread.Priority%2A></xref:System.Threading.Thread.Priority%2A>|Ottiene o imposta un valore che viene utilizzato dal sistema operativo per definire le priorità di pianificazione dei thread.|  
|<xref:System.Threading.Thread.ThreadState%2A></xref:System.Threading.Thread.ThreadState%2A>|Contiene un valore che descrive lo stato o gli stati di un thread.|  
  
## <a name="thread-priorities"></a>Priorità dei thread  
 Ogni thread dispone di una proprietà di priorità che determina la quantità di tempo del processore che è necessario eseguire. Il sistema operativo alloca più lunghi rispetto ai thread ad alta priorità e tempi più brevi per i thread con priorità bassa. Nuovi thread vengono creati con il valore di `Normal`, ma è possibile modificare il <xref:System.Threading.Thread.Priority%2A>qualsiasi valore nella proprietà di <xref:System.Threading.ThreadPriority>enumerazione.</xref:System.Threading.ThreadPriority> </xref:System.Threading.Thread.Priority%2A>  
  
 Vedere <xref:System.Threading.ThreadPriority>per una descrizione dettagliata delle priorità dei thread.</xref:System.Threading.ThreadPriority>  
  
## <a name="foreground-and-background-threads"></a>Thread in primo piano e in background  
 Oggetto *thread in primo piano* viene eseguito all'infinito, mentre un *thread in background* arresta non appena l'ultimo thread in foreground. È possibile utilizzare il <xref:System.Threading.Thread.IsBackground%2A>proprietà per impostare o modificare lo stato di un thread di background.</xref:System.Threading.Thread.IsBackground%2A>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Thread></xref:System.Threading.Thread>   
 [Sincronizzazione dei thread (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md)   
 [Parametri e valori restituiti per routine multithreading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md)   
 [Threading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md)
