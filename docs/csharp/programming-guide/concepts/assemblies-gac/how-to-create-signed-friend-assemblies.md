---
title: 'Procedura: Creare assembly Friend firmati (C#) | Microsoft Docs'
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
ms.assetid: bab62063-61e6-453f-905f-77673df9534e
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
ms.openlocfilehash: 890cead4b28b8532dd7bd7f571defe7e280e4cdc
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-signed-friend-assemblies-c"></a>Procedura: Creare assembly Friend firmati (C#)
In questo esempio viene illustrato come usare assembly Friend e assembly con nomi sicuri. È necessario che entrambi i tipi di assembly abbiano un nome sicuro. Gli assembly in questo esempio usano le stesse chiavi. È comunque possibile usare chiavi diverse per i due assembly.  
  
### <a name="to-create-a-signed-assembly-and-a-friend-assembly"></a>Per creare un assembly firmato e un assembly friend  
  
1.  Aprire un prompt dei comandi.  
  
2.  Eseguire la sequenza di comandi seguente con lo strumento Nome sicuro per generare un keyfile e per visualizzare la relativa chiave pubblica. Per altre informazioni, vedere [Sn.exe (Strong Name Tool)](https://msdn.microsoft.com/library/k5b5tt23).  
  
    1.  Generare una chiave con nome sicuro per questo esempio e archiviarla nel file FriendAssemblies.snk:  
  
         `sn -k FriendAssemblies.snk`  
  
    2.  Estrarre la chiave pubblica da FriendAssemblies.snk e inserirla in FriendAssemblies.publickey:  
  
         `sn -p FriendAssemblies.snk FriendAssemblies.publickey`  
  
    3.  Visualizzare la chiave pubblica archiviata nel file FriendAssemblies.publickey:  
  
         `sn -tp FriendAssemblies.publickey`  
  
3.  Creare un file C# denominato `friend_signed_A` contenente il codice seguente. Il codice usa l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> per dichiarare che friend_signed_B è un assembly Friend.  
  
     Ogni volta che viene eseguito, lo strumento Nome sicuro genera una chiave pubblica nuova. È pertanto necessario sostituire la chiave pubblica nel codice seguente con la chiave pubblica appena generata, come illustrato nell'esempio seguente.  
  
    ```csharp  
    // friend_signed_A.cs  
    // Compile with:   
    // csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
    using System.Runtime.CompilerServices;  
  
    [assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")]  
    class Class1  
    {  
        public void Test()  
        {  
            System.Console.WriteLine("Class1.Test");  
            System.Console.ReadLine();  
        }  
    }  
    ```  
  
4.  Compilare e firmare friend_signed_A usando il comando seguente.  
  
    ```csharp  
    csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
    ```  
  
5.  Creare un file C# denominato `friend_signed_B` contenente il codice seguente. Poiché friend_signed_A specifica che friend_signed_B è un assembly Friend, il codice in friend_signed_B può accedere ai tipi e ai membri `internal` da friend_signed_A. Il file contiene il codice seguente.  
  
    ```csharp  
    // friend_signed_B.cs  
    // Compile with:   
    // csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
    public class Program  
    {  
        static void Main()  
        {  
            Class1 inst = new Class1();  
            inst.Test();  
        }  
    }  
    ```  
  
6.  Compilare e firmare friend_signed_B usando il comando seguente.  
  
    ```csharp  
    csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
    ```  
  
     Il nome dell'assembly generato dal compilatore deve corrispondere al nome dell'assembly Friend passato all'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>. È necessario specificare in modo esplicito il nome dell'assembly di output (con estensione exe o dll) usando il compilatore `/out`.  Per altre informazioni, vedere [/out (Opzioni del compilatore C#)](../../../../csharp/language-reference/compiler-options/out-compiler-option.md).  
  
7.  Eseguire il file friend_signed_B.exe.  
  
     Il programma stampa la stringa "Class1.Test".  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Tra l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> e la classe <xref:System.Security.Permissions.StrongNameIdentityPermission> esistono analogie. La differenza principale è che <xref:System.Security.Permissions.StrongNameIdentityPermission> può chiedere le autorizzazioni di sicurezza per l'esecuzione di una particolare sezione di codice, mentre il l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> controlla la visibilità dei tipi e dei membri `internal`.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Assemblies and the Global Assembly Cache (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)  (Assembly e Global Assembly Cache (C#))  
 [Assembly Friend (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [How to: Create Unsigned Friend Assemblies (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)  (Procedura: Creare assembly Friend non firmati)  
 [/keyfile](../../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [Sn.exe (strumento Nome sicuro)](https://msdn.microsoft.com/library/k5b5tt23)   
 [Creazione e uso degli assembly con nome sicuro](https://msdn.microsoft.com/library/xwb8f617)   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)
