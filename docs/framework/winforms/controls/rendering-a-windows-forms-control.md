---
title: "Rendering di un controllo Windows Form | Microsoft Docs"
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
  - "controlli personalizzati [Windows Form], risorse grafiche"
  - "controlli personalizzati [Windows Form], invalidazione e disegno"
  - "controlli personalizzati [Windows Form], rendering"
  - "OnPaintBackground (metodo), chiamata in controlli Windows Form personalizzati"
ms.assetid: aae8e1e6-4786-432b-a15e-f4c44760d302
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Rendering di un controllo Windows Form
Il rendering rappresenta il processo di creazione di una rappresentazione visiva sullo schermo dell'utente.  In Windows Form per il rendering viene utilizzato [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)], la nuova libreria grafica di Windows.  Le classi gestite che forniscono l'accesso a [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] si trovano nello spazio dei nomi <xref:System.Drawing?displayProperty=fullName> e nei relativi sottospazi dei nomi.  
  
 Di seguito sono indicati gli elementi interessati dal rendering dei controlli.  
  
-   Le funzionalità di disegno fornite dalla classe base <xref:System.Windows.Forms.Control?displayProperty=fullName>.  
  
-   Gli elementi essenziali della libreria grafica [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)].  
  
-   La geometria della regione di disegno.  
  
-   La procedura per la liberazione di risorse grafiche.  
  
## Funzionalità di disegno fornite da Control  
 La classe base <xref:System.Windows.Forms.Control> fornisce funzionalità di disegno tramite l'evento <xref:System.Windows.Forms.Control.Paint>.  L'evento <xref:System.Windows.Forms.Control.Paint> viene generato dal controllo ogni volta che è necessario aggiornare la relativa visualizzazione.  Per ulteriori informazioni sugli eventi di .NET Framework, vedere [Gestione e generazione di eventi](../../../../docs/standard/events/index.md).  
  
 La classe dei dati evento per <xref:System.Windows.Forms.Control.Paint>, <xref:System.Windows.Forms.PaintEventArgs>, contiene i dati necessari per il disegno di un controllo, un handle a un oggetto grafico e un oggetto rettangolo che rappresenta la regione in cui eseguire il disegno.  Questi oggetti sono indicati in grassetto nel codice riportato di seguito.  
  
```vb  
Public Class PaintEventArgs  
   Inherits EventArgs  
   Implements IDisposable  
  
   Public ReadOnly Property ClipRectangle() As System.Drawing.Rectangle  
      ...  
   End Property  
  
   Public ReadOnly Property Graphics() As System.Drawing.Graphics  
      ...  
   End Property  
   ' Other properties and methods.  
   ...  
End Class  
```  
  
```csharp  
public class PaintEventArgs : EventArgs, IDisposable {  
public System.Drawing.Rectangle ClipRectangle {get;}  
public System.Drawing.Graphics Graphics {get;}  
// Other properties and methods.  
...  
}  
```  
  
 <xref:System.Drawing.Graphics> è una classe gestita che incapsula funzionalità di disegno, come descritto a proposito di [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] più avanti in questo argomento.  La proprietà <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> è un'istanza della struttura <xref:System.Drawing.Rectangle> e definisce l'area disponibile per il disegno di un controllo.  Gli sviluppatori possono calcolare <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> attraverso la proprietà <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> di un controllo, come descritto a proposito della geometria più avanti in questo argomento.  
  
 È necessario che un controllo fornisca logica di rendering mediante l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> ereditato dalla classe <xref:System.Windows.Forms.Control>.  Il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> accede all'oggetto grafico e al rettangolo in cui effettuare il disegno tramite le proprietà <xref:System.Drawing.Design.PaintValueEventArgs.Graphics%2A> e <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> dell'istanza <xref:System.Windows.Forms.PaintEventArgs> a esso passata.  
  
```vb  
Protected Overridable Sub OnPaint(pe As PaintEventArgs)  
```  
  
```csharp  
protected virtual void OnPaint(PaintEventArgs pe);  
```  
  
 Il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base <xref:System.Windows.Forms.Control> non implementa alcuna funzionalità di disegno ma richiama unicamente i delegati registrati con l'evento <xref:System.Windows.Forms.Control.Paint>.  Quando si sottopone a override <xref:System.Windows.Forms.Control.OnPaint%2A>, è in genere opportuno richiamare il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base in modo che i delegati registrati ricevano l'evento <xref:System.Windows.Forms.Control.Paint>.  Per i controlli di cui viene disegnata l'intera superficie è tuttavia opportuno non richiamare il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base, in quanto si verificherebbe uno sfarfallio.  Per un esempio dell'override dell'evento <xref:System.Windows.Forms.Control.OnPaint%2A>, vedere [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md).  
  
> [!NOTE]
>  Non richiamare il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> direttamente dal controllo. Richiamare invece il metodo <xref:System.Windows.Forms.Control.Invalidate%2A>, ereditato dalla classe <xref:System.Windows.Forms.Control>, o un altro metodo che richiami <xref:System.Windows.Forms.Control.Invalidate%2A>.  Il metodo <xref:System.Windows.Forms.Control.Invalidate%2A> richiamerà a sua volta <xref:System.Windows.Forms.Control.OnPaint%2A>.  Il metodo <xref:System.Windows.Forms.Control.Invalidate%2A> `e` è sottoposto a overload e, a seconda degli argomenti a esso forniti, l'area visualizzata di un controllo viene ridisegnata interamente o in parte.  
  
 La classe base <xref:System.Windows.Forms.Control> definisce un altro metodo utile per il disegno: il metodo <xref:System.Windows.Forms.Control.OnPaintBackground%2A>.  
  
```vb  
Protected Overridable Sub OnPaintBackground(pevent As PaintEventArgs)  
```  
  
```csharp  
protected virtual void OnPaintBackground(PaintEventArgs pevent);  
```  
  
 Il metodo <xref:System.Windows.Forms.Control.OnPaintBackground%2A> disegna lo sfondo, e di conseguenza la forma, della finestra ed è sempre veloce, mentre il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> disegna i dettagli e può risultare più lento, in quanto tutte le singole richieste di disegno vengono combinate in un unico evento <xref:System.Windows.Forms.Control.Paint> che copre tutte le aree da ridisegnare.  È possibile richiamare il metodo <xref:System.Windows.Forms.Control.OnPaintBackground%2A> se, ad esempio, si desidera applicare al controllo uno sfondo di colore sfumato.  
  
 Mentre il metodo <xref:System.Windows.Forms.Control.OnPaintBackground%2A> presenta una nomenclatura analoga a quella degli eventi e accetta lo stesso argomento del metodo `OnPaint`, <xref:System.Windows.Forms.Control.OnPaintBackground%2A> non è un vero metodo di evento.  Non esiste infatti alcun evento `PaintBackground` e il metodo <xref:System.Windows.Forms.Control.OnPaintBackground%2A> non richiama delegati di evento.  Quando si sottopone a override il metodo <xref:System.Windows.Forms.Control.OnPaintBackground%2A>, non è necessaria alcuna classe derivata per richiamare il metodo <xref:System.Windows.Forms.Control.OnPaintBackground%2A> della relativa classe base.  
  
## Nozioni fondamentali su GDI\+  
 La classe <xref:System.Drawing.Graphics> fornisce metodi per il disegno di varie forme, quali cerchi, triangoli, archi ed ellissi, nonché metodi per la visualizzazione di testo.  Lo spazio dei nomi <xref:System.Drawing?displayProperty=fullName> e i relativi sottospazi dei nomi contengono classi che incapsulano elementi grafici quali forme \(cerchi, rettangoli, archi e altre\), colori, tipi di carattere, pennelli e così via.  Per ulteriori informazioni su [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)], vedere [Utilizzo di classi grafiche gestite](../../../../docs/framework/winforms/advanced/using-managed-graphics-classes.md).  Per informazioni di base su [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)], vedere inoltre [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md).  
  
## Geometria della regione di disegno  
 La proprietà <xref:System.Windows.Forms.Control.ClientRectangle%2A> di un controllo specifica la regione rettangolare a disposizione del controllo sullo schermo dell'utente, mentre la proprietà <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> della classe <xref:System.Windows.Forms.PaintEventArgs> specifica l'area effettivamente disegnata.  Tenere presente che il disegno viene eseguito nel metodo per l'evento <xref:System.Windows.Forms.Control.Paint> cui viene fornito come argomento un'istanza di  <xref:System.Windows.Forms.PaintEventArgs>.  Può essere necessario ridisegnare solo una parte dell'area disponibile a un controllo, ad esempio nel caso in cui venga modificata solo una piccola sezione del controllo visualizzato.  In queste situazioni lo sviluppatore del controllo deve calcolare l'effettivo rettangolo in cui è necessario disegnare e passarlo a <xref:System.Windows.Forms.Control.Invalidate%2A>.  Le versioni sottoposte a overload del metodo <xref:System.Windows.Forms.Control.Invalidate%2A> cui viene fornito come argomento <xref:System.Drawing.Rectangle> o <xref:System.Drawing.Region> utilizzano l'argomento per generare la proprietà <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> della classe <xref:System.Windows.Forms.PaintEventArgs>.  
  
 Nel codice seguente viene illustrato come calcolare nel controllo personalizzato `FlashTrackBar` l'area rettangolare in cui si esegue il disegno.  La variabile `client` denota la proprietà <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>.  Per un esempio completo, vedere [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md).  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#6)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#6)]  
  
## Liberazione di risorse grafiche  
 Gli oggetti grafici utilizzano molte risorse di sistema.  Questi oggetti includono istanze della classe <xref:System.Drawing.Graphics?displayProperty=fullName>, nonché istanze delle classi <xref:System.Drawing.Brush?displayProperty=fullName>, <xref:System.Drawing.Pen?displayProperty=fullName> e altre classi di grafica.  È importante creare una risorsa grafica solo quando è effettivamente necessaria e rilasciarla appena si termina di utilizzarla.  Se si crea un tipo che implementa l'interfaccia <xref:System.IDisposable>, chiamare il relativo metodo <xref:System.IDisposable.Dispose%2A> quando si cessa di utilizzarla, in modo da liberare risorse.  
  
 Nel codice seguente viene illustrato come viene creata e rilasciata una risorsa <xref:System.Drawing.Brush> dal controllo personalizzato `FlashTrackBar`.  Per il codice sorgente completo, vedere [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md).  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#5)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#5)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#4)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#4)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#3)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#3)]  
  
## Vedere anche  
 [Procedura: creare un controllo di Windows Form che visualizzi lo stato di avanzamento](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)