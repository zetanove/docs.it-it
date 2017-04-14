---
title: "Procedura: disegnare linee opache e semitrasparenti | Microsoft Docs"
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
  - "sfumatura alfa, disegno di linee"
  - "disegno, linee"
  - "linee, disegno con sfumatura alfa"
  - "trasparenza, linee"
ms.assetid: 8f2508af-f495-4223-b5cc-646cbbb520eb
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: disegnare linee opache e semitrasparenti
Quando si disegna una linea, è necessario passare un oggetto <xref:System.Drawing.Pen> al metodo <xref:System.Drawing.Graphics.DrawLine%2A> della classe <xref:System.Drawing.Graphics>.  Uno dei parametri del costruttore <xref:System.Drawing.Pen.%23ctor%2A> è un oggetto <xref:System.Drawing.Color>.  Per disegnare una linea opaca, impostare il componente alfa del colore su 255.  Per disegnare una linea semitrasparente, impostare il componente alfa su un valore qualsiasi compreso tra 1 e 254.  
  
 Quando si disegna una linea semitrasparente su uno sfondo, il colore della linea viene sfumato con i colori dello sfondo.  Il componente alfa specifica come si combinano i colori della linea e dello sfondo. I valori alfa vicini a 0 rendono più intensi i colori di sfondo, mentre i valori alfa più vicini a 255 rendono più intenso il colore della linea.  
  
## Esempio  
 L'esempio seguente disegna un'immagine bitmap e quindi tre linee che usano la stessa bitmap come sfondo.  Per la prima linea si usa un componente alfa con un valore pari a 255, quindi la linea risulta opaca.  Per la seconda e la terza linea si usa un componente alfa con un valore pari a 128, quindi le linee risultano semitrasparenti. L'immagine di sfondo è visibile attraverso le linee.  L'istruzione che imposta la proprietà <xref:System.Drawing.Graphics.CompositingQuality%2A> determina la sfumatura della terza riga ottenuta in combinazione con la correzione gamma.  
  
 L'immagine seguente illustra l'output del codice riportato di seguito.  
  
 ![Opaco e semitrasparente](../../../../docs/framework/winforms/advanced/media/compqualline.png "compqualline")  
  
 [!code-csharp[System.Drawing.AlphaBlending#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.AlphaBlending#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio precedente è progettato per l'uso con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Linee e riempimenti con fusione alfa](../../../../docs/framework/winforms/advanced/alpha-blending-lines-and-fills.md)   
 [Procedura: assegnare uno sfondo trasparente al controllo](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)   
 [Procedura: disegnare con pennelli opachi e semitrasparenti](../../../../docs/framework/winforms/advanced/how-to-draw-with-opaque-and-semitransparent-brushes.md)