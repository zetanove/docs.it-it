---
title: "Gestione dello stato di un oggetto Graphics | Microsoft Docs"
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
  - "grafica, area di visualizzazione"
  - "grafica, gestione dello stato"
ms.assetid: 6207cad1-7a34-4bd6-bfc1-db823ca7a73e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Gestione dello stato di un oggetto Graphics
La classe <xref:System.Drawing.Graphics> è un elemento essenziale di [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  Per disegnare qualunque elemento, è necessario ottenere un oggetto <xref:System.Drawing.Graphics>, impostarne le proprietà e chiamarne i metodi, ad esempio <xref:System.Drawing.Graphics.DrawLine%2A>, <xref:System.Drawing.Graphics.DrawImage%2A>, <xref:System.Drawing.Graphics.DrawString%2A>.  
  
 Nell'esempio qui di seguito viene chiamato il metodo <xref:System.Drawing.Graphics.DrawRectangle%2A> dell'oggetto <xref:System.Drawing.Graphics>.  Il primo argomento passato al metodo <xref:System.Drawing.Graphics.DrawRectangle%2A> è un oggetto <xref:System.Drawing.Pen>.  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue) ' Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  // Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100);  
```  
  
## Stato graphics  
 In un oggetto <xref:System.Drawing.Graphics> non vengono solo forniti metodi per il disegno, come <xref:System.Drawing.Graphics.DrawLine%2A> e <xref:System.Drawing.Graphics.DrawRectangle%2A>.  ma viene anche conservato lo stato graphics, che può essere suddiviso nelle seguenti categorie:  
  
-   Impostazioni di qualità  
  
-   Trasformazioni  
  
-   Area di ridimensionamento  
  
### Impostazioni di qualità  
 Con un oggetto <xref:System.Drawing.Graphics> si dispone di numerose proprietà che consentono di influenzare la qualità degli elementi disegnati.  È possibile ad esempio impostare la proprietà <xref:System.Drawing.Graphics.TextRenderingHint%2A> per specificare il tipo dell'eventuale anti\-aliasing applicato al testo.  Altre proprietà che consentono di influire sulla qualità sono <xref:System.Drawing.Graphics.SmoothingMode%2A>, <xref:System.Drawing.Graphics.CompositingMode%2A>, <xref:System.Drawing.Graphics.CompositingQuality%2A> e <xref:System.Drawing.Graphics.InterpolationMode%2A>.  
  
 Nell'esempio che segue vengono disegnate due ellissi, una con modalità di smussatura impostata su <xref:System.Drawing.Drawing2D.SmoothingMode> e una con la stessa modalità impostata su <xref:System.Drawing.Drawing2D.SmoothingMode>:  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue)  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias  
graphics.DrawEllipse(pen, 0, 0, 200, 100)  
graphics.SmoothingMode = SmoothingMode.HighSpeed  
graphics.DrawEllipse(pen, 0, 150, 200, 100)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias;  
graphics.DrawEllipse(pen, 0, 0, 200, 100);  
graphics.SmoothingMode = SmoothingMode.HighSpeed;  
graphics.DrawEllipse(pen, 0, 150, 200, 100);  
```  
  
### Trasformazioni  
 In un oggetto <xref:System.Drawing.Graphics> è possibile gestire due trasformazioni, world e page, che si applicano a tutti gli elementi disegnati tramite l'oggetto stesso.  Qualsiasi trasformazione affine può essere memorizzata nella trasformazione world.  Esempi di trasformazioni affini comprendono rotazione, creazione di un riflesso, inclinazione e traslazione.  La trasformazione page può essere utilizzata per l'adattamento e per la modifica delle unità, ad esempio da pixel a pollici.  Per ulteriori informazioni, vedere [Sistemi di coordinate e trasformazioni](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md).  
  
 Nell'esempio che segue si impostano le trasformazioni di tipo world e di tipo page di un oggetto <xref:System.Drawing.Graphics>.  La trasformazione world viene impostata su una rotazione di 30 gradi.  La trasformazione page viene impostata in modo che le coordinate passate al secondo <xref:System.Drawing.Graphics.DrawEllipse%2A> siano considerate come espresse in millimetri anziché in pixel.  Vengono effettuate due chiamate identiche al metodo <xref:System.Drawing.Graphics.DrawEllipse%2A>.  La trasformazione di tipo world viene applicata durante la prima chiamata a <xref:System.Drawing.Graphics.DrawEllipse%2A>; con la seconda chiamata a <xref:System.Drawing.Graphics.DrawEllipse%2A> vengono applicate entrambe le trasformazioni \(world e page\).  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Red)  
  
graphics.ResetTransform()  
graphics.RotateTransform(30) ' world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
graphics.PageUnit = GraphicsUnit.Millimeter ' page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Red);   
  
graphics.ResetTransform();  
graphics.RotateTransform(30);                    // world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
graphics.PageUnit = GraphicsUnit.Millimeter;     // page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
```  
  
 Nell'illustrazione che segue sono mostrate le due ellissi.  Si noti che la rotazione di 30 gradi avviene rispetto all'origine del sistema di coordinate \(angolo in alto a sinistra dell'area client\), anziché rispetto al centro delle ellissi.  Si noti inoltre che la larghezza della penna, pari a 1, indica 1 pixel per la prima ellisse e 1 millimetro per la seconda.  
  
 ![Ovali](../../../../docs/framework/winforms/advanced/media/csgraphicsascon1.png "csgraphicsascon1")  
  
### Area di ridimensionamento  
 Tramite un oggetto <xref:System.Drawing.Graphics> è possibile gestire un'area di ridimensionamento applicabile a tutti gli elementi disegnati dall'oggetto stesso.  È possibile impostare tale area chiamando il metodo <xref:System.Drawing.Graphics.SetClip%2A>.  
  
 Nell'esempio che segue si crea un'area a forma di segno più tramite l'unione di due rettangoli.  Tale area è designata come area di ridimensionamento di un oggetto <xref:System.Drawing.Graphics>.  Quindi vengono disegnate due linee limitate dall'interno dell'area.  
  
```vb  
Dim graphics As Graphics = e.Graphics  
  
' Opaque red, width 5  
Dim pen As New Pen(Color.Red, 5)  
  
' Opaque aqua  
Dim brush As New SolidBrush(Color.FromArgb(255, 180, 255, 255))  
  
' Create a plus-shaped region by forming the union of two rectangles.  
Dim [region] As New [Region](../../../../amples/snippets/visualbasic/VS_Snippets_Wpf/ToolBarOrient_snip/visualbasic/toolbargraphics/new.bmp Rectangle(50, 0, 50, 150))  
[region].Union(New Rectangle(0, 50, 150, 50))  
graphics.FillRegion(brush, [region])  
  
' Set the clipping region.  
graphics.SetClip([region], CombineMode.Replace)  
  
' Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160)  
graphics.DrawLine(pen, 40, 20, 190, 150)  
  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
  
// Opaque red, width 5  
Pen pen = new Pen(Color.Red, 5);    
  
// Opaque aqua  
SolidBrush brush = new SolidBrush(Color.FromArgb(255, 180, 255, 255));    
  
// Create a plus-shaped region by forming the union of two rectangles.  
Region region = new Region(new Rectangle(50, 0, 50, 150));  
region.Union(new Rectangle(0, 50, 150, 50));  
graphics.FillRegion(brush, region);  
  
// Set the clipping region.  
graphics.SetClip(region, CombineMode.Replace);  
  
// Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160);  
graphics.DrawLine(pen, 40, 20, 190, 150);  
```  
  
 Nell'illustrazione che segue sono mostrate le linee tagliate.  
  
 ![Area di ritaglio limitata](../../../../docs/framework/winforms/advanced/media/graphicsascon2.png "graphicsascon2")  
  
## Vedere anche  
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Utilizzo di contenitori di grafica annidati](../../../../docs/framework/winforms/advanced/using-nested-graphics-containers.md)