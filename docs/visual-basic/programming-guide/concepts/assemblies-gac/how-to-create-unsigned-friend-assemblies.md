---
title: 'Procedura: creare assembly Friend non firmati (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 5735eb79-9729-4c46-ac1f-537ada3acaa7
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ceddb35c306f72c8927deda326d9fcca6c75d786
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-unsigned-friend-assemblies-visual-basic"></a>Procedura: creare assembly Friend non firmati (Visual Basic)
In questo esempio viene illustrato come utilizzare gli assembly friend con assembly non firmati.  
  
### <a name="to-create-an-assembly-and-a-friend-assembly"></a>Per creare un assembly e un assembly friend  
  
1.  Aprire un prompt dei comandi.  
  
2.  Creare un file di Visual Basic denominato `friend_signed_A.` che contiene il codice seguente. Il codice utilizza il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo per dichiarare friend_signed_B come assembly friend.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>  
  
    ```vb  
    ' friend_unsigned_A.vb  
    ' Compile with:   
    ' Vbc /target:library friend_unsigned_A.vb  
    Imports System.Runtime.CompilerServices  
    Imports System  
  
    <Assembly: InternalsVisibleTo("friend_unsigned_B")>   
  
    ' Friend type.  
    Friend Class Class1  
        Public Sub Test()  
            Console.WriteLine("Class1.Test")  
        End Sub  
    End Class  
  
    ' Public type with Friend member.  
    Public Class Class2  
        Friend Sub Test()  
            Console.WriteLine("Class2.Test")  
        End Sub  
    End Class  
    ```  
  
3.  Compilare e firmare friend_signed_A utilizzando il comando seguente.  
  
    ```vb  
    Vbc /target:library friend_unsigned_A.vb  
    ```  
  
4.  Creare un file di Visual Basic denominato `friend_unsigned_B` che contiene il codice seguente. Poiché friend_unsigned_A specifica friend_unsigned_B come assembly friend, il codice di friend_unsigned_B può accedere `Friend` tipi e membri da friend_unsigned_A.  
  
    ```vb  
    ' friend_unsigned_B.vb  
    ' Compile with:   
    ' Vbc /r:friend_unsigned_A.dll friend_unsigned_B.vb  
    Module Module1  
        Sub Main()  
            ' Access a Friend type.  
            Dim inst1 As New Class1()  
            inst1.Test()  
  
            Dim inst2 As New Class2()  
            ' Access a Friend member of a public type.  
            inst2.Test()  
  
            System.Console.ReadLine()  
        End Sub  
    End Module  
    ```  
  
5.  Compilare friend_signed_B utilizzando il comando seguente.  
  
    ```vb  
    Vbc /r:friend_unsigned_A.dll friend_unsigned_B.vb  
    ```  
  
     Il nome dell'assembly generato dal compilatore deve corrispondere il nome dell'assembly friend che viene passato per il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> È possibile impostare in modo esplicito l'assembly utilizzando il `/out` l'opzione del compilatore.  
  
6.  Eseguire il file friend_signed_B.exe.  
  
     Il programma stampa due stringhe: "Class1" e "Class2. test".  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Esistono analogie tra l' <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo e la <xref:System.Security.Permissions.StrongNameIdentityPermission>classe.</xref:System.Security.Permissions.StrongNameIdentityPermission> </xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> La differenza principale è che <xref:System.Security.Permissions.StrongNameIdentityPermission>può richiedere le autorizzazioni di sicurezza per l'esecuzione di una particolare sezione di codice, mentre il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo controlla la visibilità di `Friend` tipi e membri.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> </xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Gli assembly e Global Assembly Cache (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Assembly Friend (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [Procedura: creare assembly Friend firmati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [Concetti relativi alla Guida di programmazione](../../../../visual-basic/programming-guide/concepts/index.md)
