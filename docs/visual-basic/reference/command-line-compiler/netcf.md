---
title: "/netcf | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/netcf"
  - "netcf"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-netcf compiler option [Visual Basic]"
  - "netcf compiler option [Visual Basic]"
  - "/netcf compiler option [Visual Basic]"
ms.assetid: db7cfa59-c315-401c-a59b-0daf355343d6
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /netcf
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Imposta il compilatore in modo che punti a [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)].  
  
## Sintassi  
  
```  
/netcf  
```  
  
## Note  
 L'opzione `/netcf` fa si che il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] punti a [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] piuttosto che alla versione completa di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  La funzionalità del linguaggio, presente solo nella versione completa di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)], è disabilitata.  
  
 L'opzione `/netcf` è stata progettata per essere utilizzata con [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md).  Le funzionalità del linguaggio disabilitate da `/netcf` sono le stesse non presenti nei file a cui si fa riferimento con `/sdkpath`.  
  
> [!NOTE]
>  L'opzione `/netcf` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  L'opzione `/netcf` viene impostata al caricamento di un progetto per dispositivi [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
 L'opzione `/netcf` consente di modificare le seguenti funzionalità del linguaggio:  
  
-   La parola chiave [End \<keyword\> Statement](../../../visual-basic/language-reference/statements/end-keyword-statement.md), che termina l'esecuzione di un programma, è disabilitata.  Il programma riportato di seguito viene compilato ed eseguito correttamente senza `/netcf`,mentre con `/netcf` non riesce in fase di compilazione.  
  
     [!code-vb[VbVbalrCompiler#34](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/netcf_1.vb)]  
  
-   L'associazione tardiva, in tutte le sue forme, viene disabilitata.  Gli errori in fase di compilazione vengono generati quando vengono rilevati scenari di associazione tardiva riconosciuti.  Il programma riportato di seguito viene compilato ed eseguito correttamente senza `/netcf`,mentre con `/netcf` non riesce in fase di compilazione.  
  
     [!code-vb[VbVbalrCompiler#35](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/netcf_2.vb)]  
  
-   I modificatori [Auto](../../../visual-basic/language-reference/modifiers/auto.md), [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md) e [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md) sono disabilitati.  La sintassi dell'[Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md), inoltre, viene modificata in `Declare Sub|Function name Lib "library" [Alias "alias"] [([arglist])]`.  Nel codice riportato di seguito viene illustrato l'effetto di `/netcf` su una compilazione:  
  
     [!code-vb[VbVbalrCompiler#36](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/netcf_3.vb)]  
  
-   L'utilizzo di parole chiave Visual Basic 6.0 rimosse da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] genera un errore diverso quando si utilizza `/netcf`.  Ciò influisce sui messaggi di errore visualizzati per le seguenti parole chiave:  
  
    -   `Open`  
  
    -   `Close`  
  
    -   `Put`  
  
    -   `Print`  
  
    -   `Write`  
  
    -   `Input`  
  
    -   `Lock`  
  
    -   `Unlock`  
  
    -   `Seek`  
  
    -   `Width`  
  
    -   `Name`  
  
    -   `FreeFile`  
  
    -   `EOF`  
  
    -   `Loc`  
  
    -   `LOF`  
  
    -   `Line`  
  
## Esempio  
 Nel codice riportato di seguito viene eseguita la compilazione di `Myfile.vb` con [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] utilizzando le versioni di Mscorlib.dll e Microsoft.VisualBasic.dll presenti nella directory di installazione predefinita di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] nell'unità C.  Generalmente, viene utilizzata la versione più recente di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)].  
  
```  
vbc /netcf /sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)