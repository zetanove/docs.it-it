---
title: "Procedura: copiare i pixel per ridurre lo sfarfallio in Windows Form | Microsoft Docs"
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
  - "trasferimento di blocchi di bit"
  - "bitblt"
  - "sfarfallio"
  - "sfarfallio, riduzione in Windows Form"
  - "grafica, copia"
  - "grafica, riduzione dello sfarfallio"
  - "pixel, copia"
ms.assetid: 33b76910-13a3-4521-be98-5c097341ae3b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: copiare i pixel per ridurre lo sfarfallio in Windows Form
Quando si anima un oggetto grafico semplice, è possibile che si verifichino lo sfarfallio dell'immagine o altri effetti visivi indesiderati.  Un modo per limitare tale problema consiste nell'utilizzare un processo "bitblt" sull'oggetto grafico.  Per bitblt si intende il "trasferimento di blocchi di bit" dei dati relativi al colore da un rettangolo di pixel di origine a un rettangolo di pixel di destinazione.  
  
 In Windows Forms il processo bitblt viene ottenuto utilizzando il metodo <xref:System.Drawing.Graphics.CopyFromScreen%2A> della classe <xref:System.Drawing.Graphics>.  Si specificano, nei parametri del metodo, l'origine e la destinazione \(espressi in punti\), le dimensioni dell'area da copiare e l'oggetto grafico utilizzato per disegnare la nuova forma.  
  
 Nell'esempio seguente viene disegnata una forma sul form nel gestore eventi <xref:System.Windows.Forms.Control.Paint>.  Viene quindi utilizzato il metodo <xref:System.Drawing.Graphics.CopyFromScreen%2A> per duplicare la forma.  
  
> [!NOTE]
>  L'impostazione della proprietà <xref:System.Windows.Forms.Control.DoubleBuffered%2A> del form su `true` comporta l'esecuzione del doppio buffer del codice basato su grafica contenuto nell'evento <xref:System.Windows.Forms.Control.Paint>.  Pe quanto tale evenienza non equivalga a un miglioramento sensibile delle prestazioni quando si utilizza il codice riportato di seguito, è opportuno tenerne conto quando si utilizza codice più complesso per la modifica di oggetti grafici.  
  
## Esempio  
  
```vb  
Private Sub Form1_Paint(ByVal sender As Object, ByVal e As _  
    System.Windows.Forms.PaintEventArgs) Handles MyBase.Paint  
    ' Draw a circle with a bar on top.  
        e.Graphics.FillEllipse(Brushes.DarkBlue, New Rectangle _  
             (10, 10, 60, 60))  
        e.Graphics.FillRectangle(Brushes.Khaki, New Rectangle _  
             (20, 30, 60, 10))  
    ' Copy the graphic to a new location.  
        e.Graphics.CopyFromScreen(New Point(10, 10), New Point _  
             (100, 100), New Size(70, 70))  
End Sub  
  
```  
  
```csharp  
private void Form1_Paint(System.Object sender,  
    System.Windows.Forms.PaintEventArgs e)  
        {  
        e.Graphics.FillEllipse(Brushes.DarkBlue, new  
            Rectangle(10,10,60,60));  
        e.Graphics.FillRectangle(Brushes.Khaki, new  
            Rectangle(20,30,60,10));  
        e.Graphics.CopyFromScreen(new Point(10, 10), new Point(100, 100),   
            new Size(70, 70));  
}  
```  
  
## Compilazione del codice  
 Il codice precedente viene eseguito nel gestore eventi <xref:System.Windows.Forms.Control.Paint> del form affinché la grafica persista quando il form viene ridisegnato.  Per tale ragione, non eseguire chiamate a metodi correlati a grafica nel gestore eventi <xref:System.Windows.Forms.Form.Load> perché il contenuto disegnato non verrà ridisegnato se il form viene ridimensionato o nascosto da un altro form.  
  
## Vedere anche  
 <xref:System.Drawing.CopyPixelOperation>   
 <xref:System.Drawing.Graphics.FillRectangle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.OnPaint%2A?displayProperty=fullName>   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Utilizzo di un oggetto Pen per creare linee e forme](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)