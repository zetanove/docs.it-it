---
title: "How to: Write an Extension Method (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "extending data types"
  - "writing extension methods"
  - "extension methods [Visual Basic]"
ms.assetid: fb2739cc-958d-4ef4-a38b-214a74c93413
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Write an Extension Method (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

I metodi estensione consentono di aggiungere metodi a una classe esistente.  Il metodo di estensione può essere chiamato come se fosse un'istanza di tale classe.  
  
### Per definire un metodo di estensione  
  
1.  Aprire un'applicazione Visual Basic nuova o esistente in Visual Studio.  
  
2.  All'inizio del file nel quale si desidera definire un metodo di estensione, includere l'istruzione Import seguente:  
  
    ```  
    Imports System.Runtime.CompilerServices  
    ```  
  
3.  All'interno di un modulo dell'applicazione nuova o esistente, iniziare la definizione del metodo con l'attributo di estensione:  
  
    ```  
    <Extension()>  
    ```  
  
4.  Dichiarare il metodo nella modalità comune, con l'eccezione che il tipo del primo parametro deve essere il tipo di dati da estendere.  
  
    ```  
    <Extension()>   
    Public Sub subName (ByVal para1 As ExtendedType, <other parameters>)  
         ' < Body of the method >  
    End Sub  
    ```  
  
## Esempio  
 Nell'esempio riportato di seguito viene dichiarato un metodo di estensione in un modulo `StringExtensions`.  Un secondo modulo, `Module1`, importa `StringExtensions` e chiama il metodo.  Il metodo di estensione deve essere nell'ambito quando viene chiamato.  Il metodo di estensione `PrintAndPunctuate` estende la classe <xref:System.String> con un metodo che visualizza l'istanza della stringa seguita da una stringa di simboli di punteggiatura inviati come parametro.  
  
```vb#  
' Declarations will typically be in a separate module.  
Imports System.Runtime.CompilerServices  
  
Module StringExtensions  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
  
End Module  
```  
  
```vb#  
' Import the module that holds the extension method you want to use,   
' and call it.  
  
Imports ConsoleApplication2.StringExtensions  
  
Module Module1  
  
    Sub Main()  
        Dim example = "Hello"  
        example.PrintAndPunctuate("?")  
        example.PrintAndPunctuate("!!!!")  
    End Sub  
  
End Module  
  
```  
  
 Notare che il metodo viene definito con due parametri e chiamato solo con uno.  Il primo parametro, `aString`, della definizione di metodo è associato a `example`, l'istanza di `String` che chiama il metodo.  Di seguito è riportato l'output dell'esempio:  
  
 `Hello?`  
  
 `Hello!!!!`  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.ExtensionAttribute>   
 [Metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Module Statement](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)