---
title: "How to: Implement Callback Functions | Microsoft Docs"
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
  - "callback function, implementing"
ms.assetid: e55b3712-b9ea-4453-bd9a-ad5cfa2f6bfa
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Implement Callback Functions
La procedura e l'esempio seguenti illustrano come un'applicazione gestita, usando il platform invoke, può stampare il valore di handle per ogni finestra sul computer locale.  In particolare, la procedura e l'esempio usano la funzione **EnumWindows** per esaminare l'elenco di finestre e una funzione di callback gestita \(denominata CallBack\) per visualizzare il valore di handle della finestra.  
  
### Per implementare una funzione di callback  
  
1.  Esaminare la firma per la funzione **EnumWindows** prima di procedere con l'implementazione.  **EnumWindows** presenta in genere la firma seguente:  
  
    ```  
    BOOL EnumWindows(WNDENUMPROC lpEnumFunc, LPARAM lParam)  
    ```  
  
     Un’indicazione per cui questa funzione richiede un callback è la presenza dell’argomento **lpEnumFunc**.  È frequente vedere il prefisso **lp** \(puntatore di tipo long\) combinato con il suffisso **Func** nel nome di argomenti che accettano un puntatore a una funzione di callback.  Per informazioni sulle funzioni Win32, vedere Microsoft Platform SDK.  
  
2.  Creare la funzione di callback gestita.  Nell'esempio è dichiarato un tipo delegato, denominato `CallBack`, che accetta due argomenti \(**hwnd** e **lparam**\).  Il primo argomento è un handle alla finestra, mentre il secondo è definito dall'applicazione.  In questa versione entrambi gli argomenti devono essere numeri interi.  
  
     Funzioni di callback restituiscono in genere valori diversi da zero per indicare l’esito positivo e zero per indicare l’esito negativo.  Questo esempio imposta in modo esplicito il valore restituito **true** per continuare l'enumerazione.  
  
3.  Creare un delegato e passarlo come argomento per la funzione **EnumWindows**.  Platform invoke converte automaticamente il delegato in un formato di callback conosciuto.  
  
4.  Assicurarsi che il garbage collector non recuperi il delegato prima che venga completata la funzione di callback.  Quando si passa un delegato come parametro o si passa un delegato contenuto come campo in una struttura, questo non viene interessato per la durata della chiamata.  Quindi, come nel seguente esempio di enumerazione, la funzione di callback viene completata prima che venga restituita la chiamata e non richiede operazioni aggiuntive dal chiamante gestito.  
  
     Se, tuttavia, la funzione di callback può essere richiamata dopo che viene restituita la chiamata, il chiamante gestito deve provvedere a garantire che il delegato non venga interessato fino al completamento della funzione di richiamata.  Per informazioni dettagliate su come evitare operazioni di garbage collection, vedere [Marshalling di interoperabilità](../../../docs/framework/interop/interop-marshaling.md) con Platform Invoke.  
  
## Esempio  
  
```vb  
Imports System  
Imports System.Runtime.InteropServices  
  
Public Delegate Function CallBack( _  
hwnd As Integer, lParam As Integer) As Boolean  
  
Public Class EnumReportApp  
  
    Declare Function EnumWindows Lib "user32" ( _  
       x As CallBack, y As Integer) As Integer  
  
    Public Shared Sub Main()  
        EnumWindows(AddressOf EnumReportApp.Report, 0)  
    End Sub 'Main  
  
    Public Shared Function Report(hwnd As Integer, lParam As Integer) _  
    As Boolean  
        Console.Write("Window handle is ")  
        Console.WriteLine(hwnd)  
        Return True  
    End Function 'Report  
End Class 'EnumReportApp  
  
```  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
public delegate bool CallBack(int hwnd, int lParam);  
  
public class EnumReportApp  
{  
    [DllImport("user32")]  
    public static extern int EnumWindows(CallBack x, int y);   
  
    public static void Main()   
    {  
        CallBack myCallBack = new CallBack(EnumReportApp.Report);  
        EnumWindows(myCallBack, 0);  
    }  
  
    public static bool Report(int hwnd, int lParam)  
    {   
        Console.Write("Window handle is ");  
        Console.WriteLine(hwnd);  
        return true;  
    }  
}  
  
```  
  
```cpp  
using namespace System;  
using namespace System::Runtime::InteropServices;  
  
// A delegate type.  
delegate bool CallBack(int hwnd, int lParam);  
  
// Managed type with the method to call.  
ref class EnumReport  
{  
// Report the window handle.  
public:  
    [DllImport("user32")]  
    static int EnumWindows(CallBack^ x, int y);  
  
    static void Main()  
    {  
        EnumReport^ er = gcnew EnumReport;  
        CallBack^ myCallBack = gcnew CallBack(&EnumReport::Report);  
        EnumWindows(myCallBack, 0);  
    }  
  
    static bool Report(int hwnd, int lParam)  
    {  
       Console::Write(L"Window handle is ");  
       Console::WriteLine(hwnd);  
       return true;  
    }  
};  
  
int main()  
{  
    EnumReport::Main();  
}  
```  
  
## Vedere anche  
 [Callback Functions](../../../docs/framework/interop/callback-functions.md)   
 [Calling a DLL Function](../../../docs/framework/interop/calling-a-dll-function.md)