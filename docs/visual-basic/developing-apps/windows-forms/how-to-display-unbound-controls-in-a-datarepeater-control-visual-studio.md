---
title: "How to: Display Unbound Controls in a DataRepeater Control (Visual Studio) | Microsoft Docs"
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
  - "DataRepeater, adding unbound controls"
  - "DataRepeater"
  - "displaying unbound data"
ms.assetid: f234fa40-5a13-4209-930e-7c5f81e86e66
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Display Unbound Controls in a DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In aggiunta a controlli associati, è possibile aggiungere altri controlli a <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>, ad esempio un'etichetta statica o un'immagine ripetuta su ciascun elemento del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
> [!NOTE]
>  Inoltre, se non si dispone di almeno un controllo associato su <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> non verrà visualizzato nulla in fase di esecuzione.  
  
### Per aggiungere controlli non associati a un controllo DataRepeater  
  
1.  Trascinare un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> dalla scheda **Visual Basic Power Pack 1.1** della **Casella degli strumenti** a un form o un controllo contenitore.  
  
2.  Trascinare i quadratini di ridimensionamento e di posizionamento per impostare le dimensioni e la posizione del controllo.  
  
     Per ridimensionare e posizionare il controllo è anche possibile modificare le proprietà **Size** e **Position** nella finestra Proprietà.  
  
3.  Aggiungere almeno un controllo con associazione a dati al controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Per ulteriori informazioni, vedere la classe [How to: Display Bound Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md).  
  
4.  Trascinare un controllo dalla **Casella degli strumenti** all'area del modello di elemento del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
     Si noti che il controllo dispone di due aree rettangolari.  L'area interna è il *modello di elemento*. I controlli aggiunti al modello verranno ripetuti in fase di esecuzione in ciascun elemento del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  L'area esterna è il *riquadro di visualizzazione*, dove gli elementi verranno visualizzati. I controlli aggiunti a quest'area non verranno visualizzati in fase di esecuzione.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [How to: Display Bound Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [How to: Create a Master\/Detail Form by Using Two DataRepeater Controls](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)   
 [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)