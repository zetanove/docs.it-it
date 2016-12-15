---
title: "@ (C# Compiler Options) | Microsoft Docs"
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
  - "@"
dev_langs: 
  - "CSharp"
  - "CSharp"
helpviewer_keywords: 
  - "response files, specifying for compilation [C#]"
  - "@ compiler option"
ms.assetid: dda4fa9f-a02c-400f-8b6a-d58834e13d7f
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# @ (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione @ consente di specificare un file contenente le opzioni del compilatore e i file di codice sorgente da compilare.  
  
## Sintassi  
  
```  
@response_file  
```  
  
## Argomenti  
 `response_file`  
 Rappresenta un file in cui sono elencate le opzioni del compilatore o i file di codice sorgente da compilare.  
  
## Note  
 Le opzioni del compilatore e i file di codice sorgente verranno elaborati come se fossero stati specificati nella riga di comando.  
  
 Per specificare più file di risposta in una compilazione, definire più opzioni di file di risposta.  Di seguito è riportato un esempio:  
  
```  
@file1.rsp @file2.rsp  
```  
  
 In un file di risposta possono essere presenti, su una stessa riga, più opzioni del compilatore e più file di codice sorgente.  La specifica di una singola opzione del compilatore deve essere contenuta in un'unica riga e non deve occupare più righe.  Nei file di risposta possono essere presenti commenti che iniziano con il simbolo \#.  
  
 La specifica di opzioni del compilatore dall'interno di un file di risposta equivale all'esecuzione di tali comandi dalla riga di comando.  Per ulteriori informazioni, vedere [Compilazione dalla riga di comando](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md).  
  
 Le opzioni di comando vengono elaborate dal compilatore nel momento in cui vengono rilevate.  È pertanto possibile che argomenti della riga di comando si sovrappongano alle opzioni specificate in precedenza nei file di risposta.  Per contro, le opzioni definite in un file di risposta sostituiranno quelle specificate in precedenza alla riga di comando o in altri file di risposta.  
  
 In C\# è disponibile il file csc.rsp, nella stessa directory in cui si trova anche il file csc.exe.  Per ulteriori informazioni sul file csc.rsp, vedere [\/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md).  
  
 Questa opzione del compilatore non può essere impostata nell'ambiente di sviluppo di Visual Studio, né modificata a livello di codice.  
  
## Esempio  
 Di seguito sono riportate alcune righe di un file di risposta di esempio.  
  
```  
# build the first output file  
/target:exe /out:MyExe.exe source1.cs source2.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)