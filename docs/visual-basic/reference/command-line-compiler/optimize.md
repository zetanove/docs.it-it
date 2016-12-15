---
title: "/optimize | Microsoft Docs"
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
  - "optimize compiler option [Visual Basic]"
  - "/optimize compiler option [Visual Basic]"
  - "optimization, enabling"
  - "-optimize compiler option [Visual Basic]"
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /optimize
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di abilitare o disabilitare le ottimizzazioni del compilatore.  
  
## Sintassi  
  
```  
/optimize[ + | - ]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`+`  &#124; `-`|Parametro facoltativo.  L'opzione `/optimize-` consente di disabilitare le ottimizzazioni del compilatore,  mentre l'opzione`/optimize+` consente di abilitarle.  Per impostazione predefinita, le ottimizzazioni sono disabilitate.|  
  
## Note  
 Le ottimizzazioni del compilatore consentono di ridurre le dimensioni del file di output e di renderlo più veloce e più efficiente.  Poiché le ottimizzazioni tuttavia determinano una ridisposizione del codice nel file di output, l'opzione `/optimize+` può rendere difficoltoso il debug.  
  
 Tutti i moduli generati con `/target:module` per un assembly devono utilizzare le stesse impostazioni `/optimize` dell'assembly.  Per ulteriori informazioni, vedere [\/target](../../../visual-basic/reference/command-line-compiler/target.md).  
  
 È possibile combinare le opzioni `/optimize` e `/debug`.  
  
||  
|-|  
|Per impostare \/optimize nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.<br />     Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Fare clic sul pulsante **Avanzate**.<br />4.  Modificare la casella di controllo **Attiva ottimizzazioni**.|  
  
## Esempio  
 Il codice riportato di seguito compila `T2.vb` e attiva le ottimizzazioni del compilatore.  
  
```  
vbc t2.vb /optimize  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/debug](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)