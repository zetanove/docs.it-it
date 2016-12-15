---
title: "Esempi di righe di comando di compilazione (Visual Basic) | Microsoft Docs"
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
  - "riga di comando, compilatori"
  - "compilazione, riga di comando"
  - "riga di comando (compilatori)"
  - "compilazione di codice sorgente, da riga di comando"
  - "Visual Basic (compilatore), righe di comando di esempio"
ms.assetid: 5bfbb487-5f47-4267-969a-39dfb917beeb
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Esempi di righe di comando di compilazione (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In alternativa alla compilazione dei programmi [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] da [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], è possibile compilare dalla riga di comando per generare file eseguibili \(exe\) o di libreria a collegamento dinamico \(dll\).  
  
 Il compilatore da riga di comando di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] supporta un insieme completo di opzioni per il controllo dei file di input e di output, degli assembly e delle opzioni di debug e del preprocessore.  Ciascuna opzione è disponibile in due formati intercambiabili: `-``option` e `/``option`.  In questa documentazione è illustrato solo il formato `/``option`.  
  
 Nella tabella riportata di seguito vengono elencati alcuni esempi di righe di comando che è possibile modificare in base alle specifiche esigenze.  
  
|Per|Utilizzo|  
|---------|--------------|  
|Compilare File.vb e creare File.exe|`vbc /reference:Microsoft.VisualBasic.dll File.vb`|  
|Compilare File.vb e creare File.dll|`vbc /target:library File.vb`|  
|Compilare File.vb e creare Mio.exe|`vbc /out:Mio.exe File.vb`|  
|Compilare tutti i file di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] nella directory corrente, con ottimizzazioni attive e il simbolo `DEBUG` definito, generando File2.exe|`vbc /define:DEBUG=1 /optimize /out:File2.exe *.vb`|  
|Compilare tutti i file [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] nella directory corrente, generando una versione di debug di File2.dll senza visualizzare il logo o gli avvisi|`vbc /target:library /out:File2.dll /nowarn /nologo /debug *.vb`|  
|Compilare tutti i file di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] nella directory corrente in Qualcosa.dll|`vbc /target:library /out:Qualcosa.dll *.vb`|  
  
 Durante la compilazione dalla riga di comando, è necessario fare esplicito riferimento alla libreria di runtime di Microsoft [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tramite l'opzione del compilatore `/reference`.  
  
> [!TIP]
>  Quando si compila un progetto utilizzando l'ide di Visual Studio, è possibile visualizzare le informazioni sul comando collegato di **vbc** con le opzioni del compilatore nella finestra di output.  Per visualizzare queste informazioni, aprire [Finestra di dialogo Opzioni, Progetti e soluzioni, Compila ed esegui](/visual-studio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)quindi impostare **Livello di dettaglio output in compilazione progetto MSBuildNormale** o a un livello superiore di dettaglio.  Per ulteriori informazioni, vedere [Procedura: visualizzare, salvare e configurare file di log di compilazione](../Topic/How%20to:%20View,%20Save,%20and%20Configure%20Build%20Log%20Files.md).  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)