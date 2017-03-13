---
title: "How to: Draw Shapes with the OvalShape and RectangleShape Controls (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "OvalShape control"
  - "shapes, drawing"
  - "RectangleShape control"
ms.assetid: 0275b4c6-7a13-46c8-90f3-61db308c6b5d
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Draw Shapes with the OvalShape and RectangleShape Controls (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il controllo <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> consente di disegnare cerchi e ovali in un form o in un contenitore, sia in fase di progettazione che in fase di esecuzione.  Il controllo <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> può essere usato per disegnare quadrati, rettangoli o rettangoli con angoli arrotondati in un form o in un contenitore.  Anche questo controllo può essere usato sia in fase di progettazione che in fase di esecuzione.  
  
 È possibile personalizzare l'aspetto delle forme modificandone la larghezza, il colore e lo stile del bordo.  Lo sfondo di una forma è trasparente per impostazione predefinita. È possibile personalizzare lo sfondo per visualizzare un colore a tinta unita, un motivo, un riempimento sfumato \(una transizione da un colore a altro\) o un'immagine.  
  
### Per disegnare una forma semplice in fase di progettazione  
  
1.  Trascinare il controllo <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> o <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> dalla scheda **Visual Basic Power Packs** \(vedere [Visual Basic Power Packs Controls](../../../visual-basic/developing-apps/windows-forms/power-packs-controls.md) per installare\) della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Trascinare i quadratini di ridimensionamento e di spostamento per impostare le dimensioni e la posizione della forma.  
  
     È anche possibile ridimensionare e posizionare la forma modificando le proprietà `Size` e `Position` nella finestra **Proprietà**.  
  
     Per creare un rettangolo con gli angoli arrotondati, selezionare la proprietà `CornerRadius` nella finestra **Proprietà** e impostarla su un valore maggiore di 0.  
  
3.  Nella finestra **Proprietà** è possibile impostare proprietà facoltative aggiuntive per modificare l'aspetto delle forme.  
  
### Per disegnare una forma semplice in fase di esecuzione  
  
1.  Nel menu **Progetto** fare clic su **Aggiungi riferimento**.  
  
2.  Nella finestra di dialogo **Aggiungi riferimento**, selezionare **Microsoft.VisualBasic.PowerPacks.VS**, quindi scegliere **OK**.  
  
3.  Nell'**editor di codice**, aggiungere un'istruzione`Imports` o `using` all'inizio del modulo:  
  
    ```vb#  
    Imports Microsoft.VisualBasic.PowerPacks  
    ```  
  
    ```c#  
    using Microsoft.VisualBasic.PowerPacks;  
    ```  
  
4.  Nella routine `Event` aggiungere il codice seguente:  
  
     [!code-cs[VbPowerpacksShape#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-draw-shapes-with-the-ovalshape-and-rectangleshape-controls_1.cs)]
     [!code-vb[VbPowerpacksShape#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-draw-shapes-with-the-ovalshape-and-rectangleshape-controls_1.vb)]  
  
## Personalizzazione di forme  
 Quando si usano le impostazioni predefinite, i controlli <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> e <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> vengono visualizzati con un bordo nero continuo largo un pixel e uno sfondo trasparente.  Specifiche proprietà consentono di modificare la larghezza, lo stile e il colore del bordo.  Proprietà aggiuntive consentono di impostare lo sfondo delle forme su una tinta unita, un motivo, un riempimento sfumato o un'immagine.  
  
 Prima di modificare lo sfondo di una forma, è necessario conoscere l'interazione di diverse proprietà.  
  
-   L'impostazione della proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.BackColor%2A> ha effetto solo se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.BackStyle%2A> è impostata su <xref:Microsoft.VisualBasic.PowerPacks.BackStyle>.  
  
-   Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.FillStyle%2A> è impostata su <xref:Microsoft.VisualBasic.PowerPacks.FillStyle>, <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.FillColor%2A> esegue l'override di <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.BackColor%2A>.  
  
-   Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.FillStyle%2A> è impostata su un valore di motivo quale <xref:Microsoft.VisualBasic.PowerPacks.FillStyle> o <xref:Microsoft.VisualBasic.PowerPacks.FillStyle>, il motivo viene visualizzato in <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.FillColor%2A>.  Lo sfondo viene visualizzato in <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.BackColor%2A> se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.BackStyle%2A> è impostata su <xref:Microsoft.VisualBasic.PowerPacks.BackStyle>.  
  
-   Per visualizzare un riempimento sfumato, impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.FillStyle%2A> su <xref:Microsoft.VisualBasic.PowerPacks.FillStyle> e la proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.FillGradientStyle%2A> su un valore diverso da <xref:Microsoft.VisualBasic.PowerPacks.FillGradientStyle>.  
  
-   L'impostazione della proprietà <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape.BackgroundImage%2A> su un'immagine comporta l'override di tutte le altre impostazioni dello sfondo.  
  
#### Per disegnare un cerchio con un bordo personalizzato  
  
1.  Trascinare il controllo `OvalShape` dalla scheda **Visual Basic Power Packs** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Nella finestra **Proprietà** per la proprietà `Size` impostare valori `Height` e `Width` uguali.  
  
3.  Impostare la proprietà `BorderColor` sul colore desiderato.  
  
4.  Impostare la proprietà `BorderStyle` su qualsiasi valore diverso da `Solid`.  
  
5.  Impostare la proprietà `BorderWidth` sulle dimensioni in pixel desiderate.  
  
#### Per disegnare un cerchio con un riempimento a tinta unita  
  
1.  Trascinare il controllo `OvalShape` dalla scheda **Visual Basic Power Packs** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Nella finestra **Proprietà** per la proprietà `Size` impostare valori `Height` e `Width` uguali.  
  
3.  Impostare la proprietà `BackColor` sul colore desiderato.  
  
4.  Impostare la proprietà `BackStyle` su `Opaque`.  
  
#### Per disegnare un cerchio con un motivo di riempimento  
  
1.  Trascinare il controllo `OvalShape` dalla scheda **Visual Basic Power Packs** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Nella finestra **Proprietà** per la proprietà `Size` impostare valori `Height` e `Width` uguali.  
  
3.  Impostare la proprietà `BackColor` sul colore di sfondo desiderato.  
  
4.  Impostare la proprietà `BackStyle` su `Opaque`.  
  
5.  Impostare la proprietà `FillColor` sul colore del motivo desiderato.  
  
6.  Impostare la proprietà `FillStyle` su qualsiasi valore diverso da `Transparent` o `Solid`.  
  
#### Per disegnare un cerchio con un riempimento sfumato  
  
1.  Trascinare il controllo `OvalShape` dalla scheda **Visual Basic Power Packs** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Nella finestra **Proprietà** per la proprietà `Size` impostare valori `Height` e `Width` uguali.  
  
3.  Impostare la proprietà `FillColor` sul colore iniziale desiderato.  
  
4.  Impostare la proprietà `FillGradientColor` sul colore finale desiderato.  
  
5.  Impostare la proprietà `FillGradientStyle` su un valore diverso da `None`.  
  
#### Per disegnare un cerchio con un'immagine di riempimento  
  
1.  Trascinare il controllo `OvalShape` dalla scheda **Visual Basic Power Packs** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Nella finestra **Proprietà** per la proprietà `Size` impostare valori `Height` e `Width` uguali.  
  
3.  Selezionare la proprietà `BackgroundImage` e fare clic sul pulsante con i **puntini di sospensione** \(...\).  
  
4.  Nella finestra di dialogo **Seleziona risorsa**, selezionare l'immagine da visualizzare.  Se non viene elencata alcuna risorsa immagine, fare clic su **Importa** per individuare il percorso di un'immagine.  
  
5.  Scegliere **OK** per inserire l'immagine.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.OvalShape>   
 <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape>   
 [Introduction to the Line and Shape Controls](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-line-and-shape-controls-visual-studio.md)   
 [How to: Draw Lines with the LineShape Control](../../../visual-basic/developing-apps/windows-forms/how-to-draw-lines-with-the-lineshape-control-visual-studio.md)