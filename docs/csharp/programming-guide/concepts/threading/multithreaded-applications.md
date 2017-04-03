---
title: Applicazioni multithreading (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: b7015cfb-d506-4eac-b2f8-b2caaa9cc977
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a36fd71ff41eb219f4c4de36d4fa8da9b8ee179a
ms.lasthandoff: 03/13/2017

---
# <a name="multithreaded-applications-c"></a>Applicazioni multithreading (C#)
Con C# è possibile scrivere applicazioni in grado di eseguire più attività contemporaneamente. Le attività potenzialmente in grado di compromettere altre attività possono essere eseguite su thread separati, un processo noto con il nome di *multithreading* o *threading Free*.  
  
 Le applicazioni che usano il multithreading sono più reattive all'input dell'utente poiché l'interfaccia utente rimane attiva mentre le attività che richiedono un uso intensivo del processore vengono eseguite su thread separati. Il multithreading è utile anche durante la creazione di applicazioni scalabili poiché consente di aggiungere thread man mano che aumenta il carico di lavoro.  
  
## <a name="creating-and-using-threads"></a>Creazione e uso dei thread  
 Nel caso sia necessario un maggiore controllo sul comportamento dei thread dell'applicazione, è possibile gestirli personalmente. È tuttavia necessario tenere presente che la scrittura di applicazioni multithreading complesse può essere difficile: l'applicazione potrebbe non rispondere o essere soggetta a errori temporanei dovuti a race condition. Per altre informazioni, vedere [Componenti thread-safe](http://msdn.microsoft.com/library/4f7c7377-a782-4bd0-aaa3-9db8c12945ee).  
  
 Per creare un nuovo thread è necessario dichiarare una variabile di tipo <xref:System.Threading.Thread> e chiamare il costruttore, specificare il nome della routine o del metodo che si vuole eseguire nel nuovo thread. Nel codice seguente ne viene illustrato un esempio.  
  
```csharp  
System.Threading.Thread newThread =  
    new System.Threading.Thread(AMethod);  
```  
  
### <a name="starting-and-stopping-threads"></a>Avvio e arresto dei thread  
 Per avviare l'esecuzione di un nuovo thread, usare il metodo <xref:System.Threading.Thread.Start%2A> come illustrato nel codice seguente.  
  
```csharp  
newThread.Start();  
```  
  
 Per arrestare l'esecuzione di un thread, usare il metodo <xref:System.Threading.Thread.Abort%2A> come illustrato nel codice seguente.  
  
```csharp  
newThread.Abort();  
```  
  
 Oltre ad avviare e arrestare i thread, è anche possibile sospendere i thread chiamando il metodo <xref:System.Threading.Thread.Sleep%2A> o <xref:System.Threading.Thread.Suspend%2A>, riprendere l'esecuzione dei thread sospesi usando il metodo <xref:System.Threading.Thread.Resume%2A> ed eliminare definitivamente un thread usando il metodo <xref:System.Threading.Thread.Abort%2A>.  
  
### <a name="thread-methods"></a>Metodi di thread  
 La tabella seguente descrive alcuni metodi che è possibile usare per controllare i singoli thread.  
  
|Metodo|Azione|  
|------------|------------|  
|<xref:System.Threading.Thread.Start%2A>|Avvia l'esecuzione di un thread.|  
|<xref:System.Threading.Thread.Sleep%2A>|Sospende un thread per un determinato periodo.|  
|<xref:System.Threading.Thread.Suspend%2A>|Sospende un thread quando raggiunge un punto sicuro.|  
|<xref:System.Threading.Thread.Abort%2A>|Arresta un thread quando raggiunge un punto sicuro.|  
|<xref:System.Threading.Thread.Resume%2A>|Riavvia un thread sospeso.|  
|<xref:System.Threading.Thread.Join%2A>|Fa in modo che il thread corrente attenda il completamento di un altro thread. Se usato con un valore di timeout, questo metodo restituisce `True` se il thread viene completato nel tempo allocato.|  
  
### <a name="safe-points"></a>Punti sicuri  
 La maggior parte di questi metodi non necessita di descrizione, ma il concetto di *punto sicuro* potrebbe risultare nuovo. I punti sicuri sono posizioni nel codice in cui Common Language Runtime può eseguire in sicurezza il processo di *Garbage Collection* automatico, il rilascio delle variabili inutilizzate e la richiesta di memoria. Quando viene eseguita una chiamata al metodo <xref:System.Threading.Thread.Abort%2A> o <xref:System.Threading.Thread.Suspend%2A> di un thread, Common Language Runtime analizza il codice e determina una posizione appropriata in cui arrestare l'esecuzione del thread.  
  
### <a name="thread-properties"></a>Proprietà thread  
 I thread includono anche diverse proprietà utili, come illustrato nella tabella seguente:  
  
|Proprietà|Valore|  
|--------------|-----------|  
|<xref:System.Threading.Thread.IsAlive%2A>|Contiene il valore `True` se il thread è attivo.|  
|<xref:System.Threading.Thread.IsBackground%2A>|Ottiene o imposta un valore booleano che indica se un thread è o deve essere un thread in background. I thread in background sono simili ai thread in primo piano, ma un thread in background non impedisce l'arresto di un processo. Dopo l'arresto di tutti i thread in primo piano che appartengono a un processo, Common Language Runtime termina il processo chiamando il metodo <xref:System.Threading.Thread.Abort%2A> nei thread in background ancora attivi.|  
|<xref:System.Threading.Thread.Name%2A>|Ottiene o imposta il nome del thread. Usato in genere per individuare i singoli thread durante il debug.|  
|<xref:System.Threading.Thread.Priority%2A>|Ottiene o imposta un valore che viene usato dal sistema operativo per definire le priorità di pianificazione dei thread.|  
|<xref:System.Threading.Thread.ThreadState%2A>|Contiene un valore che descrive lo stato o gli stati di un thread.|  
  
## <a name="thread-priorities"></a>Priorità dei thread  
 Ogni thread ha una proprietà di priorità che determina il periodo di tempo del processore disponibile per la sua esecuzione. Il sistema operativo alloca periodi più lunghi ai thread ad alta priorità e periodi più brevi ai thread a bassa priorità. I nuovi thread vengono creati con il valore `Normal`, ma è possibile modificare la proprietà <xref:System.Threading.Thread.Priority%2A> impostandola su qualsiasi valore nell'enumerazione <xref:System.Threading.ThreadPriority>.  
  
 Per una descrizione dettagliata delle diverse priorità dei thread, vedere <xref:System.Threading.ThreadPriority>.  
  
## <a name="foreground-and-background-threads"></a>Thread in primo piano e in background  
 I *thread in primo piano* vengono eseguiti a oltranza, mentre i *thread in background* vengono arrestati non appena l'ultimo thread in primo piano è stato arrestato. È possibile usare la proprietà <xref:System.Threading.Thread.IsBackground%2A> per determinare o modificare lo stato di background di un thread.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Thread>   
 [Sincronizzazione di thread (C#)](../../../../csharp/programming-guide/concepts/threading/thread-synchronization.md)   
 [Parametri e valori restituiti per routine multithreading (C#)](../../../../csharp/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md)   
 [Threading (C#)](../../../../csharp/programming-guide/concepts/threading/index.md)
