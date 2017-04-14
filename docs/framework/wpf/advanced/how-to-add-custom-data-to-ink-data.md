---
title: "Procedura: aggiungere dati personalizzati ai dati dell&#39;input penna | Microsoft Docs"
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
  - "dati dell'input penna, aggiunta di dati personalizzati"
  - "InkCanvas, visualizzazione"
ms.assetid: f02aac6f-3436-4f7c-b6ea-0452cba5332c
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: aggiungere dati personalizzati ai dati dell&#39;input penna
È possibile aggiungere all'input penna dati personalizzati che verranno salvati insieme all'input in formato ISF \(Ink Serialized Format\).  È possibile salvare i dati personalizzati nell'oggetto <xref:System.Windows.Ink.DrawingAttributes>, <xref:System.Windows.Ink.StrokeCollection> o <xref:System.Windows.Ink.Stroke>.  La possibilità di salvare i dati personalizzati in tre oggetti consente di decidere la posizione migliore per l'archiviazione.  Tutte e tre le classi utilizzano metodi simili per l'archiviazione e l'accesso ai dati personalizzati.  
  
 Solo i tipi seguenti possono essere salvati come dati personalizzati:  
  
-   <xref:System.Boolean>  
  
-   <xref:System.Boolean>\[\]  
  
-   <xref:System.Byte>  
  
-   <xref:System.Byte>\[\]  
  
-   <xref:System.Char>  
  
-   <xref:System.Char>\[\]  
  
-   <xref:System.DateTime>  
  
-   <xref:System.DateTime>\[\]  
  
-   <xref:System.Decimal>  
  
-   <xref:System.Decimal>\[\]  
  
-   <xref:System.Double>  
  
-   <xref:System.Double>\[\]  
  
-   <xref:System.Int16>  
  
-   <xref:System.Int16>\[\]  
  
-   <xref:System.Int32>  
  
-   <xref:System.Int32>\[\]  
  
-   <xref:System.Int64>  
  
-   <xref:System.Int64>\[\]  
  
-   <xref:System.Single>  
  
-   <xref:System.Single>\[\]  
  
-   <xref:System.String>  
  
-   <xref:System.UInt16>  
  
-   <xref:System.UInt16>\[\]  
  
-   <xref:System.UInt32>  
  
-   <xref:System.UInt32>\[\]  
  
-   <xref:System.UInt64>  
  
-   <xref:System.UInt64>\[\]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come aggiungere e recuperare dati personalizzati da un oggetto <xref:System.Windows.Ink.StrokeCollection>.  
  
 [!code-csharp[HowToAddCustomDataToInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#1)]  
  
 Nell'esempio seguente viene creata un'applicazione che visualizza un oggetto <xref:System.Windows.Controls.InkCanvas> e due pulsanti.  Il pulsante `switchAuthor` consente a due autori diversi di utilizzare due penne.  Il pulsante `changePenColors` cambia il colore di ogni tratto sull'oggetto <xref:System.Windows.Controls.InkCanvas> a seconda dell'autore.  L'applicazione definisce due oggetti <xref:System.Windows.Ink.DrawingAttributes> e aggiunge a ognuno di essi una proprietà personalizzata che indica l'autore che ha tracciato l'oggetto <xref:System.Windows.Ink.Stroke>.  Quando l'utente fa clic su `changePenColors`, l'applicazione modifica l'aspetto del tratto a seconda del valore della proprietà personalizzata.  
  
 [!code-xml[HowToAddCustomDataToInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[HowToAddCustomDataToInk#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#3)]