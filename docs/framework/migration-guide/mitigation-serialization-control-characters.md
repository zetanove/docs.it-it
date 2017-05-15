---
title: 'Mitigazione: Serializzazione dei caratteri di controllo con DataContractJsonSerializer | Documenti di Microsoft'
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework 4.7 retargeting changes
- retargeting changes
- DataContractJsonSerializer changes
- serialization changes
ms.assetid: e065d458-a128-44f2-9f17-66af9d5be954
caps.latest.revision: 3
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9460c8b6ca8db927af4064e3567eca34c1bf5c91
ms.openlocfilehash: be68f399587910e290fc3487b887ca566c2c9f97
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-serialization-of-control-characters-with-the-datacontractjsonserializer"></a>Mitigazione: Serializzazione dei caratteri di controllo con DataContractJsonSerializer

A partire da .NET Framework 4.7 è stato modificato il modo in cui i caratteri di controllo vengono serializzati con <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> in modo da renderli conformi a ECMAScript V6 e V8. 
 
## <a name="impact"></a>Impatto

In .NET framework 4.6.2 e versioni precedenti, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> non serializzava alcuni caratteri di controllo speciali, ad esempio `\b`, `\f` e `\t`, in modo compatibile con gli standard ECMAScript V6 e V8.

Per le applicazioni destinate a versioni di .NET Framework a partire dalla 4.7, la serializzazione di questi caratteri di controllo è compatibile con ECMAScript V6 e V8. Sono interessate le seguenti API:

- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject%2A> 
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject%2A>
- <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject%2A>

## <a name="mitigation"></a>Attenuazione

Per le applicazioni destinate a versioni di .NET Framework a partire dalla 4.7, questo comportamento è abilitato per impostazione predefinita.

Se questo comportamento non è opportuno, è possibile rifiutare esplicitamente questa funzionalità aggiungendo la riga seguente alla sezione `<runtime>` del file app.config o web.config:

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseECMAScriptV6EscapeControlCharacter=false" />
</runtime>
```
 
## <a name="see-also"></a>Vedere anche
[Reindirizzamento delle modifiche in .NET Framework 4.7](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md)
