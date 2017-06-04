---
title: "Riconoscimento della grafia | Microsoft Docs"
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
  - "riconoscimento della grafia"
  - "grafia (riconoscimento)"
ms.assetid: f4e8576d-e731-4bac-9818-22e2ae636636
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Riconoscimento della grafia
In questa sezione vengono descritti gli elementi di base del riconoscimento relativamente all'input digitale nella piattaforma [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
## Soluzioni di riconoscimento  
 Nell'esempio seguente viene illustrato come riconoscere l'input penna utilizzando <xref:System.Windows.Ink.InkAnalyzer>.  
  
> [!NOTE]
>  Per questo esempio è necessario che il riconoscimento grafia sia installato nel sistema.  
  
 Creare un nuovo progetto di applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in Visual Studio 2005 denominato InkRecognition.  Sostituire il contenuto del file Window1.xaml con il codice XAML seguente.  Il codice esegue il rendering dell'interfaccia utente dell'applicazione.  
  
 [!code-xml[InkRecognition#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkRecognition/CSharp/Window1.xaml#1)]  
  
 Aggiungere un riferimento agli assembly di analisi dell'input penna di WPF, IAWinFX.dll, IACore.dll e IALoader.dll, disponibili in \\\\Programmi\\\\Reference Assemblies\\\\Microsoft\\\\Tablet PC\\\\v1 .7.  Sostituire il contenuto del file code\-behind con il codice seguente.  
  
 [!code-csharp[InkRecognition#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkRecognition/CSharp/Window1.xaml.cs#2)]
 [!code-vb[InkRecognition#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InkRecognition/VisualBasic/Window1.xaml.vb#2)]  
  
## Vedere anche  
 <xref:System.Windows.Ink.InkAnalyzer>   
 <xref:System.Windows.Ink.AnalysisStatus>   
 <xref:System.Windows.Controls.InkCanvas>