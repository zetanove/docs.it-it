---
title: /define (Visual Basic) | Documenti di Microsoft
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
- -d compiler option [Visual Basic]
- /d compiler option [Visual Basic]
- -define compiler option [Visual Basic]
- d compiler option [Visual Basic]
- /define compiler option [Visual Basic]
- define compiler option [Visual Basic]
ms.assetid: f735c57d-1cf9-4f2f-a26f-0de630fd4077
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
ms.openlocfilehash: 48c3bae1c6cf5831f95ce86dbcf6adadab9d5db8
ms.lasthandoff: 03/13/2017

---
# <a name="define-visual-basic"></a>/define (Visual Basic)
Definisce le costanti del compilatore condizionali.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/define:["]symbol[=value][,symbol[=value]]["]  
' -or-  
/d:["]symbol[=value][,symbol[=value]]["]  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`symbol`|Obbligatorio. Il simbolo da definire.|  
|`value`|Facoltativa. Il valore da assegnare a `symbol`. Se `value` è una stringa, deve essere racchiuso tra sequenze di barre rovesciate/virgolette (\\") anziché tra virgolette. Se non è specificato un valore, è considerato True.|  
  
## <a name="remarks"></a>Note  
 L'opzione `/define` ha un effetto analogo all'uso di una direttiva per il preprocessore `#Const` nel file di origine, ad eccezione del fatto che le costanti definite con `/define` sono pubbliche e si applicano a tutti i file del progetto.  
  
 È possibile usare i simboli creati mediante questa opzione con la direttiva `#If`...`Then`...`#Else` per eseguire la compilazione condizionale dei file di origine.  
  
 `/d` è la versione abbreviata di `/define`.  
  
 È possibile definire più simboli con `/define`, separando le definizioni dei simboli con una virgola.  
  
|Per impostare /define nell'ambiente di sviluppo integrato di Visual Studio|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Scegliere **Avanzate**.<br />4.  Modificare il valore di **costanti personalizzate** casella.|  
  
## <a name="example"></a>Esempio  
 Nel codice seguente sono definite e usate due costanti di compilazione condizionale.  
  
 [!code-vb[N. VbVbalrCompiler&45;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/define_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [#If... Then... #Else direttive](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [#Const (direttiva)](../../../visual-basic/language-reference/directives/const-directive.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
