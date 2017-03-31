---
title: "Procedura: Determinare se un file è un assembly (C#) | Documentazione Microsoft"
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
ms.assetid: ea5186bb-5bff-4dcb-bde9-d6ba4e2edd00
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4de303da9215fb07ecbb6bfff78d18dcd246aad3
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-determine-if-a-file-is-an-assembly-c"></a>Procedura: Determinare se un file è un assembly (C#)
Un file è un assembly unicamente nei casi in cui è gestito e include nei metadati una voce assembly. Per altre informazioni sugli assembly e sui metadati, vedere l'argomento [Manifesto dell'assembly](https://msdn.microsoft.com/library/1w45z383).  
  
### <a name="how-to-manually-determine-if-a-file-is-an-assembly"></a>Procedura: Determinare se un file è un assembly in modo manuale  
  
1.  Avviare il [Disassembler IL (Ildasm.exe)](https://msdn.microsoft.com/library/f7dy01k1).  
  
2.  Caricare il file che si intende verificare.  
  
3.  Se **ILDASM** segnala che il file non è un file eseguibile portabile (PE, portable executable), tale file non è un assembly. Per altre informazioni, vedere [Procedura: Visualizzare il contenuto dell'assembly](http://msdn.microsoft.com/library/fb7baaab-4c0d-47ad-8fd3-4591cf834709).  
  
### <a name="how-to-programmatically-determine-if-a-file-is-an-assembly"></a>Procedura: Determinare se un file è un assembly a livello di codice  
  
1.  Chiamare il metodo <xref:System.Reflection.AssemblyName.GetAssemblyName%2A>, passando il percorso completo e il nome del file che si vuole testare.  
  
2.  Se viene generata un'eccezione <xref:System.BadImageFormatException>, il file non è un assembly.  
  
## <a name="example"></a>Esempio  
 Nell'esempio riportato di seguito viene testata una DLL per verificare se è un assembly.  
  
```  
class TestAssembly  
{  
    static void Main()  
    {  
  
        try  
        {  
            System.Reflection.AssemblyName testAssembly =  
                System.Reflection.AssemblyName.GetAssemblyName(@"C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll");  
  
            System.Console.WriteLine("Yes, the file is an assembly.");  
        }  
  
        catch (System.IO.FileNotFoundException)  
        {  
            System.Console.WriteLine("The file cannot be found.");  
        }  
  
        catch (System.BadImageFormatException)  
        {  
            System.Console.WriteLine("The file is not an assembly.");  
        }  
  
        catch (System.IO.FileLoadException)  
        {  
            System.Console.WriteLine("The assembly has already been loaded.");  
        }  
    }  
}  
/* Output (with .NET Framework 3.5 installed):  
    Yes, the file is an assembly.  
*/  
```  
  
 Il metodo <xref:System.Reflection.AssemblyName.GetAssemblyName%2A> carica il file di test, quindi lo rilascia dopo averne letto i dati.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection.AssemblyName>   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)   
 [Assembly e Global Assembly Cache (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)
