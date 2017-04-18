---
title: /optimize | Documenti di Microsoft
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
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization, enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
caps.latest.revision: 15
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
ms.openlocfilehash: bb89b94ab0d431ed79f94f22afd0bd077728b754
ms.lasthandoff: 03/13/2017

---
# <a name="optimize"></a>/optimize
Abilita o disabilita le ottimizzazioni del compilatore.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/optimize[ + | - ]  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`+` &#124; `-`|Facoltativo. Il `/optimize-` opzione Disabilita le ottimizzazioni del compilatore. Il `/optimize+` opzione consente di abilitarle. Per impostazione predefinita, le ottimizzazioni vengono disabilitate.|  
  
## <a name="remarks"></a>Note  
 Le ottimizzazioni del compilatore rendono il file di output più piccolo, veloce e più efficiente. Tuttavia, poiché le ottimizzazioni comportano una riorganizzazione del codice nel file di output, `/optimize+` può rendere difficoltoso il debug.  
  
 Tutti i moduli generati con `/target:module` per un assembly deve utilizzare lo stesso `/optimize` le impostazioni dell'assembly. Per ulteriori informazioni, vedere [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md).  
  
 È possibile combinare il `/optimize` e `/debug` opzioni.  
  
|Per impostare /optimize nell'ambiente di sviluppo integrato di Visual Studio|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**.<br />     Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Fare clic su **Avanzate** .<br />4.  Modificare il **abilita ottimizzazioni** casella di controllo.|  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` e le ottimizzazioni del compilatore.  
  
```  
vbc t2.vb /optimize  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
