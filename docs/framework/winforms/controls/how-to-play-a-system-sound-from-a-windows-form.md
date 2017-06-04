---
title: "Procedura: riprodurre un suono del sistema da Windows Form | Microsoft Docs"
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
  - "suoni, riproduzione per gli eventi di sistema"
  - "riproduzione di suoni, Windows Form"
  - "suoni di sistema, la riproduzione da Windows Form"
  - "riproduzione di suoni, sistema"
  - "SoundPlayer (classe), i suoni di sistema"
  - "riproduzione di suoni"
  - "esempi [Windows Form] suoni"
ms.assetid: afb206ff-4824-4804-a8d4-185bf5ad8e7c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: riprodurre un suono del sistema da Windows Form
Nell'esempio di codice viene riprodotto il `Exclamation` suono del sistema in fase di esecuzione. Per ulteriori informazioni sui suoni del sistema, vedere <xref:System.Media.SystemSounds>.  
  
## <a name="example"></a>Esempio  
  
```vb  
Public Sub PlayExclamation()  
    SystemSounds.Exclamation.Play()  
End Sub  
  
```  
  
```csharp  
public void playExclamation()  
{  
    SystemSounds.Exclamation.Play();  
}  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un riferimento di <xref:System.Media?displayProperty=fullName> dello spazio dei nomi.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Media.SoundPlayer>   
 <xref:System.Media.SystemSounds>   
 [Procedura: riprodurre un segnale acustico da un Windows Form](../../../../docs/framework/winforms/controls/how-to-play-a-beep-from-a-windows-form.md)   
 [Procedura: riprodurre un suono da un Windows Form](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)