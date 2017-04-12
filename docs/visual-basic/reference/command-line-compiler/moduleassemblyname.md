---
title: /moduleassemblyname | Documenti di Microsoft
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
- moduleassemblyname compiler option [Visual Basic]
- /moduleassemblyname compiler option [Visual Basic]
- -moduleassemblyname compiler option [Visual Basic]
ms.assetid: 013a57b6-f425-4dd3-b333-512d72c42f55
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
ms.openlocfilehash: f6b042b26ad866f177158562653c91f4f7527c04
ms.lasthandoff: 03/13/2017

---
# <a name="moduleassemblyname"></a>/moduleassemblyname
Specifica il nome dell'assembly di cui fa parte il modulo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/moduleassemblyname:assembly_name  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`assembly_name`|Il nome dell'assembly che conterrà una parte di questo modulo.|  
  
## <a name="remarks"></a>Note  
 Il compilatore elabora il `/moduleassemblyname` solo se opzione il `/target:module` è stata specificata l'opzione. Ciò indica al compilatore di creare un modulo. Il modulo creato dal compilatore è valido solo per l'assembly specificato con il `/moduleassemblyname` (opzione). Se si inserisce il modulo in un assembly diverso, si verificheranno errori in fase di esecuzione.  
  
 Il `/moduleassemblyname` opzione è necessaria solo quando vengono soddisfatte le seguenti:  
  
-   Un tipo di dati nel modulo deve accedere a un `Friend` tipo in un assembly di riferimento.  
  
-   L'assembly di riferimento ha concesso l'accesso assembly friend all'assembly in cui verrà compilato il modulo.  
  
 Per ulteriori informazioni sulla creazione di un modulo, vedere [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md). Per ulteriori informazioni sugli assembly friend, vedere [assembly Friend](http://msdn.microsoft.com/library/df0c70ea-2c2a-4bdc-9526-df951ad2d055).  
  
> [!NOTE]
>  Il `/moduleassemblyname` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo quando esegue la compilazione da un prompt dei comandi.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: compilare un Assembly su più file](http://msdn.microsoft.com/library/261c5583-8a76-412d-bda7-9b8ee3b131e5)   
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [/Main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [/Reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)   
 [Gli assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Assembly Friend](http://msdn.microsoft.com/library/df0c70ea-2c2a-4bdc-9526-df951ad2d055)
