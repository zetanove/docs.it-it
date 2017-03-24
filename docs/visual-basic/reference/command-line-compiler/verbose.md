---
title: l&quot;opzione /verbose | Documenti di Microsoft
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
- verbose compiler option [Visual Basic]
- -verbose compiler option [Visual Basic]
- /verbose compiler option [Visual Basic]
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
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
ms.openlocfilehash: f6d8a8b914ccffff72128bbc907482816b95b8a0
ms.lasthandoff: 03/13/2017

---
# <a name="verbose"></a>/verbose
Indica al compilatore di generare messaggi di stato e di errore dettagliati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/verbose[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Facoltativo. Specifica di `/verbose` equivale a specificare `/verbose+`, che indica al compilatore di messaggi dettagliati. Il valore predefinito per questa opzione è `/verbose-`.  
  
## <a name="remarks"></a>Note  
 Il `/verbose` opzione Visualizza informazioni sul numero totale di errori generati dal compilatore, sugli assembly che vengono caricati da un modulo e quali file sono attualmente in fase di compilazione.  
  
> [!NOTE]
>  Il `/verbose` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `In.vb` e indica al compilatore di visualizzare informazioni dettagliate sullo stato.  
  
```  
vbc /verbose in.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
