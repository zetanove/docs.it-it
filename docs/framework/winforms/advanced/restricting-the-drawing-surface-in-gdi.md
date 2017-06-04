---
title: "Limitazione della superficie di disegno in GDI+ | Microsoft Docs"
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
  - "area di visualizzazione, utilizzo di GDI+"
  - "GDI+, area di visualizzazione"
  - "GDI+, limitazione delle aree di disegno"
ms.assetid: 8b5f71d9-d2f0-4540-9c41-740f90fd4c26
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Limitazione della superficie di disegno in GDI+
La definizione dell'area di visualizzazione implica la delimitazione dell'area di disegno a un determinato rettangolo o a una determinata regione.  Nell'immagine seguente viene mostrata la stringa "Hello" inserita in una regione a forma di cuore.  
  
 ![Superficie di disegno limitata](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art30.png "AboutGdip02\_Art30")  
  
## Area di visualizzazione tramite regioni  
 È possibile costruire delle regioni basandosi su percorsi, che possono contenere contorni di stringhe. Il testo con contorni può essere utilizzato per la definizione dell'area di visualizzazione.  Nell'immagine seguente viene mostrato un insieme di ellissi concentriche, la cui area di visualizzazione corrisponde all'interno di una stringa di testo.  
  
 ![Superficie di disegno limitata](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art31.png "AboutGdip02\_Art31")  
  
 Per tracciare elementi utilizzando l'area di visualizzazione, creare un oggetto <xref:System.Drawing.Graphics>, impostare la relativa proprietà <xref:System.Drawing.Graphics.Clip%2A>, quindi chiamare i metodi di disegno di tale oggetto <xref:System.Drawing.Graphics>:  
  
 [!code-csharp[LinesCurvesAndShapes#91](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#91)]
 [!code-vb[LinesCurvesAndShapes#91](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#91)]  
  
## Vedere anche  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Region?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Utilizzo delle regioni](../../../../docs/framework/winforms/advanced/using-regions.md)