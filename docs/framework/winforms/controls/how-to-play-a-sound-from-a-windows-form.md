---
title: "Procedura: riprodurre un suono da un Windows Form | Microsoft Docs"
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
  - "riproduzione di suoni, Windows Form"
  - "riproduzione di suoni"
  - "SoundPlayer (classe)"
  - "suoni"
  - "My.Computer.Audio (oggetto), la riproduzione di suoni"
  - "esempi [Windows Form] suoni"
ms.assetid: 3d3350b7-1ebd-4e05-a738-48ca1160a19d
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: riprodurre un suono da un Windows Form
In questo esempio riproduce un suono in un percorso specificato in fase di esecuzione.  
  
## <a name="example"></a>Esempio  
  
```vb  
Sub PlaySimpleSound()  
    My.Computer.Audio.Play("c:\Windows\Media\chimes.wav")  
End Sub  
```  
  
```csharp  
private void playSimpleSound()  
{  
    SoundPlayer simpleSound = new SoundPlayer(@"c:\Windows\Media\chimes.wav");  
    simpleSound.Play();  
}  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Sostituzione del nome del file `"c:\Windows\Media\chimes.wav"` con un nome file valido.  
  
-   (C#) Un riferimento di <xref:System.Media?displayProperty=fullName> dello spazio dei nomi.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Operazioni sui file devono essere racchiusi da Gestione blocchi appropriata delle eccezioni strutturata.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome del percorso non è valido. Ad esempio, contiene caratteri non validi o solo spazi vuoti (<xref:System.ArgumentException> classe).  
  
-   Il percorso è di sola lettura (<xref:System.IO.IOException> classe).  
  
-   Il percorso è `null` (<xref:System.ArgumentNullException> classe).  
  
-   Il nome del percorso è troppo lungo (<xref:System.IO.PathTooLongException> classe).  
  
-   Il percorso è valido (<xref:System.IO.DirectoryNotFoundException> classe).  
  
-   Il percorso contiene solo due punti, ":" (<xref:System.NotSupportedException> classe).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto. È possibile ad esempio che il file `Form1.vb` non sia un file di origine di Visual Basic. Prima di usare i dati nell'applicazione verificare tutti gli input.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Media.SoundPlayer>   
 [Procedura: caricare un suono in modo asincrono in un Windows Form](../../../../docs/framework/winforms/controls/how-to-load-a-sound-asynchronously-within-a-windows-form.md)   
 