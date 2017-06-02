---
title: "Utilizzo di contenitori di grafica annidati | Microsoft Docs"
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
  - "grafica [Windows Form], area di visualizzazione"
  - "grafica, contenitori annidati"
  - "grafica, trasformazioni in oggetti annidati"
ms.assetid: a0d9f178-43a4-4323-bb5a-d3e3f77ae6c1
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Utilizzo di contenitori di grafica annidati
In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili contenitori utilizzabili per sostituire temporaneamente o per migliorare parte dello stato in un oggetto <xref:System.Drawing.Graphics>.  Per creare un contenitore, chiamare il metodo <xref:System.Drawing.Graphics.BeginContainer%2A> di un oggetto <xref:System.Drawing.Graphics>.  È possibile chiamare <xref:System.Drawing.Graphics.BeginContainer%2A> più volte per creare contenitori annidati.  Ciascuna chiamata a <xref:System.Drawing.Graphics.BeginContainer%2A> deve essere accoppiata a una chiamata a <xref:System.Drawing.Graphics.EndContainer%2A>.  
  
## Trasformazioni in contenitori annidati  
 Nell'esempio che segue viene creato un oggetto <xref:System.Drawing.Graphics> e un contenitore all'interno di esso.  La trasformazione complessiva dell'oggetto <xref:System.Drawing.Graphics> consiste in una traslazione di 100 unità sull'asse x e di 80 sull'asse y.  La trasformazione world del contenitore consiste in una rotazione di 30 gradi.  L'oggetto  `DrawRectangle(pen, -60, -30, 120, 60)`  viene chiamato due volte.  La prima chiamata a <xref:System.Drawing.Graphics.DrawRectangle%2A> viene effettuata all'interno del contenitore. Ciò significa che è compresa tra le due chiamate a <xref:System.Drawing.Graphics.BeginContainer%2A> e <xref:System.Drawing.Graphics.EndContainer%2A>.  La seconda chiamata a <xref:System.Drawing.Graphics.DrawRectangle%2A> avviene dopo la chiamata a <xref:System.Drawing.Graphics.EndContainer%2A>.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.MiscLegacyTopics#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#61)]  
  
 Nel codice precedente, al rettangolo disegnato dall'interno del contenitore viene applicata prima una rotazione tramite la trasformazione world del contenitore, poi una traslazione tramite la trasformazione world dell'oggetto <xref:System.Drawing.Graphics>.  Al rettangolo disegnato dall'esterno del contenitore viene applicata una traslazione tramite la trasformazione world dell'oggetto <xref:System.Drawing.Graphics>.  Nell'illustrazione che segue vengono mostrati i due rettangoli.  
  
 ![Contenitori annidati](../../../../docs/framework/winforms/advanced/media/csnestedcontainers1.png "csnestedcontainers1")  
  
## Ridimensionamento di contenitori annidati  
 Nell'esempio che segue si illustra la gestione delle aree di ridimensionamento da parte dei contenitori annidati.  Viene creato un oggetto <xref:System.Drawing.Graphics> e un contenitore all'interno di esso.  L'area di ridimensionamento dell'oggetto <xref:System.Drawing.Graphics> è un rettangolo, mentre quella del contenitore è un'ellisse.  Vengono effettuate due chiamate al metodo <xref:System.Drawing.Graphics.DrawLine%2A>.  La prima chiamata a <xref:System.Drawing.Graphics.DrawLine%2A> viene effettuata all'interno del contenitore mentre la seconda chiamata a <xref:System.Drawing.Graphics.DrawLine%2A> si trova all'esterno del contenitore, dopo la chiamata a <xref:System.Drawing.Graphics.EndContainer%2A>\).  La prima linea viene tagliata dall'intersezione delle due aree di ridimensionamento.  La seconda linea viene tagliata solo dall'area di ridimensionamento rettangolare dell'oggetto <xref:System.Drawing.Graphics>.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#62](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#62)]
 [!code-vb[System.Drawing.MiscLegacyTopics#62](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#62)]  
  
 Nell'illustrazione che segue vengono mostrate le due linee tagliate.  
  
 ![Contenitore annidato](../../../../docs/framework/winforms/advanced/media/nestedcontainers2.png "nestedcontainers2")  
  
 Come nei due esempi precedenti, trasformazioni e aree di ridimensionamento sono cumulative nei contenitori annidati.  Se si impostano le trasformazioni world del contenitore e dell'oggetto <xref:System.Drawing.Graphics> agli elementi disegnati dall'interno del contenitore verranno applicate entrambe le trasformazioni.  La trasformazione del contenitore sarà applicata per prima, quella dell'oggetto <xref:System.Drawing.Graphics> per seconda.  Se si impostano le aree di ridimensionamento del contenitore e dell'oggetto <xref:System.Drawing.Graphics>, gli elementi disegnati dall'interno del contenitore saranno tagliati dall'intersezione delle due aree di ridimensionamento.  
  
## Impostazioni di qualità in contenitori annidati  
 Le impostazioni di qualità, quali <xref:System.Drawing.Graphics.SmoothingMode%2A>, <xref:System.Drawing.Graphics.TextRenderingHint%2A>, nei contenitori annidati non sono cumulative ma consentono di sostituire temporaneamente le impostazioni di qualità di un oggetto <xref:System.Drawing.Graphics>.  Quando si crea un nuovo contenitore le relative impostazioni di qualità sono impostate sui valori predefiniti.  Si supponga ad esempio di avere un oggetto <xref:System.Drawing.Graphics> con modalità di smussatura <xref:System.Drawing.Drawing2D.SmoothingMode>.  Quando si crea un contenitore la modalità di smussatura all'interno del contenitore è quella predefinita.  È possibile impostare liberamente la modalità di smussatura del contenitore; qualunque elemento disegnato dall'interno di questo sarà creato in conformità alla modalità impostata.  Gli elementi disegnati dopo la chiamata a <xref:System.Drawing.Graphics.EndContainer%2A> saranno creati in base alla modalità di smussatura <xref:System.Drawing.Drawing2D.SmoothingMode> impostata prima della chiamata a <xref:System.Drawing.Graphics.BeginContainer%2A>.  
  
## Livelli multipli dei contenitori annidati  
 In un oggetto <xref:System.Drawing.Graphics> sono disponibili più contenitori.  È possibile creare una sequenza di contenitori, ciascuno annidato nel precedente, specificando la trasformazione world, l'area di ridimensionamento e le impostazioni di qualità di ciascuno di essi.  Se si chiama un metodo di creazione dall'interno del contenitore più interno le trasformazioni saranno applicate in ordine, a partire dal contenitore più interno fino a quello più esterno.  Gli elementi disegnati dall'interno del contenitore più interno saranno tagliati dall'intersezione di tutte le aree di ridimensionamento.  
  
 Nell'esempio che segue si crea un oggetto <xref:System.Drawing.Graphics> e se ne imposta l'hint di rendering del testo su <xref:System.Drawing.Drawing2D.SmoothingMode>.  Vengono creati due contenitori, uno annidato dentro l'altro.  L'hint di rendering di testo del contenitore esterno è impostato su <xref:System.Drawing.Text.TextRenderingHint>, mentre quello del contenitore interno è impostato su <xref:System.Drawing.Drawing2D.SmoothingMode>.  Vengono create tre stringhe: una dal contenitore interno, una da quello esterno e una direttamente dell'oggetto <xref:System.Drawing.Graphics>.  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#63](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#63)]
 [!code-vb[System.Drawing.MiscLegacyTopics#63](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#63)]  
  
 Nell'illustrazione che segue sono mostrate le tre stringhe.  Alla stringa creata dal contenitore interno e dall'oggetto <xref:System.Drawing.Graphics> è applicata la smussatura tramite anti\-aliasing.  La stringa creata dal contenitore esterno non è smussata tramite anti\-aliasing perché la proprietà <xref:System.Drawing.Graphics.TextRenderingHint%2A> è impostata su <xref:System.Drawing.Text.TextRenderingHint>.  
  
 ![Contenitori annidati](../../../../docs/framework/winforms/advanced/media/nestedcontainers3.png "nestedcontainers3")  
  
## Vedere anche  
 <xref:System.Drawing.Graphics>   
 [Gestione dello stato di un oggetto Graphics](../../../../docs/framework/winforms/advanced/managing-the-state-of-a-graphics-object.md)