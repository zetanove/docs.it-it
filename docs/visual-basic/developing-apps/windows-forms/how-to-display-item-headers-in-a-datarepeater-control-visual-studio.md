---
title: "How to: Display Item Headers in a DataRepeater Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, item headers"
  - "DataRepeater, selection indicators"
ms.assetid: 37321447-0ffa-43e1-bdc9-0480e392b90f
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# How to: Display Item Headers in a DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'intestazione elemento in un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> fornisce un indicatore visivo della selezione di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>.  Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> è impostata su <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles> \(impostazione predefinita\), l'intestazione elemento viene visualizzata a sinistra di ciascun elemento.  Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> è impostata su <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles>, l'intestazione elemento viene visualizzata nella parte superiore di ciascun elemento.  
  
 Quando viene selezionata per la prima volta, l'intestazione elemento viene visualizzata nel colore specificato dalla proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> e viene visualizzata un'icona costituita da una freccia bianca.  
  
> [!NOTE]
>  Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> è impostata su <xref:System.Drawing.Color.White%2A>, il simbolo di selezione non sarà visibile quando l'elemento viene selezionato per la prima volta.  
  
 Quando un campo in <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> ha lo stato attivo, il colore dell'intestazione elemento passa al colore di sfondo di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> e l'icona a forma di freccia diventa nera.  Se i dati vengono modificati, nell'intestazione elemento viene visualizzato il simbolo di una matita.  
  
 La larghezza \(oppure l'altezza, se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> è impostata su <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles>\) predefinita dell'intestazione elemento è di 15 pixel.  Per modificare la larghezza, impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A>.  
  
> [!NOTE]
>  Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> è impostata su un valore minore di 11, i simboli degli indicatori non verranno visualizzati nell'intestazione elemento.  
  
 Per nascondere le intestazioni degli elementi, impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderVisible%2A> su **False**.  Quando la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderVisible%2A> è impostata su **False**, la selezione di un elemento è indicata unicamente da una linea punteggiata attorno al perimetro di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>.  
  
> [!NOTE]
>  È inoltre possibile fornire un indicatore di selezione personalizzato monitorando la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A> di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> nell'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A>.  
  
### Per modificare l'aspetto delle intestazioni degli elementi  
  
1.  In Progettazione Windows Form, selezionare l'area inferiore del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
    > [!NOTE]
    >  Selezionare l'area inferiore del controllo.  Selezionando l'area del modello di elemento, nella finestra Proprietà verrà visualizzato un diverso insieme di proprietà.  
  
2.  Nella finestra Proprietà, utilizzare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> per modificare il colore delle intestazioni degli elementi.  
  
    > [!NOTE]
    >  Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> è impostata su <xref:System.Drawing.Color.White%2A>, il simbolo di selezione non sarà visibile quando l'elemento viene selezionato per la prima volta.  
  
3.  Utilizzare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> per modificare la larghezza \(o l'altezza\) delle intestazioni degli elementi.  
  
    > [!NOTE]
    >  Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> è impostata su un valore minore di 11, i simboli degli indicatori non verranno visualizzati nell'intestazione elemento.  
  
### Per nascondere le intestazioni degli elementi  
  
1.  In Progettazione Windows Form, selezionare l'area inferiore del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
    > [!NOTE]
    >  Selezionare l'area inferiore del controllo.  Selezionando l'area del modello di elemento, nella finestra Proprietà verrà visualizzato un diverso insieme di proprietà.  
  
2.  Nella finestra Proprietà, impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderVisible%2A> su **False**.  
  
     Quando viene selezionato un elemento in <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, tale selezione è indicata unicamente da una linea punteggiata attorno al perimetro di <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [How to: Change the Layout of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)