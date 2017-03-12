---
title: "/win32icon | Microsoft Docs"
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
  - "win32icon compiler option [Visual Basic]"
  - "-win32icon compiler option [Visual Basic]"
  - "/win32icon compiler option [Visual Basic]"
ms.assetid: aecaab01-9353-46c5-941c-6edabd4eff92
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# /win32icon
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di inserire un file ICO nel file di output.  Questo file .ico rappresenta il file di output in **Esplora file**.  
  
## Sintassi  
  
```  
/win32icon:filename  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`filename`|File ICO da aggiungere al file di output.  Racchiudere il nome file tra virgolette \(""\) se contiene uno spazio.|  
  
## Note  
 È possibile creare un file ICO con il compilatore di risorse \(RC\) di Microsoft Windows  che viene richiamato quando si compila un programma Visual C\+\+. Il file ICO viene creato sulla base del file RC.  Le opzioni `/win32icon` e `/win32resource` si escludono reciprocamente.  
  
 Vedere [\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md) per un riferimento a un file di risorse [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] o [\/resource](../../../visual-basic/reference/command-line-compiler/resource.md) per la connessione a un file di risorse [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  Per informazioni sull'importazione di un file RES, vedere [\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md).  
  
||  
|-|  
|Per impostare \/win32icon nell'IDE di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Applicazione**.<br />3.  Modificare il valore della casella **Icona**.|  
  
## Esempio  
 Il codice riportato di seguito consente di compilare `In.vb` e di collegare il file `Rf.ico`.  
  
```  
vbc /win32icon:rf.ico in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)