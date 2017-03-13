---
title: "How to: Change the Appearance of a DataRepeater Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, customizing"
  - "DataRepeater, changing run time appearance"
ms.assetid: 2af6dfce-760b-489e-b863-8da967f315c3
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# How to: Change the Appearance of a DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile modificare l'aspetto dei controlli <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> in fase di progettazione mediante l'impostazione di specifiche proprietà oppure in fase di esecuzione mediante la gestione dell'evento <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>.  
  
 Le proprietà impostate in fase di progettazione quando viene selezionata l'area del modello di elemento del controllo verranno ripetute in fase di esecuzione per ogni <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem>.  Le proprietà correlate all'aspetto del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> stesso saranno visibili in fase di esecuzione soltanto se una parte del contenitore viene lasciata scoperta \(ad esempio, se la proprietà <xref:System.Windows.Forms.Control.Padding%2A> è impostata su un valore elevato\).  
  
 In fase di esecuzione, le proprietà correlate all'aspetto possono essere impostate in base a condizioni.  Ad esempio, in un'applicazione di pianificazione, è possibile modificare il colore di sfondo di un elemento per avvisare gli utenti quando un elemento è scaduto.  Nel gestore eventi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>, se si imposta una proprietà in un'istruzione condizionale, ad esempio `If…Then`, è necessario utilizzare anche una clausola `Else` per specificare l'aspetto quando la condizione non viene soddisfatta.  
  
### Per modificare l'aspetto in fase di progettazione  
  
1.  In Progettazione Windows Form, selezionare l'area del modello di elemento \(l'area superiore\) del controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
2.  Nella finestra Proprietà, selezionare una proprietà e modificarne il valore.  Tra le proprietà comuni che influiscono sull'aspetto sono incluse le proprietà <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.BackgroundImage%2A>, <xref:System.Windows.Forms.Panel.BorderStyle%2A> e <xref:System.Windows.Forms.Control.ForeColor%2A>.  
  
### Per modificare l'aspetto in fase di esecuzione  
  
1.  Nell'elenco a discesa Evento dell'editor di codice, fare clic su **DrawItem**.  
  
2.  Nel gestore eventi <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>, aggiungere codice per impostare le proprietà:  
  
     [!code-cs[VbPowerPacksDataRepeaterAppearance#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksDataRepeaterAppearance#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_1.vb)]  
  
## Esempio  
 Alcune personalizzazioni comuni per il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> includono la visualizzazione delle righe in colori alternati e la modifica del colore di un campo in base a una condizione.  Nell'esempio riportato di seguito viene mostrato come eseguire queste personalizzazioni.  In questo esempio si suppone di disporre di un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> associato alla tabella Products nel database Northwind.  
  
 [!code-vb[VbPowerPacksDataRepeaterAlternateBackColor#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_2.vb)]
 [!code-cs[VbPowerPacksDataRepeaterAlternateBackColor#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_2.cs)]  
  
 Si noti che, per entrambe le personalizzazioni, è necessario fornire codice per impostare le proprietà per entrambi i lati della condizione.  Se non si specifica la condizione `Else`, in fase di esecuzione si potranno avere risultati inattesi.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [How to: Display Bound Data in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [How to: Display Unbound Controls in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [How to: Display Item Headers in a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)