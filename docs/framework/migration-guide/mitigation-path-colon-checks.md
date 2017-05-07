---
title: 'Mitigazione: Verifica della presenza dei due punti nel percorso | Documenti di Microsoft'
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
ms.assetid: a0bb52de-d279-419d-8f23-4b12d1a3f36e
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: b5e2426fc81c8fd38994a4124cf71af8ec445bfb
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-path-colon-checks"></a>Mitigazione: Verifica della presenza dei due punti nel percorso
A partire dalle applicazioni dedicate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], sono state apportate alcune modifiche per supportare i percorsi in precedenza non supportati (entrambi in termini di lunghezza e il formato). In particolare, i controlli per la sintassi del separatore dell'unità appropriata (due punti) sono stati resi più corretti.  
  
## <a name="impact"></a>Impatto  
 Queste modifiche bloccano alcuni percorsi URI che i metodi <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=fullName> e <xref:System.IO.Path.GetPathRoot%2A?displayProperty=fullName> supportavano in precedenza.  
  
## <a name="mitigation"></a>Attenuazione  
 Per risolvere il problema di un percorso precedentemente accettabile che non è più supportato dai metodi <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=fullName> e <xref:System.IO.Path.GetPathRoot%2A?displayProperty=fullName> è possibile eseguire le operazioni seguenti:  
  
-   Rimuovere manualmente lo schema da un URL. Ad esempio, rimuovere `file://` da un URL.  
  
-   Passare l'URI a un costruttore <xref:System.Uri> e recuperare il valore della proprietà <xref:System.Uri.LocalPath%2A?displayProperty=fullName>.  
  
-   Rifiutare esplicitamente la normalizzazione percorso nuovo impostando il commutatore `Switch.System.IO.UseLegacyPathHandling`<xref:System.AppContext> su `true`.  
  
    ```xml  
  
    <runtime>  
        <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />    
    </runtime>  
  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)
