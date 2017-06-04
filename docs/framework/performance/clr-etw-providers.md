---
title: "CLR ETW Providers | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ETW, CLR providers"
  - "CLR ETW providers"
ms.assetid: 0beafad4-b2c8-47f4-b342-83411d57a51f
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# CLR ETW Providers
Common Language Runtime \(CLR\) dispone di due provider: il provider di runtime e il provider di rundown.  
  
 Il provider di runtime genera eventi in base alle parole chiave \(categorie di eventi\) abilitate.  Ad esempio, è possibile raccogliere eventi del caricatore abilitando la parola chiave `LoaderKeyword`.  
  
 Gli eventi ETW \(Event tracking for Windows\) vengono registrati in un file con estensione etl che, in un secondo momento, può essere post\-elaborato in file \(con estensione csv\) con valori separati da virgole secondo necessità.  Per informazioni sulla conversione del file con estensione etl nel file con estensione csv, vedere [Controlling .NET Framework Logging](../../../docs/framework/performance/controlling-logging.md).  
  
## Provider di runtime  
 Il provider di runtime è il provider ETW CLR principale.  
  
 Il GUID del provider di runtime CLR è e13c0d23\-ccbc\-4e12\-931b\-d9cc2eee27e4.  
  
 Per alcuni esempi di registrazione e visualizzazione di eventi ETW CLR tramite strumenti comunemente disponibili, vedere [Controlling .NET Framework Logging](../../../docs/framework/performance/controlling-logging.md).  
  
 Oltre all'utilizzo di parole chiave quali `LoaderKeyword`, potrebbe essere necessario abilitare parole chiave per la registrazione di eventi che possono essere generati troppo di frequente.  Le parole chiave `StartEnumerationKeyword` e `EndEnumerationKeyword` abilitano questi eventi sono riassunte in [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md)  
  
## Provider di rundown  
 Il provider di rundown deve essere attivato per determinati utilizzi finalizzati a scopi specifici.  Per la maggior parte degli utenti, tuttavia, dovrebbe risultare sufficiente il provider di runtime.  
  
 Il GUID del provider di rundown CLR è A669021C\-C450\-4609\-A035\-5AF59AF4DF18.  
  
 In genere, la registrazione ETW viene abilitata prima dell'avvio di un processo e disattivata al termine dello stesso.  Tuttavia, se la registrazione ETW viene attivata durante l'esecuzione del processo, saranno necessarie informazioni aggiuntive su di esso.  Per la risoluzione dei simboli, ad esempio, è necessario registrare gli eventi di metodo per i metodi già caricati prima dell'attivazione della registrazione.  
  
 Gli eventi `DCStart` e `DCEnd` acquisiscono lo stato del processo al momento dell'avvio e dell'arresto della raccolta dati. Lo stato fa riferimento a informazioni di livello elevato, inclusi i metodi già compilati Just\-In\-Time \(JIT\) e gli assembly caricati. Questi due eventi possono fornire informazioni su ciò che è già avvenuto nel processo, ad esempio sui metodi compilati JIT e così via.  
  
 Soltanto gli eventi il cui nome contiene `DC`, `DCStart`, `DCEnd` o `DCInit` vengono generati nel provider di rundown.  Inoltre, questi eventi vengono generati unicamente nel provider di rundown.  
  
 Oltre ai filtri delle parole chiave di evento, il provider di rundown supporta anche le parole chiave `StartRundownKeyword` e `EndRundownKeyword` per fornire un filtro di destinazione.  
  
### Rundown iniziale  
 Quando si abilita la registrazione nel provider di rundown tramite la parola chiave `StartRundownKeyword`, viene attivato un rundown iniziale.  Ciò causa la generazione dell'evento `DCStart` e l'acquisizione dello stato del sistema.  Prima che inizi l'enumerazione, viene generato l'evento `DCStartInit`.  Al termine dell'enumerazione viene generato l'evento `DCStartComplete` per notificare al controller la regolare conclusione della raccolta dati.  
  
### Rundown finale  
 Quando si abilita la registrazione nel provider di rundown tramite la parola chiave `EndRundownKeyword`, viene attivato un rundown finale.  Questo rundown interrompe l'esecuzione del profilo in un processo che continua a essere eseguito.  Gli eventi `DCEnd` acquisiscono lo stato del sistema nel momento in cui viene interrotta l'esecuzione del profilo.  
  
 Prima che inizi l'enumerazione, viene generato l'evento `DCEndInit`.  Al termine dell'enumerazione viene generato l'evento `DCEndComplete` per notificare al consumer la regolare conclusione della raccolta dati.  Il rundown iniziale e il rundown finale vengono utilizzati principalmente per la risoluzione di simboli gestiti.  Il rundown iniziale può fornire informazioni sull'intervallo di indirizzi per i metodi già compilati JIT prima dell'avvio della sessione di profilatura.  Il rundown finale può fornire informazioni sull'intervallo di indirizzi per tutti i metodi compilati JIT quando la profilatura sta per essere disattivata.  
  
 Il rundown finale non si verifica automaticamente quando viene interrotta una sessione di profilo.  Al contrario, uno strumento che stia tentando di eseguire la risoluzione di simboli gestiti deve richiamare in modo esplicito una sessione del provider di rundown CLR con la parola chiave `EndRundownKeyword` abilitata, appena prima che l'esecuzione del profilo venga interrotta.  
  
 Sebbene il rundown iniziale o il rundown finale possano fornire informazioni sull'intervallo di indirizzi dei metodi per la risoluzione di simboli gestiti, si consiglia di utilizzare la parola chiave `EndRundownKeyword` \(che fornisce eventi `DCEnd`\) anziché la parola chiave `StartRundownKeyword` \(che fornisce eventi `DCStart`\).  Se si utilizza `StartRundownKeyword`, il rundown si verifica durante la sessione di profilatura, il che può pregiudicare lo scenario profilato.  
  
## Raccolta dati ETW tramite i provider di runtime e rundown  
 Nell'esempio seguente viene illustrato come utilizzare il provider di rundown CLR in modo tale che la risoluzione dei simboli di processi gestiti abbia un impatto minimo, indipendentemente dal fatto che i processi abbiano inizio o fine all'interno o all'esterno della finestra profilata.  
  
1.  Attivare la registrazione ETW tramite il provider di runtime CLR:  
  
    ```  
    xperf -start clr -on e13c0d23-ccbc-4e12-931b-d9cc2eee27e4:0x1CCBD:0x5 -f clr1.etl      
    ```  
  
     Il log verrà salvato nel file clr1.etl.  
  
2.  Per interrompere l'esecuzione del profilo mentre il processo continua a essere eseguito, avviare il provider di rundown per acquisire gli eventi `DCEnd`:  
  
    ```  
    xperf -start clrRundown -on A669021C-C450-4609-A035-5AF59AF4DF18:0xB8:0x5 -f clr2.etl      
    ```  
  
     In questo modo la raccolta di eventi `DCEnd` potrà avviare una sessione di rundown.  La raccolta di tutti gli eventi può richiedere un'attesa che va da 30 a 60 secondi.  Il log verrà salvato nel file clr1.et2.  
  
3.  Disattivare tutti i profili ETW:  
  
    ```  
    xperf -stop clrRundown   
    xperf -stop clr  
    ```  
  
4.  Unire i profili per creare un unico file di log:  
  
    ```  
    xperf -merge -d clr1.etl clr2.etl merged.etl  
    ```  
  
     Il file merged.etl conterrà gli eventi delle sessioni dei provider di runtime e rundown.  
  
 Uno strumento può eseguire i passaggi 2 e 3 \(avvio di una sessione di rundown e conclusione dell'esecuzione del profilo\) anziché disattivare immediatamente i profili nel momento in cui un utente ne richiede l'interruzione.  Uno strumento può eseguire inoltre il passaggio 4.  
  
## Vedere anche  
 [ETW Events in the Common Language Runtime](../../../docs/framework/performance/etw-events-in-the-common-language-runtime.md)