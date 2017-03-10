---
title: "/win32resource | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/win32resource"
  - "win32resource"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/win32resource compiler option [Visual Basic]"
  - "-win32resource compiler option [Visual Basic]"
  - "win32resource compiler option [Visual Basic]"
ms.assetid: e226946d-19ce-4cc9-91f5-aed24f77aa2b
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# /win32resource
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Inserisce un file di risorse Win32 nel file di output.  
  
## Sintassi  
  
```  
/win32resource:filename  
```  
  
## Argomenti  
 `filename`  
 Nome del file di risorse da aggiungere al file di output.  Racchiudere il nome file tra virgolette \(""\) se contiene uno spazio.  
  
## Note  
 È possibile creare un file di risorse Win32 con il compilatore di risorse \(RC\) di Microsoft Windows.  
  
 Una risorsa Win32 può contenere le informazioni della bitmap o della versione \(un'icona\) che consente di identificare l'applicazione in **Esplora file**.  Se l'opzione `/win32resource` non viene specificata, durante la compilazione verranno generate informazioni di versione basate sulla versione dell'assembly.  Le opzioni `/win32resource` e `/win32icon` si escludono reciprocamente.  
  
 Vedere [\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md) per un riferimento a un file di risorse [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] o [\/resource](../../../visual-basic/reference/command-line-compiler/resource.md) per la connessione a un file di risorse [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)].  
  
> [!NOTE]
>  L'opzione `/win32resource` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice seguente consente di compilare `In.vb` e di allegare il file di risorse Win32 `Rf.res`:  
  
```  
vbc /win32resource:rf.res in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)