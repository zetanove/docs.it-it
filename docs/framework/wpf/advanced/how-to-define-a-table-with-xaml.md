---
title: "Procedura: definire un oggetto Table tramite XAML | Microsoft Docs"
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
  - "documenti, definizione di tabelle con XAML"
  - "tabelle, definizione con XAML"
  - "XAML, definizione di tabelle"
ms.assetid: 83f2dc58-437e-4cdc-b5dd-0019810c7a85
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: definire un oggetto Table tramite XAML
Nell'esempio riportato di seguito viene illustrato come definire un oggetto <xref:System.Windows.Documents.Table> utilizzando [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  La tabella dell'esempio ha quattro colonne, rappresentate da elementi <xref:System.Windows.Documents.TableColumn>, e numerose righe, rappresentate da elementi <xref:System.Windows.Documents.TableRow>, che contengono dati e informazioni relative a titolo, intestazione e piè di pagina.  Le righe devono essere contenute in un elemento <xref:System.Windows.Documents.TableRowGroup>.  Ogni riga della tabella è costituita da una o più celle, rappresentate da elementi <xref:System.Windows.Documents.TableCell>.  Il contenuto di una cella della tabella deve essere trovarsi in elemento <xref:System.Windows.Documents.Block>; in questo caso vengono utilizzati gli elementi <xref:System.Windows.Documents.Paragraph>.  Nella riga a piè di pagina, la tabella ospita anche un collegamento ipertestuale, rappresentato dall'elemento <xref:System.Windows.Documents.Hyperlink>.  
  
## Esempio  
 [!code-xml[TableSnippetsXAML#_TableXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TableSnippetsXAML/CS/Window1.xaml#_tablexaml)]  
  
 Nella figura riportata di seguito viene illustrato il rendering della tabella definita in questo esempio.  
  
 ![Tabella sottoposta a rendering](../../../../docs/framework/wpf/advanced/media/tableeg.png "TableEG")