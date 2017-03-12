---
title: "/help, /? (Visual Basic) | Microsoft Docs"
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
  - "/? compiler option [Visual Basic]"
  - "-help compiler option [Visual Basic]"
  - "/help compiler option [Visual Basic]"
  - "help compiler option [Visual Basic]"
  - "-? compiler option [Visual Basic]"
  - "? compiler option [Visual Basic]"
ms.assetid: eb984aa5-ac98-4d0b-a0d2-24238d7bc8dc
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# /help, /? (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di visualizzare le opzioni del compilatore.  
  
## Sintassi  
  
```  
/help  
' -or-  
/?  
```  
  
## Note  
 Se l'opzione è inclusa in una compilazione, non verrà creato alcun file di output e non avrà luogo alcuna compilazione.  
  
> [!NOTE]
>  L'opzione `/help` non è disponibile dall'interno dell'ambiente di sviluppo di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)], ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice riportato di seguito consente di visualizzare la Guida dalla riga di comando.  
  
```  
vbc /help  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)