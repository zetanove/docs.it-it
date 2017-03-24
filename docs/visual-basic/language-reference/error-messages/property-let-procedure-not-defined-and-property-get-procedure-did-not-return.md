---
title: "Property let procedure not defined and property get procedure did not return an object | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID451"
dev_langs: 
  - "VB"
ms.assetid: 8542382a-689f-4e1b-abc0-c1e2dadb92f4
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Property let procedure not defined and property get procedure did not return an object
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Alcune proprietà, metodi e operazioni sono applicabili solo agli oggetti `Collection`.  È stata specificata un'operazione o proprietà utilizzabile esclusivamente nelle raccolte, ma l'oggetto non è una raccolta.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che il nome della proprietà o dell'oggetto sia stato digitato correttamente o che l'oggetto sia di tipo `Collection`.  
  
2.  Controllare il metodo `Add`utilizzato per aggiungere l'oggetto alla raccolta per assicurarsi che la sintassi sia corretta e che gli identificatori siano stati digitati correttamente.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Collection>