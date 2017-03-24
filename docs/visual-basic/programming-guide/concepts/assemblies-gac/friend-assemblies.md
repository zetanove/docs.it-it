---
title: Assembly Friend (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 9b3d5716-e6e4-47a7-a3e9-084d7fba5c28
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
ms.openlocfilehash: c6e01ae91b9d5d875bb618993cd9eda82db59399
ms.lasthandoff: 03/13/2017

---
# <a name="friend-assemblies-visual-basic"></a>Assembly Friend (Visual Basic)
Oggetto *assembly friend* è un assembly che può accedere a un altro assembly [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) tipi e membri. Se si individua un assembly come assembly friend, non è necessario contrassegnare tipi e membri come pubblici affinché possano essere accessibili da altri assembly. Questo è particolarmente utile negli scenari seguenti:  
  
-   Durante gli unit test, quando il codice di test viene eseguito in un assembly separato ma richiede l'accesso ai membri nell'assembly sottoposto a test che sono contrassegnati come `Friend`.  
  
-   Quando si sviluppa una libreria di classi e le aggiunte alla libreria sono contenute in assembly separati ma richiedono l'accesso ai membri nell'assembly esistenti contrassegnati come `Friend`.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo per identificare uno o più assembly friend per un determinato assembly.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> Nell'esempio seguente viene utilizzata la <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo nell'assembly e specifica l'assembly `AssemblyB` come assembly friend.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> In questo modo l'assembly `AssemblyB` accesso a tutti i tipi e membri nell'assembly che sono contrassegnati come `Friend`.  
  
> [!NOTE]
>  Quando si compila un assembly (assembly `AssemblyB`) che accederà ai tipi interni o i membri interni di un altro assembly (assembly *A*), è necessario specificare esplicitamente il nome del file di output (.exe o DLL) utilizzando il **/out** l'opzione del compilatore. Ciò è necessario perché il compilatore non ha ancora generato il nome dell'assembly in fase di compilazione in fase di che cui è associato a riferimenti esterni. Per ulteriori informazioni, vedere [/out (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/out.md).  
  
```vb  
Imports System.Runtime.CompilerServices  
Imports System  
<Assembly: InternalsVisibleTo("AssemblyB")>   
  
' Friend class.  
Friend Class FriendClass  
    Public Sub Test()  
        Console.WriteLine("Sample Class")  
    End Sub  
End Class  
  
' Public class with a Friend method.  
Public Class ClassWithFriendMethod  
    Friend Sub Test()  
        Console.WriteLine("Sample Method")  
    End Sub  
End Class  
  
```  
  
 Solo gli assembly specificati in modo esplicito come Friend possono accedere `Friend` tipi e membri. Ad esempio, se l'assembly B è un elemento friend di assembly A e assembly C fa riferimento all'assembly B, C non dispone dell'accesso al `Friend` tipi di A.  
  
 Il compilatore esegue alcune convalide di base del nome dell'assembly friend passato per il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> Se assembly *A* dichiara *B* come assembly friend, le regole di convalida sono i seguenti:  
  
-   Se assembly *A* è con nome sicuro, assembly *B* deve avere un nome sicuro. Il nome dell'assembly friend passato all'attributo deve includere il nome dell'assembly e la chiave pubblica della chiave con nome sicuro utilizzato per firmare l'assembly *B*.  
  
     Il nome dell'assembly friend che viene passato per il <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>attributo non può essere il nome sicuro dell'assembly *B*: non includono la versione dell'assembly, le impostazioni cultura, architettura o token di chiave pubblica.</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>  
  
-   Se assembly *A* non è sicuro denominata, il nome dell'assembly friend deve essere costituito solo il nome dell'assembly. Per ulteriori informazioni, vedere [procedura: creare assembly non firmati Friend (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md).  
  
-   Se assembly *B* è con nome sicuro, è necessario specificare la chiave con nome sicuro per l'assembly *B* utilizzando l'impostazione di progetto o la riga di comando `/keyfile` l'opzione del compilatore. Per ulteriori informazioni, vedere [procedura: creare effettuato l'accesso Friend Assemblies (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md).  
  
 La <xref:System.Security.Permissions.StrongNameIdentityPermission>classe fornisce inoltre la possibilità di condividere i tipi, con le seguenti differenze:</xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
-   <xref:System.Security.Permissions.StrongNameIdentityPermission>si applica a un singolo tipo, mentre un assembly friend valido per l'intero assembly.</xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
-   Se sono presenti centinaia di tipi in assembly *A* che si desidera condividere con assembly *B*, è necessario aggiungere <xref:System.Security.Permissions.StrongNameIdentityPermission>su tutti gli elementi.</xref:System.Security.Permissions.StrongNameIdentityPermission> Se si utilizza un assembly friend, è sufficiente dichiarare la relazione friend una sola volta.  
  
-   Se si utilizza <xref:System.Security.Permissions.StrongNameIdentityPermission>, i tipi che si desidera condividere devono essere dichiarati come pubblici.</xref:System.Security.Permissions.StrongNameIdentityPermission> Se si utilizza un assembly friend, i tipi condivisi vengono dichiarati come `Friend`.  
  
 Per informazioni su come accedere a un assembly `Friend` tipi e metodi da un file di modulo (file con estensione netmodule), vedere [/moduleassemblyname (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 <xref:System.Security.Permissions.StrongNameIdentityPermission></xref:System.Security.Permissions.StrongNameIdentityPermission>   
 [Procedura: creare assembly Friend non firmati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)   
 [Procedura: creare assembly Friend firmati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [Gli assembly e Global Assembly Cache (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Nozioni di base sulla programmazione](../../../../visual-basic/programming-guide/concepts/index.md)
