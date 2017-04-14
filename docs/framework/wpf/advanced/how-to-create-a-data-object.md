---
title: "Procedura: creare un oggetto dati | Microsoft Docs"
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
  - "oggetti dati [WPF], creazione"
  - "DataObject (classe) [WPF], creazione"
  - "trascinamento [WPF], creazione di oggetti dati"
ms.assetid: 022fa142-717d-4fea-a53c-3b52e9d91aff
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: creare un oggetto dati
Negli esempi seguenti vengono illustrate varie modalità di creazione di un oggetto dati utilizzando i costruttori forniti dalla classe <xref:System.Windows.DataObject>.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito viene creato un nuovo oggetto dati e viene utilizzato uno dei costruttori di overload \(<xref:System.Windows.DataObject.%23ctor%28System.Object%29>\) per inizializzare l'oggetto dati con una stringa.  In questo caso, viene determinato automaticamente un formato dati appropriato in base al tipo di dati archiviati e la conversione automatica dei dati archiviati è consentita per impostazione predefinita.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_simple)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_simple)]  
  
### Descrizione  
 L'esempio di codice seguente è una versione ridotta del codice illustrato in precedenza.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple_Condensed](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_simple_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple_Condensed](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_simple_condensed)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito viene creato un nuovo oggetto dati e viene utilizzato uno dei costruttori di overload \(<xref:System.Windows.DataObject.%23ctor%28System.String%2CSystem.Object%29>\) per inizializzare l'oggetto dati con una stringa e un formato dati specificato.  In questo caso, il formato dati è specificato da una stringa; la classe <xref:System.Windows.DataFormats> fornisce un insieme di stringhe di tipo predefinite.  La conversione automatica dei dati archiviati è consentita per impostazione predefinita.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring)]  
  
### Descrizione  
 L'esempio di codice seguente è una versione ridotta del codice illustrato in precedenza.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString_Condensed](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString_Condensed](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring_condensed)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito viene creato un nuovo oggetto dati e viene utilizzato uno dei costruttori di overload \(<xref:System.Windows.DataObject.%23ctor%2A>\) per inizializzare l'oggetto dati con una stringa e un formato dati specificato.  In questo caso il formato dati è specificato da un parametro <xref:System.Type>.  La conversione automatica dei dati archiviati è consentita per impostazione predefinita.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_type)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_type)]  
  
### Descrizione  
 L'esempio di codice seguente è una versione ridotta del codice illustrato in precedenza.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type_Condensed](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_type_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type_Condensed](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_type_condensed)]  
  
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito viene creato un nuovo oggetto dati e viene utilizzato uno dei costruttori di overload \(<xref:System.Windows.DataObject.%23ctor%28System.String%2CSystem.Object%2CSystem.Boolean%29>\) per inizializzare l'oggetto dati con una stringa e un formato dati specificato.  In questo caso, il formato dati è specificato da una stringa; la classe <xref:System.Windows.DataFormats> fornisce un insieme di stringhe di tipo predefinite.  Questo particolare overload del costruttore consente al chiamante di specificare se è consentita la conversione automatica.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_autoconvert)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_autoconvert)]  
  
### Descrizione  
 L'esempio di codice seguente è una versione ridotta del codice illustrato in precedenza.  
  
### Codice  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert_Condensed](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_autoconvert_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert_Condensed](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_autoconvert_condensed)]  
  
## Vedere anche  
 <xref:System.Windows.IDataObject>