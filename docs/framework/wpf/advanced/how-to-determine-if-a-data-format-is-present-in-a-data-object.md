---
title: "Procedura: determinare se un formato di dati &#232; presente in un oggetto dati | Microsoft Docs"
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
  - "formati di dati [WPF], rilevamento eventuale presenza"
  - "DataFormats (classe) [WPF]"
  - "trascinamento [WPF], formati di dati presenti"
ms.assetid: e487a454-c9fc-4e53-aeaa-c458d059ad4c
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: determinare se un formato di dati &#232; presente in un oggetto dati
Negli esempi seguenti viene mostrato come utilizzare i diversi overload del metodo <xref:System.Windows.DataObject.GetDataPresent%2A> per eseguire una query al fine di determinare se un particolare formato di dati è presente in un oggetto dati.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice seguente viene utilizzato l'overload di <xref:System.Windows.DataObject.GetDataPresent%28System.String%29> per eseguire una query per la presenza di un particolare formato dati in base alla stringa del descrittore.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_String](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_querydataformats_string)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_String](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_querydataformats_string)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice seguente viene utilizzato l'overload di <xref:System.Windows.DataObject.GetDataPresent%28System.Type%29> per eseguire una query per la presenza di un particolare formato dati in base al tipo.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Type](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_querydataformats_type)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Type](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_querydataformats_type)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice seguente viene utilizzato l'overload di <xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> per eseguire una query per i dati in base alla stringa del descrittore e specificando il modo in cui trattare i formati dati convertibili automaticamente.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Autoconvert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_querydataformats_autoconvert)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Autoconvert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_querydataformats_autoconvert)]  
  
## Vedere anche  
 <xref:System.Windows.IDataObject>