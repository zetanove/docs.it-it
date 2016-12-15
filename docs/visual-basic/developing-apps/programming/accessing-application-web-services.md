---
title: "Accessing Application Web Services (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Web services, My.WebServices object"
  - "My.WebServices object"
  - "applications [Visual Basic], Web services"
ms.assetid: 8ad5405b-e771-42b1-82d3-ce97af2cea9e
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Accessing Application Web Services (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'oggetto `My.WebServices` fornisce un'istanza di ciascun servizio Web a cui fa riferimento il progetto corrente.  Ciascuna istanza viene istanziata su richiesta.  È possibile accedere a questi servizi Web tramite le proprietà dell'oggetto `My.WebServices`.  Il nome della proprietà è uguale al nome del servizio Web a cui accede la proprietà.  Qualsiasi classe che eredita da <xref:System.Web.Services.Protocols.SoapHttpClientProtocol> è un servizio Web.  
  
## Attività  
 Nella tabella riportata di seguito sono elencati i possibili modi per accedere ai servizi Web a cui fa riferimento un'applicazione.  
  
|||  
|-|-|  
|Per|Vedere|  
|Chiamare un servizio Web|[My.WebServices Object](../../../visual-basic/language-reference/objects/my-webservices-object.md)|  
|Chiamare un servizio Web in modo asincrono e gestire un evento al termine della chiamata|[How to: Call a Web Service Asynchronously](../../../visual-basic/developing-apps/programming/how-to-call-a-web-service-asynchronously.md)|  
  
## Vedere anche  
 [My.WebServices Object](../../../visual-basic/language-reference/objects/my-webservices-object.md)