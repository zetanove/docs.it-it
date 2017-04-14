---
title: "Procedura: gestire un evento caricato | Microsoft Docs"
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
  - "eventi, Caricato"
  - "Loaded (eventi)"
  - "XAML, Loaded (eventi)"
ms.assetid: 0cf8d003-8441-4df4-807a-6db09347e829
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: gestire un evento caricato
In questo esempio viene illustrato come gestire l'evento <xref:System.Windows.FrameworkElement.Loaded?displayProperty=fullName> e viene descritto uno scenario adatto per la gestione di tale evento.  Il gestore crea <xref:System.Windows.Controls.Button> quando viene caricata la pagina.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] con un file code\-behind.  
  
 [!code-xml[FELoaded#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FELoaded/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FELoaded#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FELoaded/CSharp/default.xaml.cs#handler)]
 [!code-vb[FELoaded#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FELoaded/VisualBasic/default.xaml.vb#handler)]  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement>   
 [Eventi di durata degli oggetti](../../../../docs/framework/wpf/advanced/object-lifetime-events.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)