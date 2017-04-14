---
title: "Specifying an Entry Point | Microsoft Docs"
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
  - "EntryPoint field"
  - "platform invoke, attribute fields"
  - "attribute fields in platform invoke, EntryPoint"
ms.assetid: d1247f08-0965-416a-b978-e0b50652dfe3
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Specifying an Entry Point
Un punto di ingresso identifica la posizione di una funzione in una DLL.  All'interno di un progetto gestito, il nome originale o il punto di ingresso ordinale di una funzione di destinazione identifica tale funzione oltre i limiti di interoperabilità.  È inoltre possibile associare il punto di ingresso a un nome diverso, rinominando così la funzione.  
  
 Di seguito è riportato un elenco delle ragioni che possono spingere a rinominare una funzione di DLL:  
  
-   Per evitare l'uso di nomi che si distinguono solo per differenze di lettere maiuscole e minuscole  
  
-   Per conformarsi a standard di denominazione esistenti  
  
-   Per adattare funzioni che accettano diversi tipi di dati \(dichiarando più versioni della stessa funzione di DLL\)  
  
-   Per semplificare l'utilizzo delle API che contengono versioni ANSI e Unicode  
  
 In questo argomento viene illustrato come si rinomina una funzione di DLL nel codice gestito.  
  
## Ridenominazione di una funzione in Visual Basic  
 In Visual Basic viene utilizzata la parola chiave **Function** nell'istruzione **Declare** per impostare il campo <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=fullName>.  Nell'esempio che segue viene illustrata una dichiarazione tipica.  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
    Declare Auto Function MessageBox Lib "user32.dll" _  
       (ByVal hWnd As Integer, ByVal txt As String,_  
       ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
 È possibile sostituire il punto di ingresso **MessageBox** con **MsgBox** includendo la parola chiave **Alias** nella definizione, come illustrato nell'esempio riportato di seguito.  In entrambi gli esempi l'utilizzo della parola chiave **Auto** consente di non specificare la versione del set di caratteri del punto di ingresso.  Per ulteriori informazioni sulla selezione di un set di caratteri, vedere [Specifica di un set di caratteri](../../../docs/framework/interop/specifying-a-character-set.md).  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
    Declare Auto Function MsgBox Lib "user32.dll" _  
       Alias "MessageBox" (ByVal hWnd As Integer, ByVal txt As String,_  
       ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
## Ridenominazione di una funzione in C\# e in C\+\+  
 È possibile utilizzare il campo <xref:System.Runtime.InteropServices.DllImportAttribute.EntryPoint?displayProperty=fullName> per specificare una funzione DLL in base al nome o all'ordinale.  Se il nome della funzione nella propria definizione del metodo è uguale al punto di ingresso nella DLL, non occorrerà identificare esplicitamente la funzione con il campo **EntryPoint**.  In caso contrario, utilizzare una delle seguenti forme dell'attributo per indicare un nome o un numero ordinale:  
  
```  
[DllImport("dllname", EntryPoint="Functionname")]  
[DllImport("dllname", EntryPoint="#123")]  
```  
  
 Si noti che il numero ordinale deve essere preceduto dal segno di cancelletto \(\#\).  
  
 Nell'esempio seguente viene illustrato come sostituire **MessageBoxA** con **MsgBox** a livello di codice utilizzando il campo **EntryPoint**.  
  
```csharp  
using System.Runtime.InteropServices;  
  
public class Win32 {  
    [DllImport("user32.dll", EntryPoint="MessageBoxA")]  
    public static extern int MsgBox(int hWnd, String text, String caption,  
                                    uint type);  
}  
  
```  
  
```cpp  
using namespace System::Runtime::InteropServices;  
  
typedef void* HWND;  
[DllImport("user32", EntryPoint="MessageBoxA")]  
extern "C" int MsgBox(HWND hWnd,  
                      String*  pText,  
                      String*  pCaption,  
                      unsigned int uType);  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Creating Prototypes in Managed Code](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [Platform Invoke Examples](../../../docs/framework/interop/platform-invoke-examples.md)   
 [Marshaling Data with Platform Invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)