---
title: "Procedura: convertire i colori delle immagini | Microsoft Docs"
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
  - "bitmap [Windows Form], modifica dei colori"
  - "immagini (colori) [Windows Form]"
  - "immagini [Windows Form], modifica dei colori"
ms.assetid: 2106fb9a-4d60-4dcf-9220-9f189a6c4d19
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: convertire i colori delle immagini
Una conversione consente di aggiungere un valore a una o più delle quattro componenti di colore.  Le voci della matrice di colore che rappresentano le traslazioni sono indicate nella tabella che segue.  
  
|Componente da convertire|Voce della matrice|  
|------------------------------|------------------------|  
|Rosso|\[4\]\[0\]|  
|Verde|\[4\]\[1\]|  
|Blu|\[4\]\[2\]|  
|Alfa|\[4\]\[3\]|  
  
## Esempio  
 Nell'esempio che segue viene costruito un oggetto <xref:System.Drawing.Image> dal file ColorBars.bmp.  Nel codice viene quindi aggiunto 0,75 alla componente rossa di ogni pixel dell'immagine.  L'immagine originale viene disegnata accanto all'immagine trasformata.  
  
 Nell'illustrazione che segue si mostra l'immagine originale a sinistra e l'immagine trasformata a destra.  
  
 ![Conversione dei colori](../../../../docs/framework/winforms/advanced/media/colortrans2.png "colortrans2")  
  
 Nella tabella che segue sono elencati i vettori di colore per le quattro barre prima e dopo la conversione della componente rossa.  Si noti che, poiché il valore massimo per una componente di colore è 1, la componente rossa nella seconda riga non cambia.  Il valore minimo per una componente di colore è invece 0.  
  
|Originale|Convertito|  
|---------------|----------------|  
|Nero \(0, 0, 0, 1\)|\(0.75, 0, 0, 1\)|  
|Rosso \(1, 0, 0, 1\)|\(1, 0, 0, 1\)|  
|Verde \(0, 1, 0, 1\)|\(0.75, 1, 0, 1\)|  
|Blu \(0, 0, 1, 1\)|\(0.75, 0, 1, 1\)|  
  
 [!code-csharp[System.Drawing.RecoloringImages#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.RecoloringImages#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Sostituire `ColorBars.bmp`  con il percorso e il nome del file di immagine validi per il sistema.  
  
## Vedere anche  
 <xref:System.Drawing.Imaging.ColorMatrix>   
 <xref:System.Drawing.Imaging.ImageAttributes>   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Ricolorazione di immagini](../../../../docs/framework/winforms/advanced/recoloring-images.md)