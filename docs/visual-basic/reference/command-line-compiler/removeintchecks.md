---
title: /removeintchecks | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- removeintchecks
- /removeintchecks
dev_langs:
- VB
helpviewer_keywords:
- removeintchecks compiler option [Visual Basic]
- /removeintchecks compiler option [Visual Basic]
- -removeintchecks compiler option [Visual Basic]
ms.assetid: c1835bd5-1e38-4fba-bd2f-6984774765d4
caps.latest.revision: 14
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
ms.openlocfilehash: 8e50200b8755ccc6b1c173024856955f5075b67e
ms.lasthandoff: 03/13/2017

---
# <a name="removeintchecks"></a>/removeintchecks
Attiva il controllo per le operazioni di tipo integer o disattivare l'errore di overflow.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/removeintchecks[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`+` &#124; `-`|Facoltativo. Il `/removeintchecks-` opzione indica al compilatore di verificare tutti i calcoli integer per errori di overflow. Il valore predefinito è `/removeintchecks-`.<br /><br /> Specifica di `/removeintchecks` o `/removeintchecks+` il controllo degli errori e rendere integer risultano più rapide. Tuttavia, senza errori, e se ha causato un overflow capacità di tipo di dati, possono essere memorizzati risultati errati senza che venga generato un errore.|  
  
|Per impostare /removeintchecks in Visual Studio ambiente di sviluppo integrato|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Fare clic su **Avanzate** .<br />4.  Modificare il valore di **Rimuovi controllo dell'overflow di integer** casella.|  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `Test.vb` e consente di disattivare il controllo dell'overflow integer.  
  
```  
vbc /removeintchecks+ test.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
