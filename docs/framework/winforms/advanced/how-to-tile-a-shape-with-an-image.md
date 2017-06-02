---
title: "Procedura: riempire una forma con immagini affiancate | Microsoft Docs"
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
  - "bitmap [Windows Form], riempimento di forme"
  - "immagini [Windows Form], riempimento di forme"
  - "forme, affiancamento con immagini"
  - "pennelli della struttura, affiancamento di immagini"
ms.assetid: 6d407891-6e5c-4495-a546-3da5604e9fb8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: riempire una forma con immagini affiancate
Per riempire una forma è possibile collocare una accanto all'altra, ovvero affiancare, immagini di forma rettangolare.  Per riempire l'interno di una forma utilizzare un pennello a trama.  Quando si costruisce un oggetto <xref:System.Drawing.TextureBrush> tra gli argomenti passati al costruttore è presente un oggetto <xref:System.Drawing.Image>.  Quando si utilizza il pennello a trama per l'interno di una forma questa viene riempita con copie ripetute dell'immagine.  
  
 La proprietà Wrap Mode dell'oggetto <xref:System.Drawing.TextureBrush> determina l'orientamento dell'immagine quando viene ripetuta in una griglia rettangolare.  È possibile fare in modo che tutte le immagini affiancate della griglia abbiano lo stesso orientamento, oppure che ogni immagine in una posizione della griglia sia capovolta rispetto alla precedente.  Il capovolgimento può essere in orizzontale, in verticale o in entrambi i sensi.  Negli esempi che seguono si illustra l'affiancamento con tipi diversi di capovolgimento.  
  
### Per affiancare un'immagine  
  
-   Nell'esempio l'immagine 75×75 riportata di seguito viene affiancata all'interno di un rettangolo 200×200.  
  
 ![Affianca 1](../../../../docs/framework/winforms/advanced/media/tile1.png "tile1")  
  
-   Nell'illustrazione che segue si mostra come il rettangolo viene utilizzato per riempire l'immagine.  Si noti che tutte le immagini affiancate hanno lo stesso orientamento. Non è stato applicato nessun capovolgimento.  
  
 ![Affianca 2](../../../../docs/framework/winforms/advanced/media/tile2.png "tile2")  
  
 [!code-csharp[System.Drawing.UsingABrush#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingABrush#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#31)]  
  
### Per capovolgere un'immagine orizzontalmente durante l'affiancamento  
  
-   In questo esempio la stessa immagine 75×75 viene utilizzata per riempire un rettangolo 200×200.  La modalità di wrap è impostata in modo che l'immagine sia capovolta orizzontalmente.  Nell'illustrazione che segue si mostra come il rettangolo viene utilizzato per riempire l'immagine.  Si noti che, spostandosi da un'immagine all'altra in una riga data, l'immagine si capovolge orizzontalmente.  
  
 ![Affianca 3](../../../../docs/framework/winforms/advanced/media/tile3.png "tile3")  
  
 [!code-csharp[System.Drawing.UsingABrush#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.UsingABrush#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#32)]  
  
### Per capovolgere un'immagine verticalmente durante l'affiancamento  
  
-   In questo esempio la stessa immagine 75×75 viene utilizzata per riempire un rettangolo 200×200.  La modalità di wrap è impostata in modo che l'immagine sia capovolta verticalmente.  
  
     [!code-csharp[System.Drawing.UsingABrush#33](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#33)]
     [!code-vb[System.Drawing.UsingABrush#33](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#33)]  
  
### Per capovolgere un'immagine orizzontalmente e verticalmente durante l'affiancamento  
  
-   In questo esempio la stessa immagine 75×75 viene affiancata all'interno di un rettangolo 200×200.  La modalità di wrap è impostata in modo che l'immagine sia capovolta sia orizzontalmente sia verticalmente.  Nell'illustrazione che segue si mostra come il rettangolo viene utilizzato per riempire l'immagine.  Si noti che, spostandosi da un'immagine alla successiva in una riga data, l'immagine si capovolge orizzontalmente, mentre spostandosi da un'immagine alla successiva in una colonna data, l'immagine si capovolge verticalmente.  
  
 ![Affianca 5](../../../../docs/framework/winforms/advanced/media/tile5.png "tile5")  
  
 [!code-csharp[System.Drawing.UsingABrush#34](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#34)]
 [!code-vb[System.Drawing.UsingABrush#34](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#34)]  
  
## Vedere anche  
 [Utilizzo di un oggetto Brush per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)