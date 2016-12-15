---
title: "Introduction to the Line and Shape Controls (Visual Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Line control, overview"
  - "Shape control, overview"
  - "lines, drawing"
  - "shapes, drawing"
ms.assetid: 5c4e8b1a-0733-4020-af6c-f582f4026728
caps.latest.revision: 6
caps.handback.revision: 6
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Introduction to the Line and Shape Controls (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

I controlli Line e Shape di Visual Basic Power Pack 1.1 sono un insieme di tre controlli grafici che consentono di disegnare righe e forme su form e contenitori.  Il controllo <xref:Microsoft.VisualBasic.PowerPacks.LineShape> consente di disegnare righe orizzontali, verticali e diagonali.  Il controllo <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> consente di disegnare cerchi e ovali. Il controllo <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> consente di disegnare rettangoli e quadrati.  
  
## Controlli Line e Shape  
 I controlli Line e Shape incapsulano molti dei metodi grafici contenuti nello spazio dei nomi <xref:System.Drawing>.  Ciò consente di disegnare righe e forme in un solo passaggio senza dover creare oggetti grafici, penne e pennelli.  È possibile utilizzare tecniche grafiche complesse quale il riempimento sfumato semplicemente impostando alcune proprietà.  
  
 Sebbene sia possibile disegnare righe e forme anche con metodi grafici, l'utilizzo dei controlli Line e Shape presenta diversi vantaggi:  
  
-   I metodi grafici possono essere chiamati solo in fase di esecuzione.  I controlli Line e Shape, invece, possono essere aggiunti a un form in fase di progettazione.  In tal modo è possibile visualizzarne l'aspetto e posizionarli correttamente. Possono inoltre essere aggiunti in fase di esecuzione.  
  
-   I controlli Line e Shape possono essere selezionati in fase di esecuzione e forniscono eventi quali <xref:Microsoft.VisualBasic.PowerPacks.Shape.Click> e <xref:Microsoft.VisualBasic.PowerPacks.Shape.OnDoubleClick%2A>.  Gli output dei metodi grafici, invece, non sono selezionabili e non forniscono eventi.  
  
-   I controlli Line e Shape forniscono metodi <xref:Microsoft.VisualBasic.PowerPacks.Shape.BringToFront%2A> e <xref:Microsoft.VisualBasic.PowerPacks.Shape.SendToBack%2A> che consentono di controllare il relativo ordine Z in fase di progettazione e in fase di esecuzione.  L'ordine Z dei metodi grafici può essere controllato unicamente modificando il relativo ordine di esecuzione in fase di esecuzione.  
  
-   I controlli Line e Shape sono privi di finestre. Non dispongono di handle di finestra e comportano pertanto un minore utilizzo delle risorse di sistema.  
  
### Modello a oggetti  
 I controlli Line e Shape derivano da una classe base <xref:Microsoft.VisualBasic.PowerPacks.Shape> in cui vengono definite le relative proprietà condivise, i metodi e gli eventi.  
  
 Nell'immagine riportata di seguito viene illustrata la gerarchia di oggetti Line e Shape.  
  
 ![Diagramma della gerarchia di oggetti Line e Shape](../../../visual-basic/developing-apps/windows-forms/media/lineshapeobject.png "LineShapeObject")  
Gerarchia di oggetti Line e Shape  
  
 Nella classe derivata <xref:Microsoft.VisualBasic.PowerPacks.LineShape> sono contenuti metodi, proprietà ed eventi relativi esclusivamente alle righe.  La classe derivata <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape> rappresenta la classe base per <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> e <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> e contiene proprietà, metodi ed eventi comuni a tutte le forme.  È anche possibile utilizzare <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape> per creare controlli `Shape` personalizzati derivati.  
  
 Le classi <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> e <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> consentono di disegnare cerchi, ovali, rettangoli e rettangoli con angoli arrotondati.  
  
 Quando si aggiunge un controllo Line o Shape a un form o a un contenitore, viene creato un oggetto <xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer> invisibile.  L'oggetto <xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer> funge da area di disegno per le forme all'interno di ciascun controllo contenitore. Ogni <xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer> dispone di un oggetto <xref:Microsoft.VisualBasic.PowerPacks.ShapeCollection> corrispondente che consente di scorrere i controlli Line e Shape.  È possibile spostare forme da un contenitore a un altro mediante un'operazione di taglia e incolla o di trascinamento della selezione.  Una volta rimossa l'ultima forma da un contenitore, viene rimosso anche l'oggetto <xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer>.  
  
> [!NOTE]
>  I controlli Line e Shape non sono supportati da tutti i controlli contenitore.  I controlli Line o Shape non possono essere contenuti in <xref:System.Windows.Forms.TableLayoutPanel> o <xref:System.Windows.Forms.FlowLayoutPanel>.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks>   
 [How to: Draw Lines with the LineShape Control](../../../visual-basic/developing-apps/windows-forms/how-to-draw-lines-with-the-lineshape-control-visual-studio.md)   
 [How to: Draw Shapes with the OvalShape and RectangleShape Controls](../../../visual-basic/developing-apps/windows-forms/how-to-draw-shapes-with-the-ovalshape-and-rectangleshape-controls.md)   
 [How to: Enable Tabbing Between Shapes](../../../visual-basic/developing-apps/windows-forms/how-to-enable-tabbing-between-shapes-visual-studio.md)