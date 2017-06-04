---
title: "Implementazione di un metodo Dispose | Microsoft Docs"
ms.custom: ""
ms.date: "04/07/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dispose (metodo)"
  - "operazione di Garbage collection, il metodo Dispose"
ms.assetid: eb4e1af0-3b48-4fbc-ad4e-fc2f64138bf9
caps.latest.revision: 44
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 44
---
# Implementazione di un metodo Dispose
Il metodo <xref:System.IDisposable.Dispose%2A> viene implementato per rilasciare le risorse non gestite usate dall'applicazione. Il Garbage Collector di .NET Framework non alloca e non rilascia la memoria non gestita.  
  
 Il modello per eliminare un oggetto, definito come un [modello dispose](../../../docs/standard/design-guidelines/dispose-pattern.md), impone ordine nella durata di un oggetto. Il modello Dispose viene usato solo per gli oggetti che accedono a risorse non gestite, quali handle di file e pipe, handle del Registro di sistema, handle di attesa o puntatori ai blocchi di memoria non gestita. Ciò è dovuto al fatto che il Garbage Collector è molto efficiente nel recupero degli oggetti gestiti inutilizzati, ma non è in grado di recuperare gli oggetti non gestiti.  
  
 Il modello Dispose precede due variazioni:  
  
-   Si esegue il wrapping di ogni risorsa non gestita usata da un tipo in un handle sicuro (ovvero in una classe derivata da <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName>). In questo caso, viene implementata l'interfaccia <xref:System.IDisposable> e un metodo `Dispose(Boolean)` aggiuntivo. Questa è la variazione consigliata e non richiede l'override del metodo <xref:System.Object.Finalize%2A?displayProperty=fullName>.  
  
    > [!NOTE]
    >  Lo spazio dei nomi <xref:Microsoft.Win32.SafeHandles?displayProperty=fullName> offre un set di classi derivate da <xref:System.Runtime.InteropServices.SafeHandle>, che sono elencate nella sezione [Uso degli handle sicuri](#SafeHandles). Se non è possibile trovare una classe in grado di rilasciare la risorsa non gestita, è possibile implementare una propria sottoclasse di <xref:System.Runtime.InteropServices.SafeHandle>.  
  
-   Implementare il <xref:System.IDisposable> interfaccia e un ulteriore `Dispose(Boolean)` (metodo) e anche l'override di <xref:System.Object.Finalize%2A?displayProperty=fullName> (metodo). È necessario eseguire l'override di <xref:System.Object.Finalize%2A> per assicurarsi che le risorse non gestite vengano eliminate se l'implementazione <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> non viene chiamata da un consumer del tipo proprio. Se si usa la tecnica consigliata discussa nel precedente punto, questa operazione viene eseguita automaticamente dalla classe <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName>.  
  
 Per garantire la corretta pulitura delle risorse in ogni occasione, deve essere possibile chiamare il metodo <xref:System.IDisposable.Dispose%2A> più volte senza che venga generata un'eccezione.  
  
> [!IMPORTANT]
>  Se siete programmatori C++, non implementare il <xref:System.IDisposable.Dispose%2A> metodo. Al contrario, seguire le istruzioni nella sezione "Distruttori e finalizzatori" di [procedura: definire e usare classi e struct (C + c++ CLI)](../Topic/How%20to:%20Define%20and%20Consume%20Classes%20and%20Structs%20\(C++-CLI\).md). A partire da .NET Framework 2.0, il compilatore C++ supporta l'eliminazione deterministica delle risorse e non consente l'implementazione diretta del <xref:System.IDisposable.Dispose%2A> metodo.  
  
 L'esempio di codice per il metodo <xref:System.GC.KeepAlive%2A?displayProperty=fullName> illustra come una procedura di Garbage Collection troppo incisiva possa determinare l'esecuzione di un finalizzatore mentre un membro dell'oggetto recuperato è ancora in esecuzione. È consigliabile chiamare il <xref:System.GC.KeepAlive%2A> metodo alla fine di una lunga <xref:System.IDisposable.Dispose%2A> metodo.  
  
<a name="Dispose2"></a>   
## <a name="dispose-and-disposeboolean"></a>Dispose() e Dispose(Boolean)  
 L'interfaccia <xref:System.IDisposable> richiede l'implementazione di un singolo metodo senza parametri, ovvero <xref:System.IDisposable.Dispose%2A>. Tuttavia, il modello Dispose richiede due metodi `Dispose` per essere implementato:  
  
-   Un'implementazione di <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> pubblica non virtuale (`NonInheritable` in Visual Basic) senza parametri.  
  
-   Un metodo `Overridable` protetto virtuale (`Dispose` in Visual Basic) la cui firma è indicata di seguito:  
  
     [!code-csharp[Conceptual.Disposable#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#8)]
     [!code-vb[Conceptual.Disposable#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#8)]  
  
### <a name="the-dispose-overload"></a>Overload Dispose()  
 Poiché il metodo pubblico, non virtuale (`NonInheritable` in Visual Basic), privo di parametri `Dispose` è chiamato da un consumer del tipo, lo scopo è liberare le risorse non gestite e indicare che non è necessario eseguire il finalizzatore, se disponibili. Per questo motivo il metodo ha un'implementazione standard:  
  
 [!code-csharp[Conceptual.Disposable#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/dispose1.cs#7)]
 [!code-vb[Conceptual.Disposable#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/dispose1.vb#7)]  
  
 Il metodo `Dispose` esegue la pulizia di tutti gli oggetti, quindi Garbage Collector non deve più chiamare l'override di <xref:System.Object.Finalize%2A?displayProperty=fullName> degli oggetti. Pertanto, la chiamata per il <xref:System.GC.SuppressFinalize%2A> metodo impedisce al garbage collector di eseguire il finalizzatore. Se il tipo non dispone di alcun finalizzatore, la chiamata a <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> non ha alcun effetto. Si noti che l'effettiva operazione di rilascio delle risorse non gestite viene eseguita dal secondo overload del metodo `Dispose`.  
  
### <a name="the-disposeboolean-overload"></a>Overload Dispose(Boolean)  
 Nel secondo overload, il `disposing` parametro è un <xref:System.Boolean> che indica se la chiamata al metodo proviene da un <xref:System.IDisposable.Dispose%2A> (metodo) (il valore è `true`) o da un finalizzatore (il valore è `false`).  
  
 Il corpo del metodo è costituito da due blocchi di codice:  
  
-   Un blocco che libera le risorse non gestite. Questo blocco viene eseguito indipendentemente dal valore del parametro `disposing`.  
  
-   Un blocco condizionale che libera le risorse gestite. Il blocco è eseguito se il valore di `disposing` è `true`. Le risorse gestite liberate possono includere:  
  
     **Oggetti gestiti che implementano <xref:System.IDisposable>.**  
     Il blocco condizionale può essere usato per chiamare la relativa implementazione di <xref:System.IDisposable.Dispose%2A>. Se è stato usato un handle sicuro per eseguire il wrapping della risorsa non gestita, è necessario chiamare il <xref:System.Runtime.InteropServices.SafeHandle.Dispose%28System.Boolean%29?displayProperty=fullName> qui l'implementazione.  
  
     **Oggetti gestiti che usano grandi quantità di memoria o risorse insufficienti.**  
     La liberazione esplicita di questi oggetti nel metodo `Dispose` ne consente un rilascio più veloce rispetto al recupero non deterministico eseguito dal Garbage Collector.  
  
 Se la chiamata al metodo proviene da un finalizzatore (ovvero se `disposing` è `false`), viene eseguito solo il codice che libera le risorse non gestite. Poiché l'ordine in cui il Garbage Collector elimina gli oggetti gestiti durante la finalizzazione non è definito, la chiamata a questo overload `Dispose` con valore `false` impedisce che il finalizzatore tenti di liberare risorse gestite che potrebbero essere già state recuperate.  
  
## <a name="implementing-the-dispose-pattern-for-a-base-class"></a>Implementazione del modello Dispose per una classe di base  
 Per implementare il modello Dispose per una classe di base, è necessario predisporre quanto segue:  
  
> [!IMPORTANT]
>  È necessario implementare questo modello per tutte le classi base che implementano <xref:System.IDisposable> e non sono `sealed` (`NotInheritable` in Visual Basic).  
  
-   Un'implementazione di <xref:System.IDisposable.Dispose%2A> che chiami il metodo `Dispose(Boolean)`.  
  
-   Un metodo `Dispose(Boolean)` che esegua l'effettiva operazione di rilascio delle risorse.  
  
-   Una classe derivata da <xref:System.Runtime.InteropServices.SafeHandle> che esegua il wrapping della risorsa non gestita (operazione consigliata) o un override al metodo <xref:System.Object.Finalize%2A?displayProperty=fullName>. La classe <xref:System.Runtime.InteropServices.SafeHandle> offre un finalizzatore, quindi non è necessario codificarne uno.  
  
 Di seguito è illustrato il modello generale per implementare il modello Dispose per una classe di base che usa un handle sicuro.  
  
 [!code-csharp[System.IDisposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base1.cs#3)]
 [!code-vb[System.IDisposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base1.vb#3)]  
  
> [!NOTE]
>  L'esempio precedente usa un oggetto <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> per illustrare il criterio; in alternativa è possibile usare qualsiasi oggetto derivato da <xref:System.Runtime.InteropServices.SafeHandle>. Si noti che l'esempio non crea correttamente un'istanza del relativo oggetto <xref:Microsoft.Win32.SafeHandles.SafeFileHandle>.  
  
 Di seguito è illustrato il modello generale per implementare il criterio Dispose per una classe di base che esegue l'override di <xref:System.Object.Finalize%2A?displayProperty=fullName>.  
  
 [!code-csharp[System.IDisposable#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/base2.cs#5)]
 [!code-vb[System.IDisposable#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/base2.vb#5)]  
  
> [!NOTE]
>  In c#, si esegue l'override <xref:System.Object.Finalize%2A?displayProperty=fullName> definendo un [distruttore](../Topic/Destructors%20\(C%23%20Programming%20Guide\).md).  
  
## <a name="implementing-the-dispose-pattern-for-a-derived-class"></a>Implementazione del modello Dispose per una classe derivata  
 Una classe derivata da una classe che implementa l'interfaccia <xref:System.IDisposable> non deve implementare <xref:System.IDisposable>, poiché l'implementazione della classe di base di <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> viene ereditata dalle classi derivate. Al contrario, per implementare il modello Dispose per una classe derivata, è necessario predisporre quanto segue:  
  
-   Un metodo `protected``Dispose(Boolean)` che esegua l'override del metodo della classe di base ed esegua l'effettiva operazione di rilascio delle risorse della classe derivata. Questo metodo deve anche chiamare il metodo `Dispose(Boolean)` della classe di base e passare un valore `true` per l'argomento `disposing`.  
  
-   Una classe derivata da <xref:System.Runtime.InteropServices.SafeHandle> che esegua il wrapping della risorsa non gestita (operazione consigliata) o un override al metodo <xref:System.Object.Finalize%2A?displayProperty=fullName>. La classe <xref:System.Runtime.InteropServices.SafeHandle> offre un finalizzatore, quindi non è necessario codificarne uno. Se si fornisce un finalizzatore, questo deve chiamare l'overload di `Dispose(Boolean)` con un argomento `disposing` uguale a `false`.  
  
 Di seguito è illustrato il modello generale per implementare il modello Dispose per una classe derivata che usa un handle sicuro:  
  
 [!code-csharp[System.IDisposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived1.cs#4)]
 [!code-vb[System.IDisposable#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived1.vb#4)]  
  
> [!NOTE]
>  L'esempio precedente usa un oggetto <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> per illustrare il criterio; in alternativa è possibile usare qualsiasi oggetto derivato da <xref:System.Runtime.InteropServices.SafeHandle>. Si noti che l'esempio non crea correttamente un'istanza del relativo oggetto <xref:Microsoft.Win32.SafeHandles.SafeFileHandle>.  
  
 Di seguito è illustrato il modello generale per implementare il criterio Dispose per una classe derivata che esegue l'override di <xref:System.Object.Finalize%2A?displayProperty=fullName>:  
  
 [!code-csharp[System.IDisposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.idisposable/cs/derived2.cs#6)]
 [!code-vb[System.IDisposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.idisposable/vb/derived2.vb#6)]  
  
> [!NOTE]
>  In c#, si esegue l'override <xref:System.Object.Finalize%2A?displayProperty=fullName> definendo un [distruttore](../Topic/Destructors%20\(C%23%20Programming%20Guide\).md).  
  
<a name="SafeHandles"></a>   
## <a name="using-safe-handles"></a>Utilizzo degli handle sicuri  
 La scrittura di codice per il finalizzatore di un oggetto è un'attività complessa che può causare problemi se non eseguita correttamente. È pertanto consigliabile costruire oggetti <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName> anziché implementare un finalizzatore.  
  
 Le classi derivate dalla classe <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName> semplificano i problemi di durata degli oggetti assegnando e rilasciando handle senza interruzione. Contengono un finalizzatore critico la cui esecuzione è garantita durante lo scaricamento di un dominio dell'applicazione. Per ulteriori informazioni sui vantaggi dell'utilizzo di un handle sicuro, vedere <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName>. Le seguenti classi derivate nello spazio dei nomi <xref:Microsoft.Win32.SafeHandles> offrono handle sicuri:  
  
-   Classi <xref:Microsoft.Win32.SafeHandles.SafeFileHandle>, <xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedFileHandle> e <xref:Microsoft.Win32.SafeHandles.SafePipeHandle> per file, file mappati alla memoria e pipe.  
  
-   Classe <xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedViewHandle> per le visualizzazioni di memoria.  
  
-   Classi <xref:Microsoft.Win32.SafeHandles.SafeNCryptKeyHandle>, <xref:Microsoft.Win32.SafeHandles.SafeNCryptProviderHandle> e <xref:Microsoft.Win32.SafeHandles.SafeNCryptSecretHandle> per i costrutti di crittografia.  
  
-   Classe <xref:Microsoft.Win32.SafeHandles.SafeRegistryHandle> per le chiavi del Registro di sistema.  
  
-   Classe <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> per gli handle di attesa.  
  
<a name="base"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-base-class"></a>Uso di un handle sicuro per implementare il modello Dispose per una classe di base  
 L'esempio seguente illustra il modello Dispose per una classe di base, `DisposableStreamResource`, che usa handle sicuri per incapsulare le risorse non gestite. Definisce una classe `DisposableResource` che usa <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> per eseguire il wrapping di un oggetto <xref:System.IO.Stream> che rappresenta un file aperto. Il metodo `DisposableResource` include anche una singola proprietà, `Size`, che restituisce il numero totale di byte nel flusso di file.  
  
 [!code-csharp[Conceptual.Disposable#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/base1.cs#9)]
 [!code-vb[Conceptual.Disposable#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/base1.vb#9)]  
  
<a name="derived"></a>   
## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-derived-class"></a>Utilizzo di un handle sicuro per implementare il modello Dispose per una classe derivata  
 Nell'esempio seguente viene illustrato il modello Dispose per una classe derivata, `DisposableStreamResource2`, che eredita dalla classe `DisposableStreamResource` presentata nell'esempio precedente. La classe aggiunge un altro metodo, `WriteFileInfo`, e usa un oggetto <xref:Microsoft.Win32.SafeHandles.SafeFileHandle> per il wrapping dell'handle del file modificabile.  
  
 [!code-csharp[Conceptual.Disposable#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/derived1.cs#10)]
 [!code-vb[Conceptual.Disposable#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/derived1.vb#10)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.GC.SuppressFinalize%2A>   
 <xref:System.IDisposable>   
 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>   
 <xref:Microsoft.Win32.SafeHandles>   
 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName>   
 <xref:System.Object.Finalize%2A?displayProperty=fullName>   
 [Procedura: definire e utilizzare classi e struct (C + c++ /CLI)](../Topic/How%20to:%20Define%20and%20Consume%20Classes%20and%20Structs%20\(C++-CLI\).md)   
 [Modello Dispose](../../../docs/standard/design-guidelines/dispose-pattern.md)