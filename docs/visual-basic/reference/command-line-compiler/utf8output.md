---
title: /utf8output (Visual Basic) | Documenti di Microsoft
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
- -utf8output compiler option [Visual Basic]
- utf8output compiler option [Visual Basic]
- /utf8output compiler option [Visual Basic]
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
caps.latest.revision: 11
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
ms.openlocfilehash: 89f41527703df781f32015f386bf87c1383d9769
ms.lasthandoff: 03/13/2017

---
# <a name="utf8output-visual-basic"></a>/utf8output (Visual Basic)
Visualizza l'output del compilatore usando la codifica UTF-8.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/utf8output[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Facoltativo. Il valore predefinito per questa opzione è `/utf8output-`, pertanto non verrà utilizzata la codifica UTF-8. Specifica di `/utf8output` equivale a specificare `/utf8output+`.  
  
## <a name="remarks"></a>Note  
 In alcune configurazioni internazionali, output del compilatore non può essere visualizzato correttamente nella console. In tali situazioni, utilizzare `/utf8output` e reindirizzare l'output del compilatore a un file.  
  
> [!NOTE]
>  Il `/utf8output` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `In.vb` e indica al compilatore di visualizzare l'output utilizzando la codifica UTF-8.  
  
```  
vbc /utf8output in.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
