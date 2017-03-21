---
title: "&quot;&lt;interfacename&gt;.&lt; MemberName&gt;&quot;è già implementata dalla classe di base&quot;&lt;baseclassname&gt;&quot;. Nuova implementazione di &lt;tipo&gt; presuppone | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42015
- bc42015
dev_langs:
- VB
helpviewer_keywords:
- BC42015
ms.assetid: 658c070a-113e-4bd8-b294-12c243191160
caps.latest.revision: 12
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
ms.openlocfilehash: 5ab2041826f74fdc5aceab7b1ceb26563d9b3f0a
ms.lasthandoff: 03/13/2017

---
# <a name="39ltinterfacenamegtltmembernamegt39-is-already-implemented-by-the-base-class-39ltbaseclassnamegt39-re-implementation-of-lttypegt-assumed"></a>'&lt;interfacename&gt;.&lt; MemberName&gt;'è già implementata dalla classe di base'&lt;baseclassname&gt;'. Nuova implementazione di &lt;tipo&gt; presuppone
Una proprietà, una routine o un evento in una classe derivata utilizza un `Implements` clausola che specifica un membro di interfaccia che è già implementato nella classe di base.  
  
 Una classe derivata può reimplementare un membro di interfaccia implementato dalla sua classe base. Questo non equivale a eseguire l'override dell'implementazione della classe base. Per ulteriori informazioni, vedere [implementa](../../../visual-basic/language-reference/statements/implements-clause.md).  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42015  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se si intende reimplementare il membro di interfaccia, non occorre fare nulla. Il codice nella classe derivata accede al membro reimplementato se non si utilizza il `MyBase` (parola chiave) per accedere all'implementazione della classe base.  
  
-   Se non si intende reimplementare il membro di interfaccia, rimuovere la clausola `Implements` dalla dichiarazione di proprietà, routine o evento.  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
