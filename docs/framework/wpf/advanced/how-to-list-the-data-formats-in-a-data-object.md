---
title: "Procedura: elencare i formati dati in un oggetto dati | Microsoft Docs"
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
  - "formati di dati [WPF], elenco"
  - "DataFormats (classe) [WPF]"
  - "trascinamento [WPF], elenco di formati di dati"
ms.assetid: 18e7ba4b-ccef-4815-ae2d-3a32891010c0
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: elencare i formati dati in un oggetto dati
Negli esempi riportati di seguito viene illustrato come utilizzare gli overlod di metodo <xref:System.Windows.DataObject.GetFormats%2A> per ottenere una matrice di stringhe che indicano ogni formato dati disponibile in un oggetto dati.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito viene utilizzato l'overload di <xref:System.Windows.DataObject.GetFormats%2A> per ottenere una matrice di stringhe contenente l'indicazione di tutti i formati dati disponibili in un oggetto dati \(nativo e a conversione automatica\).  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito viene utilizzato l'overload di <xref:System.Windows.DataObject.GetFormats%2A> per ottenere una matrice di stringhe contenente l'indicazione dei soli formati dati disponibili in un oggetto dati \(i formati dati a conversione automatica sono filtrati\).  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats_nativeonly)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats_nativeonly)]  
  
## Vedere anche  
 <xref:System.Windows.IDataObject>   
 [Cenni preliminari sul trascinamento della selezione](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)