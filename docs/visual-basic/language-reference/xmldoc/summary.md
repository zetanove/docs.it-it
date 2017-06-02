---
title: '&lt;riepilogo&gt; (Visual Basic) | Documenti di Microsoft'
ms.custom: 
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
- <summary> XML tag
- summary XML tag
ms.assetid: 861c847d-dd94-478a-aa23-bf4899cdc848
caps.latest.revision: 12
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ad2053e21e58c49205fe869a484cb2dffd2169ee
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="ltsummarygt-visual-basic"></a>&lt;riepilogo&gt; (Visual Basic)
Specifica il riepilogo del membro.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<summary>description</summary>  
```  
  
#### <a name="parameters"></a>Parametri  
 `description`  
 Un riepilogo dell'oggetto.  
  
## <a name="remarks"></a>Note  
 Utilizzare il `<summary>` tag per descrivere un tipo o un membro del tipo. Utilizzare [ \<osservazioni >](../../../visual-basic/language-reference/xmldoc/remarks.md) per aggiungere informazioni supplementari per una descrizione del tipo.  
  
 Il testo per il `<summary>` tag è l'unica fonte di informazioni sul tipo in IntelliSense e viene anche visualizzato nel Visualizzatore oggetti. Per informazioni sul Visualizzatore oggetti, vedere [visualizzando il codice di struttura](https://docs.microsoft.com/visualstudio/ide/viewing-the-structure-of-code).  
  
 Esegue la compilazione con [/doc](../../../visual-basic/reference/command-line-compiler/doc.md) ai commenti di documentazione di processo in un file.  
  
## <a name="example"></a>Esempio  
 Questo esempio viene utilizzato il `<summary>` tag per descrivere il `ResetCounter` (metodo) e `Counter` proprietà.  
  
 [!code-vb[VbVbcnXmlDocComments n.&1;](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/summary_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Tag di commento XML](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)
