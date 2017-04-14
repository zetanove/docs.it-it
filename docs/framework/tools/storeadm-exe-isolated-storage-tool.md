---
title: "Storeadm.exe (Isolated Storage Tool) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Storeadm.exe"
  - "listing stores for current user"
  - "Isolated Storage tool"
  - "stores, current user"
  - "removing stores"
ms.assetid: b81202b8-d91d-4b23-9c53-4a112f74a44a
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# Storeadm.exe (Isolated Storage Tool)
Lo strumento per lo spazio di memorizzazione isolato elenca o rimuove tutti gli archivi esistenti dell'utente attualmente connesso.  
  
 Viene installato automaticamente con Visual Studio.  Per eseguire lo strumento, utilizzare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7.  Per ulteriori informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
storeadm [/list][/machine][/remove][/roaming][/quiet]  
```  
  
#### Parametri  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\/h**\[**elp**\]|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|**\/list**|Visualizza tutti gli archivi esistenti dell'utente attualmente connesso,  inclusi gli archivi di tutte le applicazioni e di tutti gli assembly eseguiti da tale utente.|  
|**\/machine**|Seleziona l'archivio computer.  Utilizzare questa opzione insieme a **\/list** o **\/remove** per specificare che l'operazione deve essere applicata all'archivio computer.<br /><br /> Questa è una nuova opzione di .NET Framework versione 2.0.|  
|**\/quiet**|Specifica la modalità non interattiva. Evita la visualizzazione dell'output informativo, in modo che vengano visualizzati solo i messaggi di errore.|  
|**\/remove**|Rimuove definitivamente tutti gli archivi esistenti dell'utente attualmente connesso.|  
|**\/roaming**|Seleziona l'archivio roaming.  Utilizzare questa opzione con l'opzione **\/list** o **\/remove** per specificare che l'operazione deve essere applicata all'archivio roaming.|  
|**\/?**|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
## Note  
 Se si esegue Storeadm.exe dalla riga di comando senza specificare alcuna opzione, verranno visualizzate la sintassi e le opzioni dello strumento.  
  
 Le opzioni **\/list** e **\/remove** sono in genere utilizzate singolarmente. Se tuttavia vengono specificate due o più opzioni, queste verranno eseguite nell'ordine in cui sono state immesse sulla riga di comando.  
  
 Le applicazioni possono scegliere di salvare i dati in uno di due archivi relativi a un utente o nell'archivio computer:  
  
-   L'archivio locale si trova in un percorso per cui è escluso il roaming \(in Windows 2000 e versioni successive\) anche se per l'utente è abilitato il roaming dei dati.  
  
-   L'archivio roaming si trova in un percorso in cui il roaming è consentito, ma solo se è abilitato anche per l'utente attraverso l'amministrazione di Windows NT.  
  
-   L'archivio computer è comune a tutti gli utenti di un computer e quindi si trova in una directory comune del computer.  
  
    > [!NOTE]
    >  L'archivio computer è stato introdotto con .NET Framework versione 2.0.  
  
 L'eventuale abilitazione del roaming per l'utente non ha alcun effetto sull'amministrazione di Storeadm.exe.  Se lo strumento viene eseguito senza opzioni, tutte le operazioni verranno applicate all'archivio locale.  Se lo strumento viene eseguito con l'opzione **\/roaming**, tutte le operazioni verranno applicate all'archivio abilitato al roaming.  Se lo strumento viene eseguito con l'opzione **\/machine**, tutte le operazioni verranno applicate all'archivio computer.  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Spazio di memorizzazione isolato](../../../docs/standard/io/isolated-storage.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)