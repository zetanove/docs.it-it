---
title: 'Procedura: Creare assembly Friend non firmati (C#) | Documentazione Microsoft'
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
ms.assetid: 78cbc4f0-b021-4141-a4ff-eb4edbd814ca
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
ms.openlocfilehash: c7d2924f0a619c234871232e155bb6f23e43aee4
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-unsigned-friend-assemblies-c"></a>Procedura: Creare assembly Friend non firmati (C#)
In questo esempio viene illustrato come usare assembly Friend e assembly non firmati.  
  
### <a name="to-create-an-assembly-and-a-friend-assembly"></a>Per creare un assembly e un assembly Friend  
  
1.  Aprire un prompt dei comandi.  
  
2.  Creare un file C# denominato `friend_signed_A.` contenente il codice seguente. Il codice usa l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> per dichiarare che friend_signed_B è un assembly Friend.  
  
    ```csharp  
    // friend_unsigned_A.cs  
    // Compile with:   
    // csc /target:library friend_unsigned_A.cs  
    using System.Runtime.CompilerServices;  
    using System;  
  
    [assembly: InternalsVisibleTo("friend_unsigned_B")]  
  
    // Type is internal by default.  
    class Class1  
    {  
        public void Test()  
        {  
            Console.WriteLine("Class1.Test");  
        }  
    }  
  
    // Public type with internal member.  
    public class Class2  
    {  
        internal void Test()  
        {  
            Console.WriteLine("Class2.Test");  
        }  
    }  
    ```  
  
3.  Compilare e firmare friend_signed_A usando il comando seguente.  
  
    ```csharp  
    csc /target:library friend_unsigned_A.cs  
    ```  
  
4.  Creare un file C# denominato `friend_unsigned_B` contenente il codice seguente. Poiché friend_unsigned_A specifica che friend_unsigned_B è un assembly Friend, il codice in friend_unsigned_B può accedere ai tipi e ai membri `internal` da friend_unsigned_A.  
  
    ```csharp  
    // friend_unsigned_B.cs  
    // Compile with:   
    // csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs  
    public class Program  
    {  
        static void Main()  
        {  
            // Access an internal type.  
            Class1 inst1 = new Class1();  
            inst1.Test();  
  
            Class2 inst2 = new Class2();  
            // Access an internal member of a public type.  
            inst2.Test();  
  
            System.Console.ReadLine();  
        }  
    }  
    ```  
  
5.  Compilare friend_signed_B usando il comando seguente.  
  
    ```csharp  
    csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs  
    ```  
  
     Il nome dell'assembly generato dal compilatore deve corrispondere al nome dell'assembly Friend passato all'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>. È necessario specificare in modo esplicito il nome dell'assembly di output (con estensione exe o dll) usando il compilatore `/out`. Per altre informazioni, vedere [/out (Opzioni del compilatore C#)](../../../../csharp/language-reference/compiler-options/out-compiler-option.md).  
  
6.  Eseguire il file friend_signed_B.exe.  
  
     Il programma stampa due stringhe: "Class1.Test" e "Class2.Test".  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Tra l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> e la classe <xref:System.Security.Permissions.StrongNameIdentityPermission> esistono analogie. La differenza principale è che <xref:System.Security.Permissions.StrongNameIdentityPermission> può chiedere le autorizzazioni di sicurezza per l'esecuzione di una particolare sezione di codice, mentre il l'attributo <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> controlla la visibilità dei tipi e dei membri `internal`.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Assembly e Global Assembly Cache (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)   
 [Assembly Friend (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [Procedura: Creare assembly Friend firmati (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [Guida per programmatori C#](../../../../csharp/programming-guide/index.md)
