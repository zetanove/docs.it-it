---
title: 'Procedura: creare e utilizzare assembly dalla riga di comando (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 229ff9fb-1bd1-403b-946b-526104864c60
caps.latest.revision: 6
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 363bca806736e5540165ea96e9b4fe60d0968098
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-and-use-assemblies-using-the-command-line-visual-basic"></a>Procedura: creare e utilizzare assembly dalla riga di comando (Visual Basic)
Un assembly o una libreria a collegamento dinamico (DLL), è collegata al programma in fase di esecuzione. Per illustrare la creazione e utilizzo di una DLL, si consideri lo scenario seguente:  
  
-   `MathLibrary.DLL`: Il file di libreria che contiene i metodi da chiamare in fase di esecuzione. In questo esempio, la DLL contiene due metodi, `Add` e `Multiply`.  
  
-   `Add`: Il file di origine che contiene il metodo `Add`. Restituisce la somma dei relativi parametri. La classe `AddClass` che contiene il metodo `Add` è un membro dello spazio dei nomi `UtilityMethods`.  
  
-   `Mult`: Il codice sorgente che contiene il metodo `Multiply`. Restituisce il prodotto dei parametri. La classe `MultiplyClass` che contiene il metodo `Multiply` è anche un membro dello spazio dei nomi `UtilityMethods`.  
  
-   `TestCode`: Il file che contiene il `Main` metodo. Vengono utilizzati i metodi nel file DLL per calcolare la somma e il prodotto degli argomenti in fase di esecuzione.  
  
## <a name="example"></a>Esempio  
  
```vb  
' File: Add.vb   
Namespace UtilityMethods  
    Public Class AddClass  
        Public Shared Function Add(ByVal i As Long, ByVal j As Long) As Long  
            Return i + j  
        End Function  
    End Class  
End Namespace  
```  
  
```vb  
' File: Mult.vb  
Namespace UtilityMethods  
    Public Class MultiplyClass  
        Public Shared Function Multiply(ByVal x As Long, ByVal y As Long) As Long  
            Return x * y  
        End Function  
    End Class  
End Namespace  
```  
  
```vb  
' File: TestCode.vb  
  
Imports UtilityMethods  
  
Module Test  
  
    Sub Main(ByVal args As String())  
  
        System.Console.WriteLine("Calling methods from MathLibrary.DLL:")  
  
        If args.Length <> 2 Then  
            System.Console.WriteLine("Usage: TestCode <num1> <num2>")  
            Return  
        End If  
  
        Dim num1 As Long = Long.Parse(args(0))  
        Dim num2 As Long = Long.Parse(args(1))  
  
        Dim sum As Long = AddClass.Add(num1, num2)  
        Dim product As Long = MultiplyClass.Multiply(num1, num2)  
  
        System.Console.WriteLine("{0} + {1} = {2}", num1, num2, sum)  
        System.Console.WriteLine("{0} * {1} = {2}", num1, num2, product)  
  
    End Sub  
  
End Module  
  
' Output (assuming 1234 and 5678 are entered as command-line arguments):  
' Calling methods from MathLibrary.DLL:  
' 1234 + 5678 = 6912  
' 1234 * 5678 = 7006652  
```  
  
 Questo file contiene l'algoritmo che utilizza i metodi della DLL `Add` e `Multiply`. Inizia con l'analisi degli argomenti immessi dalla riga di comando, `num1` e `num2`. Quindi calcola la somma utilizzando il `Add` metodo il `AddClass` classe e il prodotto utilizzando il `Multiply` metodo la `MultiplyClass` classe.  
  
 Si noti che il `Imports` istruzione all'inizio del file consente di utilizzare i nomi di classe non qualificati per fare riferimento ai metodi della DLL in fase di compilazione, come indicato di seguito:  
  
```vb  
MultiplyClass.Multiply(num1, num2)  
```  
  
 In caso contrario, è necessario utilizzare nomi completi, come indicato di seguito:  
  
```vb  
UtilityMethods.MultiplyClass.Multiply(num1, num2)  
```  
  
## <a name="execution"></a>Esecuzione  
 Per eseguire il programma, immettere il nome del file EXE, seguito da due numeri, come indicato di seguito:  
  
 `TestCode 1234 5678`  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Per compilare il file `MathLibrary.DLL`, compilare i due file `Add` e `Mult` utilizzando la seguente riga di comando.  
  
```vb  
vbc /target:library /out:MathLibrary.DLL Add.vb Mult.vb  
```  
  
 Il [/target (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/target.md) l'opzione del compilatore indica al compilatore di generare un file DLL anziché un file EXE. Il [/out (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/out.md) opzione seguita da un nome di file utilizzato per specificare il nome del file DLL. In caso contrario, il compilatore utilizza il primo file (`Add.vb`) come nome della DLL.  
  
 Per compilare il file eseguibile, `TestCode.exe`, utilizzare la seguente riga di comando:  
  
```vb  
vbc /out:TestCode.exe /reference:MathLibrary.DLL TestCode.vb  
```  
  
 Il **/out** l'opzione del compilatore indica al compilatore di generare un file EXE e specifica il nome del file di output (`TestCode.exe`). L'opzione del compilatore è facoltativa. Il [/reference (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/reference.md) l'opzione del compilatore specifica il file DLL o file utilizzati dal programma.  
  
 Per ulteriori informazioni sulla compilazione dalla riga di comando, vedere e [compilazione dalla riga di comando](../../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti di programmazione](../../../../visual-basic/programming-guide/concepts/index.md)   
 [Gli assembly e Global Assembly Cache (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Creazione di una classe che contenga le funzioni DLL](http://msdn.microsoft.com/library/e08e4c34-0223-45f7-aa55-a3d8dd979b0f)
