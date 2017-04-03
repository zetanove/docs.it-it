---
title: Assembly Friend (C#) | Microsoft Docs
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
ms.assetid: b65ea7de-0801-477a-a39c-e914c2cc107c
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
ms.openlocfilehash: ca01b9e91de08f3bdf53cd0572a3e1d1af0cf0af
ms.lasthandoff: 03/13/2017

---
# <a name="friend-assemblies-c"></a>Assembly Friend (C#)
Un *assembly Friend* può accedere ai tipi e ai membri [interni](../../../../csharp/language-reference/keywords/internal.md) di un altro assembly. Se un assembly viene riconosciuto di tipo Friend, non è più necessario contrassegnare tipi e membri come pubblici perché altri assembly possano accedervi. Questo metodo è particolarmente utile negli scenari seguenti:  
  
-   Durante il test dell'unità, quando il codice di test eseguito in un assembly separato deve accedere ai membri nell'assembly sottoposto a test che sono contrassegnati come `internal`.  
  
-   Quando si sviluppa una libreria di classi e le aggiunte alla libreria sono contenute in assembly separati che devono accedere ai membri negli assembly esistenti che sono contrassegnati come `internal` .  
  
## <a name="remarks"></a>Note  
 Per identificare uno o più assembly Friend per un determinato assembly, è possibile usare l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>. Nell'esempio seguente viene usato l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> nell'assembly A e l'assembly `AssemblyB` viene riconosciuto di tipo Friend. In questo modo l'assembly `AssemblyB` può accedere a tutti i tipi e i membri nell'assembly A che sono contrassegnati come `internal`.  
  
> [!NOTE]
>  Quando si compila un assembly (assembly `AssemblyB`) che deve accedere ai tipi o ai membri interni di un altro assembly (assembly *A*), è necessario specificare in modo esplicito il nome del file di output (con estensione exe o dll) usando l'opzione del compilatore **/out**. Il compilatore non ha infatti ancora generato il nome dell'assembly in fase di compilazione quando crea l'associazione a riferimenti esterni. Per altre informazioni, vedere [/out (C#)](../../../../csharp/language-reference/compiler-options/out-compiler-option.md).  
  
```csharp  
using System.Runtime.CompilerServices;  
using System;  
  
[assembly: InternalsVisibleTo("AssemblyB")]  
  
// The class is internal by default.  
class FriendClass  
{  
    public void Test()  
    {  
        Console.WriteLine("Sample Class");  
    }  
}  
  
// Public class that has an internal method.  
public class ClassWithFriendMethod  
{  
    internal void Test()  
    {  
        Console.WriteLine("Sample Method");  
    }  
  
}  
```  
  
 Possono accedere ai tipi e ai membri `internal` solo gli assembly che sono stati definiti di tipo Friend in modo esplicito. Ad esempio, se l'assembly B è un elemento di tipo Friend per l'assembly A e l'assembly C fa riferimento all'assembly B, l'assembly C non può accedere ai tipi `internal` in A.  
  
 Il compilatore esegue alcune convalide di base del nome dell'assembly Friend che viene passato all'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>. Se l'assembly *A* dichiara che *B* è un assembly Friend, le regole di convalida sono le seguenti:  
  
-   Se *A* è un assembly con nome sicuro, anche *B* deve essere un assembly con nome sicuro. Il nome dell'assembly Friend passato all'attributo deve includere il nome dell'assembly e la chiave pubblica della chiave con nome sicuro usata per firmare l'assembly *B*.  
  
     Il nome dell'assembly Friend passato all'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> non può essere il nome sicuro dell'assembly *B*. Non includere la versione dell'assembly, l'impostazione cultura, l'architettura o il token di chiave pubblica.  
  
-   Se *A* non è un assembly con nome sicuro, il nome dell'assembly Friend deve comprendere solo il nome dell'assembly. Per altre informazioni, vedere [How to: Create Unsigned Friend Assemblies (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md) (Procedura: Creare assembly Friend non firmati (C#)).  
  
-   Se *B* è un assembly con nome sicuro, è necessario specificare la chiave con nome sicuro per l'assembly *B* usando l'impostazione di progetto o l'opzione del compilatore `/keyfile` della riga di comando. Per altre informazioni, vedere [Procedura: Creare assembly Friend firmati (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md).  
  
 La classe <xref:System.Security.Permissions.StrongNameIdentityPermission> consente anche la condivisione dei tipi, con le differenze seguenti:  
  
-   <xref:System.Security.Permissions.StrongNameIdentityPermission> si applica a un singolo tipo, mentre un assembly Friend si applica all'intero assembly.  
  
-   Se un assembly *A* contiene centinaia di tipi che si vuole condividere con l'assembly *B*, è necessario aggiungere <xref:System.Security.Permissions.StrongNameIdentityPermission> a tutti i tipi. Se invece si usa un assembly Friend, è sufficiente dichiarare una volta che si tratta di una relazione di tipo Friend.  
  
-   Se si usa <xref:System.Security.Permissions.StrongNameIdentityPermission>, i tipi che si vogliono condividere devono essere dichiarati pubblici. Se si usa un assembly Friend, i tipi condivisi vengono dichiarati `internal`.  
  
 Per informazioni su come accedere ai tipi e ai metodi `internal` di un assembly da un file di modulo, vale a dire un file con estensione netmodule, vedere [/moduleassemblyname (C#)](../../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 <xref:System.Security.Permissions.StrongNameIdentityPermission>   
 [How to: Create Unsigned Friend Assemblies (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)  (Procedura: Creare assembly Friend non firmati)  
 [Procedura: Creare assembly Friend firmati (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [Assemblies and the Global Assembly Cache (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)  (Assembly e Global Assembly Cache (C#))  
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)
