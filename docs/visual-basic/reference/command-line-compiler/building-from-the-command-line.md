---
title: "Compilazione dalla riga di comando (Visual Basic) | Microsoft Docs"
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
  - "compilazioni [Visual Basic], riga di comando"
  - "Visual Basic (compilatore), informazioni"
  - "riga di comando [Visual Basic], compilatori"
  - "riga di comando [Visual Basic], compilazione da"
  - "riga di comando [Visual Basic], compilazioni"
  - "compilatori, richiamo dalla riga di comando"
  - "compilazioni dalla riga di comando"
  - "compilazione di codice sorgente"
  - "compilatori della riga di comando, Visual Basic"
  - "riga di comando [Visual Basic], Visual Basic"
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Compilazione dalla riga di comando (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un progetto [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è costituito da uno o più file di origine distinti.  Durante il processo noto come compilazione, questi file vengono riuniti in un package, ovvero un singolo file eseguibile che può essere eseguito come un'applicazione.  
  
 In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è disponibile un compilatore da riga di comando come alternativa alla compilazione dei programmi dall'interno dell'ambiente di sviluppo integrato \(IDE\) di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)].  Il compilatore basato su riga di comando è progettato per situazioni che non richiedono l'intero insieme di funzionalità dell'ambiente di sviluppo integrato, ad esempio quando si utilizza o scrive codice per computer con limitata disponibilità di memoria di sistema o spazio su disco.  
  
 Durante la compilazione dalla riga di comando, è necessario fare esplicito riferimento alla libreria di runtime di Microsoft [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tramite l'opzione del compilatore `/reference`.  
  
 Per compilare file di origine dall'interno dell'ambiente di sviluppo integrato di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], scegliere il comando **Compila** dal menu **Compila**.  
  
> [!TIP]
>  Quando si compila i file di progetto utilizzando l'ide di Visual Studio, è possibile visualizzare le informazioni sul comando collegato di **vbc** e le relative opzioni nella finestra di output.  Per visualizzare queste informazioni, aprire [Finestra di dialogo Opzioni, Progetti e soluzioni, Compila ed esegui](/visual-studio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)quindi impostare **Livello di dettaglio output in compilazione progetto MSBuildNormale** o a un livello superiore di dettaglio.  Per ulteriori informazioni, vedere [Procedura: visualizzare, salvare e configurare file di log di compilazione](../Topic/How%20to:%20View,%20Save,%20and%20Configure%20Build%20Log%20Files.md).  
  
 È possibile compilare i file di progetto \(vbproj\) a un prompt dei comandi tramite MSBuild.  Per ulteriori informazioni, vedere [Command\-Line Reference](/visual-studio/msbuild/msbuild-command-line-reference) e [Walkthrough: Using MSBuild](../Topic/Walkthrough:%20Using%20MSBuild.md).  
  
## In questa sezione  
 [How to: Invoke the Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)  
 Viene descritto come richiamare il compilatore dalla riga di comando dalla finestra di MS\-DOS o da una specifica sottodirectory.  
  
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 Viene fornito un elenco di righe di comando di esempio che è possibile modificare e utilizzare.  
  
## Sezioni correlate  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)  
 Vengono forniti elenchi di opzioni del compilatore, ordinate alfabeticamente o in base alla funzione.  
  
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 Viene descritto come compilare particolari sezioni di codice.  
  
 [Compilazione e pulizia di progetti e soluzioni in Visual Studio](/visual-studio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)  
 Viene descritto come organizzare il contenuto delle diverse compilazioni, come scegliere le proprietà del progetto e assicurarsi che la compilazione dei progetti avvenga nell'ordine corretto.