---
title: "/nostdlib (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/nostdlib"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nostdlib compiler option [C#]"
  - "-nostdlib compiler option [C#]"
  - "/nostdlib compiler option [C#]"
ms.assetid: ec197989-fa49-4725-a455-e06b551eb65f
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# /nostdlib (C# Compiler Options)
**\/nostdlib** impedisce l'importazione di mscorlib.dll, che definisce l'intero spazio dei nomi System.  
  
## Sintassi  
  
```  
/nostdlib[+ | -]  
```  
  
## Note  
 Usare questa opzione se si vuole definire o creare uno spazio dei nomi e oggetti System personalizzati.  
  
 Se non si specifica **\/nostdlib**, mscorlib.dll verrà importata nel programma \(equivale a specificare **\/nostdlib\-**\). Specificare **\/nostdlib** equivale a specificare **\/nostdlib\+**.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina di proprietà **Compilazione**.  
  
3.  Fare clic su **Avanzate**.  
  
4.  Modificare la proprietà **Ometti riferimenti a libreria standard \(mscorlib.dll\)**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.NoStdLib%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)