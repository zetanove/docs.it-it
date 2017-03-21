---
title: /optionexplicit | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /optionexplicit
dev_langs:
- VB
helpviewer_keywords:
- /optionexplicit compiler option [Visual Basic]
- optionexplicit compiler option [Visual Basic]
- -optionexplicit compiler option [Visual Basic]
ms.assetid: 5d296ab3-bafe-4c4d-9887-78f162ed86c7
caps.latest.revision: 16
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
ms.openlocfilehash: cfdad72c21b7886f9ea8a2d46e7c457087e7049d
ms.lasthandoff: 03/13/2017

---
# <a name="optionexplicit"></a>/optionexplicit
Indica al compilatore per segnalare gli errori se le variabili non vengono dichiarate prima che vengano utilizzati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/optionexplicit[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Facoltativo. Specificare `/optionexplicit+` per richiedere la dichiarazione esplicita delle variabili. Il `/optionexplicit+` opzione è l'impostazione predefinita ed è identico `/optionexplicit`. Il `/optionexplicit-` opzione consente la dichiarazione implicita delle variabili.  
  
## <a name="remarks"></a>Note  
 Se il file di codice di origine contiene un [istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md), l'istruzione esegue l'override di `/optionexplicit` impostazione del compilatore da riga di comando.  
  
### <a name="to-set-optionexplicit-in-the-visual-studio-ide"></a>Per impostare /optionexplicit nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Modificare il valore di **Option Explicit** casella.  
  
## <a name="example"></a>Esempio  
 Il codice seguente viene compilato quando `/optionexplicit-` viene utilizzato.  
  
 [!code-vb[VbVbalrCompiler n.&5;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/optionexplicit_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
