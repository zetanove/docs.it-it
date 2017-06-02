---
title: "Procedura: archiviare pi&#249; formati di dati in un oggetto dati | Microsoft Docs"
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
  - "DataFormats (classe) [WPF], archiviazione in più formati"
  - "DataObject (classe) [WPF], archiviazione in più formati"
  - "trascinamento [WPF], archiviazione in più formati"
ms.assetid: 941ace29-29c4-4c26-b75b-ea7d06aa0d69
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: archiviare pi&#249; formati di dati in un oggetto dati
Nell'esempio riportato di seguito viene illustrato come utilizzare il metodo <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29> per aggiungere dati a un oggetto dati in più formati.  
  
## Esempio  
  
### Descrizione  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
## Vedere anche  
 <xref:System.Windows.IDataObject>   
 [Cenni preliminari sul trascinamento della selezione](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)