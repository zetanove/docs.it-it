---
title: "Option Explicit Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Explicit"
  - "vb.OptionExplicit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declaring variables, explicit"
  - "forced variable declaration in Option Explicit statement"
  - "Explicit keyword"
  - "explicit variable declaration"
  - "Option Explicit statement"
ms.assetid: e82ac1ad-2cd3-49b2-b985-8bcf016f3fcc
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Option Explicit Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Forza la dichiarazione esplicita di tutte le variabili in un file o consente dichiarazioni implicite delle variabili.  
  
## Sintassi  
  
```  
Option Explicit { On | Off }  
```  
  
## Parti  
 `On`  
 Parametro facoltativo.  Abilita la verifica dell'istruzione `Option Explicit`.  Se `On` o `Off` non è specificato, il valore predefinito è `On`.  
  
 `Off`  
 Parametro facoltativo.  Disabilita la verifica dell'istruzione `Option Explicit`.  
  
## Note  
 Quando in un file è presente l'istruzione `Option Explicit On` o `Option Explicit`, tutte le variabili devono essere dichiarate in modo esplicito utilizzando le istruzioni `Dim` o `ReDim`.  Se si utilizza il nome di una variabile non dichiarata, in fase di compilazione verrà visualizzato un errore.  L'istruzione `Option Explicit Off` consente la dichiarazione implicita di variabili.  
  
 Se utilizzato, è necessario includere l'istruzione `Option Explicit` in un file prima di tutte le altre istruzioni del codice sorgente.  
  
> [!NOTE]
>  L'impostazione di `Option Explicit` su `Off` in genere non è consigliabile.  L'ortografia di un nome di variabile in uno o più i percorsi potrebbe essere errata e generare, in tal modo, risultati imprevisti quando viene eseguito il programma.  
  
## Quando non è presente un'istruzione Option Explicit  
 Se nel codice sorgente non è presente un'istruzione `Option Explicit`, si utilizza l'impostazione **Option Explicit** disponibile in [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic).  Se si utilizza il compilatore della riga di comando, viene utilizzata l'opzione del compilatore [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md).  
  
#### Per impostare Option Explicit nell'IDE  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Impostare il valore nella casella **Option Explicit**.  
  
 Quando si crea un nuovo progetto, l'impostazione **Option Explicit** nella scheda **Compila** viene definita in base all'impostazione **Option Explicit** della finestra di dialogo **Impostazioni predefinite di Visual Basic**.  Per accedere alla finestra di dialogo **Impostazioni predefinite di Visual Basic**, scegliere **Opzioni** dal menu **Strumenti**.  Nella finestra di dialogo **Opzioni** espandere **Progetti e soluzioni**, quindi fare clic su **Impostazioni predefinite di Visual Basic**.  L'impostazione predefinita iniziale in **Impostazioni predefinite di Visual Basic** è `On`.  
  
#### Per impostare Option Explicit nella riga di comando  
  
-   Includere l'opzione del compilatore [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md) nel comando **vbc**.  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Option Explicit` viene utilizzata per imporre la dichiarazione esplicita di tutte le variabili.  Se si utilizza una variabile non dichiarata, in fase di compilazione verrà generato un errore.  
  
 [!code-vb[VbVbalrStatements#47](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/option-explicit-statement_1.vb)]  
  
 [!code-vb[VbVbalrStatements#48](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/option-explicit-statement_2.vb)]  
  
## Vedere anche  
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [ReDim Statement](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [\/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)