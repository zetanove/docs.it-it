---
title: "Procedura: riconoscere i movimenti dell&#39;applicazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "applicazione (movimenti), riconoscimento"
  - "movimenti, riconoscimento"
ms.assetid: d58b740f-5192-4a3e-af59-7aa162e6ca15
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: riconoscere i movimenti dell&#39;applicazione
Nell'esempio seguente viene illustrato come cancellare l'input penna quando un utente esegue un movimento di tipo <xref:System.Windows.Ink.ApplicationGesture> su un oggetto <xref:System.Windows.Controls.InkCanvas>.  In questo esempio si presuppone che nel file XAML sia stato dichiarato un oggetto <xref:System.Windows.Controls.InkCanvas> denominato `inkCanvas1`.  
  
## Esempio  
 [!code-csharp[HowToRecognizeGestures#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToRecognizeGestures/CSharp/Window1.xaml.cs#1)]
 [!code-vb[HowToRecognizeGestures#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToRecognizeGestures/VisualBasic/Window1.xaml.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Ink.ApplicationGesture>   
 <xref:System.Windows.Controls.InkCanvas>   
 <xref:System.Windows.Controls.InkCanvas.Gesture>