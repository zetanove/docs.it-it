---
title: 'Mitigazione: Supporto del percorso lungo | Documenti di Microsoft'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3cbe2d77-6e2c-4665-a6c5-7000b9ad6890
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 40b4b94ac3058dda88b44c82110d4c749566e2b2
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="mitigation-long-path-support"></a>Mitigazione: Supporto del percorso lungo
A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], i metodi I/O del file system non generano più automaticamente un'eccezione <xref:System.IO.PathTooLongException> se un percorso o nome completo del file supera i 260 (o `MAX_PATH`) caratteri. Al contrario, sono supportati i percorsi lunghi con un massimo di 32 mila caratteri.  
  
## <a name="impact"></a>Impatto  
 Le applicazioni ricompilate destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] e che in precedenza generavano automaticamente un'eccezione <xref:System.IO.PathTooLongException>, perché un percorso con più di 260 caratteri genera ora un'eccezione <xref:System.IO.PathTooLongException> solo nelle condizioni seguenti:  
  
-   La lunghezza della stringa deve essere maggiore di <xref:System.Int16.MaxValue?displayProperty=fullName> (32,767) caratteri.  
  
-   Il sistema operativo restituisce `COR_E_PATHTOOLONG` o equivalente.  
  
 Il comportamento legacy per le applicazioni destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti è che il runtime genera automaticamente un'eccezione <xref:System.IO.PathTooLongException> ogni volta che un percorso supera i 260 caratteri.  
  
## <a name="mitigation"></a>Mitigazione  
 Per le applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], è possibile rifiutare esplicitamente il supporto del percorso lungo, nel caso non sia opportuno, aggiungendo il codice seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) sezione del file app. config:  
  
```xml  
<runtime>   
   <AppContextSwitchOverrides value="Switch.System.IO.BlockLongPaths=true" />   
</runtime>  
```  
  
 Per le applicazioni destinate alle versioni precedenti di .NET framework, ma eseguite in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] o versioni successive è possibile consentire esplicitamente il supporto per il percordo lungo aggiungendo il codice seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file app.config:  
  
```xml  
<runtime>   
   <AppContextSwitchOverrides value="Switch.System.IO.BlockLongPaths=false" />   
</runtime>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)

