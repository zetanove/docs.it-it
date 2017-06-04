---
title: "Procedura: riprodurre un suono ripetutamente in un Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "riproduzione di suoni, scorrimento in ciclo"
  - "cicli di suoni"
  - "SoundPlayer (classe), riproduzione di cicli"
  - "suoni, scorrimento in ciclo"
ms.assetid: ea95dd46-10a3-46c0-8263-4b205f00df7f
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: riprodurre un suono ripetutamente in un Windows Form
Nell'esempio di codice seguente un suono viene riprodotto ripetutamente.  Quando viene eseguito il codice nel gestore dell'evento `stopPlayingButton_Click`, l'eventuale riproduzione corrente di un suono viene interrotta.  Se non è in corso di riproduzione alcun suono, non accadrà nulla.  
  
## Esempio  
 [!code-csharp[System.Media.SoundPlayer.PlayLooping#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/CS/Form1.cs#1)]
 [!code-vb[System.Media.SoundPlayer.PlayLooping#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/VB/Form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System e System.Windows.Forms.  
  
-   Sostituzione del nome del file `"c:\Windows\Media\chimes.wav"` con un nome file valido.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Programmazione efficiente  
 Le operazioni sui file devono essere racchiuse tra blocchi di gestione delle eccezioni appropriati.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome del percorso non è valido.  Ad esempio, contiene caratteri non validi o solo uno spazio vuoto \(classe <xref:System.ArgumentException>\).  
  
-   Il percorso è di sola lettura \(classe <xref:System.IO.IOException>\).  
  
-   Il nome del percorso è `Nothing` \(classe <xref:System.ArgumentNullException>\).  
  
-   Il nome del percorso è troppo lungo \(classe <xref:System.IO.PathTooLongException>\).  
  
-   Il percorso non è valido \(classe <xref:System.IO.DirectoryNotFoundException>\).  
  
-   Il percorso contiene solo due punti ":" \(classe <xref:System.NotSupportedException>\).  
  
## Sicurezza di .NET Framework  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto.  È possibile ad esempio che il file Form1.vb non sia un file di origine di Visual Basic.  Prima di usare i dati nell'applicazione verificare tutti gli input.  
  
## Vedere anche  
 <xref:System.Media.SoundPlayer.PlayLooping%2A>   
 [Procedura: riprodurre un suono da un Windows Form](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)   
 [Cenni preliminari sulla classe SoundPlayer](../../../../docs/framework/winforms/controls/soundplayer-class-overview.md)