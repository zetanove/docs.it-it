---
title: /noconfig | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- noconfig compiler option [Visual Basic]
- -noconfig compiler option [Visual Basic]
- /noconfig compiler option [Visual Basic]
ms.assetid: a7405067-bd21-4171-adf4-a126fa3ad6c3
caps.latest.revision: 15
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 304d0e7fc787adb1d7776a2c047090ffc230fcc1
ms.lasthandoff: 03/13/2017

---
# <a name="noconfig"></a>/noconfig
Specifica che il compilatore non automaticamente fare riferimento a quelle di uso comune [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] assembly o importazione di `System` e `Microsoft.VisualBasic` gli spazi dei nomi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/noconfig  
```  
  
## <a name="remarks"></a>Note  
 Il `/noconfig` opzione indica al compilatore di non eseguire la compilazione con il file Vbc. rsp, che si trova nella stessa directory del file Vbc.exe. Il file Vbc. rsp fa riferimento il diffuso [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] assembly e le importazioni di `System` e `Microsoft.VisualBasic` gli spazi dei nomi. Il compilatore fa riferimento in modo implicito all'assembly System. dll, a meno che il `/nostdlib` opzione specificata. Il `/nostdlib` opzione indica al compilatore di non compilare con Vbc. rsp o automaticamente fare riferimento all'assembly System. dll.  
  
> [!NOTE]
>  Gli assembly mscorlib. dll e Microsoft.VisualBasic.dll fa sempre riferimento.  
  
 È possibile modificare il file Vbc. rsp per specificare ulteriori opzioni del compilatore che devono essere incluse in ogni compilazione Vbc.exe (tranne quando si specifica il `/noconfig` opzione). Per altre informazioni, vedere [@ (specifica di un file di risposta)](../../../visual-basic/reference/command-line-compiler/specify-response-file.md).  
  
 Il compilatore elabora le opzioni passate al `vbc` ultimo comando. Di conseguenza, le opzioni della riga di comando sostituiscono l'impostazione dell'opzione stesso in tale file.  
  
> [!NOTE]
>  Il `/noconfig` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="see-also"></a>Vedere anche  
 [/nostdlib (Visual Basic)](../../../visual-basic/reference/command-line-compiler/nostdlib.md)   
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [@ (Specify Response File)](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)   
 [/Reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)
