---
title: "How to: Invoke the Command-Line Compiler (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "command-line arguments"
  - "vbc.exe"
  - "Visual Basic compiler, starting"
  - "command line, arguments"
ms.assetid: 0fd9a8f6-f34e-4c35-a49d-9b9bbd8da4a9
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# How to: Invoke the Command-Line Compiler (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile richiamare il compilatore dalla riga di comando digitando il nome del relativo file eseguibile nella riga di comando, nota anche come finestra di MS\-DOS.  Se si effettua la compilazione dal prompt dei comandi predefinito di Windows, è necessario digitare il percorso completo nel file eseguibile.  Per eseguire l'override di questo comportamento predefinito, è possibile utilizzare il prompt dei comandi di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] o modificare la variabile di ambiente PATH.  Entrambe le soluzioni consentono di effettuare la compilazione a partire da una directory qualsiasi digitando semplicemente il nome del compilatore.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per richiamare il compilatore utilizzando il prompt dei comandi di Visual Studio  
  
1.  Aprire la cartella di programmi Visual Studio Tools nel gruppo di programmi Microsoft Visual Studio.  
  
2.  È possibile utilizzare il prompt dei comandi di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] per accedere al compilatore da qualsiasi directory del computer, se è installato Visual Studio.  
  
3.  Richiamare il prompt dei comandi di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)].  
  
4.  Nella riga di comando, digitare `vbc.exe` *NomeFileOrigine* e premere INVIO.  
  
     Se il codice sorgente fosse stato memorizzato in una directory denominata `SourceFiles`, ad esempio, per passare a quella directory sarebbe possibile aprire il prompt dei comandi e digitare `cd SourceFiles`.  Se la directory contenesse un file di origine denominato `Source.vb`, sarebbe possibile compilarlo digitando `vbc.exe Source.vb`.  
  
### Per impostare la variabile d'ambiente PATH nel compilatore per il prompt dei comandi di Windows  
  
1.  Utilizzare la funzionalità di ricerca di Windows per individuare Vbc.exe sul disco locale.  
  
     Il nome esatto della directory in cui si trova il compilatore dipende dalla posizione della directory di Windows e dalla versione di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] installata.  Se si sono installate più versioni di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)], è necessario determinare la versione correntemente utilizzata, solitamente la versione più recente.  
  
2.  Fare clic sul pulsante **Start**, fare clic con il pulsante destro del mouse su **Risorse del computer**, quindi scegliere **Proprietà** dal menu di scelta rapida.  
  
3.  Scegliere la scheda **Avanzate**, quindi fare clic su **Variabili di ambiente**.  
  
4.  Nel riquadro **Variabili di sistema** selezionare **Percorso** nell'elenco e scegliere **Modifica**.  
  
5.  Nella finestra di dialogo **Modifica variabile di sistema** spostare il punto di inserimento alla fine della stringa contenuta nel campo **Valore variabile** e digitare un punto e virgola \(;\) seguito dal nome completo della directory individuato al passaggio 1.  
  
6.  Scegliere **OK** per confermare le modifiche e chiudere le finestre di dialogo.  
  
     Una volta modificata la variabile di ambiente PATH, sarà possibile avviare il compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] dal prompt dei comandi di Windows da qualsiasi directory del computer.  
  
### Per richiamare il compilatore utilizzando il prompt dei comandi di Windows  
  
1.  Fare clic sul pulsante **Start**, quindi sulla cartella **Accessori** e aprire il **Prompt dei comandi** di Windows.  
  
2.  Nella riga di comando, digitare `vbc.exe`*NomeFileOrigine* e premere INVIO.  
  
     Se il codice sorgente fosse stato memorizzato in una directory denominata `SourceFiles`, ad esempio, per passare a quella directory sarebbe possibile aprire il prompt dei comandi e digitare `cd SourceFiles`.  Se la directory contenesse un file di origine denominato `Source.vb`, sarebbe possibile compilarlo digitando `vbc.exe Source.vb`.  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)