---
title: "Default Marshaling for Strings | Microsoft Docs"
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
  - "strings, interop marshaling"
  - "interop marshaling, strings"
ms.assetid: 9baea3ce-27b3-4b4f-af98-9ad0f9467e6f
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Default Marshaling for Strings
Le classi <xref:System.String?displayProperty=fullName> e <xref:System.Text.StringBuilder?displayProperty=fullName> presentano un comportamento del marshalling simile.  
  
 Viene eseguito il marshalling delle stringhe come tipo `BSTR` di tipo COM oppure come stringa con terminazione Null \(matrice di caratteri che termina con un carattere Null\).  È possibile eseguire il marshalling dei caratteri all'interno della stringa come Unicode \(impostazione predefinita nei sistemi Windows\) o ANSI.  
  
 Questo argomento fornisce le informazioni seguenti sul marshalling dei tipi di stringa:  
  
-   [Stringhe usate nelle interfacce](#cpcondefaultmarshalingforstringsanchor1)  
  
-   [Stringhe usate in Platform invoke](#cpcondefaultmarshalingforstringsanchor5)  
  
-   [Stringhe usate nelle strutture](#cpcondefaultmarshalingforstringsanchor2)  
  
-   [Buffer di stringhe di lunghezza fissa](#cpcondefaultmarshalingforstringsanchor3)  
  
<a name="cpcondefaultmarshalingforstringsanchor1"></a>   
## Stringhe usate nelle interfacce  
 La tabella seguente illustra le opzioni di marshalling per il tipo di dati stringa quando il marshalling viene eseguito come argomento di metodo in codice non gestito.  L'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> fornisce alcuni valori di enumerazione <xref:System.Runtime.InteropServices.UnmanagedType> per il marshalling di stringhe in interfacce COM.  
  
|Tipo di enumerazione|Descrizione del formato non gestito|  
|--------------------------|-----------------------------------------|  
|`UnmanagedType.BStr` \(impostazione predefinita\)|`BSTR` di tipo COM con lunghezza fissa e caratteri Unicode.|  
|`UnmanagedType.LPStr`|Puntatore a matrice di caratteri ANSI con terminazione Null.|  
|`UnmanagedType.LPWStr`|Puntatore a una matrice con terminazione Null di caratteri Unicode.|  
  
 Questa tabella è applicabile alle stringhe.  Per <xref:System.Text.StringBuilder>, tuttavia, le uniche opzioni consentite sono `UnmanagedType.LPStr` e `UnmanagedType.LPWStr`.  
  
 L'esempio seguente mostra stringhe dichiarate nell'interfaccia `IStringWorker`.  
  
```cpp  
public interface IStringWorker {  
void PassString1(String s);  
void PassString2([MarshalAs(UnmanagedType.BStr)]String s);  
void PassString3([MarshalAs(UnmanagedType.LPStr)]String s);  
void PassString4([MarshalAs(UnmanagedType.LPWStr)]String s);  
void PassStringRef1(ref String s);  
void PassStringRef2([MarshalAs(UnmanagedType.BStr)]ref String s);  
void PassStringRef3([MarshalAs(UnmanagedType.LPStr)]ref String s);  
void PassStringRef4([MarshalAs(UnmanagedType.LPWStr)]ref String s);  
);  
```  
  
 L'esempio seguente mostra l'interfaccia corrispondente descritta in una libreria dei tipi.  
  
```  
[…]  
interface IStringWorker : IDispatch {  
HRESULT PassString1([in] BSTR s);  
HRESULT PassString2([in] BSTR s);  
HRESULT PassString3([in] LPStr s);  
HRESULT PassString4([in] LPWStr s);  
HRESULT PassStringRef1([in, out] BSTR *s);  
HRESULT PassStringRef2([in, out] BSTR *s);  
HRESULT PassStringRef3([in, out] LPStr *s);  
HRESULT PassStringRef4([in, out] LPWStr *s);  
);  
```  
  
<a name="cpcondefaultmarshalingforstringsanchor5"></a>   
## Stringhe usate in Platform invoke  
 Platform invoke copia argomenti di stringa, effettuando la conversione dal formato .NET Framework \(Unicode\) al formato della piattaforma non gestita.  Le stringhe non sono modificabili e non vengono copiate di nuovo dalla memoria non gestita alla memoria gestita quando la chiamata restituisce un risultato.  
  
 La tabella seguente elenca le opzioni di marshalling per le stringhe quando il marshalling viene eseguito come argomento di metodo di una chiamata Platform invoke.  L'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> fornisce alcuni valori di enumerazione <xref:System.Runtime.InteropServices.UnmanagedType> per il marshalling di stringhe.  
  
|Tipo di enumerazione|Descrizione del formato non gestito|  
|--------------------------|-----------------------------------------|  
|`UnmanagedType.AnsiBStr`|`BSTR` di tipo COM con lunghezza fissa e caratteri ANSI.|  
|`UnmanagedType.BStr`|`BSTR` di tipo COM con lunghezza fissa e caratteri Unicode.|  
|`UnmanagedType.LPStr`|Puntatore a matrice di caratteri ANSI con terminazione Null.|  
|`UnmanagedType.LPTStr` \(impostazione predefinita\)|Puntatore a una matrice con terminazione Null di caratteri dipendenti dalla piattaforma.|  
|`UnmanagedType.LPWStr`|Puntatore a una matrice con terminazione Null di caratteri Unicode.|  
|`UnmanagedType.TBStr`|`BSTR` di tipo COM con lunghezza fissa e caratteri dipendenti dalla piattaforma.|  
|`VBByRefStr`|Valore che consente a Visual Basic .NET di modificare una stringa in codice non gestito e riflettere i risultati in codice gestito.  Questo valore è supportato solo per platform invoke.|  
  
 Questa tabella è applicabile alle stringhe.  Per <xref:System.Text.StringBuilder>, tuttavia, le uniche opzioni consentite sono `LPStr`, `LPTStr` e `LPWStr`.  
  
 La definizione del tipo seguente mostra l'uso corretto di `MarshalAsAttribute` per chiamate Platform invoke.  
  
```vb  
Class StringLibAPI      
Public Declare Auto Sub PassLPStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.LPStr)> s As String)      
Public Declare Auto Sub PassLPWStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.LPWStr)> s As String)      
Public Declare Auto Sub PassLPTStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.LPTStr)> s As String)      
Public Declare Auto Sub PassBStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.BStr)> s As String)      
Public Declare Auto Sub PassAnsiBStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.AnsiBStr)> s As String)      
Public Declare Auto Sub PassTBStr Lib "StringLib.Dll" _  
(<MarshalAs(UnmanagedType.TBStr)> s As String)  
End Class  
  
```  
  
```csharp  
class StringLibAPI {  
[DllImport("StringLib.Dll")]  
public static extern void PassLPStr([MarshalAs(UnmanagedType.LPStr)]  
String s);  
[DllImport("StringLib.Dll")]  
public static extern void   
PassLPWStr([MarshalAs(UnmanagedType.LPWStr)]String s);  
[DllImport("StringLib.Dll")]  
public static extern void   
PassLPTStr([MarshalAs(UnmanagedType.LPTStr)]String s);  
[DllImport("StringLib.Dll")]  
public static extern void PassBStr([MarshalAs(UnmanagedType.BStr)]  
String s);  
[DllImport("StringLib.Dll")]  
public static extern void   
PassAnsiBStr([MarshalAs(UnmanagedType.AnsiBStr)]String s);  
[DllImport("StringLib.Dll")]  
public static extern void PassTBStr([MarshalAs(UnmanagedType.TBStr)]  
String s);  
}  
```  
  
<a name="cpcondefaultmarshalingforstringsanchor2"></a>   
## Stringhe usate nelle strutture  
 Le stringhe sono membri validi delle strutture, ma i buffer <xref:System.Text.StringBuilder> non sono validi nelle strutture.  La tabella seguente illustra le opzioni di marshalling per il tipo di dati stringa quando viene eseguito il marshalling del tipo come campo.  L'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> fornisce alcuni valori di enumerazione <xref:System.Runtime.InteropServices.UnmanagedType> per il marshalling di stringhe in un campo.  
  
|Tipo di enumerazione|Descrizione del formato non gestito|  
|--------------------------|-----------------------------------------|  
|`UnmanagedType.BStr`|`BSTR` di tipo COM con lunghezza fissa e caratteri Unicode.|  
|`UnmanagedType.LPStr`|Puntatore a matrice di caratteri ANSI con terminazione Null.|  
|`UnmanagedType.LPTStr`|Puntatore a una matrice con terminazione Null di caratteri dipendenti dalla piattaforma.|  
|`UnmanagedType.LPWStr`|Puntatore a una matrice con terminazione Null di caratteri Unicode.|  
|`UnmanagedType.ByValTStr`|Matrice di caratteri a lunghezza fissa. Il tipo della matrice viene determinato dal set di carattere della struttura che la contiene.|  
  
 Il tipo `ByValTStr` viene usato per matrici di caratteri inline e di lunghezza fissa, disponibili all'interno di una struttura.  Altri tipi sono applicabili a riferimenti di stringa contenuti in strutture che includono puntatori ad altre stringhe.  
  
 L'argomento `CharSet` dell'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute> applicato alla struttura contenitore determina il formato dei caratteri delle stringhe nelle strutture.  Le strutture di esempio seguenti contengono riferimenti a stringhe e stringhe inline, oltre a caratteri ANSI, Unicode e dipendenti dalla piattaforma.  
  
### Rappresentazione di libreria dei tipi  
  
```  
struct StringInfoA {  
   char *    f1;  
   char      f2[256];  
};  
struct StringInfoW {  
   WCHAR *   f1;  
   WCHAR     f2[256];  
   BSTR      f3;  
};  
struct StringInfoT {  
   TCHAR *   f1;  
   TCHAR     f2[256];  
};  
```  
  
 L'esempio di codice seguente illustra come usare l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> per definire la stessa struttura in formati diversi.  
  
```vb  
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Ansi)> _  
Structure StringInfoA  
<MarshalAs(UnmanagedType.LPStr)> Public f1 As String  
<MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _  
Public f2 As String  
End Structure  
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Unicode)> _  
Structure StringInfoW  
<MarshalAs(UnmanagedType.LPWStr)> Public f1 As String  
<MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _  
Public f2 As String  
<MarshalAs(UnmanagedType.BStr)> Public f3 As String  
End Structure  
<StructLayout(LayoutKind.Sequential, CharSet := CharSet.Auto)> _  
Structure StringInfoT  
<MarshalAs(UnmanagedType.LPTStr)> Public f1 As String  
<MarshalAs(UnmanagedType.ByValTStr, SizeConst := 256)> _  
Public f2 As String  
End Structure  
  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]  
struct StringInfoA {  
   [MarshalAs(UnmanagedType.LPStr)] public String f1;  
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256)] public String f2;  
}  
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]  
struct StringInfoW {  
   [MarshalAs(UnmanagedType.LPWStr)] public String f1;  
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256)] public String f2;  
   [MarshalAs(UnmanagedType.BStr)] public String f3;  
}  
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]  
struct StringInfoT {  
   [MarshalAs(UnmanagedType.LPTStr)] public String f1;  
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256)] public String f2;  
}  
```  
  
<a name="cpcondefaultmarshalingforstringsanchor3"></a>   
## Buffer di stringhe di lunghezza fissa  
 In alcuni casi, è necessario passare un buffer di caratteri a lunghezza fissa nel codice non gestito da modificare.  Il semplice passaggio di una stringa non funziona in questo caso perché il chiamato non può modificare il contenuto del buffer passato.  Anche se la stringa viene passata per riferimento, non è possibile inizializzare il buffer su una dimensione specifica.  
  
 La soluzione consiste nel passare come argomento un buffer <xref:System.Text.StringBuilder> invece di una stringa.   Il chiamato può dereferenziare e modificare un oggetto `StringBuilder`, purché non venga superata la capacità dell'oggetto `StringBuilder` stesso.  È anche possibile inizializzare questo oggetto in base a una lunghezza fissa.  Se, ad esempio, si inizializza un buffer `StringBuilder` per una capacità pari a `N`, un buffer di caratteri di dimensione \(`N`\+1\) viene fornito dal gestore di marshalling.  Il valore \+1 tiene conto del fatto che, a differenza di `StringBuilder`, la stringa non gestita ha una terminazione Null.  
  
 La funzione `GetWindowText` dell'API Microsoft Win32 \(definita in Windows.h\) rappresenta ad esempio un buffer di caratteri a lunghezza fissa che deve essere passato nel codice non gestito per essere modificato.  `LpString` punta a un buffer allocato dal chiamante di dimensione `nMaxCount`.   Il chiamante deve allocare il buffer e impostare l'argomento `nMaxCount` sulla dimensione del buffer allocato.  Il codice seguente illustra la dichiarazione della funzione `GetWindowText` come definita in Windows.h.  
  
```  
int GetWindowText(  
HWND hWnd,        // Handle to window or control.  
LPTStr lpString,  // Text buffer.  
int nMaxCount     // Maximum number of characters to copy.  
);  
```  
  
 Il chiamato può dereferenziare e modificare un oggetto `StringBuilder`, purché non venga superata la capacità dell'oggetto `StringBuilder` stesso.  L'esempio di codice seguente illustra come inizializzare `StringBuilder` in base a una lunghezza fissa.  
  
```vb  
Public Class Win32API  
Public Declare Auto Sub GetWindowText Lib "User32.Dll" _  
(h As Integer, s As StringBuilder, nMaxCount As Integer)  
End Class  
Public Class Window  
   Friend h As Integer ' Friend handle to Window.  
   Public Function GetText() As String  
      Dim sb As New StringBuilder(256)  
      Win32API.GetWindowText(h, sb, sb.Capacity + 1)  
   Return sb.ToString()  
   End Function  
End Class  
  
```  
  
```csharp  
public class Win32API {  
[DllImport("User32.Dll")]  
public static extern void GetWindowText(int h, StringBuilder s,   
int nMaxCount);  
}  
public class Window {  
   internal int h;        // Internal handle to Window.  
   public String GetText() {  
      StringBuilder sb = new StringBuilder(256);  
      Win32API.GetWindowText(h, sb, sb.Capacity + 1);  
   return sb.ToString();  
   }  
}  
```  
  
## Vedere anche  
 [Default Marshaling Behavior](../../../docs/framework/interop/default-marshaling-behavior.md)   
 [Blittable and Non\-Blittable Types](../../../docs/framework/interop/blittable-and-non-blittable-types.md)   
 [Directional Attributes](http://msdn.microsoft.com/it-it/241ac5b5-928e-4969-8f58-1dbc048f9ea2)   
 [Copying and Pinning](../../../docs/framework/interop/copying-and-pinning.md)