---
title: "Procedura: creare un oggetto LineSegment in un oggetto PathGeometry | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PathGeometry (classe)"
  - "classi, PathGeometry"
  - "segmenti di linea, creazione"
  - "grafica [WPF], segmenti di linea"
ms.assetid: 0155ed47-a20d-49a7-a306-186d8e07fbc4
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: creare un oggetto LineSegment in un oggetto PathGeometry
In questo esempio viene illustrato come creare un segmento di linea. Per creare un segmento di linea, utilizzare il <xref:System.Windows.Media.PathGeometry>, <xref:System.Windows.Media.PathFigure>, e <xref:System.Windows.Media.LineSegment> classi.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente disegno una <xref:System.Windows.Media.LineSegment> da (10, 50) a (200, 70). La figura seguente mostra l'oggetto risultante <xref:System.Windows.Media.LineSegment>; è stato aggiunto uno sfondo della griglia per visualizzare il sistema di coordinate.  
  
 ![Un oggetto LineSegment in PathFigure](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-pathgeometrylinesegment.png "graphicsmm_pathgeometrylinesegment")  
Un oggetto LineSegment disegnato da (10,50) a (200,70)  
  
 [xaml]  
  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], è possibile utilizzare la sintassi degli attributi per descrivere un percorso.  
  
```xaml  
<Path Stroke="Black" StrokeThickness="1"    
  Data="M 10,50 L 200,70" />  
```  
  
 [xaml]  
  
 (Si noti che la sintassi di attributo crea effettivamente una <xref:System.Windows.Media.StreamGeometry>, una versione leggera di un <xref:System.Windows.Media.PathGeometry>. Per ulteriori informazioni, vedere il [sintassi del Markup percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md) pagina.)  
  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile disegnare un segmento di linea anche utilizzando la sintassi degli elementi oggetto. Di seguito è equivalente alla precedente [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] esempio.  
  
```xaml  
<Path Stroke="Black" StrokeThickness="1">  
  <Path.Data>  
    <PathGeometry>  
      <PathFigure StartPoint="10,50">  
        <LineSegment Point="200,70" />  
      </PathFigure>  
    </PathGeometry>  
  </Path.Data>  
</Path>  
```  
  
```csharp  
PathFigure myPathFigure = new PathFigure();  
myPathFigure.StartPoint = new Point(10, 50);  
  
LineSegment myLineSegment = new LineSegment();  
myLineSegment.Point = new Point(200, 70);  
  
PathSegmentCollection myPathSegmentCollection = new PathSegmentCollection();  
myPathSegmentCollection.Add(myLineSegment);  
  
myPathFigure.Segments = myPathSegmentCollection;  
  
PathFigureCollection myPathFigureCollection = new PathFigureCollection();  
myPathFigureCollection.Add(myPathFigure);  
  
PathGeometry myPathGeometry = new PathGeometry();  
myPathGeometry.Figures = myPathFigureCollection;  
  
Path myPath = new Path();  
myPath.Stroke = Brushes.Black;  
myPath.StrokeThickness = 1;  
myPath.Data = myPathGeometry;  
```  
  
```vb  
Dim myPathFigure As New PathFigure()  
            myPathFigure.StartPoint = New Point(10, 50)  
  
            Dim myLineSegment As New LineSegment()  
            myLineSegment.Point = New Point(200, 70)  
  
            Dim myPathSegmentCollection As New PathSegmentCollection()  
            myPathSegmentCollection.Add(myLineSegment)  
  
            myPathFigure.Segments = myPathSegmentCollection  
  
            Dim myPathFigureCollection As New PathFigureCollection()  
            myPathFigureCollection.Add(myPathFigure)  
  
            Dim myPathGeometry As New PathGeometry()  
            myPathGeometry.Figures = myPathFigureCollection  
  
            Dim myPath As New Path()  
            myPath.Stroke = Brushes.Black  
            myPath.StrokeThickness = 1  
            myPath.Data = myPathGeometry  
```  
  
 Questo esempio fa parte dell'esempio più ampio; per l'esempio completo, vedere il [Geometries Sample](http://go.microsoft.com/fwlink/?LinkID=159989).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Media.PathFigure>   
 <xref:System.Windows.Media.PathGeometry>   
 <xref:System.Windows.Media.GeometryDrawing>   
 <xref:System.Windows.Shapes.Path>   
 [Panoramica di geometria](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)