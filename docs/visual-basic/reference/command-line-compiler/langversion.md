---
title: "/langversion (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/langversion compiler option [Visual Basic]"
  - "langversion compiler option [Visual Basic]"
  - "-langversion compiler option [Visual Basic]"
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /langversion (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Fa in modo che il compilatore accetti solo sintassi inclusa nella versione di lingua specificata di Visual Basic.  
  
## Sintassi  
  
```  
/langversion:version  
```  
  
## Argomenti  
 `version`  
 Obbligatorio.  Versione di lingua da utilizzare durante la compilazione.  I valori accettati sono `9`, `9.0`, `10` e `10.0`.  
  
## Note  
 L'opzione `/langversion` specifica quale sintassi è accettata dal compilatore.  Se, ad esempio, si specifica che la versione di lingua è 9.0, il compilatore genera errori relativi alla sintassi valida solo nella versione 10.0 e successive.  
  
 È possibile utilizzare questa opzione quando si sviluppano applicazioni destinate a versioni diverse di .NET Framework.  Se, ad esempio, la destinazione è .NET Framework 3.5, è possibile utilizzare questa opzione per assicurarsi di non utilizzare la sintassi dalla versione di lingua 10.0.  
  
 È possibile impostare `/langversion` direttamente utilizzando solo la riga di comando.  Per ulteriori informazioni, vedere [Sviluppo per una versione specifica di .NET Framework](/visual-studio/ide/targeting-a-specific-dotnet-framework-version).  
  
## Esempio  
 Il codice seguente compila `sample.vb` per Visual Basic 9.0.  
  
```  
vbc /langversion:9.0 sample.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Sviluppo per una versione specifica di .NET Framework](/visual-studio/ide/targeting-a-specific-dotnet-framework-version)