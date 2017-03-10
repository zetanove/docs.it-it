---
title: "Debugging Your Visual Basic Application | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "debugging [Visual Basic], common tasks"
ms.assetid: 904760b8-9fe9-42a7-9d65-d93774253219
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# Debugging Your Visual Basic Application
[!INCLUDE[vs2017banner](../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa pagina vengono forniti collegamenti alla documentazione per le funzionalità di debug incorporate in [!INCLUDE[vsprvs](../../csharp/includes/vsprvs-md.md)].  Ad esempio, è possibile trovare errori semantici nell'applicazione osservando il comportamento in fase di esecuzione nel debugger stesso.  
  
 Utilizzando il debugger, è possibile esaminare il contenuto delle variabili dell'applicazione senza dover inserire chiamate aggiuntive per ottenere la restituzione dei valori.  In modo analogo, nel codice è possibile inserire un punto di interruzione per interrompere l'esecuzione nel punto specificato.  
  
## Controllo dell'esecuzione  
 Nella tabella che segue sono elencate le attività di debug relative al controllo dell'esecuzione e vengono forniti i collegamenti alle pagine della Guida associate.  
  
|||  
|-|-|  
|Per|Vedere|  
|Avviare il debug di un progetto di Visual Studio, connettersi a un processo, entrare nel codice, eseguire passo passo il codice, eseguire fino al cursore, eseguire a una funzione nello stack di chiamate, impostare l'istruzione successiva, eseguire passo passo Just My Code, arrestare il debug, riavviare il debug o disconnettersi da un processo sottoposto a debug.|[Spostarsi nel codice con il Debugger](/visual-studio/debugger/navigating-through-code-with-the-debugger)|  
|Specificare le configurazioni per le versioni di debug e finali di un programma.|[Debug and Release Project Configurations](http://msdn.microsoft.com/it-it/0440b300-0614-4511-901a-105b771b236e)|  
|Impostare le opzioni di avvio \(argomenti della riga di comando, directory di lavoro, computer remoto\)|[NIB: How to: Set Start Options for Application Debugging](http://msdn.microsoft.com/it-it/ce792058-7bac-4dd6-858b-466e872687b8)|  
|Eseguire il debug in fase di progettazione.|[Procedura dettagliata: debug in fase di progettazione](../Topic/Walkthrough:%20Debugging%20at%20Design%20Time.md)|  
|Attivare il debug JIT, una funzionalità che consente di avviare il debugger di Visual Studio quando un programma in esecuzione all'esterno di Visual Studio riscontra un errore irreversibile.|[Debug JIT](/visual-studio/debugger/just-in-time-debugging-in-visual-studio)|  
|Impostare i punti di interruzione per le righe di codice sorgente, le istruzioni di assembly e la funzione dello stack di chiamate.  Specificare le condizioni, il numero di passaggi e il percorso di esecuzione.|[Uso di punti di interruzione](/visual-studio/debugger/using-breakpoints)|  
  
## Gestione delle eccezioni  
 Nella tabella riportata di seguito vengono elencate le attività di debug relative alla gestione delle eccezioni con i riferimenti alle relative della Guida associate.  
  
|||  
|-|-|  
|Per|Vedere|  
|Interrompere in corrispondenza di eccezioni non gestite.|[Procedura: interrompere l'esecuzione in caso di eccezioni non gestite dall'utente](../Topic/How%20to:%20Break%20on%20User-Unhandled%20Exceptions.md)|  
|Interrompere quando viene generata un'eccezione.|[Procedura: interrompere l'esecuzione in caso di eccezione](../Topic/How%20to:%20Break%20When%20an%20Exception%20is%20Thrown.md)|  
|Interrompere in corrispondenza di eccezioni first\-chance.|[Procedura: interrompere l'esecuzione in caso di eccezione](../Topic/How%20to:%20Break%20When%20an%20Exception%20is%20Thrown.md)|  
|Utilizzare le informazioni sulle eccezioni.|[How to: Correct Run\-Time Errors with the Exception Assistant](../Topic/How%20to:%20Correct%20Run-Time%20Errors%20with%20the%20Exception%20Assistant.md)|  
|Aggiungere una nuova eccezione.|[Procedura: aggiungere nuove eccezioni](../Topic/How%20to:%20Add%20New%20Exceptions.md)|  
|Continuare l'esecuzione dopo che è stata generata un'eccezione.|[Continuazione dell'esecuzione dopo un'eccezione](/visual-studio/debugger/continuing-execution-after-an-exception)|  
  
## Modifica e continuazione  
 Nella tabella riportata di seguito vengono elencate le attività di debug relative a Modifica e continuazione con i riferimenti alle pagine della Guida associate.  
  
|||  
|-|-|  
|Per|Vedere|  
|Abilitare e disabilitare Modifica e continuazione.|[Procedura: attivare e disabilitare Modifica e continuazione](../Topic/How%20to:%20Enable%20and%20Disable%20Edit%20and%20Continue.md)|  
|Interrompere l'applicazione di modifiche al codice da parte di Modifica e continuazione.|[Procedura: interrompere l'applicazione di modifiche al codice](../Topic/How%20to:%20Stop%20Code%20Changes.md)|  
|Applicare le modifiche nella modalità di interruzione.|[Procedura: applicare modifiche in modalità di interruzione con Modifica e continuazione](../Topic/How%20to:%20Apply%20Edits%20in%20Break%20Mode%20with%20Edit%20and%20Continue.md)|  
  
## Esame dei dati di debug  
 Nella tabella riportata di seguito vengono elencate le attività di debug relative alla visualizzazione dei dati di debug con i riferimenti alle pagine della Guida associate.  
  
|||  
|-|-|  
|Per|Vedere|  
|Utilizzare la finestra **Registri** per visualizzare il contenuto del registro.|[Procedura: utilizzare la finestra Registri](../Topic/How%20to:%20Use%20the%20Registers%20Window.md)|  
|Utilizzare la finestra **Stack di chiamate** per visualizzare le chiamate di funzione o di routine correntemente presenti nello stack.|[Procedura: utilizzare la finestra Stack di chiamate](../Topic/How%20to:%20Use%20the%20Call%20Stack%20Window.md)|  
|Utilizzare la finestra **Disassembly** per visualizzare il codice assembly corrispondente alle istruzioni create dal compilatore.|[Procedura: utilizzare la finestra Disassembly](../Topic/How%20to:%20Use%20the%20Disassembly%20Window.md)|  
|Utilizzare la finestra **Moduli** per elencare e descrivere i moduli utilizzati dal programma.|[Procedura: utilizzare la finestra Moduli](../Topic/How%20to:%20Use%20the%20Modules%20Window.md)|  
|Utilizzare la finestra **Esplora script** per elencare i file di script attualmente caricati nel programma.|[Procedura: visualizzare documenti script](../Topic/How%20to:%20View%20Script%20Documents.md)|  
|Utilizzare la finestra **Thread** per esaminare e controllare i thread nel programma.|[Procedura: utilizzare la finestra Thread](../Topic/How%20to:%20Use%20the%20Threads%20Window.md)|  
  
## Vedere anche  
 [Procedura dettagliata: debug di un Windows Form](../Topic/Walkthrough:%20Debugging%20a%20Windows%20Form.md)   
 [Debug del codice gestito](/visual-studio/debugger/debugging-managed-code)   
 [Debug del codice nativo](/visual-studio/debugger/debugging-native-code)   
 [Debug di script e applicazioni Web](/visual-studio/debugger/debugging-web-applications-and-script)   
 [Riferimenti dell'interfaccia utente di debug](/visual-studio/debugger/debugging-user-interface-reference)   
 [Impostazioni di debug e preparazione](/visual-studio/debugger/debugger-settings-and-preparation)   
 [Nozioni di base sul debugger](/visual-studio/debugger/debugger-basics)   
 [Spostarsi nel codice con il Debugger](/visual-studio/debugger/navigating-through-code-with-the-debugger)   
 [Utilizzo di IntelliTrace](/visual-studio/debugger/intellitrace)   
 [Tipi di progetto C\#, F\# e Visual Basic](../Topic/Debugging%20Preparation:%20C%23,%20F%23,%20and%20Visual%20Basic%20Project%20Types.md)   
 [Procedura: applicare modifiche in modalità di interruzione con Modifica e continuazione](../Topic/How%20to:%20Apply%20Edits%20in%20Break%20Mode%20with%20Edit%20and%20Continue.md)