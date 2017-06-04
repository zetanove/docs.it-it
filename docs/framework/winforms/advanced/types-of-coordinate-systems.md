---
title: "Tipi di sistemi di coordinate | Microsoft Docs"
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
  - "sistemi coordinati"
  - "sistema di coordinate del dispositivo"
  - "sistema di coordinate della pagina"
  - "trasformazione della pagina"
  - "trasformazioni, pagina"
  - "trasformazioni, complessive"
  - "unità di misura"
  - "sistema di coordinate complessive"
  - "trasformazione complessiva"
ms.assetid: c61ff50a-eb1d-4e6c-83cd-f7e9764cfa9f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Tipi di sistemi di coordinate
In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] vengono utilizzati tre spazi di coordinate: complessivo, pagina e dispositivo.  Le coordinate complessive vengono utilizzate per la modellazione di un particolare grafico e in .NET Framework vengono passate ai metodi.  Le coordinate di pagina fanno riferimento al sistema di coordinate utilizzato su una superficie di disegno, ad esempio form o controllo.  Le coordinate di periferica vengono utilizzate dalla periferica fisica su cui si disegna, ad esempio uno schermo o un foglio di carta.  Quando si effettua una chiamata `myGraphics.DrawLine(myPen, 0, 0, 160, 80)`, al metodo <xref:System.Drawing.Graphics.DrawLine%2A> vengono passati i punti `(0, 0)` e `(160, 80)` inclusi nello spazio di coordinate complessivo.  Prima che in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sia possibile tracciare le linee sullo schermo, le coordinate subiscono una sequenza di trasformazioni.  Una trasformazione, chiamata trasformazione complessiva, converte le coordinate complessive in coordinate di pagina, mentre un'altra trasformazione, chiamata trasformazione di pagina, converte le coordinate di pagina in coordinate di periferica.  
  
## Trasformazioni e sistemi di coordinate  
 Si supponga che sia necessario effettuare operazioni con un sistema di coordinate la cui origine si trova nel corpo dell'area client anziché nell'angolo superiore sinistro.  Si supponga ad esempio che l'origine desiderata si trovi a 100 pixel di distanza dal margine dell'area client e a 50 pixel di distanza dall'estremità superiore dell'area client.  Nell'immagine seguente viene mostrato tale sistema di coordinate.  
  
 ![Sistema di coordinate](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art01.png "AboutGdip05\_art01")  
  
 Quando si effettua una chiamata `myGraphics.DrawLine(myPen, 0, 0, 160, 80)`, si ottengono le linee visualizzate nell'immagine seguente.  
  
 ![Sistema di coordinate](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art02.png "AboutGdip05\_art02")  
  
 Le coordinate dei punti finali della linea nei tre spazi di coordinate sono le seguenti  
  
|||  
|-|-|  
|World|Da \(0, 0\) a \(160, 80\)|  
|Page|Da \(100, 50\) a \(260, 130\)|  
|Dispositivo|Da \(100, 50\) a \(260, 130\)|  
  
 Si noti che l'origine dello spazio di coordinate della pagina si trova nell'angolo superiore sinistro dell'area client. Tale valore sarà sempre costante.  Si noti inoltre che le coordinate della periferica corrispondono alle coordinate della pagina, poiché l'unità di misura utilizzata è il pixel.  Se si utilizza un'unità di misura diversa dai pixel \(ad esempio i pollici\), le coordinate della periferica non corrisponderanno alle coordinate della pagina.  
  
 La trasformazione complessiva, che consente di associare le coordinate complessive alle coordinate della pagina, è contenuta nella proprietà <xref:System.Drawing.Graphics.Transform%2A> della classe <xref:System.Drawing.Graphics>.  La trasformazione complessiva riportata nell'esempio precedente consiste in una traslazione di 100 unità nella direzione x e 50 unità nella direzione y.  L'esempio seguente consente di impostare la trasformazione complessiva di un oggetto <xref:System.Drawing.Graphics> e di utilizzare tale oggetto per tracciare la linea mostrata nell'immagine precedente:  
  
 [!code-csharp[System.Drawing.CoordinateSystems#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.CoordinateSystems#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#31)]  
  
 La trasformazione di pagina consente di associare le coordinate della pagina alle coordinate della periferica.  Nella classe <xref:System.Drawing.Graphics> sono disponibili le proprietà <xref:System.Drawing.Graphics.PageUnit%2A> e <xref:System.Drawing.Graphics.PageScale%2A> per la modifica della trasformazione di pagina.  Nella classe <xref:System.Drawing.Graphics> sono inoltre disponibili due proprietà di sola lettura, <xref:System.Drawing.Graphics.DpiX%2A> e <xref:System.Drawing.Graphics.DpiY%2A>, che consentono di esaminare i punti in orizzontale e verticale per pollice della periferica di visualizzazione.  
  
 È possibile utilizzare la proprietà <xref:System.Drawing.Graphics.PageUnit%2A> della classe <xref:System.Drawing.Graphics> per specificare un'unità di misura diversa dal pixel.  
  
> [!NOTE]
>  Non è possibile impostare la proprietà <xref:System.Drawing.Graphics.PageUnit%2A> su <xref:System.Drawing.GraphicsUnit>, in quanto non si tratta di un'unità fisica e verrà generata un'eccezione.  
  
 L'esempio seguente consente di tracciare una linea che unisce il punto \(0, 0\) e il punto \(2, 1\), dove il punto \(2, 1\) si trova 2 pollici a destra e 1 un pollice sotto rispetto al punto \(0, 0\):  
  
 [!code-csharp[System.Drawing.CoordinateSystems#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.CoordinateSystems#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#32)]  
  
> [!NOTE]
>  Se quando si costruisce la penna non si specifica alcuno spessore, la linea tracciata nell'esempio seguente avrà spessore pari a un pollice.  È possibile specificare lo spessore della penna nel secondo argomento del costruttore <xref:System.Drawing.Pen>.  
  
 [!code-csharp[System.Drawing.CoordinateSystems#33](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#33)]
 [!code-vb[System.Drawing.CoordinateSystems#33](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#33)]  
  
 Se si suppone che nella periferica di visualizzazione siano disponibili 96 punti per pollice in direzione orizzontale e 96 punti per pollice in direzione verticale, i valori relativi ai punti finali della linea dell'esempio nei tre spazi di coordinate saranno i seguenti:  
  
|||  
|-|-|  
|World|Da \(0, 0\) a \(2, 1\)|  
|Page|Da \(0, 0\) a \(2, 1\)|  
|Dispositivo|Da \(0, 0\) a \(192, 96\)|  
  
 Si noti che le coordinate di pagina corrispondono alle coordinate complessive, poiché l'origine dello spazio di coordinate complessivo si trova nell'angolo superiore sinistro dell'area client.  
  
 È possibile combinare trasformazioni complessive e di pagina per ottenere svariati effetti.  Si supponga ad esempio che si desideri utilizzare i pollici come unità di misura e che l'origine del sistema di coordinate si trovi a 2 pollici dal margine sinistro dell'area client e a 1\/2 pollice dall'estremità superiore dell'area client.  L'esempio seguente consente di impostare le trasformazioni complessiva e di pagina di un oggetto <xref:System.Drawing.Graphics> e di tracciare una riga dal punto \(0, 0\) al punto \(2, 1\):  
  
 [!code-csharp[System.Drawing.CoordinateSystems#34](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#34)]
 [!code-vb[System.Drawing.CoordinateSystems#34](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#34)]  
  
 Nell'immagine seguente vengono mostrati la linea e il sistema di coordinate.  
  
 ![Sistema di coordinate](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art03.png "AboutGdip05\_art03")  
  
 Se si suppone che nella periferica di visualizzazione siano disponibili 96 punti per pollice in direzione orizzontale e 96 punti per pollice in direzione verticale, i valori relativi ai punti finali della linea dell'esempio nei tre spazi di coordinate saranno i seguenti:  
  
|||  
|-|-|  
|World|Da \(0, 0\) a \(2, 1\)|  
|Page|Da \(2, 0,5\) a \(4, 1,5\)|  
|Dispositivo|Da \(192, 48\) a \(384, 144\)|  
  
## Vedere anche  
 [Sistemi di coordinate e trasformazioni](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)   
 [Rappresentazione tramite matrici delle trasformazioni](../../../../docs/framework/winforms/advanced/matrix-representation-of-transformations.md)