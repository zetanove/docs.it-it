---
title: "Proprietà predefinita &quot;&lt;propertyname1&gt;&quot;è in conflitto con la proprietà predefinita&quot;&lt;propertyname2&gt;&quot;in&quot;&lt;classname&gt;&quot; e quindi deve essere dichiarata &quot;Shadows&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40007
- bc40007
dev_langs:
- VB
helpviewer_keywords:
- BC40007
ms.assetid: 692ccf76-5715-4f11-a972-84cf9de30bc1
caps.latest.revision: 9
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
ms.openlocfilehash: 803b42b7659c16fd97251635e4b6ba49362e0a02
ms.lasthandoff: 03/13/2017

---
# <a name="default-property-39ltpropertyname1gt39-conflicts-with-default-property-39ltpropertyname2gt39-in-39ltclassnamegt39-and-so-should-be-declared-39shadows39"></a>Proprietà predefinita '&lt;propertyname1&gt;'è in conflitto con la proprietà predefinita'&lt;propertyname2&gt;'in'&lt;classname&gt;' e quindi deve essere dichiarata 'Shadows'
Viene dichiarata una proprietà con lo stesso nome di una proprietà definita nella classe di base. In questo caso, la proprietà di questa classe deve nascondere la proprietà della classe base.  
  
 Si tratta di un messaggio di avviso. `Shadows`Per impostazione predefinita, viene utilizzato. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40007  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Aggiungere il `Shadows` parola chiave per la dichiarazione o la modifica viene dichiarato il nome della proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 [Ombreggiature](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Shadowing in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
