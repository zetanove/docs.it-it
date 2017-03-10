---
title: "How to: Call an Extension Method (Visual Basic) | Microsoft Docs"
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
  - "calling extension methods"
  - "extension methods [Visual Basic]"
ms.assetid: df07750f-40f4-4c07-a79e-1113a27cfbea
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# How to: Call an Extension Method (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I metodi estensione consentono di aggiungere metodi a una classe esistente.  Dopo che un metodo di estensione è stato dichiarato e inserito nell'ambito, è possibile chiamarlo come metodi di istanza del tipo che estende.  Per ulteriori informazioni sulla modalità di scrittura di un metodo di estensione, vedere [How to: Write an Extension Method](../../../../visual-basic/programming-guide/language-features/procedures/how-to-write-an-extension-method.md).  
  
 Le istruzioni seguenti fanno riferimento al metodo di estensione `PrintAndPunctuate`, che visualizza l'istanza della stringa che richiama, seguita dal valore inviato per il secondo parametro, `punc`.  
  
```vb#  
Imports System.Runtime.CompilerServices  
  
Module StringExtensions  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
  
End Module  
  
```  
  
 Il metodo deve trovarsi nell'ambito quando viene chiamato.  
  
### Per chiamare un metodo di estensione  
  
1.  Dichiarare una variabile con il tipo di dati del primo parametro del metodo di estensione.  Per `PrintAndPunctuate`, occorre una variabile <xref:System.String>:  
  
    ```  
    Dim example = "Ready"  
    ```  
  
2.  Tale variabile richiama il metodo di estensione, e il valore viene associato al primo parametro, `aString`.  Nell'istruzione di chiamata seguente viene visualizzato `Ready?`.  
  
    ```  
    example.PrintAndPunctuate("?")  
    ```  
  
     La chiamata a questo metodo di estensione è analoga a una chiamata a uno dei metodi di istanza <xref:System.String> che richiedono un parametro:  
  
    ```  
    example.EndsWith("dy")  
    example.IndexOf("R")  
    ```  
  
3.  Dichiarare un'altra variabile di stringa e chiamare nuovamente il metodo per controllare se funziona con qualsiasi stringa.  
  
    ```  
    Dim example2 = " or not"  
    example2.PrintAndPunctuate("!!!")  
    ```  
  
     Il risultato stavolta è: `or not!!!`.  
  
## Esempio  
 Il codice seguente è un esempio completo di creazione e utilizzo di un metodo di estensione semplice.  
  
```vb#  
Imports System.Runtime.CompilerServices  
Imports ConsoleApplication1.StringExtensions  
  
Module Module1  
  
    Sub Main()  
  
        Dim example = "Hello"  
        example.PrintAndPunctuate(".")  
        example.PrintAndPunctuate("!!!!")  
  
        Dim example2 = "Goodbye"  
        example2.PrintAndPunctuate("?")  
    End Sub  
  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
End Module  
  
' Output:  
' Hello.  
' Hello!!!!  
' Goodbye?  
```  
  
## Vedere anche  
 [How to: Write an Extension Method](../../../../visual-basic/programming-guide/language-features/procedures/how-to-write-an-extension-method.md)   
 [Metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)