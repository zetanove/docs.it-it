---
title: "Procedura: aggiungere colonne al controllo ListView di Windows Form | Microsoft Docs"
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
  - "colonne [Windows Form], aggiunta a controlli ListView"
  - "visualizzazioni elenco, aggiunta di colonne"
  - "ListView (controllo) [Windows Form], aggiunta di intestazioni di colonne"
ms.assetid: 79174274-12ee-4a5d-80db-6ec02976d010
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: aggiungere colonne al controllo ListView di Windows Form
In visualizzazione Dettagli, il controllo <xref:System.Windows.Forms.ListView> può visualizzare più colonne per ciascuna voce di elenco.  È possibile utilizzare le colonne per visualizzare all'utente più tipi di informazioni su ciascuna voce di elenco.  Relativamente a un elenco di file, ad esempio, è possibile visualizzare il nome, il tipo, le dimensioni e la data dell'ultima modifica.  Per informazioni sulla compilazione delle colonne una volta create, vedere [Procedura: visualizzare elementi secondari nelle colonne con il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md).  
  
### Per aggiungere le colonne a livello di codice  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.ListView.View%2A> del controllo su <xref:System.Windows.Forms.View>.  
  
2.  Utilizzare il metodo <xref:System.Windows.Forms.ListView.ColumnHeaderCollection.Add%2A> della proprietà <xref:System.Windows.Forms.ListView.Columns%2A> della visualizzazione elenco.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#31)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#31)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListView>   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)