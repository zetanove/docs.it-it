---
title: "Procedura: migliorare le prestazioni evitando l&#39;adattamento automatico | Microsoft Docs"
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
  - "ridimensionamento automatico"
  - "immagini [Windows Form], miglioramento delle prestazioni"
  - "immagini [Windows Form], utilizzo senza ridimensionamento automatico"
  - "prestazioni, miglioramento dell'immagine"
ms.assetid: 5fe2c95d-8653-4d55-bf0d-e5afa28f223b
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: migliorare le prestazioni evitando l&#39;adattamento automatico
In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è possibile che un'immagine venga automaticamente adattata mentre viene disegnata, con un conseguente calo delle prestazioni.  In alternativa, è possibile controllare l'adattamento dell'immagine passando le dimensioni del rettangolo di destinazione al metodo <xref:System.Drawing.Graphics.DrawImage%2A>.  
  
 Nella chiamata al metodo <xref:System.Drawing.Graphics.DrawImage%2A> riportata di seguito viene ad esempio specificato che l'angolo superiore sinistro deve trovarsi nel punto \(50, 30\), ma non viene specificato un rettangolo di destinazione.  
  
 [!code-csharp[System.Drawing.WorkingWithImages#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.WorkingWithImages#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#31)]  
  
 Sebbene si tratti della versione più semplice del metodo <xref:System.Drawing.Graphics.DrawImage%2A>, in termini di numero di argomenti obbligatori, non è necessariamente la più efficiente.  Se la risoluzione utilizzata in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] \(in genere 96 punti per pollice\) è diversa da quella memorizzata nell'oggetto <xref:System.Drawing.Image>, l'immagine verrà automaticamente adattata dal metodo <xref:System.Drawing.Graphics.DrawImage%2A>.  Si supponga, ad esempio, che un oggetto <xref:System.Drawing.Image> abbia una larghezza di 216 pixel e un valore di risoluzione orizzontale memorizzato di 72 punti per pollice.  Poiché 216\/72 è uguale a 3, l'immagine verrà automaticamente adattata da <xref:System.Drawing.Graphics.DrawImage%2A>, in modo da ottenere una larghezza di 3 pollici con una risoluzione di 96 punti per pollice,  ovvero l'immagine visualizzata da <xref:System.Drawing.Graphics.DrawImage%2A> avrà una larghezza di 96x3 \= 288 pixel.  
  
 Anche se la risoluzione dello schermo è diversa da 96 punti per pollice, in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] l'immagine verrà probabilmente adattata come se la risoluzione dello schermo fosse di 96 punti per pollice.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] <xref:System.Drawing.Graphics> è infatti associato a un contesto di dispositivo e, quando in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] viene eseguita una query nel contesto di dispositivo per determinare la risoluzione dello schermo, il risultato è in genere 96, indipendentemente dalla risoluzione effettiva dello schermo.  L'adattamento automatico può essere evitato specificando il rettangolo di destinazione nel metodo <xref:System.Drawing.Graphics.DrawImage%2A>.  
  
## Esempio  
 Nell'esempio che segue viene disegnata due volte la stessa immagine.  Nel primo caso la larghezza e l'altezza del rettangolo di destinazione non sono specificate e l'immagine viene adattata automaticamente.  Nel secondo caso la larghezza e l'altezza, misurate in pixel, del rettangolo di destinazione sono specificate in modo da essere uguali a quelle dell'immagine originale.  Nell'illustrazione che segue si mostra l'immagine visualizzata due volte.  
  
 ![Trama ridimensionata](../../../../docs/framework/winforms/advanced/media/csscaledtexture1.png "csscaledtexture1")  
  
 [!code-csharp[System.Drawing.WorkingWithImages#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.WorkingWithImages#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#32)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Sostituire Texture.jpg con il percorso e il nome di un file di immagine validi per il sistema.  
  
## Vedere anche  
 [Immagini, bitmap e metafile](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [Utilizzo di immagini, bitmap, icone e metafile](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)