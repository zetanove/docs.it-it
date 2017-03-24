---
title: /codepage (Visual Basic) | Documenti di Microsoft
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
- /codepage compiler option [Visual Basic]
- codepage compiler option [Visual Basic]
- -codepage compiler option [Visual Basic]
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
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
ms.openlocfilehash: 90dce6e34e52862807e2acdbf1850699316730d1
ms.lasthandoff: 03/13/2017

---
# <a name="codepage-visual-basic"></a>/codepage (Visual Basic)
Specifica la tabella codici da usare per tutti i file del codice sorgente nella compilazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/codepage:id  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`id`|Obbligatorio. Il compilatore utilizza la tabella codici specificata da `id` per interpretare la codifica dei file di origine.|  
  
## <a name="remarks"></a>Note  
 Per compilare il codice sorgente salvato con una codifica specifica, è possibile utilizzare `/codepage` per specificare la tabella codici da utilizzare. Il `/codepage` opzione si applica a tutti i file di codice sorgente nella compilazione. Per ulteriori informazioni, vedere [codifica dei caratteri in .NET Framework](http://msdn.microsoft.com/library/bf6d9823-4c2d-48af-b280-919c5af66ae9).  
  
 Il `/codepage` opzione non è necessaria se sono stati salvati i file di codice sorgente utilizzando la tabella codici ANSI corrente, Unicode o UTF-8 con una firma. [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]Salva tutti i file di codice sorgente con la tabella codici ANSI corrente per impostazione predefinita, a meno che l'utente specifichi una codifica diversa nel **codifica** la finestra di dialogo. [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]Usa il **codifica** la finestra di dialogo per aprire il file di codice sorgente salvati con una tabella codici diversa.  
  
> [!NOTE]
>  Il `/codepage` opzione non è disponibile all'interno di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] ambiente di sviluppo; è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
