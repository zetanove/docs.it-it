---
title: "/noconfig | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "noconfig compiler option [Visual Basic]"
  - "-noconfig compiler option [Visual Basic]"
  - "/noconfig compiler option [Visual Basic]"
ms.assetid: a7405067-bd21-4171-adf4-a126fa3ad6c3
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# /noconfig
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che il compilatore non deve contenere un riferimento automatico agli assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] usati comunemente o non deve importare gli spazi dei nomi `System` e `Microsoft.VisualBasic`.  
  
## Sintassi  
  
```  
/noconfig  
```  
  
## Note  
 L'opzione `/noconfig` indica al compilatore di non eseguire la compilazione utilizzando il file Vbc.rsp, disponibile nella stessa directory in cui si trova il file Vbc.exe.  Il file Vbc.rsp contiene un riferimento agli assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] usati comunemente e importa gli spazi dei nomi `System` e `Microsoft.VisualBasic`.  Il compilatore fa implicitamente riferimento all'assembly System.dll, a meno che non venga specificata l'opzione `/nostdlib`.  L'opzione `/nostdlib` indica al compilatore di non compilare con Vbc.rsp né di fare automaticamente riferimento all'assembly System.dll.  
  
> [!NOTE]
>  Viene fatto riferimento sempre agli assembly Mscorlib.dll e Microsoft.VisualBasic.dll.  
  
 È possibile modificare il file Vbc.rsp per specificare ulteriori opzioni del compilatore da includere in ogni compilazione di Vbc.exe, ad eccezione di quando si specifica `/noconfig`.  Per ulteriori informazioni, vedere [@ \(Specify Response File\)](../../../visual-basic/reference/command-line-compiler/specify-response-file.md).  
  
 Le opzioni passate al comando `vbc` vengono elaborate nel compilatore per ultime.  Le opzioni della riga di comando eseguono pertanto l'override delle impostazioni relative alle stesse opzioni nel file Vbc.rsp.  
  
> [!NOTE]
>  L'opzione `/noconfig` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Vedere anche  
 [\/nostdlib](../../../visual-basic/reference/command-line-compiler/nostdlib.md)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [@ \(Specify Response File\)](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)