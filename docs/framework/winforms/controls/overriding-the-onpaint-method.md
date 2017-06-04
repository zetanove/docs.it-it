---
title: "Override del metodo OnPaint | Microsoft Docs"
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
  - "OnPaint (metodo), override in controlli Windows Form personalizzati"
  - "Paint (evento), gestione in controlli Windows Form personalizzati"
ms.assetid: e9ca2723-0107-4540-bb21-4f5ffb4a9906
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Override del metodo OnPaint
I passaggi di base per eseguire l'override di qualsiasi evento definito in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] sono identici e vengono esposti di seguito.  
  
#### Per eseguire l'override di un evento ereditato  
  
1.  Eseguire l'override del metodo `On`*NomeEvento* protetto.  
  
2.  Chiamare il metodo `On`*NomeEvento* della classe di base dal metodo `On`*NomeEvento* di cui è stato eseguito l'override, in modo che l'evento venga ricevuto dai delegati registrati.  
  
 L'evento <xref:System.Windows.Forms.Control.Paint> è illustrato nei dettagli in questa sede perché è necessario che tutti i controlli di Windows Form eseguano l'override dell'evento <xref:System.Windows.Forms.Control.Paint> ereditato dalla classe <xref:System.Windows.Forms.Control>.  La classe base <xref:System.Windows.Forms.Control> non contiene le informazioni necessarie per il disegno dei controlli derivati e il relativo metodo <xref:System.Windows.Forms.Control.OnPaint%2A> non fornisce alcuna logica di disegno.  Il metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe <xref:System.Windows.Forms.Control> non fa che inviare l'evento <xref:System.Windows.Forms.Control.Paint> ai riceventi di eventi registrati.  
  
 Se si è esaminato l'esempio esposto in [Procedura: sviluppare un controllo di Windows Form semplice](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md), si è avuto modo di vedere un esempio di override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  Il codice che segue è tratto da tale esempio.  
  
```vb  
Public Class FirstControl  
   Inherits Control  
  
   Public Sub New()  
   End Sub  
  
   Protected Overrides Sub OnPaint(e As PaintEventArgs)  
      ' Call the OnPaint method of the base class.  
      MyBase.OnPaint(e)  
      ' Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, New SolidBrush(ForeColor), RectangleF.op_Implicit(ClientRectangle))  
   End Sub  
End Class   
```  
  
```csharp  
public class FirstControl : Control{  
   public FirstControl() {}  
   protected override void OnPaint(PaintEventArgs e) {  
      // Call the OnPaint method of the base class.  
      base.OnPaint(e);  
      // Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, new SolidBrush(ForeColor), ClientRectangle);  
   }   
}   
```  
  
 La classe <xref:System.Windows.Forms.PaintEventArgs> contiene i dati dell'evento <xref:System.Windows.Forms.Control.Paint>.  Presenta due proprietà, come illustrato nel seguente codice.  
  
```vb  
Public Class PaintEventArgs  
   Inherits EventArgs  
   ...  
   Public ReadOnly Property ClipRectangle() As System.Drawing.Rectangle  
      ...  
   End Property  
  
   Public ReadOnly Property Graphics() As System.Drawing.Graphics  
      ...  
   End Property   
   ...  
End Class  
```  
  
```csharp  
public class PaintEventArgs : EventArgs {  
...  
    public System.Drawing.Rectangle ClipRectangle {}  
    public System.Drawing.Graphics Graphics {}  
...  
}  
```  
  
 La proprietà <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> è il rettangolo da disegnare, mentre la proprietà <xref:System.Windows.Forms.PaintEventArgs.Graphics%2A> fa riferimento a un oggetto <xref:System.Drawing.Graphics>.  Le classi dello spazio dei nomi <xref:System.Drawing?displayProperty=fullName> sono classi gestite che consentono l'accesso alle funzionalità di [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], la nuova libreria grafica di Windows.  L'oggetto <xref:System.Drawing.Graphics> presenta metodi per il disegno di punti, linee, archi, ellissi e numerose altre forme.  
  
 Un controllo richiama il proprio metodo <xref:System.Windows.Forms.Control.OnPaint%2A> ogni volta che è necessario modificare l'aspetto del controllo stesso.  Questo metodo genera a sua volta l'evento <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Eventi](../../../../docs/standard/events/index.md)   
 [Rendering di un controllo Windows Form](../../../../docs/framework/winforms/controls/rendering-a-windows-forms-control.md)   
 [Definizione di un evento](../../../../docs/framework/winforms/controls/defining-an-event-in-windows-forms-controls.md)