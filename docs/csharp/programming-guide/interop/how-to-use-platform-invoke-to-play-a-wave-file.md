---
title: "Procedura: utilizzare platform invoke per riprodurre un file audio (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/13/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "file .wav"
  - "interoperabilità [C#], riproduzione di file WAV tramite PInvoke"
  - "platform invoke, file audio"
  - "file .wav"
ms.assetid: f7f62f53-e026-4c40-b221-3a26adb0c2c5
caps.latest.revision: 30
caps.handback.revision: 30
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: utilizzare platform invoke per riprodurre un file audio (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nell'esempio di codice C\# riportato di seguito viene illustrato come utilizzare i servizi platform invoke per riprodurre un file audio wave nel sistema operativo Windows.  
  
## Esempio  
 In questo esempio di codice viene utilizzato `DllImport` per importare il punto di ingresso del metodo `PlaySound` di `winmm.dll` come `Form1 PlaySound()`.  L'esempio è costituito da un semplice Windows Form con un pulsante.  Se si fa clic sul pulsante, viene visualizzata una finestra di dialogo <xref:System.Windows.Forms.OpenFileDialog> standard di Windows che consente di aprire un file da riprodurre.  Quando viene selezionato, il file wave viene riprodotto utilizzando il metodo `PlaySound()` del metodo dell'assembly winmm.DLL.  Per ulteriori informazioni sul metodo `PlaySound` di winmm.dll, vedere [Using the PlaySound function with Waveform\-Audio Files](http://go.microsoft.com/fwlink/?LinkId=148553).  Cercare e selezionare un file con estensione wav, quindi scegliere **Apri** per riprodurre il file wave utilizzando platform invoke.  Il percorso completo del file selezionato verrà visualizzato in una casella di testo.  
  
 La finestra di dialogo **File aperti** verrà filtrata in modo da visualizzare solo i file con estensione wav tramite le impostazioni di filtro:  
  
 [!code-cs[csProgGuideInterop#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_1.cs)]  
  
 [!code-cs[csProgGuideInterop#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_2.cs)]  
  
## Compilazione del codice  
  
### Per compilare il codice  
  
1.  Creare un nuovo progetto di applicazione Windows C\# in Visual Studio e assegnare a tale progetto il nome WinSound.  
  
2.  Copiare il codice precedente e incollarlo sul contenuto del file `Form1.cs`.  
  
3.  Copiare il codice riportato di seguito e incollarlo nel file `Form1.Designer.cs`, nel metodo `InitializeComponent()`, dopo il codice esistente.  
  
     [!code-cs[csProgGuideInterop#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_3.cs)]  
  
4.  Compilare il codice ed eseguirlo.  
  
## Sicurezza di .NET Framework  
 Per ulteriori informazioni, [.NET Framework Security](http://go.microsoft.com/fwlink/?LinkId=37122) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Cenni preliminari sull'interoperabilità](../../../csharp/programming-guide/interop/interoperability-overview.md)   
 [Cenni preliminari sull'interoperabilità](../../../csharp/programming-guide/interop/interoperability-overview.md)   
 [A Closer Look at Platform Invoke](http://msdn.microsoft.com/it-it/ba9dd55b-2eaa-45cd-8afd-75cb8d64d243)   
 [Marshaling Data with Platform Invoke](../Topic/Marshaling%20Data%20with%20Platform%20Invoke.md)