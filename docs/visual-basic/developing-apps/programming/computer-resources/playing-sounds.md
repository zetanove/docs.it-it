---
title: Riproduzione di suoni (Visual Basic) | Microsoft Docs
ms.custom: 
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
- system sounds, playing
- system sounds
- playing sounds, Visual Basic
- sound loops
- My.Computer.Audio object, tasks
- sounds, playing
- sounds, background
- playing sounds
ms.assetid: f0d9e4ab-57c7-47b6-86d3-99ff07078040
caps.latest.revision: 21
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ed4ee0a09067900a6bead04abec02f141936ba42
ms.lasthandoff: 03/13/2017

---
# <a name="playing-sounds-visual-basic"></a>Riproduzione di suoni (Visual Basic)
Il metodo `My.Computer.Audio` offre metodi per la riproduzione di suoni.  
  
## <a name="playing-sounds"></a>Riproduzione di suoni  
 La riproduzione in background consente all'applicazione di eseguire altro codice durante la riproduzione di suoni. Il metodo `My.Computer.Audio.Play` consente all'applicazione di riprodurre un solo suono di sottofondo alla volta: quando l'applicazione riproduce un nuovo suono di sottofondo, viene interrotta la riproduzione del suono di sottofondo precedente. È anche possibile riprodurre un suono e attendere il completamento della riproduzione.  
  
 Nell'esempio seguente il metodo `My.Computer.Audio.Play` riproduce un suono. Quando è specificato `AudioPlayMode.WaitToComplete`, `My.Computer.Audio.Play` attende il completamento del suono prima di continuare a chiamare codice. Quando si usa questo esempio è necessario assicurarsi che il nome file faccia riferimento a un file audio con estensione wav presente nel computer.  
  
 [!code-vb[VbVbalrMyComputer#15](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_1.vb)]  
  
 Nell'esempio seguente il metodo `My.Computer.Audio.Play` riproduce un suono. Quando si usa questo esempio è necessario assicurarsi che le risorse dell'applicazione includano un file audio con estensione wav denominato Waterfall.  
  
 [!code-vb[VbVbalrMyComputer#16](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_2.vb)]  
  
## <a name="playing-looping-sounds"></a>Riproduzione di file audio a ciclo continuo  
 Nell'esempio seguente il metodo `My.Computer.Audio.Play` riproduce il file audio specificato in background quando è specificato `PlayMode.BackgroundLoop`. Quando si usa questo esempio è necessario assicurarsi che il nome file faccia riferimento a un file audio con estensione wav presente nel computer.  
  
 [!code-vb[VbVbalrMyComputer#11](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_3.vb)]  
  
 Nell'esempio seguente il metodo `My.Computer.Audio.Play` riproduce il file audio specificato in background quando è specificato `PlayMode.BackgroundLoop`. Quando si usa questo esempio è necessario assicurarsi che le risorse dell'applicazione includano un file audio con estensione wav denominato Waterfall.  
  
 [!code-vb[VbVbalrMyComputer#12](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_4.vb)]  
  
 L'esempio di codice precedente è disponibile anche come frammento di codice IntelliSense. Nello strumento di selezione dei frammenti di codice il frammento di codice si trova in **Applicazioni Windows Form > Audio**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
 In generale, quando un'applicazione riproduce un file audio a ciclo continuo, la riproduzione dovrà prima o poi essere interrotta.  
  
## <a name="stopping-the-playing-of-sounds-in-the-background"></a>Interruzione della riproduzione di suoni in background  
 Usare il metodo `My.Computer.Audio.Stop` per interrompere la riproduzione di file audio in background o a ciclo continuo dell'applicazione.  
  
 In generale, quando un'applicazione riproduce un file audio a ciclo continuo, la riproduzione dovrà prima o poi essere interrotta.  
  
 L'esempio seguente interrompe la riproduzione di un file audio in background.  
  
 [!code-vb[VbVbalrMyComputer#18](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_5.vb)]  
  
 L'esempio di codice precedente è disponibile anche come frammento di codice IntelliSense. Nello strumento di selezione dei frammenti di codice il frammento di codice si trova in **Applicazioni Windows Form > Audio**. Per altre informazioni, vedere [Code Snippets](https://docs.microsoft.com/visualstudio/ide/code-snippets) (Frammenti di codice).  
  
## <a name="playing-system-sounds"></a>Riproduzione di suoni di sistema  
 Usare il metodo `My.Computer.Audio.PlaySystemSound` per riprodurre il suono di sistema specificato.  
  
 Il metodo `My.Computer.Audio.PlaySystemSound` accetta come parametro uno dei membri condivisi della classe <xref:System.Media.SystemSound>. Il suono di sistema <xref:System.Media.SystemSounds.Asterisk%2A> indica in genere la presenza di errori.  
  
 L'esempio seguente usa il metodo `My.Computer.Audio.PlaySystemSound` per riprodurre un suono di sistema.  
  
 [!code-vb[VbVbalrMyComputer#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_6.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Audio>   
 <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>   
 <xref:Microsoft.VisualBasic.Devices.Audio.PlaySystemSound%2A>   
 <xref:Microsoft.VisualBasic.Devices.Audio.Stop%2A>   
 <xref:Microsoft.VisualBasic.AudioPlayMode>
