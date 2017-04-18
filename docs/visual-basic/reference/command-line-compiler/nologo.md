---
title: /nologo (Visual Basic) | Documenti di Microsoft
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
- -nologo compiler option [Visual Basic]
- banners, suppressing startup
- nologo compiler option [Visual Basic]
- /nologo compiler option [Visual Basic]
ms.assetid: 25ef54b6-d676-4639-a2d2-a747a158bc07
caps.latest.revision: 16
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
ms.openlocfilehash: a0e309a80082f19fb47ccbbb43c00f22c8addd3b
ms.lasthandoff: 03/13/2017

---
# <a name="nologo-visual-basic"></a>/nologo (Visual Basic)
Elimina visualizzazione di informazioni sul copyright e messaggi informativi durante la compilazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/nologo  
```  
  
## <a name="remarks"></a>Note  
 Se si specifica `/nologo`, il compilatore non visualizza informazioni sul copyright. Per impostazione predefinita, l'opzione `/nologo` non è attiva.  
  
> [!NOTE]
>  Il `/nologo` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` e non visualizza informazioni sul copyright.  
  
```  
vbc /nologo t2.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
