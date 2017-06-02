---
title: "Procedura: recuperare dati in un formato dati particolare | Microsoft Docs"
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
  - "DataFormats (classe) [WPF], recupero dei dati"
  - "DataObject (classe) [WPF], recupero dei dati"
  - "trascinamento [WPF], recupero dei dati"
ms.assetid: a625acf3-1144-44cd-add7-456aefc3859f
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: recuperare dati in un formato dati particolare
Negli esempi seguenti viene mostrato come recuperare dati da un oggetto dati in un formato specifico.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice seguente viene utilizzato l'overload dell'oggetto <xref:System.Windows.DataObject.GetDataPresent%28System.String%29> per verificare innanzitutto se è disponibile un formato dati specificato \(a livello nativo o mediante conversione automatica\); se il formato specificato è disponibile, l'esempio recupera i dati utilizzando il metodo <xref:System.Windows.DataObject.GetData%28System.String%29>.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
## Esempio  
  
### Descrizione  
 Nel codice di esempio seguente viene utilizzato l'overload dell'oggetto <xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> per verificare innanzitutto se un formato dati specificato è disponibile a livello nativo \(i formati dati convertibili automaticamente sono filtrati\); se il formato specificato è disponibile, l'esempio recupera i dati utilizzando il metodo <xref:System.Windows.DataObject.GetData%28System.String%29>.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat_Native](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat_native)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat_Native](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat_native)]  
  
## Vedere anche  
 <xref:System.Windows.IDataObject>   
 [Cenni preliminari sul trascinamento della selezione](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)