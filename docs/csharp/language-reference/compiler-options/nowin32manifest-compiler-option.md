---
title: "/nowin32manifest (C# Compiler Options) | Microsoft Docs"
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
  - "/nowin32manifest"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nowin32manifest compiler option [C#]"
  - "-nowin32manifest compiler option [C#]"
  - "/nowin32manifest compiler option [C#]"
ms.assetid: 6f06365b-b87b-46a2-b187-b3bfeaf4862d
caps.latest.revision: 15
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /nowin32manifest (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Utilizzare l'opzione **\/nowin32manifest** per istruire il compilatore a non incorporare qualsiasi manifesto dell'applicazione nel file eseguibile.  
  
## Sintassi  
  
```  
/nowin32manifest  
```  
  
## Note  
 Quando viene utilizzata questa opzione, l'applicazione sarà soggetta a virtualizzazione su Windows Vista a meno che non venga fornito un manifesto dell'applicazione in un file di risorsa Win32 file o durante una successiva istruzione di compilazione.  Per ulteriori informazioni sulla virtualizzazione, vedere [New UAC Technologies for Windows Vista](http://msdn.microsoft.com/it-it/80efa4c7-3904-45c5-82e8-2d558fe67db9).  
  
 In Visual Studio, impostare questa opzione nella pagina **Proprietà applicazione** selezionando l'opzione **Crea applicazione senza manifesto** dall'elenco a discesa **Manifesto**.  Per ulteriori informazioni, vedere [Applicazione \(pagina\), Creazione progetti \(C\#\)](/visual-studio/ide/reference/application-page-project-designer-csharp).  
  
 Per ulteriori informazioni sulla creazione di manifesti, vedere [\/win32manifest \(Import a Custom Win32 Manifest File\)](../../../csharp/language-reference/compiler-options/win32manifest-compiler-option.md).  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)