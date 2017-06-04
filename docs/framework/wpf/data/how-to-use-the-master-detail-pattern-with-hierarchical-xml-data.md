---
title: "Procedura: utilizzare il modello Master-Details con dati XML gerarchici | Microsoft Docs"
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
  - "associazione dati, paradigma dati Master-Detail"
  - "paradigma dati Master-Detail"
ms.assetid: eb8dbdd8-5871-42bb-a16b-04e655fea677
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: utilizzare il modello Master-Details con dati XML gerarchici
In questo esempio viene illustrato come implementare lo scenario Master\-Details con i dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)].  
  
## Esempio  
 Questo esempio rappresenta la versione dei dati [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] dell'esempio illustrato in [Utilizzare il modello Master\-Details con dati gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md).  In questo esempio, i dati provengono dal file `League.xml`.  Notare il modo in cui il terzo controllo di <xref:System.Windows.Controls.ListBox> tiene traccia delle modifiche alla selezione apportate al secondo oggetto <xref:System.Windows.Controls.ListBox> mediante l'associazione alla relativa proprietà <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A>.  
  
 [!code-xml[MasterDetailXml#HowTo1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MasterDetailXml/CS/Window1.xaml#howto1)]  
[!code-xml[MasterDetailXml#HowTo2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MasterDetailXml/CS/Window1.xaml#howto2)]  
  
## Vedere anche  
 <xref:System.Windows.HierarchicalDataTemplate>   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)