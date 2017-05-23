---
title: 'Migrazione: Normalizzazione del percorso | Documenti di Microsoft'
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
ms.assetid: 158d47b1-ba6d-4fa6-8963-a012666bdc31
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0579bb975a62e512062b10d39c2967cdcd23438f
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-path-normalization"></a>Migrazione: Normalizzazione del percorso
A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], la normalizzazione del percorso in .NET Framework è stata modificata.  
  
## <a name="what-is-path-normalization"></a>Che cos'è la normalizzazione di un percorso?  
 La normalizzazione di un percorso include la modifica della stringa che identifica un file o il percorso in modo che sia conforme a un percorso valido sul sistema operativo di destinazione. In genere, la normalizzazione implica:  
  
-   La conversione in forma canonica dei separatori di directory e dei componenti.  
  
-   L'applicazione della directory corrente in un percorso relativo.  
  
-   La valutazione della directory relativa (`.`) o della directory padre (`..`) in un percorso.  
  
-   La rimozione di caratteri specificati.  
  
## <a name="the-changes"></a>Le modifiche  
 A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], la normalizzazione è stata modificata così come segue:  
  
-   Il runtime viene rinviato alla funzione [GetFullPathName](https://msdn.microsoft.com/library/windows/desktop/aa364963\(v=vs.85\).aspx) del sistema operativo per normalizzare i percorsi.  
  
-   La normalizzazione non consiste più nel rimuovere la fine dei segmenti di directory (ad esempio uno spazio alla fine di un nome di directory).  
  
-   Supporto per la sintassi del percorso dispositivo in attendibilità totale, tra cui `\\.\` e, per le API del file I/O in mscorlib. dll, `\\?\`.  
  
-   Il runtime non convalida i percorsi di sintassi del dispositivo.  
  
-   È supportato l'uso della sintassi del dispositivo per accedere ai flussi di dati alternativi.  
  
## <a name="impact"></a>Impatto  
 Per le applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] o versioni successive, queste modifiche sono applicate per impostazione predefinita. Tali modifiche migliorano le prestazioni, consentendo al contempo ai metodi di accedere ai percorsi in precedenza inaccessibili.  
  
 Le applicazioni destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti ma in esecuzione in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] o versioni successive non sono interessate da questa modifica.  
  
## <a name="mitigation"></a>Attenuazione  
 Le app destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] o versioni successive possono rifiutare esplicitamente questa modifica e usare la normalizzazione legacy aggiungendo il codice seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'applicazione:  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />    
</runtime>  
```  
  
 Le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] o versioni precedenti ma in esecuzione su [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] o versioni successive possono abilitare le modifiche alla normalizzazione del percorso aggiungendo la riga seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'applicazione:  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=false" />    
</runtime>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)

