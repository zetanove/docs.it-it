---
title: "IEnumRAWINPUTDEVIC:Clone | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Clone (metodo)"
ms.assetid: 2a6a1900-aa55-45fa-9382-241d569a2dc4
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# IEnumRAWINPUTDEVIC:Clone
Consente di creare un altro enumeratore del dispositivo di input non elaborato con lo stesso stato dell'enumeratore corrente per scorrere lo stesso elenco.  
  
## Sintassi  
  
```  
HRESULT Clone( [out] IEnumRAWINPUTDEVICE **ppenum);  
```  
  
#### Parametri  
 `ppenum`  
  
 \[out\] Indirizzo della variabile di output che riceve il puntatore di interfaccia [IEnumRAWINPUTDEVICE](../../../../docs/framework/wpf/app-development/ienumrawinputdevice.md).  Se il metodo ha esito negativo, il valore di questa variabile di output non è definito.  
  
## Valore proprietà\/Valore restituito  
 HRESULT: questo metodo supporta i valori restituiti standard E\_INVALIDARG, E\_OUTOFMEMORY e E\_UNEXPECTED.  
  
## Note  
 Questo metodo consente di registrare un punto nella sequenza di enumerazione per tornare a quel punto in un momento successivo.  Il chiamante deve rilasciare questo nuovo enumeratore separatamente dal primo.