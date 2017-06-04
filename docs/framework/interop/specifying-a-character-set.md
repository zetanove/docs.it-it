---
title: "Specifying a Character Set | Microsoft Docs"
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
  - "platform invoke, attribute fields"
  - "attribute fields in platform invoke, CharSet"
  - "CharSet field"
ms.assetid: a8347eb1-295f-46b9-8a78-63331f9ecc50
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Specifying a Character Set
Il campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=fullName> consente di controllare il marshalling delle stringhe e di determinare la modalità con cui vengono trovati i nomi di funzione in una DLL mediante pInvoke.  In questo argomento vengono descritte entrambe le funzionalità.  
  
 Alcune API esportano due diverse versioni di ciascuna funzione che accetta argomenti stringa: una piccola \(ANSI\) e una grande \(Unicode\).  L'API Win32 include ad esempio la funzione **MessageBox** con i seguenti nomi di punto di ingresso:  
  
-   **MessageBoxA**  
  
     Fornisce la formattazione ANSI con caratteri a byte singolo, che si distingue per il suffisso "A" aggiunto al nome del punto di ingresso.  Con le chiamate a **MessageBoxA** viene sempre eseguito il marshalling delle stringhe in formato ANSI, come avviene di solito nelle piattaforme Windows 95 e Windows 98.  
  
-   **MessageBoxW**  
  
     Fornisce la formattazione Unicode con caratteri a byte doppio, che si distingue per il suffisso "W" aggiunto al nome del punto di ingresso.  Con le chiamate a **MessageBoxW** viene sempre eseguito il marshalling delle stringhe in formato Unicode, come avviene di solito nelle piattaforme Windows NT, Windows 2000 e Windows XP.  
  
## Marshalling delle stringhe e corrispondenza dei nomi  
 Il campo **CharSet** accetta i seguenti valori:  
  
 **CharSet.Ansi** \(valore predefinito\)  
  
-   Marshalling delle stringhe  
  
     Platform invoke effettua il marshalling delle stringhe dal formato gestito \(Unicode\) al formato ANSI.  
  
-   Corrispondenza dei nomi  
  
     Quando il campo <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling?displayProperty=fullName> è impostato su **true**, ovvero l'impostazione predefinita in [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], con pInvoke viene cercato soltanto il nome specificato.  Se ad esempio si specifica **MessageBox**, con platform invoke verrà cercato **MessageBox** e l'operazione avrà esito negativo in mancanza di un'esatta corrispondenza ortografica.  
  
     Quando il campo **ExactSpelling** è impostato su **false** \(impostazione predefinita in C\+\+ e C\#\), con platform invoke viene cercato innanzitutto l'alias non modificato \(**MessageBox**\) e successivamente, in caso di esito negativo, viene cercato il nome modificato \(**MessageBoxA**\).  Si noti che il criterio adottato per la corrispondenza dei nomi ANSI differisce da quello adottato per la corrispondenza dei nomi Unicode.  
  
 **CharSet.Unicode**  
  
-   Marshalling delle stringhe  
  
     Platform invoke copia le stringhe dal relativo formato gestito \(Unicode\) al formato Unicode.  
  
-   Corrispondenza dei nomi  
  
     Quando il campo **ExactSpelling** è impostato su **true**, ovvero l'impostazione predefinita in [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], con platform invoke viene cercato soltanto il nome specificato.  Se ad esempio si specifica **MessageBox**, con platform invoke verrà cercato **MessageBox** e l'operazione avrà esito negativo in mancanza di un'esatta corrispondenza ortografica.  
  
     Quando il campo **ExactSpelling** è impostato su **false** \(impostazione predefinita in C\+\+ e C\#\), con platform invoke viene cercato innanzitutto il nome modificato \(**MessageBoxW**\) e successivamente, in caso di esito negativo, viene cercato l'alias non modificato \(**MessageBox**\).  Si noti che il criterio adottato per la corrispondenza dei nomi Unicode differisce da quello adottato per la corrispondenza dei nomi ANSI.  
  
 **CharSet.Auto**  
  
-   In platform invoke, la scelta tra i formati ANSI e Unicode viene effettuata in fase di esecuzione, in base al sistema operativo di destinazione.  
  
## Specifica di un set di caratteri in Visual Basic  
 Nell'esempio riportato di seguito la funzione **MessageBox** viene dichiarata tre volte, ogni volta con un set di caratteri diverso.  In Visual Basic è possibile specificare il comportamento dei set di caratteri aggiungendo la parola chiave **Ansi**, **Unicode** o **Auto** all'istruzione di dichiarazione.  
  
 Se si omette la parola chiave che specifica il set di caratteri, come avviene nella prima istruzione di dichiarazione, nel campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=fullName> verrà utilizzato per impostazione predefinita il set di caratteri ANSI.  La seconda e la terza istruzione dell'esempio specificano esplicitamente un set di caratteri utilizzando una parola chiave.  
  
```vb  
Imports System.Runtime.InteropServices  
  
Public Class Win32  
   Declare Function MessageBoxA Lib "user32.dll"(ByVal hWnd As Integer, _  
       ByVal txt As String, ByVal caption As String, _  
       ByVal Typ As Integer) As Integer  
  
   Declare Unicode Function MessageBoxW Lib "user32.dll" _  
       (ByVal hWnd As Integer, ByVal txt As String, _  
        ByVal caption As String, ByVal Typ As Integer) As Integer  
  
   Declare Auto Function MessageBox Lib "user32.dll" _  
       (ByVal hWnd As Integer, ByVal txt As String, _  
        ByVal caption As String, ByVal Typ As Integer) As Integer  
End Class  
```  
  
## Specifica di un set di caratteri in C\# e in C\+\+  
 Il campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=fullName> identifica il set di caratteri sottostante come ANSI o Unicode.  Il set di caratteri controlla il modo in cui deve essere effettuato il marshalling degli argomenti stringa passati a un metodo.  Per specificare il set di caratteri, utilizzare una delle seguenti forme:  
  
```csharp  
[DllImport("dllname", CharSet=CharSet.Ansi)]  
[DllImport("dllname", CharSet=CharSet.Unicode)]  
[DllImport("dllname", CharSet=CharSet.Auto)]  
  
```  
  
```cpp  
[DllImport("dllname", CharSet=CharSet::Ansi)]  
[DllImport("dllname", CharSet=CharSet::Unicode)]  
[DllImport("dllname", CharSet=CharSet::Auto)]  
```  
  
 Nell'esempio riportato di seguito vengono illustrate tre definizioni gestite della funzione **MessageBox** dotate di attributi che specificano un determinato set di caratteri.  Nella prima definizione, l'omissione del campo **CharSet** ne determina l'impostazione sul set di caratteri ANSI predefinito.  
  
```csharp  
[DllImport("user32.dll")]  
    public static extern int MessageBoxA(int hWnd, String text,   
        String caption, uint type);  
[DllImport("user32.dll", CharSet=CharSet.Unicode)]  
    public static extern int MessageBoxW(int hWnd, String text,   
        String caption, uint type);  
[DllImport("user32.dll", CharSet=CharSet.Auto)]  
    public static extern int MessageBox(int hWnd, String text,   
        String caption, uint type);  
  
```  
  
```cpp  
typedef void* HWND;  
  
//Can use MessageBox or MessageBoxA.  
[DllImport("user32")]  
extern "C" int MessageBox(HWND hWnd,  
                          String* pText,  
                          String* pCaption,  
                          unsigned int uType);  
  
//Can use MessageBox or MessageBoxW.  
[DllImport("user32", CharSet=CharSet::Unicode)]  
extern "C" int MessageBoxW(HWND hWnd,  
                          String* pText,  
                          String* pCaption,  
                          unsigned int uType);  
  
//Must use MessageBox.  
[DllImport("user32", CharSet=CharSet::Auto)]  
extern "C" int MessageBox(HWND hWnd,  
                          String* pText,  
                          String* pCaption,  
                          unsigned int uType);  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Creating Prototypes in Managed Code](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [Platform Invoke Examples](../../../docs/framework/interop/platform-invoke-examples.md)   
 [Marshaling Data with Platform Invoke](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)