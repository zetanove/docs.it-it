---
title: "Procedura: determinare se un File è un Assembly (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: de26f410-9bd1-4b55-a343-cc82f81684be
caps.latest.revision: 6
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2e58363369ae4420879310bf09ed89cdd4f5b5cc
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-determine-if-a-file-is-an-assembly-visual-basic"></a>Procedura: determinare se un File è un Assembly (Visual Basic)
Un file è un assembly se e solo se viene gestito e contiene una voce assembly nei relativi metadati. Per ulteriori informazioni sugli assembly e i metadati, vedere l'argomento [manifesto dell'Assembly](https://msdn.microsoft.com/library/1w45z383).  
  
## <a name="how-to-manually-determine-if-a-file-is-an-assembly"></a>Come determinare manualmente se un file è un assembly  
  
1.  Avviare il [Ildasm.exe (Disassembler IL)](https://msdn.microsoft.com/library/f7dy01k1).  
  
2.  Caricare il file che si desidera verificare.  
  
3.  Se **ILDASM** report che il file non è un file eseguibile portabile (PE), quindi non è un assembly. Per ulteriori informazioni, vedere l'argomento [How to: View Assembly Contents](http://msdn.microsoft.com/library/fb7baaab-4c0d-47ad-8fd3-4591cf834709).  
  
## <a name="how-to-programmatically-determine-if-a-file-is-an-assembly"></a>Come determinare se un file è un assembly a livello di codice  
  
1.  Chiamare il <xref:System.Reflection.AssemblyName.GetAssemblyName%2A>, passando il percorso completo e il nome del file di cui si sta testando.</xref:System.Reflection.AssemblyName.GetAssemblyName%2A>  
  
2.  Se un <xref:System.BadImageFormatException>viene generata un'eccezione, il file non è un assembly.</xref:System.BadImageFormatException>  
  
## <a name="example"></a>Esempio  
 In questo esempio viene testata una DLL per verificare se si tratta di un assembly.  
  
```vb  
Module Module1  
    Sub Main()  
        Try  
            Dim testAssembly As Reflection.AssemblyName =  
                                Reflection.AssemblyName.GetAssemblyName("C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll")  
            Console.WriteLine("Yes, the file is an Assembly.")  
        Catch ex As System.IO.FileNotFoundException  
            Console.WriteLine("The file cannot be found.")  
        Catch ex As System.BadImageFormatException  
            Console.WriteLine("The file is not an Assembly.")  
        Catch ex As System.IO.FileLoadException  
            Console.WriteLine("The Assembly has already been loaded.")  
        End Try  
        Console.ReadLine()  
    End Sub  
End Module  
' Output (with .NET Framework 3.5 installed):  
'        Yes, the file is an Assembly.  
```
  
 Il <xref:System.Reflection.AssemblyName.GetAssemblyName%2A>metodo carica il file di test e quindi lo rilascia una volta le informazioni vengono lette.</xref:System.Reflection.AssemblyName.GetAssemblyName%2A>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection.AssemblyName></xref:System.Reflection.AssemblyName>   
 [Concetti di programmazione](../../../../visual-basic/programming-guide/concepts/index.md)   
 [Gli assembly e Global Assembly Cache (Visual Basic)](index.md)
