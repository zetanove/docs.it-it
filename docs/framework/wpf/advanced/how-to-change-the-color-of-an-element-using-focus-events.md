---
title: "Procedura: modificare il colore di un elemento utilizzando eventi di stato attivo | Microsoft Docs"
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
  - "colori di elementi, modifica"
  - "elementi, modifica del colore"
  - "Focus (eventi), modifica del colore di elementi"
ms.assetid: 7e246802-3625-47a7-ae9d-c8a2a40fd040
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: modificare il colore di un elemento utilizzando eventi di stato attivo
In questo esempio viene mostrato come modificare il colore di un elemento quando riceve e perde lo stato attivo utilizzando gli eventi <xref:System.Windows.UIElement.GotFocus> e <xref:System.Windows.UIElement.LostFocus>.  
  
 In questo esempio sono presenti un file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e un file code\-behind.  
  
## Esempio  
 Nel linguaggio [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] seguente viene creata l'interfaccia utente, costituita da due oggetti <xref:System.Windows.Controls.Button> e vengono collegati i gestori eventi per gli eventi <xref:System.Windows.UIElement.GotFocus> e <xref:System.Windows.UIElement.LostFocus> agli oggetti <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml#gotlostfocussamplexaml)]  
  
 Nel code\-behind seguente vengono creati i gestori eventi <xref:System.Windows.UIElement.GotFocus> e <xref:System.Windows.UIElement.LostFocus>.  Quando l'oggetto <xref:System.Windows.Controls.Button> riceve lo stato attivo, la proprietà <xref:System.Windows.Controls.Control.Background%2A> dell'oggetto <xref:System.Windows.Controls.Button> viene impostata sul rosso.  Quando l'oggetto <xref:System.Windows.Controls.Button> perde lo stato attivo, la proprietà <xref:System.Windows.Controls.Control.Background%2A> dell'oggetto <xref:System.Windows.Controls.Button> viene nuovamente impostata sul bianco.  
  
 [!code-csharp[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml.cs#gotlostfocussampleeventhandlers)]
 [!code-vb[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/VisualBasic/Window1.xaml.vb#gotlostfocussampleeventhandlers)]  
  
## Vedere anche  
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)