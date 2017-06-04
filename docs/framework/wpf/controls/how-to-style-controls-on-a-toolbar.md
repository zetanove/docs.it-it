---
title: "Procedura: applicare uno stile ai controlli di un oggetto ToolBar | Microsoft Docs"
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
  - "personalizzazione di controlli sulla barra degli strumenti"
  - "stile di controlli sulla barra degli strumenti"
  - "barre degli strumenti"
ms.assetid: ba6ae056-d6a9-4c24-90f8-467ab0bc0b1a
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: applicare uno stile ai controlli di un oggetto ToolBar
L'oggetto <xref:System.Windows.Controls.ToolBar> definisce gli oggetti <xref:System.Windows.ResourceKey> per specificare lo stile dei controlli all'interno di <xref:System.Windows.Controls.ToolBar> stessa.  Per applicare uno stile a un controllo di un oggetto <xref:System.Windows.Controls.ToolBar>, impostare l'attributo `x:key` dello stile su un oggetto <xref:System.Windows.ResourceKey> definito in <xref:System.Windows.Controls.ToolBar>.  
  
 L'oggetto <xref:System.Windows.Controls.ToolBar> definisce i seguenti oggetti <xref:System.Windows.ResourceKey>:  
  
-   <xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.CheckBoxStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.ComboBoxStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.MenuStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.RadioButtonStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.SeparatorStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.TextBoxStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.ToggleButtonStyleKey%2A>  
  
## Esempio  
 Nell'esempio riportato di seguito vengono definiti gli stili dei controlli all'interno di un oggetto <xref:System.Windows.Controls.ToolBar>.  
  
 [!code-xml[ToolBar_snip#ToolBarAllStyles](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBar_snip/CS/pane1.xaml#toolbarallstyles)]  
[!code-xml[ToolBar_snip#ToolBar](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBar_snip/CS/pane1.xaml#toolbar)]  
  
## Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)