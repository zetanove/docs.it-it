---
title: "Procedura: definire un modello GroupBox | Microsoft Docs"
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
  - "controlli, GroupBox"
  - "GroupBox (controllo), creazione di modelli"
ms.assetid: 85a4d1a7-4753-4f4a-b26d-14fa10c1ddb5
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: definire un modello GroupBox
In questo esempio viene illustrato come creare un modello per un controllo <xref:System.Windows.Controls.GroupBox>.  
  
## Esempio  
 Nell'esempio seguente viene definito un modello di controllo <xref:System.Windows.Controls.GroupBox> utilizzando un controllo <xref:System.Windows.Controls.Grid> per il layout.  Nel modello viene utilizzato un oggetto <xref:System.Windows.Controls.BorderGapMaskConverter> per definire il bordo del controllo <xref:System.Windows.Controls.GroupBox> in modo che non nasconda il contenuto del controllo <xref:System.Windows.Controls.HeaderedContentControl.Header%2A>.  
  
 [!code-xml[GroupBoxSnippet#GroupBoxTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#groupboxtemplate)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.GroupBox>   
 [GroupBox How\-to Topics](http://msdn.microsoft.com/it-it/7692e155-a4c6-428c-b7e0-64b3740daca7)