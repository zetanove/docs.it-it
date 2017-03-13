---
title: "Playing Sounds (Visual Basic) | Microsoft Docs"
ms.custom: ""
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
  - "system sounds, playing"
  - "system sounds"
  - "playing sounds, Visual Basic"
  - "sound loops"
  - "My.Computer.Audio object, tasks"
  - "sounds, playing"
  - "sounds, background"
  - "playing sounds"
ms.assetid: f0d9e4ab-57c7-47b6-86d3-99ff07078040
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Playing Sounds (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'oggetto `My.Computer.Audio` fornisce metodi per la riproduzione dei suoni.  
  
## Riprodurre suoni  
 La riproduzione dei suoni di sottofondo consente all'applicazione di eseguire altro codice mentre riproduce la musica.  Il metodo `My.Computer.Audio.Play` consente all'applicazione di riprodurre solo un suono di sottofondo alla volta. Quando l'applicazione riproduce un nuovo suono di sottofondo, interrompe la riproduzione di quello precedente.  È inoltre possibile riprodurre un suono e attendere che la riproduzione sia completata.  
  
 In l ' esempio seguente, il metodo di `My.Computer.Audio.Play` riproduce un suono.  Quando è specificato `AudioPlayMode.WaitToComplete`, il metodo `My.Computer.Audio.Play` attende il completamento del suono prima di continuare a chiamare codice.  Quando si utilizza questo esempio, sarà necessario assicurarsi che il nome file fa riferimento a un file audio .wav presente sul computer  
  
 [!code-vb[VbVbalrMyComputer#15](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_1.vb)]  
  
 In l ' esempio seguente, il metodo di `My.Computer.Audio.Play` riproduce un suono.  Quando si utilizza questo esempio, è necessario assicurarsi che le risorse dell' applicazione includono un file audio .wav denominato Waterfall.  
  
 [!code-vb[VbVbalrMyComputer#16](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_2.vb)]  
  
## La riproduzione in ciclo i suoni  
 In l ' esempio seguente, il metodo di `My.Computer.Audio.Play` riprodurre il suono specificato in background quando `PlayMode.BackgroundLoop` è specificato.  Quando si utilizza questo esempio, sarà necessario assicurarsi che il nome file fa riferimento a un file audio .wav presente sul computer.  
  
 [!code-vb[VbVbalrMyComputer#11](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_3.vb)]  
  
 In l ' esempio seguente, il metodo di `My.Computer.Audio.Play` riprodurre il suono specificato in background quando `PlayMode.BackgroundLoop` è specificato.  Quando si utilizza questo esempio, è necessario assicurarsi che le risorse dell' applicazione includono un file audio .wav denominato Waterfall.  
  
 [!code-vb[VbVbalrMyComputer#12](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_4.vb)]  
  
 L'esempio di codice precedente è disponibile anche come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice, si trova in **Sistema operativo Windows \> Sound**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
 In genere, quando un'applicazione riproduce un suono ciclico, finirà per dover interrompere la riproduzione del suono.  
  
## Interrompendo la riproduzione dei suoni in background  
 Per interrompere la riproduzione di un suono ciclico o in background, utilizzare il metodo `My.Computer.Audio.Stop`.  
  
 In generale, quando un'applicazione riproduce un suono ripetitivo, a un certo punto dovrebbe smettere.  
  
 In l ' esempio viene interrotta un suono che viene riprodotto in background.  
  
 [!code-vb[VbVbalrMyComputer#18](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_5.vb)]  
  
 L'esempio di codice precedente è disponibile anche come frammento di codice IntelliSense.  Nella casella di selezione dei frammenti di codice, si trova in **Sistema operativo Windows \> Sound**.  Per ulteriori informazioni, vedere [Frammenti di codice](/visual-studio/ide/code-snippets).  
  
## Riprodurre i suoni del sistema  
 Utilizzare il metodo `My.Computer.Audio.PlaySystemSound` per riprodurre il suono di sistema specificato.  
  
 Il metodo `My.Computer.Audio.PlaySystemSound` richiede come parametro uno dei membri condivisi dalla classe <xref:System.Media.SystemSound>.  In genere, il suono di sistema <xref:System.Media.SystemSounds.Asterisk%2A> denota la presenza di errori.  
  
 In l ' esempio seguente viene utilizzato il metodo di `My.Computer.Audio.PlaySystemSound` per riprodurre un suono di sistema.  
  
 [!code-vb[VbVbalrMyComputer#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_6.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Devices.Audio>   
 <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>   
 <xref:Microsoft.VisualBasic.Devices.Audio.PlaySystemSound%2A>   
 <xref:Microsoft.VisualBasic.Devices.Audio.Stop%2A>   
 <xref:Microsoft.VisualBasic.AudioPlayMode>