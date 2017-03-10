---
title: "/optioncompare | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/optioncompare"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "optioncompare compiler option [Visual Basic]"
  - "-optioncompare compiler option [Visual Basic]"
  - "/optioncompare compiler option [Visual Basic]"
ms.assetid: 7237b766-b44d-4cc5-9a3c-885348a7d9e4
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# /optioncompare
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica la modalità con cui vengono confrontate le stringhe.  
  
## Sintassi  
  
```  
/optioncompare:{binary | text}  
```  
  
## Note  
 È possibile specificare `/optioncompare` in una delle due forme seguenti: `/optioncompare:binary` per utilizzare confronti tra stringhe binarie e `/optioncompare:text` per utilizzare confronti tra stringhe di testo.  Per impostazione predefinita, il compilatore utilizza `/optioncompare:binary`.  
  
 In Microsoft Windows la tabella codici utilizzata determina il criterio di ordinamento binario.  Di seguito viene illustrato un tipico criterio di ordinamento binario.  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 I confronti tra stringhe di testo sono basati su un criterio di ordinamento testuale senza distinzione tra maiuscole e minuscole determinato dalle impostazioni locali del sistema.  Di seguito viene illustrato un tipico criterio di ordinamento testuale.  
  
 `(A = a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
### Per impostare \/optioncompare nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Modificare il valore della casella **Option Compare**.  
  
### Per impostare \/optioncompare a livello di codice  
  
-   Vedere [Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md).  
  
## Esempio  
 Nel codice riportato di seguito viene eseguita la compilazione di P`rojFile.vb` utilizzando i confronti tra stringhe binarie.  
  
```  
vbc /optioncompare:binary projFile.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)