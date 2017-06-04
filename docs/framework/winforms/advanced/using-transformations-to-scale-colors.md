---
title: "Utilizzo delle trasformazioni per scalare i colori | Microsoft Docs"
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
  - "colori, adattamento"
  - "trasformazioni, per l'adattamento dei colori"
ms.assetid: df23c887-7fd6-4b15-ad94-e30b5bd4b849
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Utilizzo delle trasformazioni per scalare i colori
In una trasformazione per adattamento una o più delle quattro componenti di colore viene moltiplicata per un numero.  Le voci della matrice di colore che rappresentano l'adattamento sono indicate nella tabella che segue.  
  
|Componente da adattare|Voce della matrice|  
|----------------------------|------------------------|  
|Rosso|\[0\]\[0\]|  
|Verde|\[1\]\[1\]|  
|Blu|\[2\]\[2\]|  
|Alfa|\[3\]\[3\]|  
  
## Adattamento di un colore  
 Nell'esempio che segue viene costruito un oggetto <xref:System.Drawing.Image> dal file ColorBars2.bmp.  Viene quindi adattata la componente blu di ciascun pixel dell'immagine in base a un fattore 2.  L'immagine originale viene disegnata accanto all'immagine trasformata.  
  
 [!code-csharp[System.Drawing.RecoloringImages#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.RecoloringImages#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#41)]  
  
 Nell'illustrazione che segue si mostra l'immagine originale a sinistra e l'immagine adattata a destra.  
  
 ![Scalatura dei colori](../../../../docs/framework/winforms/advanced/media/colortrans3.png "colortrans3")  
  
 Nella tabella che segue sono elencati i vettori di colore per le quattro barre prima e dopo l'adattamento della componente blu.  Si noti che la componente blu nella quarta barra di colore è passata da 0,8 a 0,6.  Questo perché in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] si conserva solo la parte decimale del risultato.  Ad esempio, \(2\)\(0,8\) \= 1,6; la parte decimale di 1,6 è 0,6.  In questo modo il risultato è sempre compreso nell'intervallo \[0, 1\].  
  
|Originale|Adattato|  
|---------------|--------------|  
|\(0.4, 0.4, 0.4, 1\)|\(0.4, 0.4, 0.8, 1\)|  
|\(0.4, 0.2, 0.2, 1\)|\(0.4, 0.2, 0.4, 1\)|  
|\(0.2, 0.4, 0.2, 1\)|\(0.2, 0.4, 0.4, 1\)|  
|\(0.4, 0.4, 0.8, 1\)|\(0.4, 0.4, 0.6, 1\)|  
  
## Adattamento di più colori  
 Nell'esempio che segue viene costruito un oggetto <xref:System.Drawing.Image> dal file ColorBars2.bmp.  Vengono quindi adattate le componenti rossa, verde e blu di ciascun pixel dell'immagine.  Le componenti rosse vengono ridotte del 25%, quelle verdi del 35% e quelle blu del 50%.  
  
 [!code-csharp[System.Drawing.RecoloringImages#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#42)]
 [!code-vb[System.Drawing.RecoloringImages#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#42)]  
  
 Nell'illustrazione che segue si mostra l'immagine originale a sinistra e l'immagine adattata a destra.  
  
 ![Scalatura dei colori](../../../../docs/framework/winforms/advanced/media/colortrans4.png "colortrans4")  
  
 Nella tabella che segue sono elencati i vettori di colore per le quattro barre prima e dopo l'adattamento delle componenti rossa, verde e blu.  
  
|Originale|Adattato|  
|---------------|--------------|  
|\(0.6, 0.6, 0.6, 1\)|\(0.45, 0.39, 0.3, 1\)|  
|\(0, 1, 1, 1\)|\(0, 0.65, 0.5, 1\)|  
|\(1, 1, 0, 1\)|\(0.75, 0.65, 0, 1\)|  
|\(1, 0, 1, 1\)|\(0.75, 0, 0.5, 1\)|  
  
## Vedere anche  
 <xref:System.Drawing.Imaging.ColorMatrix>   
 <xref:System.Drawing.Imaging.ImageAttributes>   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Ricolorazione di immagini](../../../../docs/framework/winforms/advanced/recoloring-images.md)