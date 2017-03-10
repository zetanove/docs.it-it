---
title: "/nowin32manifest (Visual Basic) | Microsoft Docs"
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
  - "/nowin32manifest compiler option [Visual Basic]"
  - "nowin32manifest compiler option [Visual Basic]"
  - "-nowin32manifest compiler option [Visual Basic]"
ms.assetid: c0528aae-83b3-4425-99f0-19448e9843e3
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# /nowin32manifest (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Istruisce il compilatore a non incorporare qualsiasi manifesto dell'applicazione nel file eseguibile.  
  
## Sintassi  
  
```  
/nowin32manifest  
```  
  
## Note  
 Quando viene utilizzata questa opzione, l'applicazione sarà soggetta a virtualizzazione su Windows Vista a meno che non venga fornito un manifesto dell'applicazione in un file di risorsa Win32 file o durante una successiva istruzione di compilazione.  Per ulteriori informazioni sulla virtualizzazione, vedere [ClickOnce Deployment on Windows Vista](/visual-studio/deployment/clickonce-deployment-on-windows-vista).  
  
 Per ulteriori informazioni sulla creazione di manifesti, vedere [\/win32manifest](../../../visual-basic/reference/command-line-compiler/win32manifest.md).  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)