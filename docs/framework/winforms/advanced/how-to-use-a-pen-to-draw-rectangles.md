---
title: "Procedura: utilizzare un oggetto Pen per disegnare rettangoli | Microsoft Docs"
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
  - "penne, disegno di rettangoli"
  - "rettangoli, disegno"
ms.assetid: 54a7fa14-3ad8-4d64-b424-2a12005b250c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: utilizzare un oggetto Pen per disegnare rettangoli
Per tracciare un rettangolo, sono necessari un oggetto <xref:System.Drawing.Graphics> e un oggetto <xref:System.Drawing.Pen>.  L'oggetto <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawRectangle%2A>, mentre nell'oggetto <xref:System.Drawing.Pen> sono memorizzati gli attributi, quale il colore e lo spessore della linea.  
  
## Esempio  
 Nell'esempio che segue si traccia un rettangolo con l'angolo superiore sinistro in posizione \(10, 10\).  Il rettangolo ha larghezza 100 e altezza 50  Il secondo argomento passato al costruttore <xref:System.Drawing.Pen.%23ctor%2A> indica che lo spessore della penna è 5 pixel.  
  
 Quando viene disegnato il rettangolo la penna è centrata rispetto al limite del rettangolo.  Poiché la larghezza della penna è pari a 5, i lati del rettangolo vengono tracciati con larghezza pari a 5 pixel, in modo che 1 pixel viene disegnato sul limite, 2 pixel all'interno e 2 pixel all'esterno.  Per ulteriori informazioni sull'allineamento della penna, vedere [Procedura: impostare la larghezza e l'allineamento di un oggetto Pen](../../../../docs/framework/winforms/advanced/how-to-set-pen-width-and-alignment.md).  
  
 Nell'illustrazione che segue si mostra il rettangolo risultante.  Le linee tratteggiate indicano la posizione in cui il rettangolo sarebbe stato tracciato se la larghezza della penna fosse stata uguale a 1 pixel.  La visualizzazione estesa dell'angolo superiore sinistro del rettangolo mostra che le linee spesse di colore nero sono centrate rispetto alle linee tratteggiate.  
  
 ![Oggetti Pen](../../../../docs/framework/winforms/advanced/media/pens1.png "pens1")  
  
 [!code-csharp[System.Drawing.UsingAPen#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingAPen#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#21)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)