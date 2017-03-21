---
title: 'Procedura: creare assembly Friend firmati (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: f2afd83d-b044-484b-a56d-56d0a8a40647
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1a69f7e833800ec7417bc35fad763f1001b3e7f9
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-signed-friend-assemblies-visual-basic"></a>Procedura: creare assembly Friend firmati (Visual Basic)
In questo esempio viene illustrato come utilizzare gli assembly friend con assembly con nomi sicuri. Entrambi gli assembly devono essere sicuro. Anche se entrambi gli assembly in questo esempio utilizzano le stesse chiavi, è possibile utilizzare chiavi diverse per due assembly.  
  
### <a name="to-create-a-signed-assembly-and-a-friend-assembly"></a>Per creare un assembly firmato e un assembly friend  
  
1.  Aprire un prompt dei comandi.  
  
2.  Utilizzare la seguente sequenza di comandi con lo strumento nome sicuro per generare un file di chiave e per visualizzare la relativa chiave pubblica. Per altre informazioni, vedere [Sn.exe (Strong Name Tool)](https://msdn.microsoft.com/library/k5b5tt23).  
  
    1.  Generare una chiave con nome sicuro per questo esempio e archiviarlo nel file FriendAssemblies. snk:  
  
         `sn -k FriendAssemblies.snk`  
  
    2.  Estrarre la chiave pubblica da FriendAssemblies. snk e inserirla in FriendAssemblies. publickey:  
  
         `sn -p FriendAssemblies.snk FriendAssemblies.publickey`  
  
    3.  Visualizzare la chiave pubblica archiviata nel file FriendAssemblies. publickey:  
  
         `sn -tp FriendAssemblies.publickey`  
  
3.  Creare un file di Visual Basic denominato `friend_signed_A` che contiene il codice seguente. Il codice utilizza il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo per dichiarare friend_signed_B come assembly friend.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>  
  
     Ogni volta che viene eseguito, lo strumento nome sicuro genera una nuova chiave pubblica. Pertanto, è necessario sostituire la chiave pubblica nel codice seguente con la chiave pubblica che appena generato, come illustrato nell'esempio seguente.  
  
    ```vb  
    ' friend_signed_A.vb  
    ' Compile with:   
    ' Vbc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.vb  
    Imports System.Runtime.CompilerServices  
  
    <Assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")>   
    Public Class Class1  
        Public Sub Test()  
            System.Console.WriteLine("Class1.Test")  
            System.Console.ReadLine()  
        End Sub  
    End Class  
    ```  
  
4.  Compilare e firmare friend_signed_A utilizzando il comando seguente.  
  
    ```vb  
    Vbc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.vb  
    ```  
  
5.  Creare un file di Visual Basic denominato `friend_signed_B` e contiene il codice seguente. Poiché friend_signed_A specifica friend_signed_B come assembly friend, il codice in friend_signed_B può accedere `Friend` tipi e membri da friend_signed_A. Il file contiene il codice seguente.  
  
    ```vb  
    ' friend_signed_B.vb  
    ' Compile with:   
    ' Vbc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll friend_signed_B.vb  
    Module Sample  
        Public Sub Main()  
            Dim inst As New Class1  
            inst.Test()  
        End Sub  
    End Module  
    ```  
  
6.  Compilare e firmare friend_signed_B utilizzando il comando seguente.  
  
    ```vb  
    Vbc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll friend_signed_B.vb  
    ```  
  
     Il nome dell'assembly generato dal compilatore deve corrispondere il nome dell'assembly friend passato per il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> È possibile impostare in modo esplicito l'assembly utilizzando il `/out` l'opzione del compilatore. Per ulteriori informazioni, vedere [/out (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/out.md).  
  
7.  Eseguire il file friend_signed_B.exe.  
  
     Il programma stampa la stringa "Class1".  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Esistono analogie tra l' <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo e la <xref:System.Security.Permissions.StrongNameIdentityPermission>classe.</xref:System.Security.Permissions.StrongNameIdentityPermission> </xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> La differenza principale è che <xref:System.Security.Permissions.StrongNameIdentityPermission>può richiedere le autorizzazioni di sicurezza per l'esecuzione di una particolare sezione di codice, mentre il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo controlla la visibilità di `Friend` tipi e membri.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> </xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Gli assembly e Global Assembly Cache (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Assembly Friend (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [Procedura: creare assembly Friend non firmati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)   
 [/keyfile](../../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [Sn.exe (strumento nome sicuro)](https://msdn.microsoft.com/library/k5b5tt23)   
 [Creazione e utilizzo di assembly con nomi sicuri](https://msdn.microsoft.com/library/xwb8f617)   
 [Nozioni di base sulla programmazione](../../../../visual-basic/programming-guide/concepts/index.md)
