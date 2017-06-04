---
title: "Controlli costitutivi | Microsoft Docs"
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
  - "controlli costitutivi"
  - "controlli personalizzati [Windows Form], controlli costitutivi"
  - "controlli utente [Windows Form], controlli costitutivi"
  - "UserControl (classe)"
ms.assetid: 5565e720-198b-4bbd-a2bd-c447ba641798
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Controlli costitutivi
I controlli che costituiscono un controllo utente, o *controlli costitutivi*, sono relativamente poco flessibili per quanto riguarda il rendering grafico personalizzato.  Tutti i controlli per Windows Form gestiscono il proprio rendering mediante il metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  Poiché questo metodo è protetto, non è accessibile allo sviluppatore, quindi non è possibile impedirne l'esecuzione quando il controllo viene disegnato.  Ciò non significa, tuttavia, che non sia possibile aggiungere codice per definire l'aspetto dei controlli costitutivi.  Un ulteriore rendering può essere eseguito aggiungendo un gestore eventi.  Ad esempio, si supponga di creare un controllo <xref:System.Windows.Forms.UserControl> con un pulsante denominato `MyButton`.  Se si desidera disporre di un ulteriore rendering oltre a quello fornito dalla [classe Button](frlrfSystemWebUIWebControlsButtonClassTopic), è necessario aggiungere al controllo utente codice simile a quello riportato di seguito:  
  
```vb  
Public Sub MyPaint(ByVal sender as Object, e as PaintEventArgs) Handles _  
   MyButton.Paint  
   'Additional rendering code goes here  
End Sub  
  
```  
  
```csharp  
// Add the event handler to the button's Paint event.  
MyButton.Paint +=   
   new System.Windows.Forms.PaintEventHandler (this.MyPaint);  
// Create the custom painting method.  
protected void MyPaint (object sender,   
System.Windows.Forms.PaintEventArgs e)  
{  
   // Additional rendering code goes here.  
}  
```  
  
> [!NOTE]
>  Alcuni controlli per Windows Form, come <xref:System.Windows.Forms.TextBox>, sono disegnati direttamente da Windows.  In tali casi, l'esempio precedente non verrà mai chiamato dato che non viene mai chiamato il metodo <xref:System.Windows.Forms.Control.OnPaint%2A>.  
  
 Il metodo creato viene eseguito a ogni esecuzione dell'evento `MyButton.Paint`, aggiungendo in tal modo un'ulteriore rappresentazione grafica al controllo.  Tenere presente che ciò non impedisce l'esecuzione di `MyButton.OnPaint`, pertanto il disegno, di solito ottenuto in seguito alla selezione di un pulsante, continua a essere eseguito insieme al disegno personalizzato.  Per informazioni dettagliate sulla tecnologia GDI\+ e sul rendering personalizzato, vedere [Creazione di immagini di tipo grafico con GDI\+](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md).  Se si desidera ottenere una rappresentazione univoca del controllo, il metodo ottimale consiste nel creare un controllo ereditato per il quale scrivere un codice di rendering personalizzato.  Per informazioni dettagliate, vedere [Controlli creati dall'utente](../../../../docs/framework/winforms/controls/user-drawn-controls.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.UserControl>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [Controlli creati dall'utente](../../../../docs/framework/winforms/controls/user-drawn-controls.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)