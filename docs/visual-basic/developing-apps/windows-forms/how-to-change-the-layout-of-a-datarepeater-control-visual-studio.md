---
title: "How to: Change the Layout of a DataRepeater Control (Visual Studio) | Microsoft Docs"
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
  - "DataRepeater, changing layout style"
  - "DataRepeater, changing orientation"
ms.assetid: 33aa8fd5-ac63-4bd0-ba13-8c2ab17e7824
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Change the Layout of a DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> può essere visualizzato con un orientamento verticale, in cui gli elementi scorrono verticalmente, o orizzontale, in cui gli elementi scorrono orizzontalmente.  È possibile modificare l'orientamento in fase di progettazione o in fase di esecuzione, modificando la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A>.  Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> viene modificata in fase di esecuzione, ridimensionare <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> e riposizionare i controlli figlio.  
  
> [!NOTE]
>  Se i controlli vengono riposizionati su <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> in fase di esecuzione, chiamare i metodi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A> e <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A> all'inizio e alla fine del blocco di codice di riposizionamento dei controlli.  
  
### Per modificare il layout in fase di progettazione  
  
1.  In Progettazione Windows Form selezionare il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
    > [!NOTE]
    >  Selezionare il bordo esterno del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> facendo clic nell'area inferiore del controllo anziché nell'area <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> superiore.  
  
2.  Nella finestra Proprietà, impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> su <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles> o <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles>.  
  
### Per modificare il layout in fase di esecuzione  
  
1.  Aggiungere al gestore eventi `Click` di un pulsante o menu il codice riportato di seguito:  
  
     [!code-cs[VbPowerPacksDataRepeaterLayout#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksDataRepeaterLayout#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_1.vb)]  
  
2.  Nella maggior parte dei casi, per ridimensionare <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> e adattare la disposizione dei controlli al nuovo orientamento è consigliabile aggiungere codice simile a quello riportato nella sezione Esempio.  
  
## Esempio  
 Nell'esempio riportato di seguito viene mostrato come rispondere all'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyleChanged> in un gestore eventi.  Per questo esempio è necessario disporre di un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> denominato `DataRepeater1` in un form e che il relativo oggetto <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> contenga due controlli <xref:System.Windows.Forms.TextBox> denominati `TextBox1` e `TextBox2`.  
  
 [!code-cs[VbPowerPacksDataRepeaterLayout#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_2.cs)]
 [!code-vb[VbPowerPacksDataRepeaterLayout#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_2.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)