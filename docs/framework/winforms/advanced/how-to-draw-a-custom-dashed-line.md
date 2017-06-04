---
title: "Procedura: disegnare una linea tratteggiata personalizzata | Microsoft Docs"
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
  - "linee, personalizzati"
  - "linee, tratteggiate"
  - "linee, disegno"
ms.assetid: cd0ed96a-cce4-47b9-b58a-3bae2e3d1bee
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: disegnare una linea tratteggiata personalizzata
In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili diversi stili di tratteggio, elencati nell'enumerazione <xref:System.Drawing.Drawing2D.DashStyle>.  Se tali stili di tratteggio standard non si adattano alle esigenze dell'utente, è possibile creare un motivo di tratteggio personalizzato.  
  
## Esempio  
 Per tracciare una linea tratteggiata personalizzata, inserire la lunghezza dei trattini e degli spazi in una matrice e assegnarla come valore della proprietà <xref:System.Drawing.Pen.DashPattern%2A> di un oggetto <xref:System.Drawing.Pen>.  Nell'esempio seguente viene tracciata una linea tratteggiata personalizzata basata sulla matrice  `{5, 2, 15, 4}`.  Moltiplicando gli elementi della matrice per la larghezza della penna, pari a 5, si ottiene `{25, 10, 75, 20}`.  I trattini visualizzati hanno, alternativamente, lunghezza pari a 25 e a 75, mentre gli spazi hanno, alternativamente, lunghezza pari a 10 e a 20.  
  
 Nell'illustrazione che segue è visibile la linea tratteggiata risultante.  Si noti che il trattino finale deve essere più corto di 25 unità perché la linea possa terminare a \(405, 5\).  
  
 ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens6.png "pens6")  
  
 [!code-csharp[System.Drawing.UsingAPen#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.UsingAPen#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#51)]  
  
## Compilazione del codice  
 Creare un Windows Form e gestire l'evento <xref:System.Windows.Forms.Control.Paint> del form.  Incollare il codice precedente nel gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)