---
title: /optioncompare | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /optioncompare
dev_langs:
- VB
helpviewer_keywords:
- optioncompare compiler option [Visual Basic]
- -optioncompare compiler option [Visual Basic]
- /optioncompare compiler option [Visual Basic]
ms.assetid: 7237b766-b44d-4cc5-9a3c-885348a7d9e4
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
ms.openlocfilehash: 53dee5bb50e20204725f031e3e04f5c37c5b3f96
ms.lasthandoff: 03/13/2017

---
# <a name="optioncompare"></a>/optioncompare
Specifica la modalità con cui vengono confrontate le stringhe.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/optioncompare:{binary | text}  
```  
  
## <a name="remarks"></a>Note  
 È possibile specificare `/optioncompare` in uno dei due formati: `/optioncompare:binary` per utilizzare confronti tra stringhe binarie e `/optioncompare:text` per utilizzare confronti tra stringhe di testo. Per impostazione predefinita, il compilatore utilizza `/optioncompare:binary`.  
  
 In Microsoft Windows, la tabella codici utilizzata determina l'ordinamento binario. Un tipico ordinamento binario è il seguente:  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 Confronti tra stringhe basati su testo sono in base all'ordinamento senza distinzione tra maiuscole determinato dalle impostazioni locali del sistema. Un ordinamento testuale tipico è la seguente:  
  
 `(A = a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
### <a name="to-set-optioncompare-in-the-visual-studio-ide"></a>Per impostare /optioncompare nell'IDE di Visual Studio  
  
1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Modificare il valore di **Option Compare** casella.  
  
### <a name="to-set-optioncompare-programmatically"></a>Per impostare /optioncompare a livello di codice  
  
-   Vedere [Option Compare (istruzione)](../../../visual-basic/language-reference/statements/option-compare-statement.md).  
  
## <a name="example"></a>Esempio  
 Il codice seguente compila P`rojFile.vb` e confronti tra stringhe binarie.  
  
```  
vbc /optioncompare:binary projFile.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Istruzione Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
