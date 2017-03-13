---
title: "My.Response Object | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.MyWebExtension.Response"
  - "My.Response"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Response object"
ms.assetid: 626359bc-3165-40b4-bfaf-2c610e26eb5b
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# My.Response Object
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Ottiene l'oggetto <xref:System.Web.HttpResponse> associato alla pagina <xref:System.Web.UI.Page>.  Questo oggetto consente di inviare i dati di una risposta HTTP a un client e contiene informazioni su quella risposta.  
  
## Note  
 L'oggetto `My.Response` contiene l'oggetto <xref:System.Web.HttpResponse> corrente associato con la pagina.  
  
 L'oggetto `My.Response` è disponibile solo per le applicazioni [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp-md.md)].  
  
## Esempio  
 Nell'esempio riportato di seguito viene ottenuta la raccolta di intestazioni dall'oggetto `My.Request` e viene utilizzato l'oggetto `My.Response` per scriverlo nella pagina ASP.NET.  
  
 [!code-vb[VbVbalrMyWeb#1](../../../visual-basic/language-reference/objects/codesnippet/VisualBasic/my-response-object_1.aspx)]  
  
## Vedere anche  
 <xref:System.Web.HttpResponse>   
 [My.Request Object](../../../visual-basic/language-reference/objects/my-request-object.md)