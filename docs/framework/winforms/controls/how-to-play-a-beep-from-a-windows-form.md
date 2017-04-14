---
title: "Procedura: riprodurre un segnale acustico da un Windows Form | Microsoft Docs"
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
  - "suoni, segnale acustico"
  - "Windows Form, suoni"
  - "riproduzione di suoni"
  - "Form, suoni"
  - "esempi [Windows Form] suoni"
ms.assetid: 7ea5cded-4888-4f35-8f28-5cab1a55c973
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: riprodurre un segnale acustico da un Windows Form
In questo esempio esegue un segnale acustico in fase di esecuzione.  
  
## <a name="example"></a>Esempio  
  
```vb  
Public Sub OnePing()  
    Beep()  
End Sub  
```  
  
```csharp  
public void onePing()  
{  
    SystemSounds.Beep.Play();  
}  
```  
  
> [!NOTE]
>  Il suono riprodotto nell'esempio di codice c# è determinato dalla <xref:System.Media.SystemSounds.Beep%2A> suoni di sistema. Per ulteriori informazioni, vedere <xref:System.Media.SystemSounds>.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Per c#, in questo esempio richiede un riferimento a di <xref:System.Media?displayProperty=fullName> dello spazio dei nomi.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.Beep%2A>   
 <xref:System.Media.SoundPlayer>   
 [Procedura: riprodurre un suono del sistema da un Windows Form](../../../../docs/framework/winforms/controls/how-to-play-a-system-sound-from-a-windows-form.md)   
 [Procedura: riprodurre un suono da un Windows Form](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)