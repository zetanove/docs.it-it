---
title: "Procedura: implementare un motore di layout personalizzato | Microsoft Docs"
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
  - "FlowLayoutPanel (controllo) [Windows Form], motore di layout"
  - "motori di layout, personalizzati"
  - "motori di layout, implementazione"
  - "LayoutEngine (classe)"
  - "TableLayoutPanel (controllo) [Windows Form], motore di layout"
ms.assetid: f91aa91c-29f4-4089-95ca-5d48b774b00e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: implementare un motore di layout personalizzato
Nell'esempio di codice seguente viene illustrato come creare un modulo di layout personalizzato che esegua un layout di flusso semplice.  Implementa un pannello di controllo denominato `DemoFlowPanel`, che esegue l'override della proprietà <xref:System.Windows.Forms.Control.LayoutEngine%2A> per fornire un'istanza della classe `DemoFlowLayout`.  
  
## Esempio  
 [!code-cpp[System.Windows.Forms.Layout.LayoutEngine#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.Layout.LayoutEngine/cpp/DemoFlowLayout.cpp#1)]
 [!code-csharp[System.Windows.Forms.Layout.LayoutEngine#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Layout.LayoutEngine/CS/DemoFlowLayout.cs#1)]
 [!code-vb[System.Windows.Forms.Layout.LayoutEngine#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Layout.LayoutEngine/VB/DemoFlowLayout.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.Layout.LayoutEngine>   
 <xref:System.Windows.Forms.Control.LayoutEngine%2A?displayProperty=fullName>