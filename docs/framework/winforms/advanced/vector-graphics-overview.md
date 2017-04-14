---
title: "Cenni preliminari sulla grafica vettoriale | Microsoft Docs"
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
  - "grafica, immagini vettoriali"
  - "punti finali inclusivi"
ms.assetid: 0195df81-66be-452d-bb53-5a582ebfdc09
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Cenni preliminari sulla grafica vettoriale
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] consente di tracciare linee, rettangoli e altre forme su un sistema di coordinate.  È possibile scegliere tra svariati sistemi di coordinate, ma l'origine del sistema di coordinate predefinito si trova nell'angolo superiore sinistro, con asse x rivolto verso sinistra e asse y rivolto verso il basso.  L'unità di misura del sistema di coordinate predefinito è il pixel.  
  
## Blocchi predefiniti di GDI\+  
 ![Grafica vettoriale](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art01.png "AboutGdip02\_Art01")  
  
 Il monitor di un computer crea il proprio schermo su una matrice rettangolare di punti definiti elementi di immagine o pixel.  Il numero di pixel visualizzati sullo schermo dipende dal tipo di monitor in uso e il numero di pixel visualizzati su un monitor specifico può solitamente essere configurato fino a un dato livello dall'utente.  
  
 ![Grafica vettoriale](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art02.png "AboutGdip02\_Art02")  
  
 Quando si utilizza [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] per tracciare una linea, un rettangolo o una curva, si forniscono determinate informazioni sull'elemento da tracciare.  È ad esempio possibile tracciare una linea specificando due punti, oppure un rettangolo specificando un punto, un'altezza e una larghezza.  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] opera unitamente al software del driver video per determinare i pixel da attivare per mostrare la linea, il rettangolo o la curva.  Nell'immagine seguente vengono mostrati i pixel attivati per visualizzare una linea che unisce il punto \(4, 2\) e il punto \(12, 8\).  
  
 ![Grafica vettoriale](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art03.png "AboutGdip02\_Art03")  
  
 Nel corso del tempo determinati blocchi predefiniti si sono dimostrati più efficaci per la creazione di immagini bidimensionali.  Nell'elenco seguente sono riportati tali blocchi predefiniti, tutti supportati da [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  
  
-   Righe  
  
-   Rettangoli  
  
-   Ellissi  
  
-   Archi  
  
-   Poligoni  
  
-   Spline di tipo Cardinal  
  
-   Spline di Bézier  
  
## Metodi per disegnare con un oggetto Graphics  
 La classe <xref:System.Drawing.Graphics> in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] offre i metodi seguenti per disegnare gli elementi inclusi nell'elenco precedente: <xref:System.Drawing.Graphics.DrawLine%2A>, <xref:System.Drawing.Graphics.DrawRectangle%2A>, <xref:System.Drawing.Graphics.DrawEllipse%2A>, <xref:System.Drawing.Graphics.DrawPolygon%2A>, <xref:System.Drawing.Graphics.DrawArc%2A>, <xref:System.Drawing.Graphics.DrawCurve%2A> \(per le spline di tipo Cardinal\) e <xref:System.Drawing.Graphics.DrawBezier%2A>.  Tutti questi metodi sono sottoposti a overload, ovvero ogni metodo supporta svariati elenchi di parametri diversi.  Ad esempio, una variazione del metodo <xref:System.Drawing.Graphics.DrawLine%2A> riceve un oggetto <xref:System.Drawing.Pen> e quattro interi, mentre un'altra variazione del metodo <xref:System.Drawing.Graphics.DrawLine%2A> riceve un oggetto <xref:System.Drawing.Pen> e due oggetti <xref:System.Drawing.Point>.  
  
 Ai metodi per tracciare linee, rettangoli e spline Bézier sono associati più metodi correlati che consentono di disegnare più elementi in un'unica chiamata: <xref:System.Drawing.Graphics.DrawLines%2A>, <xref:System.Drawing.Graphics.DrawRectangles%2A> e <xref:System.Drawing.Graphics.DrawBeziers%2A>.  Al metodo <xref:System.Drawing.Graphics.DrawCurve%2A> inoltre è associato un metodo correlato <xref:System.Drawing.Graphics.DrawClosedCurve%2A>, che consente di chiudere una curva collegandone il punto finale e il punto iniziale.  
  
 Tutti i metodi di disegno della classe <xref:System.Drawing.Graphics> vengono utilizzati insieme a un oggetto <xref:System.Drawing.Pen>.  Per tracciare un qualsiasi elemento, è necessario creare almeno due oggetti: un oggetto <xref:System.Drawing.Graphics> e un oggetto <xref:System.Drawing.Pen>.  Nell'oggetto <xref:System.Drawing.Pen> vengono memorizzati gli attributi, quali lo spessore e il colore della linea, dell'elemento da tracciare.  L'oggetto <xref:System.Drawing.Pen> viene passato come uno degli argomenti del metodo di disegno.  Una variazione del metodo <xref:System.Drawing.Graphics.DrawLine%2A> ad esempio riceve un oggetto <xref:System.Drawing.Pen> e quattro interi, come illustrato nell'esempio seguente, che consentono di tracciare un rettangolo con larghezza 100, altezza 50 e angolo superiore sinistro di \(20, 10\):  
  
 [!code-csharp[LinesCurvesAndShapes#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#11)]
 [!code-vb[LinesCurvesAndShapes#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#11)]  
  
## Vedere anche  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)