---
title: "How to: Call a Windows Function that Takes Unsigned Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Windows functions, calling"
  - "unsigned data types"
  - "UShort data type, using"
  - "functions [Visual Basic], calling Windows functions"
  - "ULong data type, using"
  - "UInteger data type, using"
  - "data types [Visual Basic], using"
  - "unsigned types"
  - "data types [Visual Basic], unsigned"
  - "data types [Visual Basic], numeric"
  - "unsigned types, using"
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# How to: Call a Windows Function that Takes Unsigned Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Se si utilizza una classe, un modulo o una struttura con membri di tipo integer senza segno, è possibile accedere a questi ultimi con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
### Per chiamare una funzione Windows che accetta tipi senza segno  
  
1.  Utilizzare una [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md) per indicare a [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] la libreria che contiene la funzione in questione, il nome della funzione nella libreria specifica, la relativa sequenza di chiamata e la modalità di conversione delle stringhe in fase di chiamata della funzione.  
  
2.  Nell'istruzione `Declare` utilizzare come richiesto `UInteger`, `ULong`, `UShort` o `Byte` per ciascuno dei parametri con tipi senza segno.  
  
3.  Consultare la documentazione relativa alla funzione Windows chiamata per trovare i nomi e i valori delle costanti da essa utilizzati,  gran parte dei quali è definita nel file WinUser.h.  
  
4.  Dichiarare le costanti necessarie nel codice.  Molte costanti Windows sono valori a 32 bit senza segno e devono essere dichiarate `As` `UInteger`.  
  
5.  Chiamare la funzione normalmente.  Nell'esempio che segue viene chiamata la funzione Windows `MessageBox`, che accetta un argomento integer senza segno.  
  
    ```  
    Public Class windowsMessage  
        Private Declare Auto Function mb Lib "user32.dll" Alias "MessageBox" (  
            ByVal hWnd As Integer,   
            ByVal lpText As String,   
            ByVal lpCaption As String,   
            ByVal uType As UInteger) As Integer  
        Private Const MB_OK As UInteger = 0  
        Private Const MB_ICONEXCLAMATION As UInteger = &H30  
        Private Const IDOK As UInteger = 1  
        Private Const IDCLOSE As UInteger = 8  
        Private Const c As UInteger = MB_OK Or MB_ICONEXCLAMATION  
        Public Function messageThroughWindows() As String  
            Dim r As Integer = mb(0, "Click OK if you see this!",   
                "Windows API call", c)  
            Dim s As String = "Windows API MessageBox returned " &  
                 CStr(r)& vbCrLf & "(IDOK = " & CStr(IDOK) &  
                 ", IDCLOSE = " & CStr(IDCLOSE) & ")"  
            Return s  
        End Function  
    End Class  
    ```  
  
     È possibile verificare la funzione `messageThroughWindows` con il codice riportato di seguito.  
  
    ```  
    Public Sub consumeWindowsMessage()  
        Dim w As New windowsMessage  
        w.messageThroughWindows()  
    End Sub  
    ```  
  
    > [!CAUTION]
    >  I tipi di dati `UInteger`, `ULong`, `UShort` e `SByte` non fanno parte di CLS \([Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md)\). Pertanto, il codice compatibile con CLS non può utilizzare un componente che impiega questi tipi.  
  
    > [!IMPORTANT]
    >  Una chiamata a codice non gestito, quale un'API \(Application Programming Interface\) Windows, lo espone a potenziali rischi di sicurezza.  
  
    > [!IMPORTANT]
    >  Quando si chiama l'API Windows è necessaria l'autorizzazione di accesso al codice non gestito, che può influenzarne l'esecuzione in situazioni di attendibilità parziale.  Per ulteriori informazioni, vedere <xref:System.Security.Permissions.SecurityPermission> e [Code Access Permissions](http://msdn.microsoft.com/it-it/e5ae402f-6dda-4732-bbe8-77296630f675).  
  
## Vedere anche  
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Integer Data Type](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [UInteger Data Type](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)   
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Walkthrough: Calling Windows APIs](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)