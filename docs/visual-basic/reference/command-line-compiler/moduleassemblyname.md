---
title: "/moduleassemblyname | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "moduleassemblyname compiler option [Visual Basic]"
  - "/moduleassemblyname compiler option [Visual Basic]"
  - "-moduleassemblyname compiler option [Visual Basic]"
ms.assetid: 013a57b6-f425-4dd3-b333-512d72c42f55
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /moduleassemblyname
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica il nome dell'assembly che conterrà questo modulo.  
  
## Sintassi  
  
```  
/moduleassemblyname:assembly_name  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`assembly_name`|Nome dell'assembly di cui questo modulo farà parte.|  
  
## Note  
 L'opzione `/moduleassemblyname` viene elaborata dal compilatore solo se è stata specificata l'opzione `/target:module`.  Determina la creazione di un modulo.  Il modulo creato dal compilatore è valido solo per l'assembly specificato con l'opzione `/moduleassemblyname`.  Se si inserisce il modulo in un assembly diverso, si verificheranno errori di runtime.  
  
 L'opzione `/moduleassemblyname` è necessaria solo quando le seguenti condizioni sono vere:  
  
-   Per un tipo di dati nel modulo è necessario l'accesso a un tipo `Friend` in un assembly a cui si fa riferimento.  
  
-   L'assembly a cui si fa riferimento ha concesso l'accesso assembly Friend all'assembly in cui verrà compilato il modulo.  
  
 Per ulteriori informazioni sulla creazione di un modulo, vedere [\/target](../../../visual-basic/reference/command-line-compiler/target.md).  Per ulteriori informazioni sugli assembly Friend, vedere [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
> [!NOTE]
>  L'opzione `/moduleassemblyname` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dal prompt dei comandi.  
  
## Vedere anche  
 [Procedura: Compilare un assembly su più file](../Topic/How%20to:%20Build%20a%20Multifile%20Assembly.md)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [\/main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)   
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Assembly friend](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)