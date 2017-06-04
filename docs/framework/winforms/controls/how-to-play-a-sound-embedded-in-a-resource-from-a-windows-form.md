---
title: "Procedura: riprodurre un suono incorporato in una risorsa da un Windows Form | Microsoft Docs"
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
  - "suoni, riproduzione da risorse"
  - "risorse [Windows Form], la riproduzione di suoni"
  - "riproduzione di suoni da risorse"
  - "SoundPlayer (classe), la riproduzione di suoni da risorse"
ms.assetid: 7d148bb6-8a1e-47d7-a08d-35828d2e688f
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: riprodurre un suono incorporato in una risorsa da un Windows Form
È possibile utilizzare il <xref:System.Media.SoundPlayer> classe per riprodurre un suono da una risorsa incorporata.  
  
## <a name="example"></a>Esempio  
 [!code-csharp[System.Windows.Forms.Sound#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Sound/CS/soundtestform.cs#10)]
 [!code-vb[System.Windows.Forms.Sound#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Sound/VB/soundtestform.vb#10)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
 L'importazione di <xref:System.Media?displayProperty=fullName> dello spazio dei nomi.  
  
 Tra cui il file audio come risorsa incorporata nel progetto.  
  
 Sostituzione di "<>\>" con il nome dell'assembly in cui è incorporato il file audio. Non includere il suffisso ". dll".  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Media.SoundPlayer>   
 [Procedura: riprodurre un suono da un Windows Form](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)   
 [Procedura: riprodurre un suono ripetutamente in un Windows Form](../../../../docs/framework/winforms/controls/how-to-loop-a-sound-playing-on-a-windows-form.md)