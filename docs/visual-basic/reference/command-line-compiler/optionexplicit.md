---
title: "/optionexplicit | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/optionexplicit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/optionexplicit compiler option [Visual Basic]"
  - "optionexplicit compiler option [Visual Basic]"
  - "-optionexplicit compiler option [Visual Basic]"
ms.assetid: 5d296ab3-bafe-4c4d-9887-78f162ed86c7
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /optionexplicit
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Determina la generazione di errori nel compilatore se le variabili non vengono dichiarate prima di essere utilizzate.  
  
## Sintassi  
  
```  
/optionexplicit[+ | -]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Parametro facoltativo.  Specificare `/optionexplicit+` per richiedere la dichiarazione esplicita delle variabili.  L'opzione `/optionexplicit+` è quella predefinita ed è identica a `/optionexplicit`.  L'opzione `/optionexplicit-` consente la dichiarazione implicita di variabili.  
  
## Note  
 Se nel codice sorgente non è presente un'[Option Explicit Statement](../../../visual-basic/language-reference/statements/option-explicit-statement.md), tramite l'istruzione viene eseguito l'override dell'impostazione del compilatore basato su riga di comando `/optionexplicit`.  
  
### Per impostare \/optionexplicit nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Modificare il valore nella casella **Option Explicit**.  
  
## Esempio  
 Quando si utilizza `/optionexplicit-` viene compilato il codice riportato di seguito.  
  
 [!code-vb[VbVbalrCompiler#5](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/optionexplicit_1.vb)]  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Explicit Statement](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)