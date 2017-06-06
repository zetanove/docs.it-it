---
title: SecAnnotate.exe (strumento .NET Security Annotator) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- SecAnnotate.exe
- Security Annotator tool
ms.assetid: 8104d208-7813-4a1d-8a75-58f9a7bcb8c9
caps.latest.revision: 22
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: c274d1b9cdb0e9bf96a79d89f2f75b7f57dee25a
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="secannotateexe-net-security-annotator-tool"></a>SecAnnotate.exe (strumento .NET Security Annotator)
Lo strumento .NET Security Annotator (SecAnnotate.exe) è un'applicazione da riga di comando che identifica le parti `SecurityCritical` e `SecuritySafeCritical` di uno o più assembly.  
  
 Un'estensione di Visual Studio, [Security Annotator](http://go.microsoft.com/fwlink/?LinkId=198007), offre un'interfaccia utente grafica a SecAnnotate.exe e consente di eseguire lo strumento da Visual Studio.  
  
 Viene installato automaticamente con Visual Studio. Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7. Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi, digitare quanto segue, i cui *parametri* vengono illustrati nella sezione seguente e gli *assembly* consistono di uno o più nomi di assembly separati da spazi vuoti:  
  
## <a name="syntax"></a>Sintassi  
  
```  
SecAnnotate.exe [parameters] [assemblies]  
```  
  
#### <a name="parameters"></a>Parametri  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|`/a`<br /><br /> oppure<br /><br /> `/showstatistics`|Mostra le statistiche sull'utilizzo della trasparenza negli assembly analizzati.|  
|`/d:` *directory*<br /><br /> oppure<br /><br /> `/referencedir:` *directory*|Specifica una directory in cui cercare gli assembly dipendenti durante l'annotazione.|  
|`/i`<br /><br /> oppure<br /><br /> `/includesignatures`|Include informazioni estese sulle firme nel file di rapporto sulle annotazioni.|  
|`/n`<br /><br /> oppure<br /><br /> `/nogac`|Interrompe la ricerca degli assembly di riferimento nella Global Assembly Cache.|  
|`/o:` *output.xml*<br /><br /> oppure<br /><br /> `/out:` *output.xml*|Specifica il file delle annotazioni di output.|  
|`/p:` *maxpasses*<br /><br /> oppure<br /><br /> `/maximumpasses:` *maxpasses*|Specifica il numero massimo di passaggi di aggiunta annotazioni da effettuare sugli assembly prima di interrompere la generazione di nuove annotazioni.|  
|`/q`<br /><br /> oppure<br /><br /> `/quiet`|Specifica una modalità non interattiva, nella quale l'annotatore non restituisce messaggi di stato, ma solo informazioni sugli errori.|  
|`/r:` *assembly*<br /><br /> oppure<br /><br /> `/referenceassembly:` *assembly*|Include l'assembly specificato quando vengono risolti gli assembly dipendenti durante l'annotazione. Gli assembly di riferimento sono prioritari rispetto agli assembly trovati nel percorso di riferimento.|  
|`/s:` *rulename*<br /><br /> oppure<br /><br /> `/suppressrule:` *rulename*|Elimina l'esecuzione della regola di trasparenza specificata sugli assembly di input.|  
|`/t`<br /><br /> oppure<br /><br /> `/forcetransparent`|Forza lo strumento di annotazione a trattare tutti gli assembly che non dispongono di alcuna annotazione di trasparenza come se fossero completamente trasparenti.|  
|`/t`:*assembly*<br /><br /> oppure<br /><br /> `/forcetransparent`:*assembly*|Forza la trasparenza per l'assembly specificato, a prescindere dalle relative annotazioni correnti a livello di assembly.|  
|||  
|`/v`<br /><br /> oppure<br /><br /> `/verify`|Verifica solo che le annotazioni di un assembly siano corrette. Non tenta di eseguire più passaggi per trovare tutte le annotazioni necessarie se non supera la verifica.|  
|`/x`<br /><br /> oppure<br /><br /> `/verbose`|Specifica un output dettagliato durante l'annotazione.|  
|`/y:` *directory*<br /><br /> oppure<br /><br /> `/symbolpath:` *directory*|Include la directory specificata quando si ricercano file di simboli durante l'annotazione.|  
  
## <a name="remarks"></a>Note  
 Parametri e assembly possono essere forniti anche in un file di risposta specificato sulla riga di comando, preceduti dal simbolo di chiocciola (@). Ogni riga nel file di risposta deve contenere un solo parametro o nome di assembly.  
  
 Per altre informazioni su .NET Security Annotator, vedere il post [Using SecAnnotate to Analyze Your Assemblies for Transparency Violations](http://go.microsoft.com/fwlink/?LinkId=187648) (Uso di SecAnnotate per analizzare gli assembly con lo scopo di identificare violazioni di trasparenza) nel blog .NET Security.  
  
## <a name="examples"></a>Esempi
