---
title: "Interoperabilità nativa"
description: "Interoperabilità nativa"
keywords: .NET, .NET Core
author: blackdwarf
ms.author: ronpet
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 3c357112-35fb-44ba-a07b-6a1c140370ac
translationtype: Human Translation
ms.sourcegitcommit: d18b21b67c154c4a8cf8211aa5d1473066c53656
ms.openlocfilehash: 13a4e4e7a588d55e82c5c4cde8f825c3b4502bb4
ms.lasthandoff: 03/02/2017

---

# <a name="native-interoperability"></a>Interoperabilità nativa

In questo documento vengono descritti in modo approfondito i tre modi di ottenere l'"interoperabilità nativa" disponibili nella piattaforma .NET.

Esistono alcuni motivi che rendono necessaria la chiamata del codice nativo:

*   Sistemi operativi dotati di un volume elevato di API che non sono presenti nelle librerie di classi gestite. Un ottimo esempio è l'accesso alle funzioni di gestione dell'hardware o del sistema operativo.
*   Comunicazione con altri componenti che hanno o possono generare ABI di tipo C (ABI native). Questo può riguardare, ad esempio, codice Java esposto tramite [JNI (Java Native Interface)](http://docs.oracle.com/javase/8/docs/technotes/guides/jni/) o qualsiasi altro linguaggio gestito in grado di generare un componente nativo.
*   In Windows la maggior parte del software installato, ad esempio la suite Microsoft Office, registra i componenti COM che rappresentano i propri programmi e consente agli sviluppatori di automatizzarli o di usarli. Anche questo richiede interoperabilità nativa.

L'elenco sopra riportato, naturalmente, non esaurisce tutti i potenziali scenari e situazioni in cui lo sviluppatore vuole, preferisce o ha bisogno di interfacciarsi con i componenti nativi. La libreria di classi .NET, ad esempio, usa il supporto per l'interoperabilità nativa per implementare un numero notevole di API, ad esempio il supporto e la manipolazione della console, l'accesso al file system e altro. È tuttavia importante notare che, qualora fosse necessaria, questa opzione è comunque disponibile.

> [!NOTE]
> La maggior parte degli esempi riportati in questo documento viene presentata per tutte e tre le piattaforme supportate in .NET Core (Windows, Linux e macOS). Per alcuni esempi brevi e illustrativi, tuttavia, verrà presentata solo la versione che usa nomi file ed estensioni Windows, come "dll" per le librerie. Questo non significa che le funzionalità illustrate non siano disponibili in Linux o macOS. La scelta dipende infatti solo da motivi di praticità.

## <a name="platform-invoke-pinvoke"></a>Platform Invoke (P/Invoke)

P/Invoke è una tecnologia che consente di accedere dal codice gestito a strutture, callback e funzioni presenti in librerie non gestite. La maggior parte delle API di P/Invoke è contenuta in due spazi dei nomi: `System` e `System.Runtime.InteropServices`. Usando questi due spazi dei nomi è possibile accedere agli attributi che descrivono il modo in cui si vuole comunicare con il componente nativo.

Per iniziare viene mostrato l'esempio più comune, ovvero la chiamata di funzioni non gestite nel codice gestito. Di seguito viene visualizzata una finestra di messaggio da un'applicazione della riga di comando:

```cs
using System.Runtime.InteropServices;

public class Program {

    // Import user32.dll (containing the function we need) and define
    // the method corresponding to the native function.
    [DllImport("user32.dll")]
    public static extern int MessageBox(IntPtr hWnd, String text, String caption, int options);

    public static void Main(string[] args) {
        // Invoke the function as a regular managed method.
        MessageBox(IntPtr.Zero, "Command-line message box", "Attention!", 0);
    }
}

```

L'esempio precedente è piuttosto semplice, ma mostra chiaramente gli elementi necessari per richiamare funzioni non gestite da un codice gestito. Di seguito l'esempio viene descritto in modo dettagliato:

*   La riga 1 mostra l'uso dell'istruzione per `System.Runtime.InteropServices`, ovvero lo spazio dei nomi contenente tutti gli elementi necessari.
*   La riga 5 introduce l'attributo `DllImport`. Questo attributo è fondamentale, in quanto comunica al runtime che deve caricare la DLL non gestita. Si tratta della DLL di cui si vuole richiamare il contenuto.
*   La riga 6 è il punto cruciale dell'attività di P/Invoke. Definisce un metodo gestito che ha **esattamente la stessa firma** del metodo non gestito. Come è possibile notare, la dichiarazione dispone di una nuova parola chiave, `extern`, che indica al runtime che si tratta di un metodo esterno. Quando si richiama tale metodo, il runtime dovrebbe individuarlo nella DLL specificata nell'attributo `DllImport`.

La restante parte dell'esempio è semplicemente la chiamata del metodo, analoga alla chiamata di qualsiasi altro metodo gestito.

L'esempio è simile per macOS. Uno degli elementi che è necessario cambiare è, naturalmente, il nome della libreria nell'attributo `DllImport`, poiché macOS utilizza un differente schema di denominazione delle librerie dinamiche. Nell'esempio seguente viene usata la funzione `getpid(2)` per ottenere l'ID processo dell'applicazione e stamparlo nella console.

```cs
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

        // Import the libc and define the method corresponding to the native function.
        [DllImport("libSystem.dylib")]
        private static extern int getpid();

        public static void Main(string[] args){
            // Invoke the function and get the process ID.
            int pid = getpid();
            Console.WriteLine(pid);
        }
    }
}

```

Naturalmente, il procedimento è simile in Linux. Il nome della funzione è lo stesso, dal momento che `getpid(2)` è la chiamata di sistema [POSIX](https://en.wikipedia.org/wiki/POSIX).

```cs
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

        // Import the libc and define the method corresponding to the native function.
        [DllImport("libc.so.6")]
        private static extern int getpid();

        public static void Main(string[] args){
            // Invoke the function and get the process ID.
            int pid = getpid();
            Console.WriteLine(pid);
        }
    }
}

```

### <a name="invoking-managed-code-from-unmanaged-code"></a>Richiamare codice gestito da codice non gestito

Il runtime consente naturalmente la comunicazione in entrambe le direzioni, permettendo di chiamare elementi gestiti da funzioni native usando puntatori alle funzioni. In un codice gestito l'elemento più simile a un puntatore a funzione è un **delegato**. Viene quindi usato un delegato per consentire i callback dal codice nativo al codice gestito.

La modalità di uso di questa funzionalità è simile al processo di passaggio dal codice gestito a quello nativo descritto in precedenza. Per un determinato callback, viene definito un delegato corrispondente alla firma. Tale delegato viene quindi passato al metodo esterno. Il runtime eseguirà tutte le altre operazioni.

```cs
using System;
using System.Runtime.InteropServices;

namespace ConsoleApplication1 {

    class Program {

        // Define a delegate that corresponds to the unmanaged function.
        delegate bool EnumWC(IntPtr hwnd, IntPtr lParam);

        // Import user32.dll (containing the function we need) and define
        // the method corresponding to the native function.
        [DllImport("user32.dll")]
        static extern int EnumWindows(EnumWC hWnd, IntPtr lParam);

        // Define the implementation of the delegate; here, we simply output the window handle.
        static bool OutputWindow(IntPtr hwnd, IntPtr lParam) {
            Console.WriteLine(hwnd.ToInt64());
            return true;
        }

        static void Main(string[] args) {
            // Invoke the method; note the delegate as a first parameter.
            EnumWindows(OutputWindow, IntPtr.Zero);
        }
    }
}

```

Prima di analizzare l'esempio, è opportuno esaminare le firme delle funzioni non gestite che è necessario utilizzare. La firma della funzione da chiamare per enumerare tutte le finestre è la seguente: `BOOL EnumWindows (WNDENUMPROC lpEnumFunc, LPARAM lParam);`

Il primo parametro è un callback. La firma di tale callback è la seguente: `BOOL CALLBACK EnumWindowsProc (HWND hwnd, LPARAM lParam);`

Tenendo presente questo, passare ad analizzare l'esempio:

*   La riga 8 dell'esempio definisce un delegato che corrisponde alla firma del callback da un codice non gestito. Si noti che i tipi LPARAM e HWND vengono rappresentati usando `IntPtr` nel codice gestito.
*   Le righe 10 e 11 introducono la funzione `EnumWindows` dalla libreria user32.dll.
*   Le righe da 13 a 16 implementano il delegato. Per questo semplice esempio si vuole eseguire l'output dell'handle alla console.
*   Nella riga 19, infine, il metodo esterno viene richiamato e passato al delegato.

Gli esempi Linux e macOS sono riportati di seguito. Per questi esempi viene usata la funzione `ftw` disponibile in `libc`, la libreria C. Questa funzione viene usata per scorrere le gerarchie di directory e accetta un puntatore a una funzione come uno dei propri parametri. Tale funzione ha la firma seguente: `int (*fn) (const char *fpath, const struct stat *sb, int typeflag)`.

```cs
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

            // Define a delegate that has the same signature as the native function.
            delegate int DirClbk(string fName, StatClass stat, int typeFlag);

            // Import the libc and define the method to represent the native function.
            [DllImport("libc.so.6")]
            static extern int ftw(string dirpath, DirClbk cl, int descriptors);

            // Implement the above DirClbk delegate;
            // this one just prints out the filename that is passed to it.
            static int DisplayEntry(string fName, StatClass stat, int typeFlag) {
                    Console.WriteLine(fName);
                    return 0;
            }

            public static void Main(string[] args){
                    // Call the native function.
                    // Note the second parameter which represents the delegate (callback).
                    ftw(".", DisplayEntry, 10);
            }
    }

    // The native callback takes a pointer to a struct. The below class
    // represents that struct in managed code. You can find more information
    // about this in the section on marshalling below.
    [StructLayout(LayoutKind.Sequential)]
    public class StatClass {
            public uint DeviceID;
            public uint InodeNumber;
            public uint Mode;
            public uint HardLinks;
            public uint UserID;
            public uint GroupID;
            public uint SpecialDeviceID;
            public ulong Size;
            public ulong BlockSize;
            public uint Blocks;
            public long TimeLastAccess;
            public long TimeLastModification;
            public long TimeLastStatusChange;
    }
}

```

Nell'esempio macOS viene usata la stessa funzione. L'unica differenza è l'argomento dell'attributo `DllImport`, dal momento che macOS mantiene `libc` in una posizione differente.

```cs
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
        public static class Program {

                // Define a delegate that has the same signature as the native function.
                delegate int DirClbk(string fName, StatClass stat, int typeFlag);

                // Import the libc and define the method to represent the native function.
                [DllImport("libSystem.dylib")]
                static extern int ftw(string dirpath, DirClbk cl, int descriptors);

                // Implement the above DirClbk delegate;
                // this one just prints out the filename that is passed to it.
                static int DisplayEntry(string fName, StatClass stat, int typeFlag) {
                        Console.WriteLine(fName);
                        return 0;
                }

                public static void Main(string[] args){
                        // Call the native function.
                        // Note the second parameter which represents the delegate (callback).
                        ftw(".", DisplayEntry, 10);
                }
        }

        // The native callback takes a pointer to a struct. The below class
        // represents that struct in managed code. You can find more information
        // about this in the section on marshalling below.
        [StructLayout(LayoutKind.Sequential)]
        public class StatClass {
                public uint DeviceID;
                public uint InodeNumber;
                public uint Mode;
                public uint HardLinks;
                public uint UserID;
                public uint GroupID;
                public uint SpecialDeviceID;
                public ulong Size;
                public ulong BlockSize;
                public uint Blocks;
                public long TimeLastAccess;
                public long TimeLastModification;
                public long TimeLastStatusChange;
        }
}

```

Entrambi gli esempi precedenti dipendono da parametri e in entrambi i casi i parametri vengono forniti come tipi gestiti. Il runtime esegue le operazioni necessarie ed elabora i parametri ottenendo i relativi equivalenti sull'altro lato. Poiché questo processo è molto importante per la scrittura di codice di interoperabilità nativa di qualità, è opportuno sapere cosa succede quando il runtime _effettua il marshalling_ dei tipi.

## <a name="type-marshalling"></a>Marshalling dei tipi

Il termine **marshalling** indica il processo di trasformazione dei tipi quando questi devono passare dal codice gestito a quello nativo e viceversa.

Il motivo per cui il marshalling è necessario è che i tipi presenti nel codice gestito e quelli presenti nel codice non gestito sono differenti. Nel codice gestito, ad esempio, si ha un elemento `String`, mentre nell'ambiente non gestito le stringhe possono essere Unicode ("wide"), non Unicode, con terminazione null, ASCII, e così via. Per impostazione predefinita, il sottosistema di P/Invoke tenterà di eseguire le operazioni necessarie in base al comportamento predefinito descritto in [MSDN](https://msdn.microsoft.com/library/zah6xy75.aspx). Tuttavia, per i casi in cui è necessario un controllo aggiuntivo, è possibile usare l'attributo `MarshalAs` per specificare il tipo previsto sul lato non gestito. Ad esempio, se si vuole che la stringa venga inviata come stringa ANSI con terminazione null, è possibile usare un codice simile al seguente:

```cs
[DllImport("somenativelibrary.dll"]
static extern int MethodA([MarshalAs(UnmanagedType.LPStr)] string parameter);

```

### <a name="marshalling-classes-and-structs"></a>Marshalling di classi e strutture

Un altro aspetto del marshalling dei tipi è il modo in cui è possibile passare una struttura a un metodo non gestito. Ad esempio, alcuni dei metodi non gestiti richiedono una struttura come parametro. In questi casi, è necessario creare una classe o una struttura corrispondente nel codice gestito per usarla come parametro. La semplice definizione della classe, tuttavia, non è sufficiente. È necessario anche indicare al gestore di marshalling come eseguire il mapping dei campi della classe alla struttura non gestita. A questo punto entra in gioco l'attributo `StructLayout`.

```cs
[DllImport("kernel32.dll")]
static extern void GetSystemTime(SystemTime systemTime);

[StructLayout(LayoutKind.Sequential)]
class SystemTime {
    public ushort Year;
    public ushort Month;
    public ushort DayOfWeek;
    public ushort Day;
    public ushort Hour;
    public ushort Minute;
    public ushort Second;
    public ushort Milsecond;
}

public static void Main(string[] args) {
    SystemTime st = new SystemTime();
    GetSystemTime(st);
    Console.WriteLine(st.Year);
}

```

L'esempio precedente mostra una semplice chiamata alla funzione `GetSystemTime()`. La parte interessante è alla riga 4\. L'attributo specifica che i campi della classe devono essere mappati in modo sequenziale alla struttura sull'altro lato (non gestito). Questo significa che i nomi dei campi non sono rilevanti, ma che è importante solo l'ordine. È infatti necessario che i campi corrispondano alla struttura non gestita, come mostrato di seguito:

```c
typedef struct _SYSTEMTIME {
  WORD wYear;
  WORD wMonth;
  WORD wDayOfWeek;
  WORD wDay;
  WORD wHour;
  WORD wMinute;
  WORD wSecond;
  WORD wMilliseconds;
} SYSTEMTIME, *PSYSTEMTIME*;

```

La procedura per Linux e macOS è già stata mostrata nell'esempio precedente. Viene comunque mostrata anche di seguito.

```cs
[StructLayout(LayoutKind.Sequential)]
public class StatClass {
        public uint DeviceID;
        public uint InodeNumber;
        public uint Mode;
        public uint HardLinks;
        public uint UserID;
        public uint GroupID;
        public uint SpecialDeviceID;
        public ulong Size;
        public ulong BlockSize;
        public uint Blocks;
        public long TimeLastAccess;
        public long TimeLastModification;
        public long TimeLastStatusChange;
}

```

La classe `StatClass` rappresenta una struttura restituita dalla chiamata di sistema `stat` nei sistemi UNIX. Rappresenta informazioni su un determinato file. La classe precedente è la rappresentazione statica della struttura nel codice gestito. Anche in questo caso, i campi della classe devono essere nello stesso ordine della struttura nativa (per informazioni, consultare le pagine di manuale relative all'implementazione UNIX preferita) e devono essere dello stesso tipo sottostante.

## <a name="more-resources"></a>Altre risorse

*   [PInvoke.net wiki](http://www.pinvoke.net): accurata pagina wiki con informazioni sulle API Win32 più comuni e sul modo di richiamarle.
*   [P/Invoke in MSDN](https://msdn.microsoft.com/library/zbz07712.aspx)
*   [Documentazione su Mono in P/Invoke](http://www.mono-project.com/docs/advanced/pinvoke/)

