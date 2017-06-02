---
title: "IEnumRAWINPUTDEVICE | Microsoft Docs"
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
  - "IEnumRAWINPUTDEVICE (interfaccia)"
ms.assetid: 88c8b389-a48b-46b9-b895-8ed7b1e26fea
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# IEnumRAWINPUTDEVICE
Questa interfaccia enumera i dispositivi di input non elaborati e viene usata solo da PresentationHost.exe.  
  
> [!NOTE]
>  Questa API è solo intesa e supportata per l'uso sul computer client locale  
  
## Membri  
  
|Membro|Descrizione|  
|------------|-----------------|  
|[IEnumRAWINPUTDEVIC:Next](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-next.md)|Vengono enumerati i successivi elementi `celt` successivi \(ovvero le strutture RAWINPUTDEVICE\) nell'elenco dell'enumeratore, che vengono restituiti in `rgelt` insieme al numero effettivo di elementi enumerati in `pceltFetched`.|  
|[IEnumRAWINPUTDEVIC:Skip](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-skip.md)|Indica all'enumeratore di ignorare i successivi elementi`celt` dell'enumerazione, in modo che alla successiva chiamata a [IEnumRAWINPUTDEVIC:Next](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-next.md) tali elementi non vengano restituiti.|  
|[IEnumRAWINPUTDEVIC:Reset](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-reset.md)|Riporta all'inizio la sequenza di enumerazione.|  
|[IEnumRAWINPUTDEVIC:Clone](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-clone.md)|Crea un altro enumeratore del dispositivo di input non elaborato con lo stesso stato dell'enumeratore corrente per eseguire l'iterazione dello stesso elenco.|  
  
## Vedere anche  
 [Informazioni sull'Input non elaborato](http://msdn.microsoft.com/library/ms645543\(vs.85\).aspx)