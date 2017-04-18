---
title: /filealign | Documenti di Microsoft
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
- sections compiler option [Visual Basic]
- alignment compiler option [Visual Basic]
- -filealign compiler option [Visual Basic]
- section alignment
- /filealign compiler option [Visual Basic]
- filealign compiler option [Visual Basic]
ms.assetid: cc61ec3d-ad38-4b28-9659-099d73cad099
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
ms.openlocfilehash: 18d5c3e327e2e41f4786eda6c3e981125f87389d
ms.lasthandoff: 03/13/2017

---
# <a name="filealign"></a>/filealign
Specifica la posizione di allineamento per le sezioni del file di output.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/filealign:number  
```  
  
## <a name="arguments"></a>Argomenti  
 `number`  
 Obbligatorio. Un valore che specifica l'allineamento delle sezioni nel file di output. I valori validi sono 512, 1024, 2048, 4096 e 8192. Questi valori sono espressi in byte.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare il `/filealign` opzione per specificare l'allineamento delle sezioni nel file di output. Le sezioni sono blocchi di memoria contigua in un file eseguibile portabile (PE) che contiene codice o dati. Il `/filealign` opzione consente di compilare l'applicazione con un allineamento non standard, gli sviluppatori non è necessario utilizzare questa opzione.  
  
 Ogni sezione è allineata a un limite che è un multiplo del `/filealign` valore. Non vi è alcun valore predefinito fisso. Se `/filealign` non è specificato, il compilatore sceglie un valore predefinito in fase di compilazione.  
  
 Specificando le dimensioni della sezione, è possibile modificare le dimensioni del file di output. La modifica delle dimensioni di sezione può essere utile per i programmi che verranno eseguito su dispositivi di piccole dimensioni.  
  
> [!NOTE]
>  Il `/filealign` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
