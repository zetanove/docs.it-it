---
title: "/target (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/target"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "target compiler options [C#]"
  - "/target compiler options [C#]"
  - "assemblies [C#], compiling"
  - "-target compiler options [C#]"
ms.assetid: a18bbd8e-bbf7-49e7-992c-717d0eb1f76f
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /target (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per l'opzione del compilatore **\/target** è possibile scegliere tra quattro formati:  
  
 [\/target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md)  
 Creare un file .exe per le applicazioni [!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)].  
  
 [\/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md)  
 Per creare un file exe.  
  
 [\/target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md)  
 Per creare una libreria di codice.  
  
 [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md)  
 Per creare un modulo.  
  
 [\/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md)  
 Per creare un'applicazione per Windows.  
  
 [\/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)  
 Creare un file intermedio .winmdobj.  
  
 Se non si specifica **\/target:module**, l'opzione **\/target** determina l'inserimento di un manifesto assembly di .NET Framework in un file di output.  Per ulteriori informazioni, vedere [Assembly in Common Language Runtime](../Topic/Assemblies%20in%20the%20Common%20Language%20Runtime.md) e [Attributi comuni](../Topic/Common%20Attributes%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Il manifesto dell'assembly viene inserito nel primo file di output con estensione exe della compilazione oppure, se non è disponibile alcun file di output exe, nella prima dll.  Nella riga di comando riportata di seguito, ad esempio, il manifesto verrà inserito in `1.exe`.  
  
```  
csc /out:1.exe t1.cs /out:2.netmodule t2.cs  
```  
  
 In fase di compilazione viene creato un unico manifesto assembly per ciascuna compilazione.  Nel manifesto assembly vengono inserite le informazioni relative a tutti i file della compilazione.  In tutti i file di output, a eccezione di quelli creati con l'opzione **\/target:module**, è possibile inserire un manifesto assembly.  Quando si generano più file di output alla riga di comando, è possibile creare un solo manifesto assembly il quale verrà inserito nel primo file di output specificato alla riga di comando.  Indipendentemente da quale sia il primo file di output \(**\/target:exe**, **\/target:winexe**, **\/target:library** o **\/target:module**\), tutti gli altri file di output generati nella stessa compilazione devono essere moduli \(**\/target:module**\).  
  
 Se si crea un assembly, è possibile indicare che tutto il codice o parte di esso sia conforme a CLS mediante l'attributo <xref:System.CLSCompliantAttribute>.  
  
```  
// target_clscompliant.cs  
[assembly:System.CLSCompliant(true)]   // specify assembly compliance  
  
[System.CLSCompliant(false)]   // specify compliance for an element  
public class TestClass  
{  
    public static void Main() {}  
}  
```  
  
 Per ulteriori informazioni sull'impostazione di questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [\/subsystemversion \(Specify minimum subsystem version\)](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)