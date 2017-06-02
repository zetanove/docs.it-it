---
title: '&lt;param&gt; (Visual Basic) | Documenti di Microsoft'
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
- param XML tag
- <param> XML tag
ms.assetid: 4e32e86f-f6f3-4301-b7fc-2f321fb54368
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 41852a7fc41595050940d87f9e741df5cb23361c
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="ltparamgt-visual-basic"></a>&lt;param&gt; (Visual Basic)
Definisce un nome di parametro e una descrizione.  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<param name="name">description</param>  
```  
  
#### <a name="parameters"></a>Parametri  
 `name`  
 Il nome di un parametro di metodo. Racchiudere il nome tra virgolette doppie ("").  
  
 `description`  
 Una descrizione per il parametro.  
  
## <a name="remarks"></a>Note  
 Il `<param>` tag deve essere utilizzato nel commento per una dichiarazione di metodo per descrivere uno dei parametri per il metodo.  
  
 Il testo per il `<param>` tag verrà visualizzato nei seguenti percorsi:  
  
-   Informazioni sul parametro di IntelliSense. Per altre informazioni, vedere [Using IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense) (Uso di IntelliSense).  
  
-   Visualizzatore oggetti. Per altre informazioni, vedere [Viewing the Structure of Code](https://docs.microsoft.com/visualstudio/ide/viewing-the-structure-of-code) (Visualizzazione della struttura del codice).  
  
 Esegue la compilazione con [/doc](../../../visual-basic/reference/command-line-compiler/doc.md) ai commenti di documentazione di processo in un file.  
  
## <a name="example"></a>Esempio  
 Questo esempio viene utilizzato il `<param>` tag per descrivere il `id` parametro.  
  
 [!code-vb[6 VbVbcnXmlDocComments](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/param_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Tag di commento XML](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)
