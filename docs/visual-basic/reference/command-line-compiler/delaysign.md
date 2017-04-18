---
title: /delaysign | Documenti di Microsoft
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
- delaysign compiler option [Visual Basic]
- /delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
caps.latest.revision: 19
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
ms.openlocfilehash: 59d4ec227286c20b2b4ecf749a91f0c4ee8d25ca
ms.lasthandoff: 03/13/2017

---
# <a name="delaysign"></a>/delaysign
Specifica se l'assembly avrà firma completa o parziale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/delaysign[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Facoltativo. Usare `/delaysign-` se si desidera che l'assembly abbia firma completa. Utilizzare `/delaysign+` se si desidera inserire la chiave pubblica nell'assembly e riserva spazio per l'hash con segno. Il valore predefinito è `/delaysign-`.  
  
## <a name="remarks"></a>Note  
 Il `/delaysign` opzione ha effetto solo se utilizzata con [/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md) o [/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md).  
  
 Quando si richiede un assembly con firmato completa, il compilatore genera un hash per il file che contiene il manifesto (i metadati dell'assembly) e tale hash viene firmato con la chiave privata. La firma digitale risultante viene archiviata nel file contenente il manifesto. Quando un assembly è impostata la firma ritardata, il compilatore non calcola e archivia la firma ma riserva spazio nel file in modo che la firma possa essere aggiunta successivamente.  
  
 Ad esempio, il metodo `/delaysign+`, uno sviluppatore di un'organizzazione può distribuire versioni di prova senza segno di un assembly che i tester possono registrare con la global assembly cache e utilizzare. Termine del lavoro per l'assembly, la persona responsabile della chiave privata dell'organizzazione può firmare completamente l'assembly. Questo contesto protegge chiave privata dell'organizzazione dalla divulgazione, consentendo agli sviluppatori di utilizzare gli assembly.  
  
 Vedere [creazione e uso degli assembly](https://msdn.microsoft.com/library/xwb8f617) per ulteriori informazioni su come firmare un assembly.  
  
### <a name="to-set-delaysign-in-the-visual-studio-integrated-development-environment"></a>Per impostare /delaysign in Visual Studio ambiente di sviluppo integrato  
  
1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
2.  Fare clic su di **firma** scheda.  
  
3.  Impostare il valore di **solo firma ritardata** casella.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
