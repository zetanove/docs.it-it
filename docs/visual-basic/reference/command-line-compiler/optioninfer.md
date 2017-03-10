---
title: "/optioninfer | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/optioninfer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-optioninfer compiler option [Visual Basic]"
  - "/optioninfer compiler option [Visual Basic]"
  - "optioninfer compiler option [Visual Basic]"
ms.assetid: f6c09db1-0553-464a-abe3-d4510c61d6ed
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# /optioninfer
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di usare l'inferenza del tipo di variabile locale nelle dichiarazioni di variabile.  
  
## Sintassi  
  
```  
/optioninfer[+ | -]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`+`  &#124; `-`|Parametro facoltativo.  Specificare `/optioninfer+` per abilitare l'inferenza del tipo di variabile locale o `/optioninfer-` per bloccarla.  L'opzione `/optioninfer`, senza alcun valore specificato, equivale a `/optioninfer+`.  Il valore predefinito, quando l'opzione `/optioninfer` non è presente, è anche `/optioninfer+`.  Il valore predefinito viene impostato nel file di risposta Vbc.rsp.|  
  
> [!NOTE]
>  È possibile usare l'opzione `/noconfig` per mantenere le impostazioni predefinite interne del compilatore anziché quelle specificate in vbc.rsp.  Il valore predefinito del compilatore per questa opzione è `/optioninfer-`.  
  
## Note  
 Se nel codice sorgente non è presente un'istruzione [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md), l'istruzione esegue l'override dell'impostazione `/optioninfer` del compilatore a riga di comando.  
  
### Per impostare \/optioninfer nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per altre informazioni, vedere [NIB: Managing Project Properties with the Project Designer](http://msdn.microsoft.com/it-it/983f3c18-832f-4666-afec-74b716ff3e0e).  
  
2.  Nella scheda **Compila** modificare il valore nella casella **Option Infer**.  
  
## Esempio  
 Il codice seguente compila `test.vb` con l'inferenza del tipo locale abilitata.  
  
```  
vbc /optioninfer+ test.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)   
 [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic)   
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [Compilazione dalla riga di comando](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)