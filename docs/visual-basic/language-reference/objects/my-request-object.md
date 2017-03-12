---
title: "My.Request Object | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.MyWebExtension.Request"
  - "My.Request"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Request object"
ms.assetid: 93d5f0e2-6b60-4a2c-8652-d90216f6ad10
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# My.Request Object
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Ottiene l'oggetto <xref:System.Web.HttpRequest> per la pagina richiesta.  
  
## Note  
 L'oggetto `My.Request` contiene le informazioni relative alla richiesta HTTP corrente.  
  
 L'oggetto `My.Request` è disponibile solo per le applicazioni ASP.NET.  
  
## Esempio  
 Nell'esempio riportato di seguito viene ottenuta la raccolta di intestazioni dall'oggetto `My.Request` e viene utilizzato l'oggetto `My.Response` per scriverlo nella pagina ASP.NET.  
  
 [!code-vb[VbVbalrMyWeb#1](../../../visual-basic/language-reference/objects/codesnippet/visualbasic/my-request-object_1.aspx)]  
  
## Vedere anche  
 <xref:System.Web.HttpRequest>   
 [My.Response Object](../../../visual-basic/language-reference/objects/my-response-object.md)