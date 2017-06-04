---
title: "Procedura: creare oggetti Graphics per disegnare | Microsoft Docs"
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
  - "GDI+, creazione di immagini"
  - "grafica [Windows Form], creazione"
  - "Graphics (classe)"
  - "immagini [Windows Form], creazione"
ms.assetid: 162861f9-f050-445e-8abb-b2c43a918b8b
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: creare oggetti Graphics per disegnare
Prima di poter creare linee e forme, eseguire il rendering di testo o visualizzare e modificare immagini con [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], è necessario creare un oggetto <xref:System.Drawing.Graphics>.  L'oggetto <xref:System.Drawing.Graphics> rappresenta un'area di disegno [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], ed è l'oggetto utilizzato per la creazione di immagini grafiche.  
  
 La gestione della grafica implica due passaggi fondamentali:  
  
1.  Creazione di un oggetto <xref:System.Drawing.Graphics>.  
  
2.  Utilizzo dell'oggetto <xref:System.Drawing.Graphics> per creare linee e forme, eseguire il rendering di testo oppure visualizzare e modificare immagini.  
  
## Creazione di un oggetto Graphics  
 Un oggetto Graphics può essere creato in diversi modi.  
  
#### Per creare un oggetto Graphics  
  
-   Ricevere un riferimento a un oggetto Graphics nell'ambito di <xref:System.Windows.Forms.PaintEventArgs> nell'evento <xref:System.Windows.Forms.Control.Paint> di un form o di un controllo.  In questo modo viene in genere ottenuto un riferimento a un oggetto Graphics quando si crea codice di disegno per un controllo.  Analogamente, è inoltre possibile ottenere un oggetto Graphics come proprietà di <xref:System.Drawing.Printing.PrintPageEventArgs> quando si gestisce l'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage> per un <xref:System.Drawing.Printing.PrintDocument>.  
  
     In alternativa  
  
-   Chiamare il metodo <xref:System.Windows.Forms.Control.CreateGraphics%2A> di un controllo o form per ottenere un riferimento a un oggetto <xref:System.Drawing.Graphics> che rappresenta la superficie di disegno di tale controllo o form.  Utilizzare questo metodo se si desidera disegnare in un form o controllo già esistente.  
  
     In alternativa  
  
-   Creare un oggetto <xref:System.Drawing.Graphics> da qualsiasi oggetto che eredita da <xref:System.Drawing.Image>.  Questo metodo risulta utile quando si desidera modificare un'immagine già esistente.  
  
     Queste procedure verranno illustrate in modo approfondito nelle sezioni seguenti.  
  
## PaintEventArgs nel gestore dell'evento Paint  
 Al momento della programmazione di <xref:System.Windows.Forms.PaintEventHandler> per i controlli o <xref:System.Drawing.Printing.PrintDocument.PrintPage> per un <xref:System.Drawing.Printing.PrintDocument>, un oggetto Graphics viene fornito come proprietà di <xref:System.Windows.Forms.PaintEventArgs> oppure <xref:System.Drawing.Printing.PrintPageEventArgs>.  
  
#### Per ottenere un riferimento a un oggetto Graphics da PaintEventArgs dell'evento Paint  
  
1.  Dichiarare l'oggetto <xref:System.Drawing.Graphics>.  
  
2.  Assegnare la variabile in modo che faccia riferimento all'oggetto <xref:System.Drawing.Graphics> passato come parte di <xref:System.Windows.Forms.PaintEventArgs>.  
  
3.  Inserire il codice per disegnare il form o il controllo.  
  
     Nell'esempio seguente viene illustrato come creare un riferimento a un oggetto <xref:System.Drawing.Graphics> da un oggetto <xref:System.Windows.Forms.PaintEventArgs> nell'evento <xref:System.Windows.Forms.Control.Paint>:  
  
    ```vb  
    Private Sub Form1_Paint(sender As Object, pe As PaintEventArgs) Handles _  
       MyBase.Paint  
       ' Declares the Graphics object and sets it to the Graphics object  
       ' supplied in the PaintEventArgs.  
       Dim g As Graphics = pe.Graphics  
       ' Insert code to paint the form here.  
    End Sub  
  
    ```  
  
    ```csharp  
    private void Form1_Paint(object sender,   
       System.Windows.Forms.PaintEventArgs pe)   
    {  
       // Declares the Graphics object and sets it to the Graphics object  
       // supplied in the PaintEventArgs.  
       Graphics g = pe.Graphics;  
       // Insert code to paint the form here.  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void Form1_Paint(System::Object ^ sender,  
          System::Windows::Forms::PaintEventArgs ^ pe)  
       {  
          // Declares the Graphics object and sets it to the Graphics object  
          // supplied in the PaintEventArgs.  
          Graphics ^ g = pe->Graphics;  
          // Insert code to paint the form here.  
       }  
    ```  
  
## Metodo CreateGraphics  
 È anche possibile utilizzare il metodo <xref:System.Windows.Forms.Control.CreateGraphics%2A> di un controllo o form per ottenere un riferimento a un oggetto <xref:System.Drawing.Graphics> che rappresenta la superficie di disegno di tale controllo o form.  
  
#### Per creare un oggetto Graphics con il metodo CreateGraphics  
  
-   Chiamare il metodo <xref:System.Windows.Forms.Control.CreateGraphics%2A> del form o del controllo su cui eseguire il rendering della grafica.  
  
    ```vb  
    Dim g as Graphics  
    ' Sets g to a Graphics object representing the drawing surface of the  
    ' control or form g is a member of.  
    g = Me.CreateGraphics  
  
    ```  
  
    ```csharp  
    Graphics g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this.CreateGraphics();  
  
    ```  
  
    ```cpp  
    Graphics ^ g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this->CreateGraphics();  
    ```  
  
## Creazione da un oggetto Image  
 È inoltre possibile creare un oggetto Graphics da qualsiasi oggetto che derivi dalla classe <xref:System.Drawing.Image>.  
  
#### Per creare un oggetto Graphics da un oggetto Image  
  
-   Chiamare il metodo <xref:System.Drawing.Graphics.FromImage%2A?displayProperty=fullName> specificando il nome della variabile Image da cui creare un oggetto <xref:System.Drawing.Graphics>.  
  
     Nell'esempio che segue viene illustrato come utilizzare un oggetto <xref:System.Drawing.Bitmap>:  
  
    ```vb  
    Dim myBitmap as New Bitmap("C:\Documents and Settings\Joe\Pics\myPic.bmp")  
    Dim g as Graphics = Graphics.FromImage(myBitmap)  
  
    ```  
  
    ```csharp  
    Bitmap myBitmap = new Bitmap(@"C:\Documents and   
       Settings\Joe\Pics\myPic.bmp");  
    Graphics g = Graphics.FromImage(myBitmap);  
  
    ```  
  
    ```cpp  
    Bitmap ^ myBitmap = gcnew  
       Bitmap("D:\\Documents and Settings\\Joe\\Pics\\myPic.bmp");  
    Graphics ^ g = Graphics::FromImage(myBitmap);  
    ```  
  
> [!NOTE]
>  È possibile creare oggetti <xref:System.Drawing.Graphics> solo da file BMP non indicizzati, quali file BMP a 16, 24 e 32 bit.  Ciascun pixel di file BMP non indicizzati contiene un colore, a differenza dei pixel dei file BMP indicizzati che contengono un indice a una tabella dei colori.  
  
## Creazione e modifica di forme e immagini  
 Una volta creato, l'oggetto <xref:System.Drawing.Graphics> può essere utilizzato per creare linee e forme, eseguire il rendering di testo oppure visualizzare e modificare immagini.  Di seguito sono riportati i principali oggetti utilizzati con l'oggetto <xref:System.Drawing.Graphics>:  
  
-   Classe <xref:System.Drawing.Pen>: utilizzata per creare linee, tracciare forme oppure eseguire il rendering di altre rappresentazioni geometriche.  
  
-   Classe <xref:System.Drawing.Brush>: utilizzata per riempire aree di grafica, quali forme, immagini o testo riempiti.  
  
-   Classe <xref:System.Drawing.Font>: fornisce una descrizione delle forme da utilizzare per il rendering di testo.  
  
-   Struttura <xref:System.Drawing.Color>: rappresenta i diversi colori da visualizzare.  
  
#### Per utilizzare l'oggetto Graphics creato  
  
-   Dagli oggetti sopra elencati scegliere quello appropriato al disegno che si desidera tracciare.  
  
     Per ulteriori informazioni, vedere i seguenti argomenti:  
  
    |Per eseguire il rendering di|Vedere|  
    |----------------------------------|------------|  
    |Righe|[Procedura: disegnare una linea in un Windows Form](../../../../docs/framework/winforms/advanced/how-to-draw-a-line-on-a-windows-form.md)|  
    |forme a confronto|[Procedura: creare una forma con contorno](../../../../docs/framework/winforms/advanced/how-to-draw-an-outlined-shape.md)|  
    |Text|[Procedura: disegnare testo in un Windows Form](../../../../docs/framework/winforms/advanced/how-to-draw-text-on-a-windows-form.md)|  
    |Immagini|[Procedura: eseguire il rendering delle immagini con GDI\+](../../../../docs/framework/winforms/advanced/how-to-render-images-with-gdi.md)|  
  
## Vedere anche  
 [Guida introduttiva alla programmazione grafica](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: eseguire il rendering delle immagini con GDI\+](../../../../docs/framework/winforms/advanced/how-to-render-images-with-gdi.md)