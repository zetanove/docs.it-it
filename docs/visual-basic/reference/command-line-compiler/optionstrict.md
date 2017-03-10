---
title: "/optionstrict | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/optionstrict"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-optionstrict compiler option [Visual Basic]"
  - "optionstrict compiler option [Visual Basic]"
  - "/optionstrict compiler option [Visual Basic]"
ms.assetid: c7b10086-0fa4-49db-b3c8-4ae0db5957da
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# /optionstrict
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di attivare la semantica dei tipi rigorosa per limitare le conversioni implicite dei tipi.  
  
## Sintassi  
  
```  
/optionstrict[+ | -]  
/optionstrict[:custom]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Parametro facoltativo.  L'opzione `/optionstrict+` limita la conversione implicita dei tipi.  Il valore predefinito per questa opzione è `/optionstrict-`.  L'opzione `/optionstrict+` corrisponde a `/optionstrict`.  È possibile utilizzare entrambe per la semantica dei tipi permissiva.  
  
 `custom`  
 Obbligatorio.  Viene visualizzato un avviso quando la semantica del linguaggio rigorosa non viene rispettata.  
  
## Note  
 Quando è attiva l'opzione `/optionstrict+`, possono essere eseguite in modo implicito solo le conversioni in tipi di dati più grandi.  Le conversioni implicite in tipi di dati più piccoli, come ad esempio l'assegnazione di un oggetto di tipo `Decimal` a un oggetto di tipo integer, vengono segnalate come errori.  
  
 Per generare avvisi per conversioni in tipi di dati più piccoli, utilizzare `/optionstrict:custom`.  Utilizzare `/nowarn:numberlist` per ignorare determinati avvisi e `/warnaserror:numberlist` per considerare determinati avvisi come errori.  
  
### Per impostare \/optionstrict nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto** Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Modificare il valore della casella **Option Strict**.  
  
### Per impostare \/optionstrict a livello di codice  
  
-   Vedere [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
## Esempio  
 Il codice riportato di seguito consente di compilare `Test.vb` utilizzando la semantica dei tipi rigorosa.  
  
```  
vbc /optionstrict+ test.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [\/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [\/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [\/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)   
 [\/warnaserror](../../../visual-basic/reference/command-line-compiler/warnaserror.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](/visual-studio/ide/reference/visual-basic-defaults-projects-options-dialog-box)