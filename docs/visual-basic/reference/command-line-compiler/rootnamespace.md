---
title: "/rootnamespace | Microsoft Docs"
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
  - "/rootnamespace"
  - "rootnamespace"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/rootnamespace compiler option [Visual Basic]"
  - "-rootnamespace compiler option [Visual Basic]"
  - "rootnamespace compiler option [Visual Basic]"
ms.assetid: e9245edf-6bef-420d-a7c7-324117752783
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /rootnamespace
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica uno spazio dei nomi per tutte le dichiarazioni di tipi.  
  
## Sintassi  
  
```  
/rootnamespace:namespace  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`namespace`|Il nome dello spazio dei nomi in cui includere tutte le dichiarazioni dei tipi per il progetto corrente.|  
  
## Note  
 Se si utilizza il file eseguibile Visual Studio \(Devenv.exe\) per la compilazione di un progetto creato nell'ambiente di sviluppo integrato di Visual Studio, `/rootnamespace` consente di specificare il valore della proprietà <xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A>.  Per ulteriori informazioni, vedere [Opzioni della riga di comando devenv](/visual-studio/ide/reference/devenv-command-line-switches).  
  
 Utilizzare Disassembler MSIL di Common Language Runtime \(`ldasm.exe`\) per visualizzare i nomi degli spazi dei nomi nel file di output.  
  
||  
|-|  
|Per impostare l'opzione \/rootnamespace nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Applicazione**.<br />3.  Modificate il valore della casella **Spazio dei nomi di primo livello**.|  
  
## Esempio  
 Il codice riportato di seguito compila `In.vb` e include tutte le dichiarazioni dei tipi nello spazio dei nomi `mynamespace`  
  
```  
vbc /rootnamespace:mynamespace in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Ildasm.exe \(IL Disassembler\)](../Topic/Ildasm.exe%20\(IL%20Disassembler\).md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)