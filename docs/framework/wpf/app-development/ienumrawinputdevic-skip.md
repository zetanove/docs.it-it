---
title: "IEnumRAWINPUTDEVIC:Skip | Microsoft Docs"
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
  - "Skip (metodo)"
ms.assetid: c967b0f8-1c6a-459c-8c16-d4f08918ab65
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# IEnumRAWINPUTDEVIC:Skip
Indica all'enumeratore di ignorare i successivi elementi `celt` dell'enumerazione, in modo che alla successiva chiamata a [IEnumRAWINPUTDEVIC:Next](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-next.md) tali elementi non vengano restituiti.  
  
## Sintassi  
  
```  
HRESULT Skip( [in] ULONG celt);  
```  
  
#### Parametri  
 `celt`  
  
 \[in\] Numero di elementi da ignorare.  
  
## Valore proprietà\/Valore restituito  
 HRESULT: S\_OK se il numero di elementi forniti è `celt`; in caso contrario, S\_FALSE.