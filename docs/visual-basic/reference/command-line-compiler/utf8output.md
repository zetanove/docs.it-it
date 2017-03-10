---
title: "/utf8output (Visual Basic) | Microsoft Docs"
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
  - "-utf8output compiler option [Visual Basic]"
  - "utf8output compiler option [Visual Basic]"
  - "/utf8output compiler option [Visual Basic]"
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# /utf8output (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di visualizzare l'output del compilatore mediante la codifica UTF\-8.  
  
## Sintassi  
  
```  
/utf8output[+ | -]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Parametro facoltativo.  L'impostazione predefinita per questa opzione è `/utf8output-` che indica che non verrà utilizzata la codifica UTF\-8.  La specifica di `/utf8output` equivale a `/utf8output+`.  
  
## Note  
 Alcune configurazioni internazionali non consentono di visualizzare correttamente l'output del compilatore nella console.  In questi casi è necessario utilizzare l'opzione `/utf8output` e reindirizzare l'output del compilatore a un file.  
  
> [!NOTE]
>  L'opzione `/utf8output` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice riportato di seguito consente di compilare `In.vb` e di visualizzare l'output del compilatore utilizzando la codifica UTF\-8.  
  
```  
vbc /utf8output in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)