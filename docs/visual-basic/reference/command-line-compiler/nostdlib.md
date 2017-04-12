---
title: /nostdlib (Visual Basic) | Documenti di Microsoft
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
- nostdlib compiler option [Visual Basic]
- -nostdlib compiler option [Visual Basic]
- /nostdlib compiler option [Visual Basic]
ms.assetid: 140381b8-dc96-4ad5-ae11-792c9ed0be4d
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 3bacd7d51d12ec6c48dc11ff4b83d842a9e78a30
ms.lasthandoff: 03/13/2017

---
# <a name="nostdlib-visual-basic"></a>/nostdlib (Visual Basic)
Indica al compilatore di non automaticamente fare riferimento alle librerie standard.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/nostdlib  
```  
  
## <a name="remarks"></a>Note  
 Il `/nostdlib` opzione rimuove il riferimento automatico all'assembly System. dll e impedisce al compilatore di lettura del file Vbc. rsp. Tale file, che si trova nella stessa directory del file Vbc.exe: fa riferimento a quelle di uso comune [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] assembly e le importazioni di `System` e `Microsoft.VisualBasic` gli spazi dei nomi.  
  
> [!NOTE]
>  Gli assembly mscorlib. dll e Microsoft.VisualBasic.dll fa sempre riferimento.  
  
> [!NOTE]
>  Il `/nostdlib` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` senza fare riferimento alle librerie standard. È necessario impostare il `_MYTYPE` costante di compilazione condizionale per la stringa "Empty" per rimuovere il `My` oggetto.  
  
```  
vbc /nostdlib /define:_MYTYPE=\"Empty\" T2.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Personalizzazione degli oggetti disponibili in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)
