---
title: "Procedura: visualizzare elementi secondari nelle colonne con il controllo ListView Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Dettagli (visualizzazione)"
  - "voci elenco"
  - "ListView (controllo) [Windows Form], aggiunta di ListSubItems"
  - "elementi secondari"
ms.assetid: e465f044-cde7-4fd9-a687-788a73a0f554
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: visualizzare elementi secondari nelle colonne con il controllo ListView Windows Form
Il controllo <xref:System.Windows.Forms.ListView> di Windows Form può visualizzare testo aggiuntivo, o elementi secondari, per ciascun elemento nella visualizzazione Details.  La prima colonna visualizza il testo dell'elemento, ad esempio il numero di un dipendente.  La seconda, la terza e le colonne successive visualizzano il primo, il secondo e i successivi elementi secondari associati.  
  
### Per aggiungere elementi secondari a una voce di elenco  
  
1.  Aggiungere il numero di colonne necessario.  Poiché nella prima colonna viene visualizzata la proprietà <xref:System.Windows.Forms.ListView.Text%2A> dell'elemento, è necessario aggiungere una colonna in più rispetto al numero di elementi secondari.  Per ulteriori informazioni sull'aggiunta di colonne vedere [Procedura: aggiungere colonne al controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md).  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.ListViewItem.ListViewSubItemCollection.Add%2A> della raccolta restituita dalla proprietà <xref:System.Windows.Forms.ListViewItem.SubItems%2A> di un elemento.  Nell'esempio di codice che segue vengono impostati il nome del dipendente e il reparto cui appartiene per una voce di elenco.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#61)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#61)]  
  
## Vedere anche  
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere colonne al controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [Procedura: visualizzare icone per il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)