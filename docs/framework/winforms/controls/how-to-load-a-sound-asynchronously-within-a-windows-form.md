---
title: "Procedura: caricare in modo asincrono un suono in un Windows Form | Microsoft Docs"
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
  - "Classe SoundPlayer, caricamento asincrono di suoni"
  - "suoni, caricamento in thread separati"
  - "i suoni di threading [Windows Form]"
ms.assetid: 3b6a9296-1d5e-4d52-a4ba-94366d6fe302
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: caricare in modo asincrono un suono in un Windows Form
Nell'esempio di codice seguente viene caricato un suono in modo asincrono da un URL e quindi viene riprodotto in un nuovo thread.  
  
## <a name="example"></a>Esempio  
 [!code-csharp[System.Media.SoundPlayer.LoadAsync#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Media.SoundPlayer.LoadAsync/CS/Form1.cs#1)]
 [!code-vb[System.Media.SoundPlayer.LoadAsync#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Media.SoundPlayer.LoadAsync/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System e System.Windows.Forms.  
  
-   Sostituzione del nome del file `"http://www.tailspintoys.com/sounds/stop.wav"` con un nome file valido.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [con la creazione della riga di comando csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [procedura: compilare ed eseguire un completo esempio Windows Form codice utilizzando Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Le operazioni sui file devono essere racchiuse tra blocchi di gestione delle eccezioni appropriati.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome del percorso non è valido. Ad esempio, contiene caratteri non validi o solo spazi vuoti (<xref:System.ArgumentException> classe).  
  
-   Il percorso è di sola lettura (<xref:System.IO.IOException> classe).  
  
-   Il percorso è `Nothing` (<xref:System.ArgumentNullException> classe).  
  
-   Il nome del percorso è troppo lungo (<xref:System.IO.PathTooLongException> classe).  
  
-   Il percorso non valido (<xref:System.IO.DirectoryNotFoundException> classe).  
  
-   Il percorso contiene solo due punti ":" (<xref:System.NotSupportedException> classe).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto. È possibile ad esempio che il file `Form1.vb` non sia un file di origine di Visual Basic. Prima di usare i dati nell'applicazione verificare tutti gli input.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Media.SoundPlayer.LoadAsync%2A>   
 <xref:System.Media.SoundPlayer.LoadCompleted>   
 <xref:System.Media.SoundPlayer.Play%2A>   
 [Procedura: riprodurre un suono da un Windows Form](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)