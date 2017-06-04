---
title: "Procedura: definire l&#39;area di visualizzazione utilizzando una regione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "aree, area di visualizzazione"
  - "aree, limitazione delle aree di disegno"
ms.assetid: 43d121b4-e14c-4901-b25c-2d6c25ba4e29
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: definire l&#39;area di visualizzazione utilizzando una regione
Una delle proprietà della classe <xref:System.Drawing.Graphics> è l'area di ridimensionamento.  Tutti i disegni effettuati da un dato oggetto <xref:System.Drawing.Graphics> sono limitati dall'area di ridimensionamento di quell'oggetto.  È possibile impostare tale area chiamando il metodo <xref:System.Drawing.Graphics.SetClip%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene costruito un percorso composto da un singolo poligono.  Viene quindi costruita un'area basata su tale percorso.  L'area viene passata al metodo <xref:System.Drawing.Graphics.SetClip%2A> di un oggetto <xref:System.Drawing.Graphics> e quindi vengono create due stringhe.  
  
 Nell'illustrazione che segue sono mostrate le stringhe tagliate.  
  
 ![Ritaglio](../../../../docs/framework/winforms/advanced/media/clip1.png "clip1")  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.MiscLegacyTopics#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#41)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Regioni in GDI\+](../../../../docs/framework/winforms/advanced/regions-in-gdi.md)   
 [Utilizzo delle regioni](../../../../docs/framework/winforms/advanced/using-regions.md)