---
title: "Main Procedure in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Main"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Main procedure"
  - "Main method [Visual Basic]"
  - "main function"
ms.assetid: f0db283e-f283-4464-b521-b90858cc1b44
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Main Procedure in Visual Basic
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In ogni applicazione di Visual Basic deve essere presente una routine denominata `Main`.  Questa routine funge da punto di partenza e controllo generale dell'applicazione  In .NET Framework, la routine `Main` viene chiamata dopo che è stata caricata l'applicazione ed è possibile passarle il controllo.  A meno che non si stia creando un'applicazione Windows Forms è necessario scrivere la routine `Main` per le applicazioni che sono in esecuzione.  
  
 `Main` contiene il codice che viene eseguito inizialmente.  All'interno della routine `Main` è possibile determinare il form da caricare per primo all'avvio del programma, scoprire se una copia dell'applicazione è già in esecuzione, stabilire un insieme di variabili per l'applicazione o aprire un database necessario all'applicazione.  
  
## Requisiti per la routine Main  
 I file ad esecuzione automatica, generalmente con estensione .exe, devono contenere una routine `Main`.  Le librerie, ad esempio con estensione .dll, non vengono eseguite automaticamente e non richiedono quindi la routine `Main`.  I requisiti per i diversi tipi di progetti che è possibile creare sono i seguenti:  
  
-   Le applicazioni console vengono eseguite automaticamente e richiedono almeno una routine `Main`.  .  
  
-   Le applicazioni Windows Forms vengono eseguite automaticamente.  Tuttavia, in questo caso, la routine `Main` viene generata dal compilatore Visual Basic e non è quindi necessario scriverne una.  
  
-   Le librerie di classi non richiedono la routine `Main` perché includono le librerie Windows Control e Web Control.  Le applicazioni Web vengono distribuite come librerie di classi.  
  
## Dichiarazione della routine Main  
 Sono disponibili quattro metodi per dichiarare la routine `Main`.  La routine può accettare o meno argomenti e restituire o meno un valore.  
  
> [!NOTE]
>  Se si dichiara la routine `Main` in una classe, sarà necessario utilizzare la parola chiave `Shared`.  In un modulo `Main` non deve essere `Shared`.  
  
-   Rappresenta il modo più semplice per dichiarare una routine `Sub` che non accetta argomenti e non restituisce alcun valore.  
  
    ```  
    Module mainModule  
        Sub Main()  
            MsgBox("The Main procedure is starting the application.")  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
-   È anche possibile che la routine `Main` restituisca un valore `Integer`, utilizzato dal sistema operativo come codice di uscita del programma.  Il test di questo codice può essere eseguito da altri programmi mediante l'esame del valore ERRORLEVEL di Windows.  Per restituire un codice di uscita è necessario dichiarare `Main` come routine `Function` anziché come routine `Sub`.  
  
    ```  
    Module mainModule  
        Function Main() As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   La routine `Main` può inoltre utilizzare la matrice `String` come argomento.  Ogni stringa della matrice contiene uno degli argomenti della riga di comando utilizzati per richiamare il programma.  È possibile effettuare diverse operazioni in base ai loro valori.  
  
    ```  
    Module mainModule  
        Function Main(ByVal cmdArgs() As String) As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   È possibile dichiarare `Main` per esaminare gli argomenti della riga di comando senza restituire un codice di uscita, come nell'esempio seguente:  
  
    ```  
    Module mainModule  
        Sub Main(ByVal cmdArgs() As String)  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>   
 <xref:System.Array.Length%2A>   
 <xref:Microsoft.VisualBasic.Information.UBound%2A>   
 [Structure of a Visual Basic Program](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)   
 [NIB: Visual Basic Version of Hello, World](http://msdn.microsoft.com/it-it/9d030b60-e148-4366-a462-69532f02294c)   
 [\/main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Integer Data Type](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [String Data Type](../../../visual-basic/language-reference/data-types/string-data-type.md)