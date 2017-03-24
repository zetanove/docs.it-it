---
title: Cinese semplificato e TraditionalChinese non possono essere combinati | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrArgument_StrConvSCandTC
ms.assetid: d8e6a11b-f549-43b5-8337-0594340e1325
caps.latest.revision: 10
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 57ab14cdcb3e4b27e821097dcfca4d97e1633035
ms.lasthandoff: 03/13/2017

---
# <a name="simplifiedchinese-and-vbstrconvtraditionalchinese-cannot-be-combined"></a>SimplifiedChinese e VbStrConv.TraditionalChinese non possono essere combinati
L'applicazione sta tentando di combinare i membri `VbStrConv` e `SimplifiedChinese` dell'enumerazione `TraditionalChinese`, che si escludono reciprocamente.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Rimuovere `VbStrConv.SimplifiedChinese` o `VbStrConv.TraditionalChinese`.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Globalization>   
 [Enumerazione VbStrConv NOTINBUILD](http://msdn.microsoft.com/en-us/59f83dd9-6361-47df-a836-02ba9d4cb936)   
 [Introduzione alle applicazioni internazionali basate su .NET Framework](https://docs.microsoft.com/visualstudio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)
