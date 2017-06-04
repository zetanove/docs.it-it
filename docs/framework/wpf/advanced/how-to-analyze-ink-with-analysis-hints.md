---
title: "Procedura: analizzare l&#39;input penna con i suggerimenti dell&#39;analisi | Microsoft Docs"
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
  - "oggetti AnalysisHintNode"
  - "analisi di input penna"
  - "input penna, oggetti AnalysisHintNode"
  - "input penna, analisi"
ms.assetid: d4421ed4-77f5-4640-829e-9f1de50b2ff2
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: analizzare l&#39;input penna con i suggerimenti dell&#39;analisi
Un oggetto <xref:System.Windows.Ink.AnalysisHintNode> fornisce un suggerimento per l'oggetto <xref:System.Windows.Ink.InkAnalyzer> al quale è collegato.  Il suggerimento si applica all'area specificata dalla proprietà <xref:System.Windows.Ink.ContextNode.Location%2A> dell'oggetto <xref:System.Windows.Ink.AnalysisHintNode> e fornisce un contesto aggiuntivo all'analizzatore dell'input penna per migliorare l'accuratezza del riconoscimento.  L'oggetto <xref:System.Windows.Ink.InkAnalyzer> applica queste informazioni sul contesto quando analizza l'input penna ottenuto dall'interno dell'area del suggerimento.  
  
## Esempio  
 L'esempio seguente è un'applicazione che utilizza più oggetti <xref:System.Windows.Ink.AnalysisHintNode> in un form che accetta input penna.  L'applicazione utilizza la proprietà <xref:System.Windows.Ink.AnalysisHintNode.Factoid%2A> per fornire informazioni sul contesto per ogni voce del form.  L'applicazione utilizza l'analisi in background per analizzare l'input penna e cancella tutto l'input penna dal form cinque minuti dopo che l'utente smette di aggiungerlo.  
  
 [!code-xml[HowToAnalyzeInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml#1)]  
  
 [!code-csharp[HowToAnalyzeInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAnalyzeInk/CSharp/FormAnalyzer.xaml.cs#2)]
 [!code-vb[HowToAnalyzeInk#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToAnalyzeInk/VisualBasic/FormAnalyzer.xaml.vb#2)]