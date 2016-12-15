---
title: "/baseaddress | Microsoft Docs"
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
  - "/baseaddress"
  - "baseaddress"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-baseaddress compiler option [Visual Basic]"
  - "/baseaddress compiler option [Visual Basic]"
  - "baseaddress compiler option [Visual Basic]"
ms.assetid: c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /baseaddress
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di specificare un indirizzo di base predefinito alla creazione di una DLL.  
  
## Sintassi  
  
```  
/baseaddress:address  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`address`|Obbligatorio.  Indirizzo di base della DLL.  Questo indirizzo deve essere specificato sotto forma di numero esadecimale.|  
  
## Note  
 L'indirizzo di base predefinito di una DLL viene impostato mediante [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  
  
 Tenere presente che, in questo indirizzo, l'elemento meno significativo viene arrotondato.  Se, ad esempio, si specifica 0x11110001, verrà automaticamente effettuato l'arrotondamento a 0x11110000.  
  
 Per completare il processo di firma di una DLL, utilizzare l'opzione `–R` dello strumento Nome sicuro \(Sn.exe\).  
  
 Questa opzione viene ignorata se la destinazione non corrisponde a una DLL.  
  
||  
|-|  
|Per impostare \/baseaddress nell'IDE di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Scegliere **Avanzate**.<br />4.  Modificare il valore della casella **Indirizzo di base DLL**. **Note:**      La casella **Indirizzo di base DLL** è di sola lettura, a meno che la destinazione non sia una DLL.|  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Sn.exe \(Strong Name Tool\)](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md)