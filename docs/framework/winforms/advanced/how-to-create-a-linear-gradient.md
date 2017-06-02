---
title: "Procedura: creare una sfumatura lineare | Microsoft Docs"
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
  - "colori, creazione di gradienti lineari"
  - "sfumature"
  - "sfumature, creazione lineare"
  - "gradienti lineari, creazione"
ms.assetid: 6c88e1cc-1217-4399-ac12-cb37592b9f01
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: creare una sfumatura lineare
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] consente di utilizzare sfumature lineari in orizzontale, in verticale e in diagonale.  Per impostazione predefinita il colore di una sfumatura lineare cambia in modo uniforme.  È possibile tuttavia personalizzare una sfumatura lineare in modo che il colore si modifichi con modalità non uniforme.  
  
 Nell'esempio che segue si riempie una linea, un'ellisse e un rettangolo con un pennello a sfumatura lineare orizzontale.  
  
 Il costruttore <xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A> riceve quattro argomenti: due punti e due colori.  Il primo punto \(0, 10\) è associato al primo colore \(rosso\), il secondo \(200, 10\) è associato al secondo colore \(blu\).  Come prevedibile, la linea tracciata da \(0, 10\) a \(200, 10\) cambia gradualmente da rosso a blu.  
  
 Il numero 10 nei punti \(50, 10\) e \(200, 10\) non è rilevante.  Ciò che conta è che la seconda coordinata è uguale per i due punti; la linea che li collega è pertanto orizzontale.  Anche l'ellisse e il rettangolo passano in modo graduale da rosso a blu man mano che la coordinata passa da 0 a 200.  
  
 Nell'illustrazione che segue sono visibili la linea, l'ellisse e il rettangolo.  Si noti che la sfumatura di colore si ripete per le coordinate orizzontali superiori a 200.  
  
 ![Sfumatura lineare](../../../../docs/framework/winforms/advanced/media/cslineargradient1.png "cslineargradient1")  
  
### Per utilizzare sfumature lineari orizzontali  
  
-   Impostare i colori rosso opaco e blu opaco come terzo argomento e quarto argomento rispettivamente.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#21)]
     [!code-vb[System.Drawing.UsingaGradientBrush#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#21)]  
  
 Nell'esempio precedente le componenti del colore vengono modificate in modo lineare spostandosi dalla coordinata orizzontale 0 alla coordinata orizzontale 200.  Ad esempio, un punto che si trova a metà tra le coordinate 0 e 200 avrà una componente di blu intermedia tra 0 e 255.  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] consente di regolare le modalità di variazione di un colore da un margine all'altro di una sfumatura.  Si supponga di voler creare un pennello a sfumatura che passi da nero a rosso in conformità alla tabella che segue.  
  
|Coordinata orizzontale|Componenti RGB|  
|----------------------------|--------------------|  
|0|\(0, 0, 0\)|  
|40|\(128, 0, 0\)|  
|200|\(255, 0, 0\)|  
  
 Si noti che la componente rossa ha intensità media quando la coordinata orizzontale è solo al 20% del percorso tra 0 e 200.  
  
 Nell'esempio che segue si imposta la proprietà <xref:System.Drawing.Drawing2D.LinearGradientBrush.Blend%2A> di un oggetto <xref:System.Drawing.Drawing2D.LinearGradientBrush> per associare tre intensità relative a tre posizioni relative.  Come nella tabella precedente, un'intensità relativa di 0,5 è associata a una posizione relativa di 0,2.  Un'ellisse e un rettangolo verranno riempiti con il pennello a sfumatura.  
  
 Nell'illustrazione che segue sono visibili il rettangolo e l'ellisse risultanti.  
  
 ![Sfumatura lineare](../../../../docs/framework/winforms/advanced/media/cslineargradient2.png "cslineargradient2")  
  
### Per personalizzare sfumature lineari  
  
-   Passare i colori nero opaco e rosso opaco come terzo argomento e quarto argomento rispettivamente.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#22)]
     [!code-vb[System.Drawing.UsingaGradientBrush#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#22)]  
  
 Negli esempi precedenti si illustrava una sfumatura orizzontale, nella quale il colore cambia in modo graduale muovendosi lungo una linea orizzontale.  È anche possibile definire sfumature verticali e diagonali.  
  
 Nell'esempio che segue i punti \(0, 0\) e \(200, 100\) vengono passati a un costruttore <xref:System.Drawing.Drawing2D.LinearGradientBrush.%23ctor%2A>.  Il colore blu è associato a \(0, 0\), il colore verde a \(200, 100\).  Una linea disegnata con penna di larghezza 10 e un'ellisse vengono riempite con il pennello a sfumatura lineare.  
  
 Nell'illustrazione che segue sono visibili la linea e l'ellisse.  Si noti che il colore nell'ellisse cambia in modo graduale spostandosi lungo qualsiasi linea parallela a quella che passa per \(0, 0\) e \(200, 100\).  
  
 ![Sfumatura lineare](../../../../docs/framework/winforms/advanced/media/cslineargradient3.png "cslineargradient3")  
  
### Per creare sfumature lineari diagonali  
  
-   Passare i colori blu opaco e verde opaco come terzo argomento e quarto argomento rispettivamente.  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#23)]
     [!code-vb[System.Drawing.UsingaGradientBrush#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#23)]  
  
## Vedere anche  
 [Utilizzo di un pennello a sfumatura per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-gradient-brush-to-fill-shapes.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)