---
title: 'Procedura: chiamare una funzione Windows che accetta tipi senza segno (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Windows functions, calling
- unsigned data types
- UShort data type, using
- functions [Visual Basic], calling Windows functions
- ULong data type, using
- UInteger data type, using
- data types [Visual Basic], using
- unsigned types
- data types [Visual Basic], unsigned
- data types [Visual Basic], numeric
- unsigned types, using
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
caps.latest.revision: 18
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fbff07f4923b0633a2bc9b4fd558d9d51f64370a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-windows-function-that-takes-unsigned-types-visual-basic"></a>Procedura: chiamare una funzione Windows che accetta tipi senza segno (Visual Basic)
Se si utilizza una classe, un modulo o una struttura che dispone di membri di tipi integer senza segno, è possibile accedere a questi membri con [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### <a name="to-call-a-windows-function-that-takes-an-unsigned-type"></a>Per chiamare una funzione Windows che accetta un tipo unsigned  
  
1.  Utilizzare un [l'istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md) per indicare [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] la libreria che contiene la funzione, che cos'è il nome in tale raccolta, che cos'è la sequenza di chiamata e come convertire le stringhe per la chiamata.  
  
2.  Nel `Declare` istruzione, utilizzare `UInteger`, `ULong`, `UShort`, o `Byte` come appropriato per ogni parametro con un tipo unsigned.  
  
3.  Consultare la documentazione per la funzione di Windows che si sta chiamando per trovare i nomi e valori delle costanti utilizzate. Molte di queste sono definiti nel file winuser.  
  
4.  Dichiarare le costanti necessarie nel codice. Molte costanti Windows sono valori senza segno a 32 bit e devono essere dichiarate `As``UInteger`.  
  
5.  Chiamare la funzione nel modo consueto. Nell'esempio seguente viene chiamata la funzione Windows `MessageBox`, che accetta un argomento integer senza segno.  
  
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
  
     È possibile testare la funzione `messageThroughWindows` con il codice seguente.  
  
    ```  
    Public Sub consumeWindowsMessage()  
        Dim w As New windowsMessage  
        w.messageThroughWindows()  
    End Sub  
    ```  
  
    > [!CAUTION]
    >  Il `UInteger`, `ULong`, `UShort`, e `SByte` tipi di dati non sono in parte il [indipendenza del linguaggio e componenti indipendenti dal linguaggio](https://msdn.microsoft.com/library/12a7a7h3) (CLS), pertanto il codice conforme a CLS non può utilizzare un componente che li utilizza.  
  
    > [!IMPORTANT]
    >  Effettua una chiamata a codice non gestito, ad esempio l'interfaccia di programmazione dell'applicazione di Windows (API), espone il codice a potenziali rischi di sicurezza.  
  
    > [!IMPORTANT]
    >  Chiama l'API di Windows richiede l'autorizzazione per codice non gestito, che può influire sulla relativa esecuzione in situazioni di attendibilità parziale. Per ulteriori informazioni, vedere <xref:System.Security.Permissions.SecurityPermission>e [le autorizzazioni di accesso di codice](http://msdn.microsoft.com/en-us/e5ae402f-6dda-4732-bbe8-77296630f675).</xref:System.Security.Permissions.SecurityPermission>  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Tipo di dati integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [Tipo di dati UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)   
 [Declare (istruzione)](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Procedura dettagliata: Chiamata delle API di Windows](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
