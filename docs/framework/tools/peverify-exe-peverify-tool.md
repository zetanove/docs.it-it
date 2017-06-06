---
title: Peverify.exe (strumento PEVerify) | Microsoft Docs
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
- portable executable files, PEVerify
- verifying MSIL and metadata
- PEVerify tool
- type safety requirements
- MSIL
- PEverify.exe
- PE files, PEVerify
ms.assetid: f4f46f9e-8d08-4e66-a94b-0c69c9b0bbfa
caps.latest.revision: 18
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 14abadaf548e228244a1ff7ca72fa3896ef4eb5d
ms.openlocfilehash: 0cde5d4daeac4990dd9d1641120b19ea2413a204
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="peverifyexe-peverify-tool"></a>Peverify.exe (strumento PEVerify)
Lo strumento PEVerify aiuta gli sviluppatori che utilizzano il linguaggio MSIL (Microsoft Intermediate Language) per creare compilatori, motori di script e così via, a determinare se il codice MSIL creato e i metadati associati soddisfano i requisiti di indipendenza dai tipi. Alcuni compilatori generano codice di cui è verificabile l'indipendenza dai tipi solo se si evita di utilizzare determinati costrutti del linguaggio. Se, in qualità di sviluppatore, si utilizza un compilatore di questo tipo, sarà opportuno verificare di non aver compromesso l'indipendenza dai tipi del codice. In questa situazione è possibile eseguire lo strumento PEVerify sui file per controllare il codice MSIL e i metadati.  
  
 Viene installato automaticamente con Visual Studio. Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7. Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## <a name="syntax"></a>Sintassi  
  
```  
peverify filename [options]  
```  
  
#### <a name="parameters"></a>Parametri  
  
|Argomento|Descrizione|  
|--------------|-----------------|  
|*filename*|File eseguibile di tipo PE per il quale controllare il codice MSIL e i metadati.|  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**/break=** *maxErrorCount*|Interrompe la verifica dopo un numero di errori pari a *maxErrorCount*.<br /><br /> Questo parametro non è supportato in .NET Framework 2.0 o versione successiva.|  
|**/clock**|Misura e segnala i seguenti tempi di verifica in millisecondi:<br /><br /> **MD Val. cycle**<br /> Ciclo di convalida dei metadati<br /><br /> **MD Val. pure**<br /> Pure di convalida dei metadati<br /><br /> **IL Ver. cycle**<br /> Ciclo di verifica di MSIL (Microsoft Intermediate Language)<br /><br /> **IL Ver pure**<br /> Pure di verifica MSIL<br /><br /> I tempi **MD Val. cycle** e **IL Ver. cycle** includono il tempo richiesto per l'esecuzione delle procedure di avvio e chiusura necessarie. I tempi **MD Val. pure** e **IL Ver pure** corrispondono al tempo richiesto solo per l'esecuzione della convalida o della verifica.|  
|**/help**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|**/hresult**|Visualizza i codici di errore in formato esadecimale.|  
|**/ignore=** *hex.code* [, *hex.code*]|Ignora i codici di errore specificati.|  
|**/ignore=@** *responseFile*|Ignora i codici di errore elencati nel file di risposta specificato.|  
|**/il**|Esegue i controlli di verifica dell'indipendenza dai tipi del codice MSIL per i metodi implementati nell'assembly specificato da *filename*. Vengono restituite descrizioni dettagliate per ogni problema rilevato, a meno che non si specifichi l'opzione **/quiet**.|  
|**/md**|Esegue controlli di convalida dei metadati sull'assembly specificato da *filename*. Esamina l'intera struttura dei metadati nel file e segnala tutti i problemi di convalida rilevati.|  
|**/nologo**|Evita la visualizzazione delle informazioni sul copyright e sulla versione del prodotto.|  
|**/nosymbols**|In .NET Framework versione 2.0 evita la visualizzazione dei numeri di riga per compatibilità con le versioni precedenti.|  
|**/quiet**|Specifica la modalità non interattiva. Evita la visualizzazione dell'output dei report dei problemi di verifica. Viene comunque indicato se il file è indipendente dai tipi, ma non vengono fornite informazioni sui problemi che impediscono la verifica dell'indipendenza dai tipi.|  
|`/transparent`|Verifica solo i metodi trasparenti.|  
|**/unique**|Ignora i codici di errore ripetuti.|  
|**/verbose**|In .NET Framework versione 2.0 determina la visualizzazione di informazioni aggiuntive nei messaggi di verifica MSIL.|  
|**/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
## <a name="remarks"></a>Note  
 Common Language Runtime si basa sull'esecuzione indipendente dai tipi del codice dell'applicazione per applicare meccanismi di sicurezza e isolamento. In genere il codice di cui non è [verificabile l'indipendenza dai tipi](http://msdn.microsoft.com/en-us/095cd1f6-d8db-4c0e-bce2-83ccb34dd5dc) non può essere eseguito, anche se è possibile impostare criteri di sicurezza per consentire l'esecuzione del codice attendibile ma non verificabile.  
  
 Se non sono state specificate né l'opzione **/md** né l'opzione **/il** verranno eseguiti entrambi i tipi di controllo, iniziando dai controlli **/md**. Se non sono presenti errori vengono effettuati i controlli **/il**. Se si specifica sia **/md** sia **/il** i controlli **/il** vengono effettuati anche in presenza di errori nei metadati. Pertanto in assenza di errori nei metadati, **peverify** *filename* è equivalente a **peverify** *filename* **/md** **/il**.  
  
 Mediante Peverify.exe vengono eseguiti controlli di verifica completi del codice MSIL sulla base dell'analisi del flusso di dati nonché di un elenco di alcune centinaia di regole sui metadati validi. Per informazioni dettagliate sui controlli eseguiti da Peverify.exe, vedere le specifiche di convalida dei metadati e le specifiche del set di istruzioni MSIL nella cartella "Tools Developers Guide" di [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
 Si noti che in .NET Framework 2.0 o versione successiva sono supportate restituzioni `byref` verificabili specificate mediante le seguenti istruzioni MSIL: `dup`, `ldsflda`, `ldflda`, `ldelema`, `call` e `unbox`.  
  
## <a name="examples"></a>Esempi  
 Il comando che segue esegue controlli di convalida dei metadati e controlli di verifica dell'indipendenza dai tipi del codice MSIL per i metodi implementati nell'assembly `myAssembly.exe`.  
  
```  
peverify myAssembly.exe /md /il  
```  
  
 Al completamento della richiesta precedente, viene visualizzato il messaggio che segue.  
  
```  
All classes and methods in myAssembly.exe Verified  
```  
  
 Il comando che segue esegue controlli di convalida dei metadati e controlli di verifica dell'indipendenza dai tipi del codice MSIL per i metodi implementati nell'assembly `myAssembly.exe`. Viene visualizzato il tempo necessario per l'esecuzione di questi controlli.  
  
```  
peverify myAssembly.exe /md /il /clock  
```  
  
 Al completamento della richiesta precedente, viene visualizzato il messaggio che segue.  
  
```  
All classes and methods in myAssembly.exe Verified  
Timing: Total run     320 msec  
        MD Val.cycle  40 msec  
        MD Val.pure   10 msec  
        IL Ver.cycle  270 msec  
        IL Ver.pure   230 msec  
```  
  
 Il comando che segue esegue controlli di convalida dei metadati e controlli di verifica dell'indipendenza dai tipi del codice MSIL per i metodi implementati nell'assembly `myAssembly.exe`. Tuttavia, Peverify.exe si arresta quando raggiunge il conteggio di errori massimo di 100. Lo strumento ignora inoltre i codici di errore specificati.  
  
```  
peverify myAssembly.exe /break=100 /ignore=0x12345678,0xABCD1234  
```  
  
 Il comando che segue produce lo stesso risultato dell'esempio precedente, ma specifica i codici di errore da ignorare nel file di risposta `ignoreErrors.rsp`.  
  
```  
peverify myAssembly.exe /break=100 /ignore@ignoreErrors.rsp  
```  
  
 Il file di risposta può contenere un elenco di codici di errore separati da virgole.  
  
```  
0x12345678, 0xABCD1234  
```  
  
 In alternativa, il file di risposta può essere formattato con un codice di errore per riga.  
  
```  
0x12345678  
0xABCD1234  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti](../../../docs/framework/tools/index.md)   
 [NIB: scrittura di codice indipendente dai tipi verificabile](http://msdn.microsoft.com/en-us/d18f10ef-3b48-4f47-8726-96714021547b)   
 [Indipendenza dai tipi e sicurezza](http://msdn.microsoft.com/en-us/095cd1f6-d8db-4c0e-bce2-83ccb34dd5dc)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)

