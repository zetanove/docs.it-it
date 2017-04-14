---
title: "Procedura: selezionare un elemento nel controllo ListView Windows Form | Microsoft Docs"
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
  - "visualizzazioni elenco, selezione di elementi"
  - "elenchi, selezione di elementi"
  - "ListView (controllo) [Windows Form], selezione di elementi"
  - "selezione, in visualizzazioni elenco"
ms.assetid: ddea918e-1ddf-47f4-bd09-1e9b4c9d0c39
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: selezionare un elemento nel controllo ListView Windows Form
Nell'esempio qui di seguito viene illustrato come selezionare un elemento in un controllo <xref:System.Windows.Forms.ListView> di un Windows Form a livello di codice.  Selezionando un elemento a livello di codice non si passa automaticamente lo stato attivo al controllo <xref:System.Windows.Forms.ListView>.  Per questo motivo, quando si seleziona un elemento è in genere preferibile impostare lo stato attivo su tale elemento.  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.ListView.Misc#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ListView.Misc#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListView.Misc/VB/form1.vb#1)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.ListView> denominato `listView1` contenente almeno un elemento.  
  
-   Riferimenti agli spazi dei nomi <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ListView>   
 <xref:System.Windows.Forms.ListViewItem.Selected%2A?displayProperty=fullName>