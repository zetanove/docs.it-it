---
title: 'Mitigazione: CspParameters.ParentWindowHandle prevede un HWND | Microsoft Docs'
ms.custom: 
ms.date: 04/07/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes
- .NET Framework 4.7 retargeting changes
- CspParameters.ParentWindowHandle
- CspParameters.ParentWindowHandle retargeting change
ms.assetid: 33264333-71d6-4d43-8827-9c98878cfea7
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9460c8b6ca8db927af4064e3567eca34c1bf5c91
ms.openlocfilehash: 22c258b06a5cc8fa3fec72665d7e413b0cdd11ee
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-cspparametersparentwindowhandle-expects-an-hwnd"></a>Mitigazione: CspParameters.ParentWindowHandle prevede un HWND

La proprietà <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle%2A>, introdotta in .NET Framework 2.0, consente a un'applicazione di registrare il valore di un handle di finestra padre in modo che qualsiasi interfaccia utente necessaria per accedere alla chiave (ad esempio, una finestra di dialogo di richiesta di PIN o di consenso) venga aperta come finestra figlio modale nella finestra specificata. A partire dalle applicazioni per .NET Framework 4.7, un handle di finestra (HWND) può essere assegnato a questa proprietà.

Nelle versioni di .NET Framework fino a .NET Framework 4.6.2, il valore assegnato alla proprietà <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle%2A> deve essere <xref:System.IntPtr> per indicare la posizione in cui risiede il valore HWND nella memoria. In Windows 7 e nelle versioni precedenti del sistema operativo Windows, impostare la proprietà su `form.Handle` non ha avuto alcun effetto, mentre in Windows 8 e nelle versioni successive il risultato è <xref:System.Security.Cryptography> con il messaggio "Parametro non corretto".

A partire dalle app per NET Framework 4.7, un'applicazione Windows Forms può impostare la proprietà <xref:System.Security.Cryptography.CspParameters.ParentWindowHandle%2A> con il codice seguente:

```csharp
cspParameters.ParentWindowHandle = form.Handle;
``` 

## <a name="impact"></a>Impatto

Le applicazioni destinate a .NET Framework 4.7 o versioni successive che desiderano registrare una relazione della finestra padre sono invitate a usare la forma semplificata:

```csharp
cspParameters.ParentWindowHandle = form.Handle;
``` 

## <a name="mitigation"></a>Attenuazione

Gli sviluppatori che hanno identificato il valore corretto nell'indirizzo della posizione di memoria contenente il valore `form.Handle` possono rifiutare esplicitamente questa modifica nel comportamento impostando l'opzione <xref:System.Security.AppContext> `Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle` su `true`:

- Impostando a livello di codice le opzioni di compatibilità sull'istanza [AppContext](assetID:///T:System.Security.AppContext).

- Aggiungendo la riga seguente alla sezione `<runtime>` del file app.config:
   
   ```xml
   <runtime>
     <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.DoNotAddrOfCspParentWindowHandle=true"/>
   </runtime>
   ```

Al contrario, gli utenti che desiderano optare per il nuovo comportamento per le applicazioni che vengono eseguite in .NET Framework 4.7 ma sono destinate a una versione precedente di .NET Framework possono impostare l'opzione <xref:System.Security.AppContext> su `false`.
 
## <a name="see-also"></a>Vedere anche

[Retargeting Changes in the .NET Framework 4.7 (Reindirizzamento delle modifiche in .NET Framework 4.7)](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md)

