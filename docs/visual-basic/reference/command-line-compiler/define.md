---
title: "/define (Visual Basic) | Microsoft Docs"
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
  - "-d compiler option [Visual Basic]"
  - "/d compiler option [Visual Basic]"
  - "-define compiler option [Visual Basic]"
  - "d compiler option [Visual Basic]"
  - "/define compiler option [Visual Basic]"
  - "define compiler option [Visual Basic]"
ms.assetid: f735c57d-1cf9-4f2f-a26f-0de630fd4077
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /define (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Definisce le costanti del compilatore condizionali.  
  
## Sintassi  
  
```  
/define:["]symbol[=value][,symbol[=value]]["] ' -or- /d:["]symbol[=value][,symbol[=value]]["]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`symbol`|Obbligatorio.  Il simbolo da definire.|  
|`value`|Facoltativa.  Il valore da assegnare a `symbol`.  Se `value` è una stringa, deve essere racchiuso tra sequenze di barre rovesciate\/virgolette \(\\"\) anziché tra virgolette.  Se non è specificato un valore, è considerato True.|  
  
## Note  
 L'opzione `/define` ha un effetto analogo all'uso di una direttiva per il preprocessore `#Const` nel file di origine, ad eccezione del fatto che le costanti definite con `/define` sono pubbliche e si applicano a tutti i file del progetto.  
  
 È possibile usare i simboli creati mediante questa opzione con la direttiva `#If`...`Then`...`#Else` per eseguire la compilazione condizionale dei file di origine.  
  
 `/d` è la versione abbreviata di `/define`.  
  
 È possibile definire più simboli con `/define`, separando le definizioni dei simboli con una virgola.  
  
||  
|-|  
|Per impostare \/define nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per altre informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Scegliere **Avanzate**.<br />4.  Modificare il valore nella casella **Costanti personalizzate**.|  
  
## Esempio  
 Nel codice seguente sono definite e usate due costanti di compilazione condizionale.  
  
 [!code-vb[VbVbalrCompiler#45](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/define_1.vb)]  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [\#Const Directive](../../../visual-basic/language-reference/directives/const-directive.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)