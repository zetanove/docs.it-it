---
title: "Procedura: utilizzare una matrice di colori per impostare i valori alfa nelle immagini | Microsoft Docs"
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
  - "bitmap [Windows Form], utilizzo di matrici a colori per semitrasparenti"
  - "immagini [Windows Form], utilizzo di matrici a colori per semitrasparenti"
  - "matrici, alfa (valori)"
  - "trasparenza, matrici di colore"
ms.assetid: a27121e6-f7e9-4c09-84e2-f05aa9d2a1bb
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: utilizzare una matrice di colori per impostare i valori alfa nelle immagini
La classe <xref:System.Drawing.Bitmap>, che eredita dalla classe <xref:System.Drawing.Image>, e la classe <xref:System.Drawing.Imaging.ImageAttributes> forniscono funzionalità per ottenere e impostare i valori dei pixel.  È possibile utilizzare la classe <xref:System.Drawing.Imaging.ImageAttributes> per modificare i valori alfa per un'intera immagine, oppure chiamare il metodo <xref:System.Drawing.Bitmap.SetPixel%2A> della classe <xref:System.Drawing.Bitmap> per modificare i valori dei singoli pixel.  
  
## Esempio  
 La classe <xref:System.Drawing.Imaging.ImageAttributes> ha molte proprietà utilizzabili per modificare le immagini durante il rendering.  Nell'esempio che segue, un oggetto <xref:System.Drawing.Imaging.ImageAttributes> viene utilizzato per impostare tutti i valori alfa sull'80% del valore precedente.  Questa operazione viene eseguita inizializzando una matrice di colori e impostando il valore di adattamento alfa nella matrice su 0,8.  L'indirizzo della matrice di colori viene passato al metodo <xref:System.Drawing.Imaging.ImageAttributes.SetColorMatrix%2A> dell'oggetto <xref:System.Drawing.Imaging.ImageAttributes> e l'oggetto <xref:System.Drawing.Imaging.ImageAttributes> viene passato al metodo <xref:System.Drawing.Graphics.DrawString%2A> dell'oggetto <xref:System.Drawing.Graphics>.  
  
 Durante il rendering i valori alfa nell'immagine bitmap sono ridotti del 80%,  con il conseguente risultato di un'immagine sfumata rispetto allo sfondo.  Come mostrato dall'illustrazione riportata di seguito, l'immagine bitmap è trasparente e attraverso di essa è possibile vedere la linea nera a tinta unita.  
  
 ![Fusione alfa con una matrice](../../../../docs/framework/winforms/advanced/media/image2.png "image2")  
  
 Nel punto in cui si sovrappone alla parte bianca dello sfondo l'immagine viene sfumata con il bianco,  mentre dove si sovrappone alla linea nera viene sfumata con il nero.  
  
 [!code-csharp[System.Drawing.AlphaBlending#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.AlphaBlending#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#21)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e` un parametro di <xref:System.Windows.Forms.PaintEventHandler>.  
  
## Vedere anche  
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Linee e riempimenti con fusione alfa](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)