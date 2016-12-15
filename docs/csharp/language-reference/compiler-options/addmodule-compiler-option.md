---
title: "/addmodule (C# Compiler Options) | Microsoft Docs"
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
  - "/addmodule"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/addmodule compiler option [C#]"
  - "-addmodule compiler option [C#]"
  - "addmodule compiler option [C#]"
ms.assetid: ed604546-0dc2-4bd4-9a3e-610a8d973e58
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /addmodule (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Questa opzione consente di aggiungere un modulo creato con l'opzione target:module alla compilazione in corso.  
  
## Sintassi  
  
```  
/addmodule:file[;file2]  
```  
  
## Argomenti  
 `file`, `file2`  
 Rappresenta un file di output contenente i metadati.  Il file non può contenere un manifesto assembly.  Per importare più file, separare i nomi dei file con una virgola o un punto e virgola.  
  
## Note  
 Tutti i moduli aggiunti con **\/addmodule** dovranno trovarsi nella stessa directory del file di output in fase di esecuzione.  Vale a dire che, mentre in fase di compilazione è possibile specificare un modulo presente in qualsiasi directory, in fase di esecuzione tale modulo dovrà trovarsi nella directory dell'applicazione.  In caso contrario, verrà generata l'eccezione <xref:System.TypeLoadException>.  
  
 `file` non può contenere un assembly.  Se, ad esempio, il file di output è stato creato con [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), sarà possibile importarne i metadati con **\/addmodule**.  
  
 Se il file di output è stato creato con un'opzione **\/target** diversa da **\/target:module**, sarà possibile importarne i metadati utilizzando l'opzione [\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) e non **\/addmodule**.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio, in quanto non è possibile che un progetto faccia riferimento a un modulo.  Inoltre, non è possibile modificarla a livello di codice.  
  
## Esempio  
 Compilare il file di origine `input.cs` e aggiungere metadati da `metad1.netmodule` e `metad2.netmodule` per creare `out.exe`:  
  
```  
csc /addmodule:metad1.netmodule;metad2.netmodule /out:out.exe input.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Assembly su più file](../Topic/Multifile%20Assemblies.md)   
 [Procedura: Compilare un assembly su più file](../Topic/How%20to:%20Build%20a%20Multifile%20Assembly.md)