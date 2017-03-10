---
title: "How to: Enable Tabbing Between Shapes (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Line control, implementing tabbing"
  - "Shape control, implementing tabbing"
ms.assetid: 09731b34-3900-4fcb-a9df-ce5280328433
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Enable Tabbing Between Shapes (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I controlli Line e Shape non dispongono di proprietà `TabStop` o `TabIndex`, ma è comunque possibile attivare la tabulazione tra di esse.  Nell'esempio riportato di seguito, premendo i tasti CTRL e TAB è possibile passare da una forma all'altra. Premendo solo il tasto TAB è possibile passare da un pulsante all'altro.  
  
> [!NOTE]
>  Il computer potrebbe mostrare nomi o percorsi diversi per alcuni elementi dell'interfaccia utente di Visual Studio nelle istruzioni seguenti.  Questi elementi sono determinati dall'edizione di Visual Studio in uso e dalle impostazioni utilizzate.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per attivare la tabulazione tra le forme  
  
1.  Trascinare tre controlli <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> e due controlli <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** al form.  
  
2.  Nell'editor di codice, aggiungere un'istruzione `Imports` o `using` all'inizio del modulo:  
  
    ```vb#  
    Imports Microsoft.VisualBasic.PowerPacks  
    ```  
  
    ```c#  
    using Microsoft.VisualBasic.PowerPacks;  
    ```  
  
3.  Nella routine evento, aggiungere il codice seguente:  
  
     [!code-cs[VbPowerPacksTabbing#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksTabbingCS/VbPowerPacksTabbing.cs#1)]
     [!code-vb[VbPowerPacksTabbing#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksTabbing/VbPowerPacksTabbing.vb#1)]  
  
4.  Nella routine evento `Button1_PreviewKeyDown`, aggiungere il codice seguente:  
  
     [!code-cs[VbPowerPacksTabbing#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/VbPowerPacksTabbingCS/VbPowerPacksTabbing.cs#2)]
     [!code-vb[VbPowerPacksTabbing#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksTabbing/VbPowerPacksTabbing.vb#2)]  
  
## Vedere anche  
 [How to: Draw Shapes with the OvalShape and RectangleShape Controls](../../../visual-basic/developing-apps/windows-forms/how-to-draw-shapes-with-the-ovalshape-and-rectangleshape-controls.md)   
 [How to: Draw Lines with the LineShape Control](../../../visual-basic/developing-apps/windows-forms/how-to-draw-lines-with-the-lineshape-control-visual-studio.md)   
 [Introduction to the Line and Shape Controls](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-line-and-shape-controls-visual-studio.md)