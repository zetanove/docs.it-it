---
title: "/optimize (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/optimize"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/optimize compiler option [C#]"
  - "-o compiler option [C#]"
  - "optimize compiler option [C#]"
  - "/o compiler option [C#]"
  - "-optimize compiler option [C#]"
  - "compiler optimization [C#]"
  - "o compiler option [C#]"
ms.assetid: 6dd5b6f2-cd1d-4593-a9f4-1c2ed9404ca0
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /optimize (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/optimize** attiva o disabilita le ottimizzazioni eseguite dal compilatore per ridurre la dimensione del file di output e aumentarne la velocità e l'efficienza.  
  
## Sintassi  
  
```  
/optimize[+ | -]  
```  
  
## Note  
 **\/optimize** comunica inoltre a Common Language Runtime di ottimizzare il codice in fase di esecuzione.  
  
 Per impostazione predefinita, le ottimizzazioni sono disabilitate.  Per attivarle, specificare **\/optimize\+**.  
  
 Durante la compilazione di un modulo per l'utilizzo da parte di un assembly, specificare per **\/optimize** le stesse impostazioni utilizzate per l'assembly.  
  
 **\/o** rappresenta la versione abbreviata di **\/optimize**.  
  
 È possibile utilizzare congiuntamente le opzioni **\/optimize** e [\/debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Modificare la proprietà **Ottimizza codice**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.Optimize%2A>.  
  
## Esempio  
 Compilare `t2.cs`e abilitare le ottimizzazioni del compilatore:  
  
```  
csc t2.cs /optimize  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)