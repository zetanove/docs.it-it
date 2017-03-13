---
title: "How to: Draw Lines with the LineShape Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "LineShape control"
  - "lines, drawing"
ms.assetid: 83e71b4e-aa76-4f9b-b547-8704309fd1e5
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Draw Lines with the LineShape Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il controllo <xref:Microsoft.VisualBasic.PowerPacks.LineShape> consente di disegnare righe orizzontali, verticali o diagonali in un form o in un contenitore, sia in fase di progettazione che in fase di esecuzione.  
  
 **Nota** Nel computer in uso è possibile che vengano visualizzati nomi o percorsi diversi per alcuni elementi dell'interfaccia utente di Visual Studio nelle istruzioni seguenti.  Questi elementi sono determinati dall'edizione di Visual Studio in uso e dalle impostazioni utilizzate.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per disegnare una riga in fase di progettazione  
  
1.  Trascinare il controllo <xref:Microsoft.VisualBasic.PowerPacks.LineShape> dalla scheda **Visual Basic Power Pack 1.1** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Trascinare i quadratini di ridimensionamento e di spostamento per impostare le dimensioni e la posizione della riga.  
  
     Per ridimensionare e posizionare la riga è anche possibile modificare le proprietà `X1`, `X2`, `Y1` e `Y2` nella finestra **Proprietà**.  
  
3.  Nella finestra **Proprietà** è possibile, se lo si desidera, impostare proprietà aggiuntive quali `BorderStyle` o `BorderColor` per modificare l'aspetto delle righe.  
  
### Per disegnare una riga in fase di esecuzione  
  
1.  Scegliere **Aggiungi riferimento** dal menu **Progetto**.  
  
2.  Nella finestra di dialogo **Aggiungi riferimento**, selezionare **Microsoft.VisualBasic.PowerPacks.VS**, quindi scegliere **OK**.  
  
3.  Nell'editor di codice, aggiungere un'istruzione `Imports` o `using` all'inizio del modulo:  
  
    ```vb#  
    Imports Microsoft.VisualBasic.PowerPacks  
    ```  
  
    ```c#  
    using Microsoft.VisualBasic.PowerPacks;  
    ```  
  
4.  Nella routine `Event` aggiungere il codice seguente:  
  
     [!code-cs[VbPowerPacksLine#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-draw-lines-with-the-lineshape-control-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksLine#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-draw-lines-with-the-lineshape-control-visual-studio_1.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.LineShape>   
 [Introduction to the Line and Shape Controls](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-line-and-shape-controls-visual-studio.md)   
 [How to: Draw Shapes with the OvalShape and RectangleShape Controls](../../../visual-basic/developing-apps/windows-forms/how-to-draw-shapes-with-the-ovalshape-and-rectangleshape-controls.md)