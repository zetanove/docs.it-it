---
title: 'Procedura: richiamare il compilatore della riga di comando (Visual Basic) | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- command-line arguments
- vbc.exe
- Visual Basic compiler, starting
- command line, arguments
ms.assetid: 0fd9a8f6-f34e-4c35-a49d-9b9bbd8da4a9
caps.latest.revision: 28
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 69c95289f91f712bd3fda03a7f582d879141591a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-invoke-the-command-line-compiler-visual-basic"></a>Procedura: richiamare il compilatore da riga di comando (Visual Basic)
È possibile richiamare il compilatore della riga di comando digitando il nome del file eseguibile nella riga di comando, noto anche come finestra di MS-DOS. Se esegue la compilazione dal prompt dei comandi di Windows predefinito, è necessario digitare il percorso completo del file eseguibile. Per eseguire l'override di questo comportamento predefinito, è possibile utilizzare il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] prompt dei comandi o modificare la variabile di ambiente PATH. Entrambi consentono di compilare da qualsiasi directory semplicemente digitando il nome del compilatore.  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-invoke-the-compiler-using-the-visual-studio-command-prompt"></a>Per richiamare il compilatore dal prompt dei comandi di Visual Studio  
  
1.  Aprire la cartella di programma Visual Studio Tools all'interno del gruppo di programmi Microsoft Visual Studio.  
  
2.  È possibile utilizzare il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] prompt dei comandi per accedere al compilatore da qualsiasi directory sul computer, se è installato Visual Studio.  
  
3.  Richiamare il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] prompt dei comandi.  
  
4.  Nella riga di comando, digitare `vbc.exe` *sourceFileName* e quindi premere INVIO.  
  
     Ad esempio, se il codice sorgente è memorizzato in una directory denominata `SourceFiles`, viene aperto il prompt dei comandi e il tipo `cd SourceFiles` per passare a tale directory. Se la directory contiene un file di origine denominato `Source.vb`, sarebbe possibile compilarlo digitando `vbc.exe Source.vb`.  
  
### <a name="to-set-the-path-environment-variable-to-the-compiler-for-the-windows-command-prompt"></a>Per impostare la variabile di ambiente PATH al compilatore per il Prompt dei comandi di Windows  
  
1.  Utilizzare la funzionalità di ricerca di Windows per trovare Vbc.exe sul disco locale.  
  
     Il nome esatto della directory in cui si trova il compilatore dipende il percorso della directory di Windows e la versione di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] installato. Se si dispone di più di una versione di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] , è necessario determinare quale versione utilizzare (in genere la versione più recente).  
  
2.  Da di **avviare** Menu, fare doppio clic su **risorse del Computer**e quindi fare clic su **proprietà** dal menu di scelta rapida.  
  
3.  Fare clic su di **avanzate** tasto tab e quindi fare clic su **le variabili di ambiente**.  
  
4.  Nel **sistema** riquadro variabili, selezionare **percorso** dall'elenco e fare clic su **modificare**.  
  
5.  Nel **modifica sistema** nella finestra di dialogo variabile, spostare il punto di inserimento alla fine della stringa nel **il valore della variabile** campo e digitare un punto e virgola (;) seguito dal nome completo della directory individuato al passaggio 1.  
  
6.  Fare clic su **OK** per confermare le modifiche e chiudere le finestre di dialogo.  
  
     Dopo aver modificato la variabile di ambiente PATH, è possibile eseguire il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore in Windows Prompt dei comandi da qualsiasi directory del computer.  
  
### <a name="to-invoke-the-compiler-using-the-windows-command-prompt"></a>Per richiamare il compilatore dal prompt dei comandi di Windows  
  
1.  Dal **avviare** menu, fare clic su di **Accessori** cartella e quindi aprire il **prompt dei comandi di Windows**.  
  
2.  Nella riga di comando, digitare `vbc.exe` *sourceFileName* e quindi premere INVIO.  
  
     Ad esempio, se il codice sorgente è memorizzato in una directory denominata `SourceFiles`, viene aperto il prompt dei comandi e il tipo `cd SourceFiles` per passare a tale directory. Se la directory contiene un file di origine denominato `Source.vb`, sarebbe possibile compilarlo digitando `vbc.exe Source.vb`.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
