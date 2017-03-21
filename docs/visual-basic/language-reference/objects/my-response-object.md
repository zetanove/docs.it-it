---
title: Oggetto My. Response | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.MyWebExtension.Response
- My.Response
dev_langs:
- VB
helpviewer_keywords:
- My.Response object
ms.assetid: 626359bc-3165-40b4-bfaf-2c610e26eb5b
caps.latest.revision: 9
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
ms.openlocfilehash: e2ae9a659bb7575023dfa1847c9d405d0f7d6ac3
ms.lasthandoff: 03/13/2017

---
# <a name="myresponse-object"></a>Oggetto My.Response
Ottiene l' <xref:System.Web.HttpResponse>oggetto associato a <xref:System.Web.UI.Page>.</xref:System.Web.UI.Page> </xref:System.Web.HttpResponse> Questo oggetto consente di inviare i dati della risposta HTTP a un client e contiene informazioni sulla risposta.  
  
## <a name="remarks"></a>Note  
 Il `My.Response` oggetto contiene l'oggetto corrente <xref:System.Web.HttpResponse>oggetto associato alla pagina.</xref:System.Web.HttpResponse>  
  
 Il `My.Response` oggetto è disponibile solo per [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)] applicazioni.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente ottiene la raccolta di intestazione dal `My.Request` e Usa il `My.Response` oggetto da scrivere la pagina ASP.NET.  
  
 [!code-vb[VbVbalrMyWeb n.&1;](../../../visual-basic/language-reference/objects/codesnippet/VisualBasic/my-response-object_1.aspx)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Web.HttpResponse></xref:System.Web.HttpResponse>   
 [Oggetto My.Request](../../../visual-basic/language-reference/objects/my-request-object.md)
