---
title: "Procedura: assicurarsi che GridSplitter sia visibile | Microsoft Docs"
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
  - "GridSplitter (controllo), assicurazione di visibilità"
ms.assetid: 0a62a964-89c8-48f0-9023-5df721a8cf47
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: assicurarsi che GridSplitter sia visibile
In questo esempio viene illustrato come assicurarsi che un controllo <xref:System.Windows.Controls.GridSplitter> non sia nascosto da altri controlli in una classe <xref:System.Windows.Controls.Grid>.  
  
## Esempio  
 Il rendering della proprietà <xref:System.Windows.Controls.Panel.Children%2A> di un controllo <xref:System.Windows.Controls.Grid> viene eseguito nell'ordine di definizione nel markup o nel codice.  I controlli <xref:System.Windows.Controls.GridSplitter> possono essere nascosti da altri controlli se non vengono definiti come ultimi elementi nella raccolta <xref:System.Windows.Controls.Panel.Children%2A> o se si assegna ad altri controlli un campo <xref:System.Windows.Controls.Panel.ZIndexProperty> più alto.  
  
 Per evitare la presenza di controlli <xref:System.Windows.Controls.GridSplitter> nascosti, eseguire una delle operazioni seguenti.  
  
-   Verificare che i controlli <xref:System.Windows.Controls.GridSplitter> siano le ultime proprietà <xref:System.Windows.Controls.Panel.Children%2A> aggiunte alla classe <xref:System.Windows.Controls.Grid>.  Nell'esempio riportato di seguito viene illustrato l'oggetto <xref:System.Windows.Controls.GridSplitter> come ultimo elemento nella raccolta <xref:System.Windows.Controls.Panel.Children%2A> della classe <xref:System.Windows.Controls.Grid>.  
  
 [!code-xml[GridSplitterSnips#GridSplitterLastChild](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplitterlastchild)]  
  
-   Impostare il campo <xref:System.Windows.Controls.Panel.ZIndexProperty> su <xref:System.Windows.Controls.GridSplitter> su un valore più alto rispetto a un controllo che, in caso contrario, lo nasconderebbe.  Nell'esempio riportato di seguito viene impostato un valore più alto del campo <xref:System.Windows.Controls.Panel.ZIndexProperty> per il controllo <xref:System.Windows.Controls.GridSplitter> rispetto al controllo <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[GridSplitterSnips#GridSplitterZIndex](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplitterzindex)]  
  
-   Impostare i margini sul controllo che, in caso contrario, nasconderebbe <xref:System.Windows.Controls.GridSplitter> in modo tale che <xref:System.Windows.Controls.GridSplitter> sia esposto.  Nell'esempio riportato di seguito vengono impostati margini su un controllo che, in caso contrario, verrebbe sovrapposto e nasconderebbe l'oggetto <xref:System.Windows.Controls.GridSplitter>.  
  
 [!code-xml[GridSplitterSnips#GridSplitterMargin](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplittermargin)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.GridSplitter>   
 [Procedure relative](../../../../docs/framework/wpf/controls/gridsplitter-how-to-topics.md)