---
title: "Procedura: aggiungere un&#39;animazione in uno stile | Microsoft Docs"
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
  - "animazione, proprietà, all'interno degli stili"
  - "stili, animazione delle proprietà"
ms.assetid: 6a791f3d-6b1f-4972-a2f9-35880bcfd954
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: aggiungere un&#39;animazione in uno stile
In questo esempio viene illustrato come aggiungere un'animazione alle proprietà all'interno di uno stile.  Quando si aggiunge un'animazione all'interno di uno stile, solo l'elemento framework per il quale viene definito lo stile può essere utilizzato direttamente come destinazione.  Per utilizzare come destinazione un oggetto Freezable è necessario partire da una proprietà dell'elemento con stile.  
  
 Nell'esempio seguente, vengono definite diverse animazioni all'interno di un stile e vengono applicate a un <xref:System.Windows.Controls.Button>.  Quando l'utente sposta il mouse sul pulsante, questo cambia da opaco a semitrasparente e nuovamente a opaco più volte, ripetutamente.  Quando l'utente sposta il mouse lontano dal pulsante, questo diventa completamente opaco.  Quando si fa clic sul pulsante, il colore di sfondo cambia da arancione a bianco e di nuovo ad arancione.  Poiché l'oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzato per disegnare il pulsante non può essere utilizzato direttamente come destinazione, l'accesso a questo oggetto viene eseguito partendo dalla proprietà <xref:System.Windows.Controls.Control.Background%2A> del pulsante.  
  
## Esempio  
 [!code-xml[timingbehaviors_snip#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StyleStoryboardsExample.xaml#21)]  
  
 Notare che quando si aggiunge un'animazione all'interno di uno stile, è possibile utilizzare come destinazione oggetti che non esistono.  Si supponga, ad esempio che lo stile utilizzi un oggetto <xref:System.Windows.Media.SolidColorBrush> per impostare la proprietà dello sfondo di un pulsante, ma che a un certo punto viene eseguito l'override dello stile e lo sfondo del pulsante viene impostato con un oggetto <xref:System.Windows.Media.LinearGradientBrush>.  Il tentativo di aggiungere un'animazione all'oggetto <xref:System.Windows.Media.SolidColorBrush> non genererà un'eccezione; l'animazione avrà semplicemente un esito negativo.  
  
 Per ulteriori informazioni sulla sintassi di destinazione per storyboard, vedere [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  Per ulteriori informazioni sull'animazione, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  Per ulteriori informazioni sugli stili, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).