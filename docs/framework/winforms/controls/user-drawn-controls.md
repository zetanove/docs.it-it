---
title: "Controlli creati dall&#39;utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli personalizzati [Windows Form], creati dall'utente"
  - "OnPaint (metodo) [Windows Form]"
  - "controlli creati dall'utente [Windows Form]"
ms.assetid: 034af4b5-457f-4160-a937-22891817faa8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Controlli creati dall&#39;utente
.NET Framework consente di sviluppare facilmente controlli personalizzati.  È possibile creare un controllo utente, ovvero un insieme di controlli standard associati gli uni agli altri tramite il codice, oppure progettare dal nulla un controllo personalizzato.  È anche possibile utilizzare l'ereditarietà per creare un controllo che eredita da un controllo esistente ed estenderne le funzionalità intrinseche.  Quale che sia il meccanismo adottato, .NET Framework offre le funzionalità per la creazione di un'interfaccia grafica personalizzata per qualsiasi controllo creato.  
  
 La stampa di un controllo viene realizzata tramite esecuzione del codice nel metodo <xref:System.Windows.Forms.Control.OnPaint%2A> del controllo.  L'unico argomento del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> è un oggetto <xref:System.Windows.Forms.PaintEventArgs> che fornisce tutte le informazioni e le funzionalità richieste per il rendering del controllo.  L'oggetto <xref:System.Windows.Forms.PaintEventArgs> fornisce come proprietà due oggetti principali che vengono utilizzati nel rendering del controllo:  
  
-   L'oggetto <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>, ovvero il rettangolo che rappresenta la parte del controllo che verrà disegnata.  A seconda della modalità di disegno, può corrispondere all'intero controllo oppure solo a una parte.  
  
-   L'oggetto <xref:System.Drawing.Graphics>, in cui sono incapsulati vari oggetti e metodi orientati alla grafica che forniscono le funzionalità necessarie per disegnare il controllo.  
  
 Per ulteriori informazioni sull'oggetto <xref:System.Drawing.Graphics> e su come utilizzarlo, vedere [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md).  
  
 L'evento <xref:System.Windows.Forms.Control.OnPaint%2A> viene generato ogni volta che si disegna il controllo o se ne aggiorna la visualizzazione. L'oggetto <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> rappresenta il rettangolo in cui disegnare.  Se è necessario aggiornare l'intero controllo, l'oggetto <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> rappresenterà le dimensioni dell'intero controllo.  Se invece è necessario aggiornare solo una parte del controllo, l'oggetto <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> rappresenterà solo la regione da ridisegnare.  Un esempio è dato da un controllo parzialmente oscurato da un altro controllo o form nell'interfaccia utente.  
  
 Quando si eredita dalla classe <xref:System.Windows.Forms.Control>, è necessario eseguire l'override del metodo e <xref:System.Windows.Forms.Control.OnPaint%2A> fornire il codice del rendering grafico.  Per fornire un'interfaccia grafica personalizzata a un controllo utente o a un controllo ereditato, è possibile eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  Di seguito viene illustrato un esempio.  
  
```vb  
Protected Overrides Sub OnPaint(ByVal pe As PaintEventArgs)  
   ' Call the OnPaint method of the base class.  
   MyBase.OnPaint(pe)  
  
   ' Declare and instantiate a drawing pen.  
   Dim myPen As System.Drawing.Pen = New System.Drawing.Pen(Color.Aqua)  
  
   ' Draw an aqua rectangle in the rectangle represented by the control.  
   pe.Graphics.DrawRectangle(myPen, New Rectangle(Me.Location, Me.Size))  
End Sub  
  
```  
  
```csharp  
protected override void OnPaint(PaintEventArgs pe)  
{  
   // Call the OnPaint method of the base class.  
   base.OnPaint(pe);  
  
   // Declare and instantiate a new pen.  
   System.Drawing.Pen myPen = new System.Drawing.Pen(Color.Aqua);  
  
   // Draw an aqua rectangle in the rectangle represented by the control.  
   pe.Graphics.DrawRectangle(myPen, new Rectangle(this.Location,   
      this.Size));  
}  
  
```  
  
 L'esempio descritto dimostra come eseguire il rendering di un controllo con una rappresentazione grafica molto semplice:  chiama il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base, crea un oggetto <xref:System.Drawing.Pen> con cui disegnare e, infine, disegna un ellisse nel rettangolo determinato dalle proprietà <xref:System.Windows.Forms.Control.Location%2A> e <xref:System.Windows.Forms.Control.Size%2A> del controllo.  Benché la maggior parte del codice di rendering sia molto più complessa, in questo esempio viene illustrato l'utilizzo dell'oggetto <xref:System.Drawing.Graphics> contenuto nell'oggetto <xref:System.Windows.Forms.PaintEventArgs>.  Se si eredita da una classe che dispone già di una rappresentazione grafica, come <xref:System.Windows.Forms.UserControl> o <xref:System.Windows.Forms.Button>, e non si desidera incorporare tale rappresentazione nel proprio rendering, non chiamare il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base.  
  
 Il codice nel metodo <xref:System.Windows.Forms.Control.OnPaint%2A> del controllo viene eseguito quando il controllo viene disegnato per la prima volta e a ogni successivo aggiornamento.  Per garantire che il controllo venga ridisegnato a ogni ridimensionamento, aggiungere la riga seguente al costruttore del controllo:  
  
```vb  
SetStyle(ControlStyles.ResizeRedraw, True)  
  
```  
  
```csharp  
SetStyle(ControlStyles.ResizeRedraw, true);  
  
```  
  
> [!NOTE]
>  Utilizzare la proprietà <xref:System.Windows.Forms.Control.Region%2A?displayProperty=fullName> per implementare un controllo non rettangolare.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.Region%2A>   
 <xref:System.Windows.Forms.ControlStyles>   
 <xref:System.Drawing.Graphics>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 <xref:System.Windows.Forms.PaintEventArgs>   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Controlli costitutivi](../../../../docs/framework/winforms/controls/constituent-controls.md)   
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)