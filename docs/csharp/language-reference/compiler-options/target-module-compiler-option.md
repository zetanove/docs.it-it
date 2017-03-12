---
title: "/target:module (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/target:module"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-target compiler options [C#], /target:module"
  - "target compiler options [C#], /target:module"
  - "/target compiler options [C#], /target:module"
ms.assetid: 9af1e4fa-c749-44e7-ae58-90a3d05d4e72
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# /target:module (C# Compiler Options)
Specificando questa opzione, il compilatore non genererà un manifesto assembly.  
  
## Sintassi  
  
```  
/target:module  
```  
  
## Note  
 Per impostazione predefinita, il file di output creato eseguendo la compilazione e specificando questa opzione avrà estensione .netmodule.  
  
 Non è possibile caricare in Common Language Runtime di .NET Framework i file privi di manifesto assembly.  È tuttavia possibile incorporare tali file nel manifesto assembly di un assembly mediante [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md).  
  
 Se in un'unica compilazione vengono generati più moduli, i tipi [internal](../../../csharp/language-reference/keywords/internal.md) di un modulo verranno resi disponibili ad altri moduli della compilazione.  Quando il codice del modulo fa riferimento ai tipi `internal` di un altro modulo, sarà necessario incorporare entrambi i moduli in un manifesto assembly, tramite l'opzione **\/addmodule**.  
  
 La creazione di moduli non è supportata nell'ambiente di sviluppo di Visual Studio.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## Esempio  
 Compilare `in.cs`, creando `in.netmodule`.  
  
```  
csc /target:module in.cs  
```  
  
## Vedere anche  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)