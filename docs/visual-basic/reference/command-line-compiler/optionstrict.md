---
title: /optionstrict | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /optionstrict
dev_langs:
- VB
helpviewer_keywords:
- -optionstrict compiler option [Visual Basic]
- optionstrict compiler option [Visual Basic]
- /optionstrict compiler option [Visual Basic]
ms.assetid: c7b10086-0fa4-49db-b3c8-4ae0db5957da
caps.latest.revision: 17
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
ms.openlocfilehash: 0394d9c1f4c082271316829ef1d226bd97d136c9
ms.lasthandoff: 03/13/2017

---
# <a name="optionstrict"></a>/optionstrict
Impone la semantica dei tipi rigida per limitare le conversioni implicite.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/optionstrict[+ | -]  
/optionstrict[:custom]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Facoltativo. Il `/optionstrict+` opzione limita la conversione implicita dei tipi. Il valore predefinito per questa opzione è `/optionstrict-`. Il `/optionstrict+` opzione corrisponde al `/optionstrict`. È possibile utilizzare sia per la semantica permissiva.  
  
 `custom`  
 Obbligatorio. Avvisa quando la semantica della lingua ridotta non viene rispettata.  
  
## <a name="remarks"></a>Note  
 Quando `/optionstrict+` è in effetti, solo le conversioni di tipo possono essere apportate in modo implicito. Conversioni di tipi, ad esempio l'assegnazione di narrowing implicite un `Decimal` tipo di oggetto a un oggetto di tipo integer, vengono segnalati come errori.  
  
 Per generare avvisi per conversioni di tipo narrowing, utilizzare `/optionstrict:custom`. Utilizzare `/nowarn:numberlist` per ignorare determinati avvisi e `/warnaserror:numberlist` per considerare determinati avvisi come errori.  
  
### <a name="to-set-optionstrict-in-the-visual-studio-ide"></a>Per impostare /optionstrict nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà.** Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Modificare il valore di **Option Strict** casella.  
  
### <a name="to-set-optionstrict-programmatically"></a>Per impostare /optionstrict a livello di codice  
  
-   Vedere [Option Strict (istruzione)](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `Test.vb` mediante la semantica di tipo strict.  
  
```  
vbc /optionstrict+ test.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)   
 [/warnaserror (Visual Basic)](../../../visual-basic/reference/command-line-compiler/warnaserror.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
