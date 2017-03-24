---
title: /quiet | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /quiet
- quiet
dev_langs:
- VB
helpviewer_keywords:
- -quiet compiler option [Visual Basic]
- /quiet compiler option [Visual Basic]
- quiet compiler option [Visual Basic]
ms.assetid: 5d77fa23-4c50-4708-8535-649912b098e8
caps.latest.revision: 11
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
ms.openlocfilehash: feafed7464248c38ec70087795a28ead8b8793f3
ms.lasthandoff: 03/13/2017

---
# <a name="quiet"></a>/quiet
Impedisce al compilatore di visualizzare codice per avvisi ed errori relativi alla sintassi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/quiet  
```  
  
## <a name="remarks"></a>Note  
 Per impostazione predefinita, l'opzione `/quiet` non è attiva. Quando il compilatore segnala un errore di sintassi o un avviso, viene visualizzata anche la riga del codice sorgente. Per le applicazioni che analizzano l'output del compilatore, potrebbe essere più utile per il compilatore di generare solo il testo della diagnostica.  
  
 Nell'esempio seguente, `Module1` genera un errore che include il codice sorgente se compilato senza `/quiet`.  
  
```  
Module Module1  
    Sub Main()  
        x()  
    End Sub  
End Module  
```  
  
 Output:  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
 `x`  
  
 `~`  
  
 Compilato con `/quiet`, il compilatore restituisce solo le operazioni seguenti:  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
> [!NOTE]
>  Il `/quiet` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` e non visualizzare il codice per diagnostica relativa alla sintassi:  
  
```  
vbc /quiet t2.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
