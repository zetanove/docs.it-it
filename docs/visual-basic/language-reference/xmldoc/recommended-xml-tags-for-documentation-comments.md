---
title: Tag XML consigliati per i commenti della documentazione (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlDocComment
dev_langs:
- VB
helpviewer_keywords:
- tags, XML
- XML comments, recommended tags [Visual Basic]
- comments, recommended XML tags
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
caps.latest.revision: 14
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
ms.openlocfilehash: c6a47c12bc24864ef6ac9f80054becad98ec97f1
ms.lasthandoff: 03/13/2017

---
# <a name="recommended-xml-tags-for-documentation-comments-visual-basic"></a>Tag XML consigliati per i commenti relativi alla documentazione (Visual Basic)
Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore può elaborare i commenti della documentazione nel codice in un file XML. È possibile utilizzare strumenti aggiuntivi per elaborare il file XML nella documentazione.  
  
 I commenti XML sono consentiti sui costrutti di codice, ad esempio tipi e membri dei tipi. Per i tipi parziali, solo una parte del tipo possa contenere commenti XML, anche se vi è alcuna restrizione sui commenti sui relativi membri.  
  
> [!NOTE]
>  Impossibile applicare i commenti della documentazione per gli spazi dei nomi. Il motivo è che uno spazio dei nomi può estendersi a diversi assembly e non tutti gli assembly devono essere caricati contemporaneamente.  
  
 Il compilatore elabora qualsiasi tag XML valido. I seguenti tag forniscono funzionalità comunemente utilizzate nella documentazione per l'utente.  
  
||||  
|---|---|---|  
|[\<c >](../../../visual-basic/language-reference/xmldoc/c.md)|[\<codice >](../../../visual-basic/language-reference/xmldoc/code.md)|[\<esempio >](../../../visual-basic/language-reference/xmldoc/example.md)|  
|[\<eccezione >](../../../visual-basic/language-reference/xmldoc/exception.md) <sup>1</sup>|[\<includere >](../../../visual-basic/language-reference/xmldoc/include.md) <sup>1</sup>|[\<list>](../../../visual-basic/language-reference/xmldoc/list.md)|  
|[\<para >](../../../visual-basic/language-reference/xmldoc/para.md)|[\<param>](../../../visual-basic/language-reference/xmldoc/param.md) <sup>1</sup>|[\<paramref >](../../../visual-basic/language-reference/xmldoc/paramref.md)|  
|[\<autorizzazione >](../../../visual-basic/language-reference/xmldoc/permission.md) <sup>1</sup>|[\<la sezione Osservazioni >](../../../visual-basic/language-reference/xmldoc/remarks.md)|[\<Restituisce >](../../../visual-basic/language-reference/xmldoc/returns.md)|  
|[\<see>](../../../visual-basic/language-reference/xmldoc/see.md) <sup>1</sup>|[\<seealso >](../../../visual-basic/language-reference/xmldoc/seealso.md) <sup>1</sup>|[\<riepilogo >](../../../visual-basic/language-reference/xmldoc/summary.md)|  
|[\<typeparam >](../../../visual-basic/language-reference/xmldoc/typeparam.md) <sup>1</sup>|[\<valore >](../../../visual-basic/language-reference/xmldoc/value.md)||  
  
 (<sup>1</sup> il compilatore verifica la sintassi.)  
  
> [!NOTE]
>  Se si desidera vengano visualizzate nel testo di un commento di documentazione parentesi angolari, utilizzare `<` e `>`. Ad esempio, la stringa `"<text in angle brackets>"` verrà visualizzato come `<text in angle``brackets>`.  
  
## <a name="see-also"></a>Vedere anche  
 [Documentazione del codice tramite XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)   
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)   
 [Procedura: Creare documentazione XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
