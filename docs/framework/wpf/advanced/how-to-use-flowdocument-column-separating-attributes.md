---
title: "Procedura: utilizzare gli attributi di separazione delle colonne di un oggetto FlowDocument | Microsoft Docs"
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
  - "attributi di separazione delle colonne"
  - "documenti, FlowDocument (attributi di separazione delle colonne)"
  - "FlowDocument (attributi di separazione delle colonne)"
ms.assetid: c7a822f8-aeca-45bd-a258-2852ff28005c
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: utilizzare gli attributi di separazione delle colonne di un oggetto FlowDocument
Nell'esempio riportato di seguito è illustrato l'utilizzo delle funzionalità di separazione delle colonne di un oggetto <xref:System.Windows.Documents.FlowDocument>.  
  
## Esempio  
 Nell'esempio seguente viene definito un oggetto <xref:System.Windows.Documents.FlowDocument> e vengono impostati gli attributi <xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>, <xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A> e <xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A>.  L'oggetto <xref:System.Windows.Documents.FlowDocument> include un solo paragrafo del contenuto di esempio.  
  
 [!code-xml[FlowDocumentSnippets#_FlowDocumentColumnStuffXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentSnippets/CSharp/Window1.xaml#_flowdocumentcolumnstuffxaml)]  
  
 Nella figura riportata di seguito vengono mostrati gli effetti degli attributi <xref:System.Windows.Documents.FlowDocument.ColumnGap%2A>, <xref:System.Windows.Documents.FlowDocument.ColumnRuleBrush%2A> e <xref:System.Windows.Documents.FlowDocument.ColumnRuleWidth%2A> in un oggetto <xref:System.Windows.Documents.FlowDocument> sottoposto a rendering.  
  
 ![Schermata: FlowDocument con colonne](../../../../docs/framework/wpf/advanced/media/flowdocumentintracolumn.png "FlowDocumentIntraColumn")