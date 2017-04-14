---
title: "Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form | Microsoft Docs"
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
  - "visualizzazioni elenco, aggiunta voci di elenco"
  - "ListView (controllo) [Windows Form], aggiunta voci di elenco"
  - "ListView (controllo) [Windows Form], compilazione"
ms.assetid: 1b35a80a-edd8-495f-a807-a28c4aae52c6
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form
Il processo di aggiunta di un elemento al controllo <xref:System.Windows.Forms.ListView> Windows Form consiste principalmente nella definizione dell'elemento e nell'assegnazione delle proprietà allo stesso.  È possibile aggiungere o rimuovere le voci di elenco in qualsiasi momento.  
  
### Per aggiungere elementi a livello di codice  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.ListView.ListViewItemCollection.Add%2A> della proprietà <xref:System.Windows.Forms.ListView.Items%2A>.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#11)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#11)]  
  
### Per rimuovere elementi a livello di codice  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.ListView.ListViewItemCollection.RemoveAt%2A> o <xref:System.Windows.Forms.ListView.ListViewItemCollection.Clear%2A> della proprietà <xref:System.Windows.Forms.ListView.Items%2A>.  Il metodo <xref:System.Windows.Forms.ListView.ListViewItemCollection.RemoveAt%2A> rimuove un singolo elemento, mentre il metodo <xref:System.Windows.Forms.ListView.ListViewItemCollection.Clear%2A> rimuove tutti gli elementi dall'elenco.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#12)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#12)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListView>   
 [Controllo ListView](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)   
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)