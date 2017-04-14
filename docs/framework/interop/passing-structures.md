---
title: "Passing Structures | Microsoft Docs"
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
  - "platform invoke, calling unmanaged functions"
ms.assetid: 9b92ac73-32b7-4e1b-862e-6d8d950cf169
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Passing Structures
Numerose funzioni non gestite prevedono il passaggio, come parametro per la funzione, di membri di strutture \(corrispondenti in Visual Basic a tipi definiti dall'utente\) o membri di classi definite nel codice gestito.  Quando si passano strutture o classi al codice non gestito mediante platform invoke, è necessario fornire informazioni aggiuntive per mantenere il layout e l'allineamento originali.  In questo argomento viene descritto l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute>, utilizzato per definire i tipi formattati.  Per le classi e le strutture gestite, è possibile effettuare una selezione tra numerosi comportamenti di layout prevedibili forniti dall'enumerazione **LayoutKind**.  
  
 In relazione ai concetti illustrati nel presente argomento si rivela essenziale un'importante differenza tra tipi classe e tipi struttura.  Le strutture costituiscono tipi valore, mentre le classi rappresentano tipi di riferimento e forniscono sempre almeno un livello di riferimenti indiretti alla memoria, ovvero un puntatore a un valore.  Questa differenza si rivela importante poiché le funzioni non gestite spesso richiedono riferimenti indiretti, come indicato dalle firme riportate nella prima colonna della tabella fornita di seguito.  Le dichiarazioni di classi e strutture gestite riportate nelle restanti colonne illustrano la misura in cui può essere modificato il livello di riferimenti indiretti nella dichiarazione.  Le dichiarazioni sono disponibili per Visual Basic e Visual C\#.  
  
|Firma non gestita|Dichiarazione gestita:                <br /> nessun riferimento indiretto               <br />  `Structure MyType`  <br />  `struct MyType;`|Dichiarazione gestita:                <br /> un livello di riferimenti indiretti               <br />  `Class MyType`  <br />  `class MyType;`|  
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|  
|`DoWork(MyType x);`<br /><br /> Non richiede alcun livello di riferimenti indiretti.|`DoWork(ByVal x As MyType)`  <br />  `DoWork(MyType x)`<br /><br /> Non aggiunge alcun livello di riferimenti indiretti.|Non supportata, poiché dispone già di un livello di riferimenti indiretti.|  
|`DoWork(MyType* x);`<br /><br /> Richiede un livello di riferimenti indiretti.|`DoWork(ByRef x As MyType)`  <br />  `DoWork(ref MyType x)`<br /><br /> Aggiunge un livello di riferimenti indiretti.|`DoWork(ByVal x As MyType)`  <br />  `DoWork(MyType x)`<br /><br /> Non aggiunge alcun livello di riferimenti indiretti.|  
|`DoWork(MyType** x);`<br /><br /> Richiede due livelli di riferimenti indiretti.|Non possibile in quanto non è possibile utilizzare **ByRef** **ByRef** o `ref` `ref`.|`DoWork(ByRef x As MyType)`  <br />  `DoWork(ref MyType x)`<br /><br /> Aggiunge un livello di riferimenti indiretti.|  
  
 Nella tabella vengono descritte le indicazioni relative alle dichiarazioni di platform invoke riportate di seguito.  
  
-   Utilizzare una struttura passata per valore quando la funzione non gestita non richiede alcun riferimento indiretto.  
  
-   Utilizzare una struttura passata per riferimento o una classe passata per valore quando la funzione non gestita richiede un livello di riferimenti indiretti.  
  
-   Utilizzare una classe passata per riferimento quando la funzione non gestita richiede due livelli di riferimenti indiretti.  
  
## Dichiarazione e passaggio di strutture  
 Nell'esempio riportato di seguito viene illustrato come definire le strutture `Point` e `Rect` nel codice gestito e passare i tipi come parametri alla funzione **PtInRect** del file User32.dll.  **PtInRect** dispone della seguente firma non gestita:  
  
```  
BOOL PtInRect(const RECT *lprc, POINT pt);  
```  
  
 Si noti che è necessario passare la struttura Rect per riferimento, perché la funzione accetta un puntatore a un tipo RECT.  
  
```vb  
Imports System.Runtime.InteropServices  
  
<StructLayout(LayoutKind.Sequential)> Public Structure Point  
    Public x As Integer  
    Public y As Integer  
End Structure  
  
Public Structure <StructLayout(LayoutKind.Explicit)> Rect  
    <FieldOffset(0)> Public left As Integer  
    <FieldOffset(4)> Public top As Integer  
    <FieldOffset(8)> Public right As Integer  
    <FieldOffset(12)> Public bottom As Integer  
End Structure  
  
Class Win32API      
    Declare Auto Function PtInRect Lib "user32.dll" _  
    (ByRef r As Rect, p As Point) As Boolean  
End Class  
  
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
  
class Win32API {  
    [DllImport("User32.dll")]  
    public static extern bool PtInRect(ref Rect r, Point p);  
}  
```  
  
## Dichiarazione e passaggio di classi  
 È possibile passare i membri di una classe a una funzione di DLL non gestita, purché la classe abbia un layout dei membri fisso.  Nell'esempio che segue viene illustrato come passare i membri della classe `MySystemTime`, che sono definiti in ordine sequenziale, a **GetSystemTime**, contenuta nel file User32.dll.  **GetSystemTime** ha la seguente firma non gestita:  
  
```  
void GetSystemTime(SYSTEMTIME* SystemTime);  
```  
  
 A differenza dei tipi valore, le classi dispongono sempre di almeno un livello di riferimenti indiretti.  
  
```vb  
Imports System  
Imports System.Runtime.InteropServices  
Imports Microsoft.VisualBasic  
  
<StructLayout(LayoutKind.Sequential)> Public Class MySystemTime  
    Public wYear As Short  
    Public wMonth As Short  
    Public wDayOfWeek As Short   
    Public wDay As Short  
    Public wHour As Short  
    Public wMinute As Short  
    Public wSecond As Short  
    Public wMiliseconds As Short  
End Class  
  
Public Class Win32  
    Declare Auto Sub GetSystemTime Lib "Kernel32.dll"(sysTime _  
        As MySystemTime)  
    Declare Auto Function MessageBox Lib "User32.dll"(hWnd As IntPtr, _  
        txt As String, caption As String, Typ As Integer) As Integer  
End Class  
  
Public Class TestPlatformInvoke      
    Public Shared Sub Main()  
        Dim sysTime As New MySystemTime()  
        Win32.GetSystemTime(sysTime)  
  
        Dim dt As String  
        dt = "System time is:" & ControlChars.CrLf & _  
              "Year: " & sysTime.wYear & _  
              ControlChars.CrLf & "Month: " & sysTime.wMonth & _  
              ControlChars.CrLf & "DayOfWeek: " & sysTime.wDayOfWeek & _  
              ControlChars.CrLf & "Day: " & sysTime.wDay  
        Win32.MessageBox(IntPtr.Zero, dt, "Platform Invoke Sample", 0)        
    End Sub  
End Class  
  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public class MySystemTime {  
    public ushort wYear;   
    public ushort wMonth;  
    public ushort wDayOfWeek;   
    public ushort wDay;   
    public ushort wHour;   
    public ushort wMinute;   
    public ushort wSecond;   
    public ushort wMilliseconds;   
}  
class Win32API {  
    [DllImport("Kernel32.dll")]  
    public static extern void GetSystemTime(MySystemTime st);  
  
    [DllImport("user32.dll", CharSet=CharSet.Auto)]  
     public static extern int MessageBox(IntPtr hWnd,  
         string text, string caption, int options);  
}  
  
public class TestPlatformInvoke  
{  
    public static void Main()  
    {  
        MySystemTime sysTime = new MySystemTime();  
        Win32API.GetSystemTime(sysTime);  
  
        string dt;  
        dt = "System time is: \n" +  
              "Year: " + sysTime.wYear + "\n" +  
              "Month: " + sysTime.wMonth + "\n" +  
              "DayOfWeek: " + sysTime.wDayOfWeek + "\n" +  
              "Day: " + sysTime.wDay;  
        Win32API.MessageBox(IntPtr.Zero, dt, "Platform Invoke Sample", 0);  
    }  
}  
```  
  
## Vedere anche  
 [Calling a DLL Function](../../../docs/framework/interop/calling-a-dll-function.md)   
 [Classe StructLayoutAttribute](frlrfSystemRuntimeInteropServicesStructLayoutAttributeClassTopic)   
 [Classe StructLayoutAttribute](frlrfSystemRuntimeInteropServicesStructLayoutAttributeClassTopic)   
 [Classe FieldOffsetAttribute](frlrfSystemRuntimeInteropServicesFieldOffsetAttributeClassTopic)