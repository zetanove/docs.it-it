---
title: "/sdkpath | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "sdkpath"
  - "/sdkpath"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-sdkpath compiler option [Visual Basic]"
  - "/sdkpath compiler option [Visual Basic]"
  - "sdkpath compiler option [Visual Basic]"
ms.assetid: fec8a3f1-b791-4a37-8af7-344859f8212d
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# /sdkpath
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di specificare il percorso di Mscorlib.dll e Microsoft.VisualBasic.dll.  
  
## Sintassi  
  
```  
/sdkpath:path  
```  
  
## Argomenti  
 `path`  
 Directory contenente le versioni di Mscorlib.dll e Microsoft.VisualBasic.dll da utilizzare per la compilazione.  Il percorso non viene verificato fino al caricamento.  Racchiudere il nome della directory tra virgolette \(""\) se contiene uno spazio.  
  
## Note  
 Questa opzione indica al compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] di caricare i file Mscorlib.dll e Microsoft.VisualBasic.dll da un percorso non predefinito.  L'opzione `/sdkpath`  è stata progettata per essere utilizzata con [\/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md).  In [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] vengono utilizzate versioni diverse delle librerie di supporto per evitare l'uso tipi e di funzionalità del linguaggio non disponibili nei dispositivi.  
  
> [!NOTE]
>  L'opzione `/sdkpath` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  L'opzione `/sdkpath` viene impostata al caricamento di un progetto per dispositivi [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 L'opzione del compilatore `/vbruntime` consente di specificare che il compilatore esegue la compilazione senza un riferimento alla libreria di runtime di Visual Basic.  Per ulteriori informazioni, vedere [\/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md).  
  
## Esempio  
 Nel codice riportato di seguito viene eseguita la compilazione di `Myfile.vb` con [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] utilizzando le versioni di Mscorlib.dll e Microsoft.VisualBasic.dll presenti nella directory di installazione predefinita di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] nell'unità C.  Generalmente, viene utilizzata la versione più recente di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)].  
  
```  
vbc /netcf /sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)   
 [\/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)