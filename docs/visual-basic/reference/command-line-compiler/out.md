---
title: "/out (Visual Basic) | Microsoft Docs"
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
  - "/out compiler option [Visual Basic]"
  - "-out compiler option [Visual Basic]"
  - "out compiler option [Visual Basic]"
ms.assetid: 9f148c15-0909-4cb8-a2db-777f8a8b45ae
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /out (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica il nome del file di output.  
  
## Sintassi  
  
```  
/out:filename  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`filename`|Obbligatorio.  Nome del file di output creato dal compilatore.  Se il nome file contiene uno spazio, racchiudere il nome tra virgolette \(" "\).|  
  
## Note  
 Specificare il nome completo e l'estensione del file che si desidera creare.  Se non viene specificato alcun nome, il nome del file EXE corrisponderà a quello del file di codice sorgente contenente la routine `Sub Main`, mentre il nome del file DLL corrisponderà a quello del primo file di codice sorgente.  
  
 Se si specifica un nome file senza una'estensione exe o dll, l'estensione viene aggiunta automaticamente dal compilatore, in base al valore specificato per l'opzione del compilatore `/target`.  
  
||  
|-|  
|Per impostare \/out nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Applicazione**.<br />3.  Modificare il valore della casella **Nome assembly**.|  
  
## Esempio  
 Il codice che segue compila `T2.vb` e crea il file di output `T2.exe`.  
  
```  
vbc t2.vb /out:t3.exe  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)