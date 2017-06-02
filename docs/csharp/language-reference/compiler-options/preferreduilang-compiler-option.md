---
title: -preferreduilang (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /preferreduilang
dev_langs:
- CSharp
helpviewer_keywords:
- preferreduilang compiler option [C#]
- /preferreduilang compiler option [C#]
- -preferreduilang compiler option [C#]
ms.assetid: 68b2462f-6778-48d7-8052-62805fe8e02c
caps.latest.revision: 15
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 0fd8ccca016b598b14780ac6cd2190442777fb53
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="preferreduilang-c-compiler-options"></a>/preferreduilang (opzioni del compilatore C#)
Utilizzando l'opzione del compilatore `/preferreduilang`, è possibile specificare la lingua in cui tramite il compilatore C# viene visualizzato l'output, ad esempio i messaggi di errore.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
/preferreduilang: language  
```  
  
## <a name="arguments"></a>Argomenti  
 `language`  
 [Nome](http://go.microsoft.com/fwlink/p/?LinkId=236992) della lingua da usare per l'output del compilatore.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare l'opzione del compilatore `/preferreduilang` per specificare la lingua che si desidera venga utilizzata dal compilatore C# per i messaggi di errore e altri output della riga di comando. Se il Language Pack della lingua non è installato, viene utilizzata l'impostazione della lingua del sistema operativo e non viene segnalato alcun errore.  
  
```csharp  
csc.exe /preferreduilang:ja-JP  
```  
  
## <a name="requirements"></a>Requisiti  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni del compilatore C#](../../../csharp/language-reference/compiler-options/index.md)
