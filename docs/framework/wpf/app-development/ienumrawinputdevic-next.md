---
title: "IEnumRAWINPUTDEVIC:Next | Microsoft Docs"
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
  - "Metodo Next"
ms.assetid: 3698b44d-510e-4d18-b32b-85f17188ee26
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# IEnumRAWINPUTDEVIC:Next
Vengono enumerate le strutture `celt` [RAWINPUTDEVICE](http://msdn.microsoft.com/library/default.asp?url=/library/winui/winui/windowsuserinterface/userinput/rawinput/rawinputreference/rawinputstructures/rawinputdevice.asp) nell'elenco dell'enumeratore e vengono restituite in `rgelt`, insieme al numero effettivo di elementi enumerati in `pceltFetched`.  
  
## Sintassi  
  
```  
HRESULT Next(  
      [in] ULONG celt,  
      [out, size_is(celt), length_is(*pceltFetched)] RAWINPUTDEVICE *rgelt,  
      [out] ULONG *pceltFetched);  
```  
  
#### Parametri  
 `celt`  
  
 \[in\] Numero di strutture [RAWINPUTDEVICE](http://msdn.microsoft.com/library/default.asp?url=/library/winui/winui/windowsuserinterface/userinput/rawinput/rawinputreference/rawinputstructures/rawinputdevice.asp) restituite in `rgelt`.  
  
 `rgelt`  
  
 \[out\] Matrice di dimensione celt \(o superiore\) per ricevere le strutture RAWINPUTDEVICE enumerate.  
  
 `pceltFetched`  
  
 \[out\] Puntatore al numero di elementi effettivamente forniti in `rgelt`.  Il chiamante può passare `NULL` se `rgelt` è uno.  
  
## Valore proprietà\/Valore restituito  
 HRESULT: S\_OK se il numero di elementi forniti è `celt`; in caso contrario S\_FALSE.