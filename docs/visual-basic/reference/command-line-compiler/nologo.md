---
title: "/nologo (Visual Basic) | Microsoft Docs"
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
  - "-nologo compiler option [Visual Basic]"
  - "banners, suppressing startup"
  - "nologo compiler option [Visual Basic]"
  - "/nologo compiler option [Visual Basic]"
ms.assetid: 25ef54b6-d676-4639-a2d2-a747a158bc07
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /nologo (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di sopprimere la visualizzazione delle informazioni sul copyright e dei messaggi informativi durante la compilazione.  
  
## Sintassi  
  
```  
/nologo  
```  
  
## Note  
 Se si specifica `/nologo`, le informazioni sul copyright del compilatore non verranno visualizzate.  Per impostazione predefinita, l'opzione `/nologo` non è attiva.  
  
> [!NOTE]
>  L'opzione `/nologo` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice seguente consente di compilare `T2.vb` senza visualizzare le informazioni sul copyright.  
  
```  
vbc /nologo t2.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)