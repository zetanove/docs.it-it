---
title: "Clipboard format is not valid | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID460"
dev_langs: 
  - "VB"
ms.assetid: 71a4a045-65bb-417d-b3bd-99a9fa3c53f6
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Clipboard format is not valid
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il formato degli Appunti specificato non è compatibile con il metodo eseguito.  Di seguito sono riportate le cause possibili dell'errore.  
  
-   Si è tentato di utilizzare il metodo `GetText` o `SetText` degli Appunti con un formato degli Appunti diverso da `vbCFText` o `vbCFLink`.  
  
-   Si è tentato di utilizzare il metodo `GetData` o `SetData` degli Appunti con un formato degli Appunti diverso da `vbCFBitmap`, `vbCFDIB` o `vbCFMetafile`.  
  
-   Si è tentato di utilizzare il metodo `GetData` o `SetData` di `DataObject` con un formato degli Appunti nell'intervallo riservato da Microsoft Windows ai formati registrati \(&HC000\-&HFFFF\), ma il formato degli Appunti non è stato registrato in Microsoft Windows.  
  
### Per correggere l'errore  
  
-   Rimuovere il formato non valido e specificarne uno valido.  
  
## Vedere anche  
 [Appunti: aggiunta di altri formati](../Topic/Clipboard:%20Adding%20Other%20Formats.md)