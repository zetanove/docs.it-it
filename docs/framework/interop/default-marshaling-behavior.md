---
title: "Default Marshaling Behavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "interop marshaling, default"
  - "interoperation with unmanaged code, marshaling"
  - "marshaling behavior"
ms.assetid: c0a9bcdf-3df8-4db3-b1b6-abbdb2af809a
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Default Marshaling Behavior
Il marshalling di interoperabilità opera sulle regole che stabiliscono il comportamento dei dati associati a parametri del metodo durante il passaggio tra memoria gestita e non gestita.  Queste regole predefinite controllano tali attività di marshalling come le trasformazioni dei tipi di dati, il fatto che un oggetto chiamato possa modificare i dati passati e restituire tali modifiche al chiamante e le circostanze in cui il gestore di marshalling fornisce ottimizzazioni delle prestazioni.  
  
 Questa sezione identifica le caratteristiche predefinite del comportamento del servizio di marshalling di interoperabilità.  Vengono fornite informazioni dettagliate sul marshalling di matrici, tipi booleani, tipi char, delegati, classi, oggetti, stringhe e strutture.  
  
> [!NOTE]
>  Il marshalling di tipi generici non è supportato.  Per altre informazioni, vedere [Interoperating Using Generic Types](http://msdn.microsoft.com/it-it/26b88e03-085b-4b53-94ba-a5a9c709ce58).  
  
## Gestione della memoria con il marshalling di interoperabilità  
 Il gestore di marshalling di interoperabilità tenta sempre di liberare la memoria allocata dal codice gestito.  Questo comportamento è conforme alle regole di gestione della memoria COM, ma differisce dalle regole che governano il codice C\+\+ nativo.  
  
 Se si prevede un comportamento C\+\+ nativo \(memoria non liberata\) quando si usa platform invoke, che libera automaticamente la memoria per i puntatori, può insorgere confusione.  Ad esempio, se si chiama il metodo non gestito seguente da una DLL C\+\+, non viene liberata automaticamente la memoria.  
  
### Firma non gestita  
  
```  
BSTR MethodOne (BSTR b) {  
     return b;  
}  
```  
  
 Se, tuttavia, si definisce il metodo come prototipo di platform invoke, si sostituisce ogni tipo **BSTR** con un tipo <xref:System.String> e si chiama `MethodOne`, Common Language Runtime tenta di liberare `b` due volte.  È possibile modificare il comportamento di marshalling usando tipi <xref:System.IntPtr> anziché tipi **String**.  
  
 Il runtime usa sempre il metodo **CoTaskMemFree** per liberare memoria.  Se la memoria che si sta usando non è stata allocata con il metodo **CoTaskMemAlloc**, è necessario usare un tipo **IntPtr** e liberare la memoria manualmente mediante il metodo appropriato.  Analogamente, è possibile fare in modo che la memoria non venga liberata automaticamente in situazioni in cui la memoria non deve mai essere liberata, ad esempio quando si usa la funzione **GetCommandLine** da Kernel32.dll, che restituisce un puntatore alla memoria del kernel.  Per informazioni dettagliate su come liberare manualmente la memoria, vedere [Esempio di buffer](http://msdn.microsoft.com/it-it/e30d36e8-d7c4-4936-916a-8fdbe4d9ffd5).  
  
## Marshalling predefinito per le classi  
 È possibile effettuare il marshalling delle classi solo tramite l'interoperabilità COM e solo come interfacce.  In alcuni casi l'interfaccia usata per il marshalling della classe è nota come interfaccia di classe.  Per informazioni sull'override dell'interfaccia di classe con un'altra interfaccia, vedere [Introduzione all'interfaccia della classe](http://msdn.microsoft.com/it-it/733c0dd2-12e5-46e6-8de1-39d5b25df024).  
  
### Passaggio di classi a COM  
 Quando una classe gestita viene passata a COM, il marshalling di interoperabilità esegue automaticamente il wrapping della classe con un proxy COM e passa l'interfaccia di classe creata dal proxy alla chiamata al metodo COM.  Il proxy delega quindi tutte le chiamate sull'interfaccia di classe all'oggetto gestito.  Il proxy espone anche altre interfacce non implementate in modo esplicito dalla classe.  Il proxy implementa automaticamente interfacce come **IUnknown** e **IDispatch** per conto della classe.  
  
### Passaggio di classi al codice .NET  
 Le coclassi non sono in genere usate come argomenti dei metodi in COM.  Al posto della coclasse viene invece in genere passata un'interfaccia predefinita.  
  
 Quando viene passata un'interfaccia nel codice gestito, il gestore di marshalling di interoperabilità è responsabile di eseguire il wrapping dell'interfaccia con il wrapper appropriato e di passare il wrapper al metodo gestito.  La determinazione del wrapper da usare può essere complessa.  Ogni istanza di un oggetto COM prevede un singolo wrapper univoco, indipendentemente dal numero di interfacce implementate dall'oggetto.  Ad esempio, un singolo oggetto COM che implementa cinque interfacce distinte ha solo un wrapper.  Lo stesso wrapper espone tutte e cinque le interfacce.  Se vengono create due istanze dell'oggetto COM, vengono create due istanze del wrapper.  
  
 Affinché il wrapper mantenga lo stesso tipo per tutta la sua durata, il gestore di marshalling di interoperabilità deve identificare il wrapper corretto la prima volta che un'interfaccia esposta dall'oggetto viene passata attraverso di esso.  Il gestore di marshalling identifica l'oggetto analizzando una delle interfacce implementate.  
  
 Ad esempio, il gestore di marshalling determina che il wrapper della classe deve essere usato per eseguire il wrapping dell'interfaccia passata al codice gestito.  Quando l'interfaccia viene passata per la prima volta attraverso il gestore di marshalling, quest'ultimo controlla se l'interfaccia proviene da un oggetto noto.  Questo controllo viene eseguito in due situazioni:  
  
-   Quando un'interfaccia viene implementata da un altro oggetto gestito passato a COM in un'altra posizione.  Il gestore di marshalling può identificare immediatamente le interfacce esposte dagli oggetti gestiti ed è in grado di associare l'interfaccia all'oggetto gestito che fornisce l'implementazione.  L'oggetto gestito viene quindi passato al metodo e non sono necessari wrapper.  
  
-   Quando un oggetto di cui è già stato eseguito il wrapping implementa l'interfaccia.  Per determinare se questo è il caso, il gestore di marshalling invia una query all'oggetto per l'interfaccia **IUnknown** e confronta l'interfaccia restituita con le interfacce di altri oggetti di cui è già stato eseguito il wrapping.  Se l'interfaccia corrisponde a quella di un altro wrapper, gli oggetti hanno la stessa identità e il wrapper esistente viene passato al metodo.  
  
 Se un'interfaccia non proviene da un oggetto noto, il gestore di marshalling esegue le operazioni seguenti:  
  
1.  Il gestore di marshalling invia una query all'oggetto per l'interfaccia **IProvideClassInfo2**.  Se fornito, il gestore di marshalling usa il CLSID restituito da **IProvideClassInfo2.GetGUID** per identificare la coclasse che fornisce l'interfaccia.  Con il CLSID, il gestore di marshalling può individuare il wrapper dal Registro di sistema se l'assembly è stato registrato in precedenza.  
  
2.  Il gestore di marshalling invia una query all'interfaccia per l'interfaccia **IProvideClassInfo**.  Se fornito, il gestore di marshalling usa l'oggetto **ITypeInfo** restituito da **IProvideClassInfo.GetClassinfo** per determinare il CLSID della classe che espone l'interfaccia.  Il gestore di marshalling può usare il CLSID per individuare i metadati per il wrapper.  
  
3.  Se il gestore di marshalling non è ancora in grado di identificare la classe, esegue il wrapping dell'interfaccia con una classe wrapper generica denominata **System.\_\_ComObject**.  
  
## Marshalling predefinito per i delegati  
 Un delegato gestito viene sottoposto a marshalling come un'interfaccia COM o come un puntatore a funzione, in base al meccanismo di chiamata:  
  
-   Per platform invoke, un delegato viene sottoposto a marshalling come puntatore a funzione non gestito per impostazione predefinita.  
  
-   Per l'interoperabilità COM, un delegato viene sottoposto a marshalling come interfaccia COM di tipo **\_Delegate** per impostazione predefinita.  L'interfaccia **\_Delegate** è definita nella libreria dei tipi Mscorlib.tlb e contiene il metodo <xref:System.Delegate.DynamicInvoke%2A?displayProperty=fullName>, che consente di chiamare il metodo a cui fa riferimento il delegato.  
  
 La tabella seguente illustra le opzioni di marshalling per il tipo di dati delegato gestito.  L'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> fornisce diversi valori di enumerazione <xref:System.Runtime.InteropServices.UnmanagedType> per il marshalling di delegati.  
  
|Tipo di enumerazione|Descrizione del formato non gestito|  
|--------------------------|-----------------------------------------|  
|**UnmanagedType.FunctionPtr**|Puntatore alla funzione non gestita.|  
|**UnmanagedType.Interface**|Interfaccia di tipo **\_Delegate**, come definita in Mscorlib.tlb.|  
  
 Si consideri l'esempio di codice seguente in cui i metodi di `DelegateTestInterface` vengono esportati in una libreria dei tipi COM.  Si noti che solo i delegati contrassegnati con la parola chiave **ref** \(o **ByRef**\) vengono passati come parametri in\/out.  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
public interface DelegateTest {  
void m1(Delegate d);  
void m2([MarshalAs(UnmanagedType.Interface)] Delegate d);     
void m3([MarshalAs(UnmanagedType.Interface)] ref Delegate d);    
void m4([MarshalAs(UnmanagedType.FunctionPtr)] Delegate d);   
void m5([MarshalAs(UnmanagedType.FunctionPtr)] ref Delegate d);     
}  
```  
  
### Rappresentazione di libreria dei tipi  
  
```  
importlib("mscorlib.tlb");  
interface DelegateTest : IDispatch {  
[id(…)] HRESULT m1([in] _Delegate* d);  
[id(…)] HRESULT m2([in] _Delegate* d);  
[id(…)] HRESULT m3([in, out] _Delegate** d);  
[id()] HRESULT m4([in] int d);  
[id()] HRESULT m5([in, out] int *d);  
   };  
```  
  
 È possibile dereferenziare un puntatore a funzione, così come qualsiasi altro puntatore a funzione non gestito.  
  
> [!NOTE]
>  Un riferimento al puntatore a funzione a un delegato gestito tramite codice non gestito non impedisce a Common Language Runtime di eseguire un'operazione di Garbage Collection nell'oggetto gestito.  
  
 Il codice seguente, ad esempio, non è corretto perché il riferimento all'oggetto `cb`, passato al metodo  `SetChangeHandler` non mantiene attivo `cb` oltre la durata del metodo `Test`.  Dopo che l'oggetto `cb` è stato sottoposto a Garbage Collection, il puntatore a funzione passato a `SetChangeHandler` non è più valido.  
  
```csharp  
public class ExternalAPI {  
   [DllImport("External.dll")]  
   public static extern void SetChangeHandler(  
      [MarshalAs(UnmanagedType.FunctionPtr)]ChangeDelegate d);  
}  
public delegate bool ChangeDelegate([MarshalAs(UnmanagedType.LPWStr) string S);  
public class CallBackClass {  
   public bool OnChange(string S){ return true;}  
}  
internal class DelegateTest {  
   public static void Test() {  
      CallBackClass cb = new CallBackClass();  
      // Caution: The following reference on the cb object does not keep the   
      // object from being garbage collected after the Main method   
      // executes.  
      ExternalAPI.SetChangeHandler(new ChangeDelegate(cb.OnChange));     
   }  
}  
```  
  
 Per compensare un'operazione di Garbage Collection non prevista, il chiamante deve fare in modo che l'oggetto `cb` venga mantenuto attivo fino a quando il puntatore a funzione non gestito è in uso.  Facoltativamente, è possibile fare in modo che il codice non gestito segnali al codice gestito quando il puntatore a funzione non è più necessario, come illustrato nell'esempio seguente.  
  
```csharp  
internal class DelegateTest {  
   CallBackClass cb;  
   // Called before ever using the callback function.  
   public static void SetChangeHandler() {  
      cb = new CallBackClass();  
      ExternalAPI.SetChangeHandler(new ChangeDelegate(cb.OnChange));  
   }  
   // Called after using the callback function for the last time.  
   public static void RemoveChangeHandler() {  
      // The cb object can be collected now. The unmanaged code is   
      // finished with the callback function.  
      cb = null;  
   }  
}  
```  
  
## Marshalling predefinito per i tipi di valore  
 La maggior parte dei tipi di valore, ad esempio numeri a virgola mobile e interi, è [copiabile da BLT](../../../docs/framework/interop/blittable-and-non-blittable-types.md) e non richiede il marshalling.  Altri tipi [non copiabili da BLT](../../../docs/framework/interop/blittable-and-non-blittable-types.md) hanno rappresentazioni diverse nella memoria gestita e non gestita e richiedono il marshalling.  Altri tipi ancora richiedono la formattazione esplicita oltre i limiti di interoperabilità.  
  
 Questo argomento fornisce le informazioni seguenti sui tipi di valore formattati:  
  
-   [Tipi di valore usati in platform invoke](#cpcondefaultmarshalingforvaluetypesanchor2)  
  
-   [Tipi di valore usati nell'interoperabilità COM](#cpcondefaultmarshalingforvaluetypesanchor3)  
  
 Oltre a descrivere i tipi formattati, questo argomento identifica i [tipi di valore di sistema](#cpcondefaultmarshalingforvaluetypesanchor1) che presentano un comportamento di marshalling insolito.  
  
 Un tipo formattato è un tipo complesso che contiene informazioni che controllano in modo esplicito il layout dei relativi membri in memoria.  Le informazioni sul layout dei membri vengono fornite tramite l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute>.  Il layout può essere uno dei seguenti valori di enumerazione <xref:System.Runtime.InteropServices.LayoutKind>:  
  
-   **LayoutKind.Automatic**  
  
     Indica che Common Language Runtime può riordinare i membri del tipo per migliorare l'efficienza.  Tuttavia, quando un tipo di valore viene passato al codice non gestito, il layout dei membri è prevedibile.  Un tentativo di effettuare automaticamente il marshalling di tale struttura provoca un'eccezione.  
  
-   **LayoutKind.Sequential**  
  
     Indica che i membri del tipo devono essere disposti nella memoria non gestita nello stesso ordine in cui appaiono nella definizione del tipo gestito.  
  
-   **LayoutKind.Explicit**  
  
     Indica che i membri vengono disposti in base all'oggetto <xref:System.Runtime.InteropServices.FieldOffsetAttribute> fornito con ogni campo.  
  
<a name="cpcondefaultmarshalingforvaluetypesanchor2"></a>   
### Tipi di valore usati in platform invoke  
 Nell'esempio seguente i tipi `Point` e `Rect` forniscono informazioni sul layout dei membri tramite **StructLayoutAttribute**.  
  
```vb  
Imports System.Runtime.InteropServices  
<StructLayout(LayoutKind.Sequential)> Public Structure Point  
   Public x As Integer  
   Public y As Integer  
End Structure  
<StructLayout(LayoutKind.Explicit)> Public Structure Rect  
   <FieldOffset(0)> Public left As Integer  
   <FieldOffset(4)> Public top As Integer  
   <FieldOffset(8)> Public right As Integer  
   <FieldOffset(12)> Public bottom As Integer  
End Structure  
  
```  
  
```csharp  
using System.Runtime.InteropServices;  
[StructLayout(LayoutKind.Sequential)]  
public struct Point {  
   public int x;  
   public int y;  
}     
  
[StructLayout(LayoutKind.Explicit)]  
public struct Rect {  
   [FieldOffset(0)] public int left;  
   [FieldOffset(4)] public int top;  
   [FieldOffset(8)] public int right;  
   [FieldOffset(12)] public int bottom;  
}  
```  
  
 Quando si effettua il marshalling nel codice non gestito, questi tipi formattati vengono sottoposti a marshalling come strutture di tipo C.  Ciò consente di chiamare in modo semplice un'API non gestita con argomenti di struttura.  Ad esempio, le strutture `POINT` e `RECT` possono essere passate alla funzione  **PtInRect** dell'API Win32 Microsoft come indicato di seguito:  
  
```  
BOOL PtInRect(const RECT *lprc, POINT pt);  
```  
  
 È possibile passare le strutture usando la definizione di platform invoke seguente:  
  
```vb  
Class Win32API      
   Declare Auto Function PtInRect Lib "User32.dll" _  
    (ByRef r As Rect, p As Point) As Boolean  
End Class  
  
```  
  
```csharp  
class Win32API {  
   [DllImport("User32.dll")]  
   public static extern Bool PtInRect(ref Rect r, Point p);  
}  
```  
  
 Il tipo di valore `Rect` deve essere passato mediante riferimento in quanto l'API non gestita richiede che alla funzione venga passato un puntatore a un oggetto `RECT`.  Il tipo di valore `Point` viene passato mediante valore in quanto l'API non gestita richiede che nello stack venga passato un oggetto `POINT`.  Questa sottile differenza è molto importante.  I riferimenti vengono passati al codice non gestito come puntatori.  I valori vengono passati al codice non gestito nello stack.  
  
> [!NOTE]
>  Quando viene effettuato il marshalling di un tipo formattato come struttura, solo i campi all'interno del tipo sono accessibili.  Se il tipo dispone di metodi, proprietà o eventi, non è possibile accedervi dal codice non gestito.  
  
 È anche possibile effettuare il marshalling delle classi nel codice non gestito come strutture di tipo C, a condizione che il layout dei membri sia fisso.  Le informazioni sul layout dei membri per una classe vengono fornite anche tramite l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute>.  La differenza principale tra i tipi di valore con layout fisso e le classi con layout fisso riguarda il modo in cui viene effettuato il marshalling nel codice non gestito.  I tipi di valore vengono passati mediante valore \(nello stack\) e, di conseguenza, le eventuali modifiche apportate ai membri del tipo dall'oggetto chiamato non sono visibili al chiamante.  I tipi di riferimento vengono passati mediante riferimento \(un riferimento al tipo viene passato nello stack\) e, di conseguenza, tutte le modifiche apportate ai membri di un tipo copiabile da BLT dall'oggetto chiamato sono visibili al chiamante.  
  
> [!NOTE]
>  Se un tipo di riferimento dispone di membri di tipi non copiabili da BLT, è necessario eseguire la conversione due volte: la prima volta quando un argomento viene passato al lato non gestito e la seconda volta quando viene restituito dalla chiamata.  A causa di questo sovraccarico aggiuntivo, è necessario applicare in modo esplicito i parametri in\/out a un argomento se il chiamante desidera visualizzare le modifiche apportate dall'oggetto chiamato.  
  
 Nell'esempio seguente, la classe `SystemTime` ha un layout dei membri sequenziale e può essere passata alla funzione **GetSystemTime** dell'API Win32.  
  
```vb  
<StructLayout(LayoutKind.Sequential)> Public Class SystemTime  
   Public wYear As System.UInt16  
   Public wMonth As System.UInt16  
   Public wDayOfWeek As System.UInt16  
   Public wDay As System.UInt16  
   Public wHour As System.UInt16  
   Public wMinute As System.UInt16  
   Public wSecond As System.UInt16  
   Public wMilliseconds As System.UInt16  
End Class  
  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
   public class SystemTime {  
   public ushort wYear;   
   public ushort wMonth;  
   public ushort wDayOfWeek;   
   public ushort wDay;   
   public ushort wHour;   
   public ushort wMinute;   
   public ushort wSecond;   
   public ushort wMilliseconds;   
}  
```  
  
 La funzione **GetSystemTime** è definita come indicato di seguito:  
  
```  
void GetSystemTime(SYSTEMTIME* SystemTime);  
```  
  
 La definizione di platform invoke equivalente per **GetSystemTime** è la seguente:  
  
```vb  
Public Class Win32  
   Declare Auto Sub GetSystemTime Lib "Kernel32.dll" (ByVal sysTime _  
   As SystemTime)  
End Class  
  
```  
  
```csharp  
class Win32API {  
   [DllImport("Kernel32.dll", CharSet=CharSet.Auto)]  
   public static extern void GetSystemTime(SystemTime st);  
}  
```  
  
 Si noti che l'argomento `SystemTime` non è tipizzato come argomento di riferimento poiché `SystemTime` è una classe e non un tipo di valore.  A differenza dei tipi di valore, le classi vengono sempre passate mediante riferimento.  
  
 L'esempio di codice seguente mostra una classe `Point` diversa con un metodo denominato `SetXY`.  Poiché il tipo ha un layout sequenziale, può essere passato al codice non gestito e sottoposto a marshalling come una struttura.  Tuttavia, il membro `SetXY` non può essere chiamato dal codice non gestito, anche se l'oggetto viene passato mediante riferimento.  
  
```vb  
<StructLayout(LayoutKind.Sequential)> Public Class Point  
   Private x, y As Integer  
   Public Sub SetXY(x As Integer, y As Integer)  
      Me.x = x  
      Me.y = y  
   End Sub  
End Class  
  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public class Point {  
   int x, y;  
   public void SetXY(int x, int y){   
      this.x = x;  
      this.y = y;  
   }  
}  
```  
  
<a name="cpcondefaultmarshalingforvaluetypesanchor3"></a>   
### Tipi di valore usati nell'interoperabilità COM  
 I tipi formattati possono anche essere passati alle chiamate ai metodi di interoperabilità COM.  Quando vengono esportati in una libreria dei tipi, infatti, i tipi di valore vengono convertiti automaticamente in strutture.  Come illustrato nell'esempio seguente, il tipo di valore `Point` diventa una definizione di tipo \(typedef\) con il nome `Point`.  Tutti i riferimenti al tipo di valore `Point` in altre posizioni nella libreria dei tipi vengono sostituiti con la definizione di tipo `Point`.  
  
 **Rappresentazione di libreria dei tipi**  
  
```  
typedef struct tagPoint {  
   int x;  
   int y;  
} Point;  
interface _Graphics {  
   …  
   HRESULT SetPoint ([in] Point p)  
   HRESULT SetPointRef ([in,out] Point *p)  
   HRESULT GetPoint ([out,retval] Point *p)  
}  
```  
  
 Le stesse regole usate per il marshalling di valori e riferimenti nelle chiamate di platform invoke vengono usate per il marshalling tramite le interfacce COM.  Ad esempio, quando un'istanza del tipo di valore `Point` viene passata da .NET Framework a COM, `Point` viene passato mediante valore.  Se il tipo di valore `Point` viene passato mediante riferimento, viene passato un puntatore a un oggetto `Point` nello stack.  Il gestore marshalling di interoperabilità non supporta livelli superiori di riferimento indiretto \(**Point \*\***\) in entrambe le direzioni.  
  
> [!NOTE]
>  Le strutture con valore di enumerazione <xref:System.Runtime.InteropServices.LayoutKind> impostato su **Explicit** non possono essere usate nell'interoperabilità COM perché la libreria dei tipi esportata non può esprimere un layout esplicito.  
  
<a name="cpcondefaultmarshalingforvaluetypesanchor1"></a>   
### Tipi di valore di sistema  
 Lo spazio dei nomi <xref:System> include diversi tipi di valore che rappresentano il formato sottoposto a conversione boxing dei tipi primitivi di runtime.  Ad esempio, la struttura <xref:System.Int32?displayProperty=fullName> del tipo di valore rappresenta il formato sottoposto a conversione boxing di **ELEMENT\_TYPE\_I4**.  Anziché effettuare il marshalling di questi tipi come strutture, come nel caso di altri tipi formattati, si effettua il marshalling nello stesso modo dei tipi primitivi di cui viene eseguita la conversione boxing.  Per **System.Int32** viene quindi effettuato il marshalling come **ELEMENT\_TYPE\_I4** anziché come una struttura contenente un singolo membro di tipo **long**.  La tabella seguente contiene un elenco dei tipi di valore nello spazio dei nomi **System** che costituiscono rappresentazioni sottoposte a conversione boxing di tipi primitivi.  
  
|Tipo di valore di sistema|Tipo di elemento|  
|-------------------------------|----------------------|  
|<xref:System.Boolean?displayProperty=fullName>|**ELEMENT\_TYPE\_BOOLEAN**|  
|<xref:System.SByte?displayProperty=fullName>|**ELEMENT\_TYPE\_I1**|  
|<xref:System.Byte?displayProperty=fullName>|**ELEMENT\_TYPE\_UI1**|  
|<xref:System.Char?displayProperty=fullName>|**ELEMENT\_TYPE\_CHAR**|  
|<xref:System.Int16?displayProperty=fullName>|**ELEMENT\_TYPE\_I2**|  
|<xref:System.UInt16?displayProperty=fullName>|**ELEMENT\_TYPE\_U2**|  
|<xref:System.Int32?displayProperty=fullName>|**ELEMENT\_TYPE\_I4**|  
|<xref:System.UInt32?displayProperty=fullName>|**ELEMENT\_TYPE\_U4**|  
|<xref:System.Int64?displayProperty=fullName>|**ELEMENT\_TYPE\_I8**|  
|<xref:System.UInt64?displayProperty=fullName>|**ELEMENT\_TYPE\_U8**|  
|<xref:System.Single?displayProperty=fullName>|**ELEMENT\_TYPE\_R4**|  
|<xref:System.Double?displayProperty=fullName>|**ELEMENT\_TYPE\_R8**|  
|<xref:System.String?displayProperty=fullName>|**ELEMENT\_TYPE\_STRING**|  
|<xref:System.IntPtr?displayProperty=fullName>|**ELEMENT\_TYPE\_I**|  
|<xref:System.UIntPtr?displayProperty=fullName>|**ELEMENT\_TYPE\_U**|  
  
 Alcuni altri tipi di valore nello spazio dei nomi **System** vengono gestiti diversamente.  Poiché il codice non gestito dispone già di formati ben definiti per questi tipi, il gestore di marshalling ha regole speciali per il loro marshalling.  La tabella seguente elenca i tipi di valore speciali nello spazio dei nomi **System**, nonché il tipo non gestito a cui viene effettuato il marshalling.  
  
|Tipo di valore di sistema|Tipo IDL|  
|-------------------------------|--------------|  
|<xref:System.DateTime?displayProperty=fullName>|**DATE**|  
|<xref:System.Decimal?displayProperty=fullName>|**DECIMAL**|  
|<xref:System.Guid?displayProperty=fullName>|**GUID**|  
|<xref:System.Drawing.Color?displayProperty=fullName>|**OLE\_COLOR**|  
  
 Il codice seguente mostra la definizione dei tipi non gestiti **DATE**, **GUID**, **DECIMAL** e **OLE\_COLOR** nella libreria dei tipi Stdole2.  
  
#### Rappresentazione di libreria dei tipi  
  
```  
typedef double DATE;  
typedef DWORD OLE_COLOR;  
  
typedef struct tagDEC {  
    USHORT    wReserved;  
    BYTE      scale;  
    BYTE      sign;  
    ULONG     Hi32;  
    ULONGLONG Lo64;  
} DECIMAL;  
  
typedef struct tagGUID {  
    DWORD Data1;  
    WORD  Data2;  
    WORD  Data3;  
    BYTE  Data4[ 8 ];  
} GUID;  
```  
  
 Il codice seguente mostra le definizioni corrispondenti nell'interfaccia `IValueTypes` gestita.  
  
```vb  
Public Interface IValueTypes  
   Sub M1(d As System.DateTime)  
   Sub M2(d As System.Guid)  
   Sub M3(d As System.Decimal)  
   Sub M4(d As System.Drawing.Color)  
End Interface  
  
```  
  
```csharp  
public interface IValueTypes {  
   void M1(System.DateTime d);  
   void M2(System.Guid d);  
   void M3(System.Decimal d);  
   void M4(System.Drawing.Color d);  
}  
```  
  
#### Rappresentazione di libreria dei tipi  
  
```  
[…]  
interface IValueTypes : IDispatch {  
   HRESULT M1([in] DATE d);  
   HRESULT M2([in] GUID d);  
   HRESULT M3([in] DECIMAL d);  
   HRESULT M4([in] OLE_COLOR d);  
};  
```  
  
## Vedere anche  
 [Blittable and Non\-Blittable Types](../../../docs/framework/interop/blittable-and-non-blittable-types.md)   
 [Copying and Pinning](../../../docs/framework/interop/copying-and-pinning.md)   
 [Default Marshaling for Arrays](../../../docs/framework/interop/default-marshaling-for-arrays.md)   
 [Default Marshaling for Objects](../../../docs/framework/interop/default-marshaling-for-objects.md)   
 [Default Marshaling for Strings](../../../docs/framework/interop/default-marshaling-for-strings.md)