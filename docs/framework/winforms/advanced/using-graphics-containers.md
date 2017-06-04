---
title: "Utilizzo dei contenitori di grafica | Microsoft Docs"
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
  - "esempi [Windows Form], oggetti Graphics (contenitori)"
  - "oggetti Graphics (contenitori)"
  - "grafica, utilizzo dei contenitori"
ms.assetid: 74632f91-cefa-4f51-ab7c-f9ac91942caf
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Utilizzo dei contenitori di grafica
Un oggetto <xref:System.Drawing.Graphics> fornisce metodi come <xref:System.Drawing.Graphics.DrawLine%2A>, <xref:System.Drawing.Graphics.DrawImage%2A> e <xref:System.Drawing.Graphics.DrawString%2A> per la visualizzazione di immagini vettoriali, immagini raster e testo.  Un oggetto <xref:System.Drawing.Graphics> possiede anche numerose proprietà che hanno effetto sulla qualità e l'orientamento degli elementi disegnati.  La proprietà relativa alla modalità di smussatura, ad esempio, consente di determinare l'applicazione o meno dell'antialias a linee e curve; la proprietà relativa alla trasformazione di tipo world consente di influenzare la posizione e la rotazione degli elementi disegnati.  
  
 Un oggetto <xref:System.Drawing.Graphics> è associato a una periferica di visualizzazione specifica.  Quando si utilizza un oggetto <xref:System.Drawing.Graphics> per disegnare all'interno di una finestra l'oggetto <xref:System.Drawing.Graphics> viene anche associato a quella particolare finestra.  
  
 Un oggetto <xref:System.Drawing.Graphics> può essere considerato come un contenitore, perché include un gruppo di proprietà che influenza il disegno ed è collegato a informazioni specifiche della periferica.  È possibile creare un contenitore secondario all'interno un oggetto <xref:System.Drawing.Graphics> esistente chiamando il metodo <xref:System.Drawing.Graphics.BeginContainer%2A> di tale oggetto <xref:System.Drawing.Graphics>.  
  
## In questa sezione  
 [Gestione dello stato di un oggetto Graphics](../../../../docs/framework/winforms/advanced/managing-the-state-of-a-graphics-object.md)  
 Descrive come gestire le impostazioni relative alla qualità, l'area di ridimensionamento e le trasformazioni di un oggetto <xref:System.Drawing.Graphics>.  
  
 [Utilizzo di contenitori di grafica annidati](../../../../docs/framework/winforms/advanced/using-nested-graphics-containers.md)  
 Mostra come utilizzare i contenitori per controllare lo stato dell'oggetto <xref:System.Drawing.Graphics>.