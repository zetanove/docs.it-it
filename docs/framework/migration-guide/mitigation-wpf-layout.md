---
title: 'Mitigazione: Layout WPF | Documenti di Microsoft'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 805ffd7f-8d1e-427e-a648-601ca8ec37a5
caps.latest.revision: 3
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: bb9208e030de676bf18f405d1f1ca0e78308899d
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-wpf-layout"></a>Mitigazione: Layout WPF
Il layout dei controlli WPF può cambiare leggermente.  
  
## <a name="impact"></a>Impatto  
 Come conseguenza di questo cambiamento:  
  
-   La larghezza o l'altezza degli elementi può aumentare o diminuire al massimo di un pixel.  
  
-   La posizione di un oggetto può cambiare al massimo di un pixel.  
  
-   Gli elementi centrati possono risultare decentrati in orizzontale o in verticale al massimo di un pixel.  
  
 Per impostazione predefinita, questo nuovo layout è disponibile solo per app destinate a .NET Framework 4.6.  
  
## <a name="mitigation"></a>Attenuazione  
 Poiché questa modifica tende a eliminare il ritaglio del lato destro o inferiore dei controlli WPF a DPI elevati, le app destinate a versioni precedenti di .NET Framework ma eseguite su .NET Framework 4.6 possono adottare questo nuovo comportamento aggiungendo la riga seguente alla sezione `<runtime>` del file app.config:  
  
```xml  
<AppContextSwitchOverrides value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false" />  
```  
  
 Le app destinate a .NET Framework 4.6 ma che richiedono che il rendering dei controlli WPF venga eseguito mediante l'algoritmo di layout precedente possono aggiungere a questo scopo la riga seguente alla sezione `<runtime>` del file app.config:  
  
```xml  
<AppContextSwitchOverrides value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=true" />  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)
