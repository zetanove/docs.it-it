---
title: "/moduleassemblyname (C# Compiler Option) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/moduleassemblyname"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "moduleassemblyname compiler option [C#]"
  - "/moduleassemblyname compiler option [C#]"
  - ".moduleassemblyname compiler option [C#]"
ms.assetid: d464d9b9-f18d-423b-95e9-66c7878fd53a
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# /moduleassemblyname (C# Compiler Option)
Specifica un assembly i cui tipi non pubblici possono accedere ai file con estensione netmodule.  
  
## Sintassi  
  
```  
/moduleassemblyname:assembly_name  
```  
  
## Argomenti  
 `assembly_name`  
 Il nome dell'assembly dei cui membri non pubblici il .netmodule può accedere.  
  
## Note  
 **\/moduleassemblyname** deve essere utilizzato quando viene compilato un .netmodule e dove le condizioni seguenti sono vere:  
  
-   Il file .netmodule richiede l'accesso a tipi non pubblici in un assembly esistente.  
  
-   Si conosce il nome dell'assembly in cui il .netmodule verrà compilato.  
  
-   L'assembly esistente ha concesso l'accesso assembly Friend all'assembly in cui verrà compilato il .netmodule.  
  
 Per ulteriori informazioni sulla compilazione di un .netmodule, vedere [\/target:module \(Create Module to Add to Assembly\)](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md).  
  
 Per ulteriori informazioni sugli assembly Friend, vedere [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
 L'opzione non è disponibile dall'interno dell'ambiente di sviluppo, ma soltanto durante la compilazione dalla riga di comando.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio e non può essere modificata a livello di codice.  
  
## Esempio  
 Nell'esempio viene compilato un assembly che dispone di un tipo privato e che fornisce l'accesso assembly Friend a un assembly denominato csman\_an\_assembly.  
  
```  
// moduleassemblyname_1.cs  
// compile with: /target:library  
using System;  
using System.Runtime.CompilerServices;  
  
[assembly:InternalsVisibleTo ("csman_an_assembly")]  
  
class An_Internal_Class   
{  
    public void Test()   
    {   
        Console.WriteLine("An_Internal_Class.Test called");   
    }  
}  
```  
  
## Esempio  
 Questo esempio compila un .netmodule che accede a un tipo non pubblico nell'assembly moduleassemblyname\_1.dll.  Sapendo che questo .netmodule verrà compilato in un assembly denominato csman\_an\_assembly, è possibile specificare **\/moduleassemblyname**, consentendo al .netmodule di accedere i tipi non pubblici in un assembly che consente l'accesso assembly Friend a csman\_an\_assembly.  
  
```  
// moduleassemblyname_2.cs  
// compile with: /moduleassemblyname:csman_an_assembly /target:module /reference:moduleassemblyname_1.dll  
class B {  
    public void Test() {  
        An_Internal_Class x = new An_Internal_Class();  
        x.Test();  
    }  
}  
```  
  
## Esempio  
 In questo esempio di codice viene compilato l'assembly csman\_an\_assembly facendo riferimento all'assembly compilato in precedenza e al .netmodule.  
  
```  
// csman_an_assembly.cs  
// compile with: /addmodule:moduleassemblyname_2.netmodule /reference:moduleassemblyname_1.dll  
class A {  
    public static void Main() {  
        B bb = new B();  
        bb.Test();  
    }  
}  
```  
  
  **An\_Internal\_Class.Test chiamato**   
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)