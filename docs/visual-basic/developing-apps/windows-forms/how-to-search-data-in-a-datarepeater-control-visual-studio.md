---
title: "How to: Search Data in a DataRepeater Control (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, implementing search"
  - "DataRepeater, searching data"
ms.assetid: a8ab5d17-b94f-43c4-8dd7-d0450226d73f
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# How to: Search Data in a DataRepeater Control (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando si utilizza un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> contenente molti record, è necessario fornire agli utenti la possibilità di cercare un record specifico.  Anziché cercare i dati nel controllo stesso, è possibile implementare una ricerca tramite query sull'oggetto <xref:System.Windows.Forms.BindingSource> sottostante.  Una volta trovato l'elemento sarà possibile utilizzare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.CurrentItemIndex%2A> per selezionare l'elemento e scorrerlo nella visualizzazione.  
  
### Per implementare una ricerca  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TextBox> dalla **Casella degli strumenti** al form contenente il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
2.  Nella finestra Proprietà modificare la proprietà **Name** in SearchTextBox.  
  
3.  Trascinare un controllo <xref:System.Windows.Forms.Button> dalla **Casella degli strumenti** al form contenente il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
4.  Nella finestra Proprietà modificare la proprietà **Name** in SearchButton.  Modificare la proprietà **Text** in Search.  
  
5.  Fare doppio clic sul controllo <xref:System.Windows.Forms.Button> per aprire l'editor di codice, quindi aggiungere il codice seguente al gestore eventi `SearchButton_Click`:  
  
     [!code-vb[VbPowerPacksDataRepeaterSearch#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/VbPowerPacksDataRepeaterSearch/DataRepeaterSearch.vb#1)]
     [!code-cs[VbPowerPacksDataRepeaterSearch#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DataRepeaterSearchCS/DataRepeaterSearch.cs#1)]  
  
     Sostituire *ProductsBindingSource* con il nome dell'oggetto <xref:System.Windows.Forms.BindingSource> per <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> e sostituire *ProductID* con il nome del campo che si desidera cercare.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [How to: Change the Appearance of a DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)