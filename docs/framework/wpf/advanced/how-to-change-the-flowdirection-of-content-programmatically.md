---
title: "Procedura: cambiare la propriet&#224; FlowDirection del contenuto a livello di codice | Microsoft Docs"
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
  - "documenti, modifica della proprietà FlowDirection a livello di codice"
  - "FlowDirection (proprietà), modifica a livello di codice"
ms.assetid: 02f5a8ba-f8c0-4e5a-84b9-4c5bf12922a2
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: cambiare la propriet&#224; FlowDirection del contenuto a livello di codice
In questo esempio viene illustrato come cambiare a livello di codice la proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A> di un oggetto <xref:System.Windows.Controls.FlowDocumentReader>.  
  
## Esempio  
 Vengono creati due elementi <xref:System.Windows.Controls.Button>, ognuno dei quali rappresenta uno dei valori possibili di <xref:System.Windows.FlowDirection>.  Quando viene fatto clic su un pulsante, il valore della proprietà associata viene applicato al contenuto di un oggetto <xref:System.Windows.Controls.FlowDocumentReader> denominato `tf1`.  Il valore della proprietà viene inoltre scritto in un oggetto <xref:System.Windows.Controls.TextBlock> denominato `txt1`.  
  
 [!code-xml[FlowDirectionSnippets#_FlowDirectionXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml#_flowdirectionxaml)]  
  
## Esempio  
 Gli eventi associati ai clic sui pulsanti definiti in precedenza sono gestiti in un file code\-behind di [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)].  
  
 [!code-csharp[FlowDirectionSnippets#_FlowDirection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml.cs#_flowdirection)]
 [!code-vb[FlowDirectionSnippets#_FlowDirection](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDirectionSnippets/VisualBasic/Window1.xaml.vb#_flowdirection)]