---
title: Implementazione di un metodo Dispose
description: Implementazione di un metodo Dispose
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: eca6cdc3-6a14-4296-86fb-1eb2f21455b0
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: dfe2cebfbcf1f4c2697683ebda8c1e11567fd015

---

# <a name="implementing-a-dispose-method"></a>Implementazione di un metodo Dispose

Il metodo [Dispose](xref:System.IDisposable.Dispose) viene implementato per rilasciare le risorse non gestite usate dall'applicazione. Garbage Collector di .NET non alloca e non rilascia la memoria non gestita. 

Il criterio per eliminare un oggetto, definito come criterio Dispose, è valido per tutta la durata di un oggetto. Il modello Dispose viene usato solo per gli oggetti che accedono a risorse non gestite, quali handle di file e pipe, handle del Registro di sistema, handle di attesa o puntatori ai blocchi di memoria non gestita. Ciò è dovuto al fatto che il Garbage Collector è molto efficiente nel recupero degli oggetti gestiti inutilizzati, ma non è in grado di recuperare gli oggetti non gestiti.

Il modello Dispose precede due variazioni:

* Si esegue il wrapping di ogni risorsa non gestita usata da un tipo in un handle sicuro (ovvero in una classe derivata da [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle)). In questo caso, viene implementata l'interfaccia [IDisposable](xref:System.IDisposable) e un metodo `Dispose(Boolean)` aggiuntivo. Questa è la variazione consigliata e non richiede l'override del metodo [Object.Finalize](xref:System.Object.Finalize). 

> [!NOTE]
> Lo spazio dei nomi [Microsoft.Win32.SafeHandles](xref:Microsoft.Win32.SafeHandles) offre un set di classi derivate da [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle), che sono elencate nella sezione [Uso degli handle sicuri](#using-safe-handles). Se non è possibile trovare una classe in grado di rilasciare la risorsa non gestita, è possibile implementare una propria sottoclasse di [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle). 
 
* Si implementa l'interfaccia [IDisposable](xref:System.IDisposable) e un metodo `Dispose(Boolean` aggiuntivo e si esegue anche l'override del metodo [Object.Finalize](xref:System.Object.Finalize). È necessario eseguire l'override di [Finalize](xref:System.Object.Finalize) per assicurarsi che le risorse non gestite vengano eliminate se l'implementazione [IDisposable.Dispose](xref:System.IDisposable.Dispose) non viene chiamata da un consumer del tipo proprio. Se si usa la tecnica consigliata discussa nel precedente punto, questa operazione viene eseguita automaticamente dalla classe [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle). 

Per garantire la corretta pulitura delle risorse in ogni occasione, deve essere possibile chiamare il metodo [Dispose](xref:System.IDisposable.Dispose) più volte senza che venga generata un'eccezione. 

L'esempio di codice per il metodo [GC.KeepAlive](xref:System.GC.KeepAlive(System.Object)) illustra come una procedura di Garbage Collection troppo incisiva possa determinare l'esecuzione di un finalizzatore mentre un membro dell'oggetto recuperato è ancora in esecuzione. È consigliabile chiamare il metodo [KeepAlive](xref:System.GC.KeepAlive(System.Object)) alla fine di un metodo `Dispose` di lunga durata.

## <a name="dispose-and-disposeboolean"></a>Dispose() e Dispose(Boolean)

L'interfaccia [IDisposable](xref:System.IDisposable) richiede l'implementazione di un singolo metodo senza parametri, ovvero [Dispose](xref:System.IDisposable.Dispose). Tuttavia, il modello Dispose richiede due metodi `Dispose` per essere implementato: 

* Un'implementazione di [IDisposable.Dispose](xref:System.IDisposable.Dispose) pubblica non virtuale (`NonInheritable` in Visual Basic) senza parametri.

* Un metodo `Overridable` protetto virtuale (`Dispose` in Visual Basic) la cui firma è indicata di seguito:

  ```cs
  protected virtual void Dispose(bool disposing)
  ```

  ```vb
  Protected Overridable Sub Dispose(disposing As Boolean)
  ```

### <a name="the-dispose-overload"></a>Overload Dispose()

Poiché il metodo pubblico, non virtuale (`NonInheritable` in Visual Basic), privo di parametri `Dispose` è chiamato da un consumer del tipo, lo scopo è liberare le risorse non gestite e indicare che non è necessario eseguire il finalizzatore, se disponibili. Per questo motivo il metodo ha un'implementazione standard:

```cs
public void Dispose()
{
   // Dispose of unmanaged resources.
   Dispose(true);
   // Suppress finalization.
   GC.SuppressFinalize(this);
}
```

```vb
Public Sub Dispose() _
           Implements IDisposable.Dispose
   ' Dispose of unmanaged resources.
   Dispose(True)
   ' Suppress finalization.
   GC.SuppressFinalize(Me)
End Sub
```

Il metodo `Dispose` esegue la pulizia di tutti gli oggetti, quindi Garbage Collector non deve più chiamare l'override di [Object.Finalize](xref:System.Object.Finalize) degli oggetti. Pertanto, la chiamata al metodo [GC.SuppressFinalize](xref:System.GC.SuppressFinalize(System.Object)) impedisce a Garbage Collector di eseguire il finalizzatore. Se il tipo non dispone di un finalizzatore, la chiamata a [SuppressFinalize](xref:System.GC.SuppressFinalize(System.Object)) non ha alcun effetto. Si noti che l'effettiva operazione di rilascio delle risorse non gestite viene eseguita dal secondo overload del metodo `Dispose`.

### <a name="the-disposeboolean-overload"></a>Overload Dispose(Boolean)

Nel secondo overload, il parametro *disposing* è un valore [Boolean](xref:System.Boolean) che indica se la chiamata al metodo proviene da un metodo [Dispose](xref:System.IDisposable.Dispose) (il valore è `true`) o da un finalizzatore (il valore è `false`). 

Il corpo del metodo è costituito da due blocchi di codice: 

* Un blocco che libera le risorse non gestite. Questo blocco viene eseguito indipendentemente dal valore del parametro *disposing*. 

* Un blocco condizionale che libera le risorse gestite. Il blocco viene eseguito se il valore di *disposing* è `true`. Le risorse gestite liberate possono includere: 

    **Oggetti gestiti che implementano IDisposable**. Il blocco condizionale può essere usato per chiamare la relativa implementazione di [Dispose](xref:System.IDisposable.Dispose). Se è stato usato un handle sicuro per eseguire il wrapping della risorsa non gestita, l'implementazione di [SafeHandle.Dispose(Boolean](xref:System.Runtime.InteropServices.SafeHandle.Dispose(System.Boolean)) dovrebbe essere chiamata a questo punto. 

    **Oggetti gestiti che usano grandi quantità di memoria o risorse insufficienti.** La liberazione esplicita di questi oggetti nel metodo `Dispose` ne consente un rilascio più veloce rispetto al recupero non deterministico eseguito dal Garbage Collector. 


Se la chiamata al metodo proviene da un finalizzatore (ovvero se *disposing* è `false`), viene eseguito solo il codice che libera le risorse non gestite. Poiché l'ordine in cui il Garbage Collector elimina gli oggetti gestiti durante la finalizzazione non è definito, la chiamata a questo overload `Dispose` con valore `false` impedisce che il finalizzatore tenti di liberare risorse gestite che potrebbero essere già state recuperate. 

## <a name="implementing-the-dispose-pattern-for-a-base-class"></a>Implementazione del modello Dispose per una classe di base

Per implementare il modello Dispose per una classe di base, è necessario predisporre quanto segue: 

> [!IMPORTANT]
> È consigliabile implementare questo criterio per tutte le classi di base che implementano [IDisposable](xref:System.IDisposable) e non sono `sealed`. 
 
* Un'implementazione di [Dispose](xref:System.IDisposable.Dispose) che chiami il metodo `Dispose(Boolean)`. 

* Un metodo `Dispose(Boolean)` che esegua l'effettiva operazione di rilascio delle risorse. 

* Una classe derivata da [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) che esegua il wrapping della risorsa non gestita (operazione consigliata) o un override al metodo [Object.Finalize](xref:System.Object.Finalize). La classe [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) offre un finalizzatore, non è quindi necessario codificarne uno. 

Di seguito è illustrato il modello generale per implementare il modello Dispose per una classe di base che usa un handle sicuro. 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.Runtime.InteropServices;

class BaseClass : IDisposable
{
   // Flag: Has Dispose already been called?
   bool disposed = false;
   // Instantiate a SafeHandle instance.
   SafeHandle handle = new SafeFileHandle(IntPtr.Zero, true);

   // Public implementation of Dispose pattern callable by consumers.
   public void Dispose()
   { 
      Dispose(true);
      GC.SuppressFinalize(this);           
   }

   // Protected implementation of Dispose pattern.
   protected virtual void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         handle.Dispose();
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //
      disposed = true;
   }
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.Runtime.InteropServices

Class BaseClass : Implements IDisposable
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False
   ' Instantiate a SafeHandle instance.
   Dim handle As SafeHandle = New SafeFileHandle(IntPtr.Zero, True)

   ' Public implementation of Dispose pattern callable by consumers.
   Public Sub Dispose() _
              Implements IDisposable.Dispose
      Dispose(True)
      GC.SuppressFinalize(Me)           
   End Sub

   ' Protected implementation of Dispose pattern.
   Protected Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         handle.Dispose()
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True
   End Sub
End Class
```

> [!NOTE] 
> L'esempio precedente usa un oggetto [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) per illustrare il criterio; in alternativa è possibile usare qualsiasi oggetto derivato da [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle). Si noti che l'esempio non crea correttamente un'istanza del relativo oggetto [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle). 
 
Di seguito è illustrato il modello generale per implementare il criterio Dispose per una classe di base che esegue l'override di [Object.Finalize](xref:System.Object.Finalize). 

```cs
using System;

class BaseClass : IDisposable
{
   // Flag: Has Dispose already been called?
   bool disposed = false;

   // Public implementation of Dispose pattern callable by consumers.
   public void Dispose()
   { 
      Dispose(true);
      GC.SuppressFinalize(this);           
   }

   // Protected implementation of Dispose pattern.
   protected virtual void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //
      disposed = true;
   }

   ~BaseClass()
   {
      Dispose(false);
   }
}
```

```vb
Class BaseClass : Implements IDisposable
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False

   ' Public implementation of Dispose pattern callable by consumers.
   Public Sub Dispose() _
              Implements IDisposable.Dispose
      Dispose(True)
      GC.SuppressFinalize(Me)           
   End Sub

   ' Protected implementation of Dispose pattern.
   Protected Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True
   End Sub

   Protected Overrides Sub Finalize()
      Dispose(False)      
   End Sub
End Class
```

> [!NOTE]
> In C#, si esegue l'override di [Object.Finalize](xref:System.Object.Finalize) definendo un `destructor`. 


## <a name="implementing-the-dispose-pattern-for-a-derived-class"></a>Implementazione del modello Dispose per una classe derivata

Una classe derivata da una classe che implementa l'interfaccia [IDisposable](xref:System.IDisposable) non deve implementare [IDisposable](xref:System.IDisposable), poiché l'implementazione della classe di base di [IDisposable.Dispose](xref:System.IDisposable.Dispose) viene ereditata dalle classi derivate. Al contrario, per implementare il modello Dispose per una classe derivata, è necessario predisporre quanto segue: 

* Un metodo `protected Dispose(Boolean)` che esegua l'override del metodo della classe di base ed esegua l'effettiva operazione di rilascio delle risorse della classe derivata. Questo metodo deve anche chiamare il metodo `Dispose(Boolean)` della classe di base e passare un valore `true` per l'argomento *disposing*. 

* Una classe derivata da [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) che esegua il wrapping della risorsa non gestita (operazione consigliata) o un override al metodo [Object.Finalize](xref:System.Object.Finalize). La classe [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) offre un finalizzatore, quindi non è necessario codificarne uno. Se si specifica un finalizzatore, questo deve chiamare l'overload di `Dispose(Boolean)` con un argomento *disposing* di `false`. 

Di seguito è illustrato il modello generale per implementare il modello Dispose per una classe derivata che usa un handle sicuro: 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.Runtime.InteropServices;

class DerivedClass : BaseClass
{
   // Flag: Has Dispose already been called?
   bool disposed = false;
   // Instantiate a SafeHandle instance.
   SafeHandle handle = new SafeFileHandle(IntPtr.Zero, true);

   // Protected implementation of Dispose pattern.
   protected override void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         handle.Dispose();
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //

      disposed = true;
      // Call base class implementation.
      base.Dispose(disposing);
   }
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.Runtime.InteropServices

Class DerivedClass : Inherits BaseClass 
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False
   ' Instantiate a SafeHandle instance.
   Dim handle As SafeHandle = New SafeFileHandle(IntPtr.Zero, True)

   ' Protected implementation of Dispose pattern.
   Protected Overrides Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         handle.Dispose()
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True

      ' Call base class implementation.
      MyBase.Dispose(disposing)
   End Sub
End Class
```

> [!NOTE] 
> L'esempio precedente usa un oggetto [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) per illustrare il criterio; in alternativa è possibile usare qualsiasi oggetto derivato da [SafeHandle](xref:System.Runtime.InteropServices.SafeHandle). Si noti che l'esempio non crea correttamente un'istanza del relativo oggetto [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle). 

Di seguito è illustrato il modello generale per implementare il criterio Dispose per una classe derivata che esegue l'override di [Object.Finalize](xref:System.Object.Finalize):

```cs
using System;

class DerivedClass : BaseClass
{
   // Flag: Has Dispose already been called?
   bool disposed = false;

   // Protected implementation of Dispose pattern.
   protected override void Dispose(bool disposing)
   {
      if (disposed)
         return; 

      if (disposing) {
         // Free any other managed objects here.
         //
      }

      // Free any unmanaged objects here.
      //
      disposed = true;

      // Call the base class implementation.
      base.Dispose(disposing);
   }

   ~DerivedClass()
   {
      Dispose(false);
   }
}
```

```vb
Class DerivedClass : Inherits BaseClass
   ' Flag: Has Dispose already been called?
   Dim disposed As Boolean = False

   ' Protected implementation of Dispose pattern.
   Protected Overrides Sub Dispose(disposing As Boolean)
      If disposed Then Return

      If disposing Then
         ' Free any other managed objects here.
         '
      End If

      ' Free any unmanaged objects here.
      '
      disposed = True

      ' Call the base class implementation.
      MyBase.Dispose(disposing)
   End Sub

   Protected Overrides Sub Finalize()
      Dispose(False)
   End Sub 
End Class
```

> [!NOTE]
> In C#, si esegue l'override di [Object.Finalize](xref:System.Object.Finalize) definendo un `destructor`.

## <a name="using-safe-handles"></a>Utilizzo degli handle sicuri

La scrittura di codice per il finalizzatore di un oggetto è un'attività complessa che può causare problemi se non eseguita correttamente. È pertanto consigliabile costruire oggetti [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) anziché implementare un finalizzatore.

Le classi derivate dalla classe [System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle) semplificano i problemi di durata degli oggetti assegnando e rilasciando handle senza interruzione. Contengono un finalizzatore critico la cui esecuzione è garantita durante lo scaricamento di un dominio dell'applicazione. Le seguenti classi derivate nello spazio dei nomi [Microsoft.Win32.SafeHandles](xref:Microsoft.Win32.SafeHandles) offrono handle sicuri: 

* Classi [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle), [SafeMemoryMappedFileHandle](xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedFileHandle) e [SafePipeHandle](xref:Microsoft.Win32.SafeHandles.SafePipeHandle) per file, file mappati alla memoria e pipe. 

* Classe [SafeMemoryMappedViewHandle](xref:Microsoft.Win32.SafeHandles.SafeMemoryMappedViewHandle) per le visualizzazioni di memoria. 

* Classi [SafeNCryptKeyHandle](https://msdn.microsoft.com/en-us/library/microsoft.win32.safehandles.safencryptkeyhandle(v=vs.110).aspx), [SafeNCryptProviderHandle](https://msdn.microsoft.com/en-us/library/microsoft.win32.safehandles.safencryptproviderhandle(v=vs.110).aspx) e [SafeNCryptSecretHandle](https://msdn.microsoft.com/en-us/library/microsoft.win32.safehandles.safencryptsecrethandle(v=vs.110).aspx) per i costrutti di crittografia.

* Classe [SafeRegistryHandle](xref:Microsoft.Win32.SafeHandles.SafeRegistryHandle) per le chiavi del Registro di sistema. 

* Classe [SafeWaitHandle](xref:Microsoft.Win32.SafeHandles.SafeWaitHandle) per gli handle di attesa. 

## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-base-class"></a>Uso di un handle sicuro per implementare il modello Dispose per una classe di base

L'esempio seguente illustra il modello Dispose per una classe di base, `DisposableStreamResource`, che usa handle sicuri per incapsulare le risorse non gestite. Definisce una classe `DisposableResource` che usa [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) per eseguire il wrapping di un oggetto [Stream](xref:System.IO.Stream) che rappresenta un file aperto. Il metodo `DisposableResource` include anche una singola proprietà, `Size`, che restituisce il numero totale di byte nel flusso di file. 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.IO;
using System.Runtime.InteropServices;

public class DisposableStreamResource : IDisposable
{
   // Define constants.
   protected const uint GENERIC_READ = 0x80000000;
   protected const uint FILE_SHARE_READ = 0x00000001;
   protected const uint OPEN_EXISTING = 3;
   protected const uint FILE_ATTRIBUTE_NORMAL = 0x80;
   protected IntPtr INVALID_HANDLE_VALUE = new IntPtr(-1);
   private const int INVALID_FILE_SIZE = unchecked((int) 0xFFFFFFFF);

   // Define Windows APIs.
   [DllImport("kernel32.dll", EntryPoint = "CreateFileW", CharSet = CharSet.Unicode)]
   protected static extern IntPtr CreateFile (
                                  string lpFileName, uint dwDesiredAccess, 
                                  uint dwShareMode, IntPtr lpSecurityAttributes, 
                                  uint dwCreationDisposition, uint dwFlagsAndAttributes, 
                                  IntPtr hTemplateFile);

   [DllImport("kernel32.dll")]
   private static extern int GetFileSize(SafeFileHandle hFile, out int lpFileSizeHigh);

   // Define locals.
   private bool disposed = false;
   private SafeFileHandle safeHandle; 
   private long bufferSize;
   private int upperWord;

   public DisposableStreamResource(string filename)
   {
      if (filename == null)
         throw new ArgumentNullException("The filename cannot be null.");
      else if (filename == "")
         throw new ArgumentException("The filename cannot be an empty string.");

      IntPtr handle = CreateFile(filename, GENERIC_READ, FILE_SHARE_READ,
                                 IntPtr.Zero, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL,
                                 IntPtr.Zero);
      if (handle != INVALID_HANDLE_VALUE)
         safeHandle = new SafeFileHandle(handle, true);
      else
         throw new FileNotFoundException(String.Format("Cannot open '{0}'", filename));

      // Get file size.
      bufferSize = GetFileSize(safeHandle, out upperWord); 
      if (bufferSize == INVALID_FILE_SIZE)
         bufferSize = -1;
      else if (upperWord > 0) 
         bufferSize = (((long)upperWord) << 32) + bufferSize;
   }

   public long Size 
   { get { return bufferSize; } }

   public void Dispose()
   {
      Dispose(true);
      GC.SuppressFinalize(this);
   }           

   protected virtual void Dispose(bool disposing)
   {
      if (disposed) return;

      // Dispose of managed resources here.
      if (disposing)
         safeHandle.Dispose();

      // Dispose of any unmanaged resources not wrapped in safe handles.

      disposed = true;
   }  
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.IO

Public Class DisposableStreamResource : Implements IDisposable
   ' Define constants.
   Protected Const GENERIC_READ As UInteger = &H80000000ui
   Protected Const FILE_SHARE_READ As UInteger = &H0000000i
   Protected Const OPEN_EXISTING As UInteger = 3
   Protected Const FILE_ATTRIBUTE_NORMAL As UInteger = &H80
   Protected INVALID_HANDLE_VALUE As New IntPtr(-1)
   Private Const INVALID_FILE_SIZE As Integer = &HFFFFFFFF

   ' Define Windows APIs.
   Protected Declare Function CreateFile Lib "kernel32" Alias "CreateFileA" (
                                         lpFileName As String, dwDesiredAccess As UInt32, 
                                         dwShareMode As UInt32, lpSecurityAttributes As IntPtr, 
                                         dwCreationDisposition As UInt32, dwFlagsAndAttributes As UInt32, 
                                         hTemplateFile As IntPtr) As IntPtr
   Private Declare Function GetFileSize Lib "kernel32" (hFile As SafeFileHandle, 
                                                        ByRef lpFileSizeHigh As Integer) As Integer

   ' Define locals.
   Private disposed As Boolean = False
   Private safeHandle As SafeFileHandle 
   Private bufferSize As Long 
   Private upperWord As Integer

   Public Sub New(filename As String)
      If filename Is Nothing Then
         Throw New ArgumentNullException("The filename cannot be null.")
      Else If filename = ""
         Throw New ArgumentException("The filename cannot be an empty string.")
      End If

      Dim handle As IntPtr = CreateFile(filename, GENERIC_READ, FILE_SHARE_READ,
                                        IntPtr.Zero, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL,
                                        IntPtr.Zero)
      If handle <> INVALID_HANDLE_VALUE Then
         safeHandle = New SafeFileHandle(handle, True)
      Else
         Throw New FileNotFoundException(String.Format("Cannot open '{0}'", filename))
      End If

      ' Get file size.
      bufferSize = GetFileSize(safeHandle, upperWord) 
      If bufferSize = INVALID_FILE_SIZE Then
         bufferSize = -1
      Else If upperWord > 0 Then 
         bufferSize = (CLng(upperWord) << 32) + bufferSize
      End If     
   End Sub

   Public ReadOnly Property Size As Long
      Get
         Return bufferSize
      End Get
   End Property

   Public Sub Dispose() _
              Implements IDisposable.Dispose
      Dispose(True)
      GC.SuppressFinalize(Me)
   End Sub           

   Protected Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Exit Sub

      ' Dispose of managed resources here.
      If disposing Then
         safeHandle.Dispose()
      End If

      ' Dispose of any unmanaged resources not wrapped in safe handles.

      disposed = True
   End Sub  
End Class
```

## <a name="using-a-safe-handle-to-implement-the-dispose-pattern-for-a-derived-class"></a>Utilizzo di un handle sicuro per implementare il modello Dispose per una classe derivata

Nell'esempio seguente viene illustrato il modello Dispose per una classe derivata, `DisposableStreamResource2`, che eredita dalla classe `DisposableStreamResource` presentata nell'esempio precedente. La classe aggiunge un altro metodo, `WriteFileInfo`, e usa un oggetto [SafeFileHandle](xref:Microsoft.Win32.SafeHandles.SafeFileHandle) per il wrapping dell'handle del file modificabile. 

```cs
using Microsoft.Win32.SafeHandles;
using System;
using System.IO;
using System.Runtime.InteropServices;
using System.Threading;

public class DisposableStreamResource2 : DisposableStreamResource
{
   // Define additional constants.
   protected const uint GENERIC_WRITE = 0x40000000; 
   protected const uint OPEN_ALWAYS = 4;

   // Define additional APIs.
   [DllImport("kernel32.dll")]   
   protected static extern bool WriteFile(
                                SafeFileHandle safeHandle, string lpBuffer, 
                                int nNumberOfBytesToWrite, out int lpNumberOfBytesWritten,
                                IntPtr lpOverlapped);

   // Define locals.
   private bool disposed = false;
   private string filename;
   private bool created = false;
   private SafeFileHandle safeHandle;

   public DisposableStreamResource2(string filename) : base(filename)
   {
      this.filename = filename;
   }

   public void WriteFileInfo()
   { 
      if (! created) {
         IntPtr hFile = CreateFile(xref:".\FileInfo.txt", GENERIC_WRITE, 0, 
                                   IntPtr.Zero, OPEN_ALWAYS, 
                                   FILE_ATTRIBUTE_NORMAL, IntPtr.Zero);
         if (hFile != INVALID_HANDLE_VALUE)
            safeHandle = new SafeFileHandle(hFile, true);
         else
            throw new IOException("Unable to create output file.");

         created = true;
      }

      string output = String.Format("{0}: {1:N0} bytes\n", filename, Size);
      int bytesWritten;
      bool result = WriteFile(safeHandle, output, output.Length, out bytesWritten, IntPtr.Zero);                                     
   }

   protected new virtual void Dispose(bool disposing)
   {
      if (disposed) return;

      // Release any managed resources here.
      if (disposing)
         safeHandle.Dispose();

      disposed = true;

      // Release any unmanaged resources not wrapped by safe handles here.

      // Call the base class implementation.
      base.Dispose(true);
   }
}
```

```vb
Imports Microsoft.Win32.SafeHandles
Imports System.IO

Public Class DisposableStreamResource2 : Inherits DisposableStreamResource
   ' Define additional constants.
   Protected Const GENERIC_WRITE As Integer = &H40000000 
   Protected Const OPEN_ALWAYS As Integer = 4

   ' Define additional APIs.
   Protected Declare Function WriteFile Lib "kernel32.dll" (
                              safeHandle As SafeFileHandle, lpBuffer As String, 
                              nNumberOfBytesToWrite As Integer, ByRef lpNumberOfBytesWritten As Integer,
                              lpOverlapped As Object) As Boolean

   ' Define locals.
   Private disposed As Boolean = False
   Private filename As String
   Private created As Boolean = False
   Private safeHandle As SafeFileHandle

   Public Sub New(filename As String)
      MyBase.New(filename)
      Me.filename = filename
   End Sub

   Public Sub WriteFileInfo() 
      If Not created Then
         Dim hFile As IntPtr = CreateFile(".\FileInfo.txt", GENERIC_WRITE, 0, 
                                          IntPtr.Zero, OPEN_ALWAYS, 
                                          FILE_ATTRIBUTE_NORMAL, IntPtr.Zero)
         If hFile <> INVALID_HANDLE_VALUE Then
            safeHandle = New SafeFileHandle(hFile, True)
         Else
            Throw New IOException("Unable to create output file.")
         End If
         created = True
      End If
      Dim output As String = String.Format("{0}: {1:N0} bytes {2}", filename, Size, 
                                           vbCrLf)
      WriteFile(safeHandle, output, output.Length, 0&, Nothing)                                     
   End Sub

   Protected Overloads Overridable Sub Dispose(disposing As Boolean)
      If disposed Then Exit Sub

      ' Release any managed resources here.
      If disposing Then
         safeHandle.Dispose()
      End If

      disposed = True
      ' Release any unmanaged resources not wrapped by safe handles here.

      ' Call the base class implementation.
      MyBase.Dispose(True)
   End Sub
End Class
```

## <a name="see-also"></a>Vedere anche

[SuppressFinalize](xref:System.GC.SuppressFinalize(System.Object))

[IDisposable](xref:System.IDisposable)

[IDisposable.Dispose](xref:System.IDisposable.Dispose)

[Microsoft.Win32.SafeHandles](xref:Microsoft.Win32.SafeHandles)

[System.Runtime.InteropServices.SafeHandle](xref:System.Runtime.InteropServices.SafeHandle)

[IDisposable.Dispose](xref:System.IDisposable.Dispose)



<!--HONumber=Nov16_HO1-->


