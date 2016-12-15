---
title: "/removeintchecks | Microsoft Docs"
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
  - "removeintchecks"
  - "/removeintchecks"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "removeintchecks compiler option [Visual Basic]"
  - "/removeintchecks compiler option [Visual Basic]"
  - "-removeintchecks compiler option [Visual Basic]"
ms.assetid: c1835bd5-1e38-4fba-bd2f-6984774765d4
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /removeintchecks
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di attivare o disattivare il controllo degli errori di overflow per le operazioni sui valori integer.  
  
## Sintassi  
  
```  
/removeintchecks[+ | -]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`+`  &#124; `-`|Parametro facoltativo.  `/removeintchecks-` l'opzione indica al compilatore di controllare tutti i calcoli Integer per gli errori di overflow.  Il valore predefinito è `/removeintchecks-`.<br /><br /> Se si specifica l'opzione `/removeintchecks` o `/removeintchecks+`, non viene eseguito il controllo degli errori e le operazioni sui valori integer risultano più rapide.  Se non viene eseguito il controllo degli errori, tuttavia, e si verifica un overflow delle capacità del tipo di dati, potrebbero essere memorizzati risultati errati senza che venga generato un errore.|  
  
||  
|-|  
|Per impostare \/removeintchecks nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Fare clic sul pulsante **Avanzate**.<br />4.  Modificare il valore della casella **Rimuovi controllo dell'overflow di valori integer**.|  
  
## Esempio  
 Il codice riportato di seguito consente di compilare `Test.vb` disattivando il controllo dell'overflow dei valori integer.  
  
```  
vbc /removeintchecks+ test.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)