---
title: "Procedura: creare testo sullo sfondo di un controllo | Microsoft Docs"
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
  - "sfondi, creazione di testo"
  - "controlli, creazione di testo negli sfondi"
  - "disegno, testo per il controllo degli sfondi"
  - "testo, disegno per il controllo degli sfondi"
  - "tipografia, creazione di testo per il controllo degli sfondi"
ms.assetid: 686d8fba-f61c-4974-a871-c635d67a7f69
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: creare testo sullo sfondo di un controllo
È possibile creare testo direttamente sullo sfondo di un controllo convertendo una stringa di testo in un oggetto <xref:System.Windows.Media.FormattedText>, quindi disegnando l'oggetto nell'oggetto <xref:System.Windows.Media.DrawingContext>del controllo.  È anche possibile utilizzare questa tecnica per disegnare sullo sfondo di oggetti derivati da <xref:System.Windows.Controls.Panel>, ad esempio <xref:System.Windows.Controls.Canvas> e <xref:System.Windows.Controls.StackPanel>.  
  
 ![Controlli che visualizzano testo come sfondo](../../../../docs/framework/wpf/advanced/media/drawtext2background01.png "DrawText2Background01")  
Esempio di controlli con sfondi di testo personalizzati  
  
## Esempio  
 Per disegnare sullo sfondo di un controllo, creare un oggetto <xref:System.Windows.Media.DrawingBrush> nuovo e disegnare il testo convertito nell'oggetto <xref:System.Windows.Media.DrawingContext> dell'oggetto.  Quindi, assegnare il nuovo oggetto <xref:System.Windows.Media.DrawingBrush> alla proprietà dello sfondo del controllo.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come creare un oggetto <xref:System.Windows.Media.FormattedText> e  disegnare sullo sfondo di un oggetto <xref:System.Windows.Controls.Label> e di un oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-csharp[DrawTextToControlBackground#DrawTextToControlBackground1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawTextToControlBackground/CSHARP/Window1.xaml.cs#drawtexttocontrolbackground1)]  
  
## Vedere anche  
 <xref:System.Windows.Media.FormattedText>   
 [Disegno di testo formattato](../../../../docs/framework/wpf/advanced/drawing-formatted-text.md)