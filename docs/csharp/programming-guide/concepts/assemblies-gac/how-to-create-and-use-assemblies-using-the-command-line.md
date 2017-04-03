---
title: 'Procedura: creare e usare assembly dalla riga di comando | Documentazione Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 408ddce3-89e3-4e12-8353-34a49beeb72b
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 08bf434503d92fcf999dc4defb6a0322bceff020
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-and-use-assemblies-using-the-command-line-c"></a>Procedura: creare e usare assembly dalla riga di comando (C#)
Un assembly, o libreria a collegamento dinamico (DLL), viene collegato al programma in fase di esecuzione. Per illustrare la creazione e l'uso di una DLL, si consideri lo scenario seguente:  
  
-   `MathLibrary.DLL`: il file libreria che contiene i metodi da chiamare in fase di esecuzione. In questo esempio la DLL contiene due metodi: `Add` e `Multiply`.  
  
-   `Add`: il file di origine che contiene il metodo `Add`. Restituisce la somma dei suoi parametri. La classe `AddClass` che contiene il metodo `Add` è un membro dello spazio dei nomi `UtilityMethods`.  
  
-   `Mult`: il codice sorgente che contiene il metodo `Multiply`. Restituisce il prodotto dei suoi parametri. Anche la classe `MultiplyClass` che contiene il metodo `Multiply` è un membro dello spazio dei nomi `UtilityMethods`.  
  
-   `TestCode`: il file che contiene il metodo `Main`. Usa i metodi del file DLL per calcolare la somma e il prodotto degli argomenti in fase di esecuzione.  
  
## <a name="example"></a>Esempio  
  
```csharp  
// File: Add.cs   
namespace UtilityMethods  
{  
    public class AddClass   
    {  
        public static long Add(long i, long j)   
        {   
            return (i + j);  
        }  
    }  
}  
```  
  
```csharp  
// File: Mult.cs  
namespace UtilityMethods   
{  
    public class MultiplyClass  
    {  
        public static long Multiply(long x, long y)   
        {  
            return (x * y);   
        }  
    }  
}  
```  
  
```csharp  
// File: TestCode.cs  
  
using UtilityMethods;  
  
class TestCode  
{  
    static void Main(string[] args)   
    {  
        System.Console.WriteLine("Calling methods from MathLibrary.DLL:");  
  
        if (args.Length != 2)  
        {  
            System.Console.WriteLine("Usage: TestCode <num1> <num2>");  
            return;  
        }  
  
        long num1 = long.Parse(args[0]);  
        long num2 = long.Parse(args[1]);  
  
        long sum = AddClass.Add(num1, num2);  
        long product = MultiplyClass.Multiply(num1, num2);  
  
        System.Console.WriteLine("{0} + {1} = {2}", num1, num2, sum);  
        System.Console.WriteLine("{0} * {1} = {2}", num1, num2, product);  
    }  
}  
/* Output (assuming 1234 and 5678 are entered as command-line arguments):  
    Calling methods from MathLibrary.DLL:  
    1234 + 5678 = 6912  
    1234 * 5678 = 7006652          
*/  
```  
  
 Questo file contiene l'algoritmo che usa i metodi della DLL: `Add` e `Multiply`. Inizia con l'analisi degli argomenti immessi dalla riga di comando: `num1` e `num2`. Quindi calcola la somma usando il metodo `Add` sulla classe `AddClass` e il prodotto usando il metodo `Multiply` sulla classe `MultiplyClass`.  
  
 Si noti che la direttiva `using` all'inizio del file consente di usare i nomi di classe non qualificati per fare riferimento ai metodi della DLL in fase di compilazione, come indicato di seguito:  
  
```csharp  
MultiplyClass.Multiply(num1, num2);  
```  
  
 In caso contrario è necessario usare nomi completi, come indicato di seguito:  
  
```csharp  
UtilityMethods.MultiplyClass.Multiply(num1, num2);  
```  
  
## <a name="execution"></a>Esecuzione  
 Per eseguire il programma immettere il nome del file EXE, seguito da due numeri, come indicato di seguito:  
  
 `TestCode 1234 5678`  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Per compilare il file `MathLibrary.DLL`, compilare i due file `Add` e `Mult` usando la seguente riga di comando.  
  
```csharp  
csc /target:library /out:MathLibrary.DLL Add.cs Mult.cs  
```  
  
 L'opzione [/target:library](../../../../csharp/language-reference/compiler-options/target-library-compiler-option.md) del compilatore indica al compilatore di generare un file DLL anziché un file EXE. L'opzione [/out](../../../../csharp/language-reference/compiler-options/out-compiler-option.md) del compilatore seguita da un nome di file viene usata per specificare il nome di file della DLL. In caso contrario il compilatore usa il primo file (`Add.cs`) come nome della DLL.  
  
 Per compilare il file eseguibile, `TestCode.exe`, usare la seguente riga di comando:  
  
```csharp  
csc /out:TestCode.exe /reference:MathLibrary.DLL TestCode.cs  
```  
  
 L'opzione **/out** del compilatore indica al compilatore di generare un file EXE e specifica il nome del file che deve essere generato (`TestCode.exe`). Questa opzione del compilatore è opzionale. L'opzione [/reference](../../../../csharp/language-reference/compiler-options/reference-compiler-option.md) del compilatore specifica il file o i file DLL utilizzati dal programma. Per altre informazioni, vedere [/reference](../../../../csharp/language-reference/compiler-options/reference-compiler-option.md).  
  
 Per altre informazioni sulla compilazione dalla riga di comando, vedere [Compilazione dalla riga di comando con csc.exe](../../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)   
 [Assembly e Global Assembly Cache (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)   
 [Creazione di una classe che contenga le funzioni DLL](http://msdn.microsoft.com/library/e08e4c34-0223-45f7-aa55-a3d8dd979b0f)
