---
title: "/nostdlib (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "nostdlib compiler option [Visual Basic]"
  - "-nostdlib compiler option [Visual Basic]"
  - "/nostdlib compiler option [Visual Basic]"
ms.assetid: 140381b8-dc96-4ad5-ae11-792c9ed0be4d
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# /nostdlib (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica al compilatore di non fare riferimento automaticamente alle librerie standard.  
  
## Sintassi  
  
```  
/nostdlib  
```  
  
## Note  
 Mediante l'opzione `/nostdlib` viene rimosso il riferimento automatico all'assembly System.dll e viene impedita al compilatore la lettura del file Vbc.rsp.  Il file Vbc.rsp, posizionato nella stessa directory del file Vbc.exe, fa riferimento agli assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] comunemente utilizzati e importa gli spazi dei nomi `System` e `Microsoft.VisualBasic`.  
  
> [!NOTE]
>  Viene fatto riferimento sempre agli assembly Mscorlib.dll e Microsoft.VisualBasic.dll.  
  
> [!NOTE]
>  L'opzione `/nostdlib` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Nel codice riportato di seguito `T2.vb` viene compilato senza riferimenti alle librerie standard.  È necessario impostare la costante `_MYTYPE` di compilazione condizionale sulla stringa "Empty" per rimuovere l'oggetto `My`.  
  
```  
vbc /nostdlib /define:_MYTYPE=\"Empty\" T2.vb  
```  
  
## Vedere anche  
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Customizing Which Objects are Available in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)