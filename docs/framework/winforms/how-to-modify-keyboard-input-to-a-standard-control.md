---
title: "How to: Modify Keyboard Input to a Standard Control | Microsoft Docs"
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
  - "keyboard input, modifying"
  - "modifying keyboard input"
  - "Windows Forms, modifying keyboard input"
  - "keyboards, keyboard input"
ms.assetid: 626d3712-d866-4988-bcda-a2d5b36ec0ba
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# How to: Modify Keyboard Input to a Standard Control
Windows Forms permette di usare e modificare l'input da tastiera.  L'utilizzo di una chiave fa riferimento alla gestione di una chiave entro un metodo o un gestore eventi, in modo che altri metodi ed eventi successivi nella coda di messaggi non ricevano il valore della chiave.  Per modifica di una chiave si intente la modifica del valore di una chiave, in modo che i metodi e i gestori eventi successivi nella coda di messaggi ricevano un valore di chiave diverso.  Questo argomento illustra come completare queste attività.  
  
### Per usare una chiave  
  
-   In un gestore eventi <xref:System.Windows.Forms.Control.KeyPress> impostare la proprietà <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> della classe <xref:System.Windows.Forms.KeyPressEventArgs> su `true`.  
  
     \-oppure\-  
  
     In un gestore eventi <xref:System.Windows.Forms.Control.KeyDown> impostare la proprietà <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> della classe <xref:System.Windows.Forms.KeyEventArgs> su `true`.  
  
    > [!NOTE]
    >  L'impostazione della proprietà <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> nel gestore eventi <xref:System.Windows.Forms.Control.KeyDown> non impedisce la generazione degli eventi <xref:System.Windows.Forms.Control.KeyPress> e <xref:System.Windows.Forms.Control.KeyUp> per la sequenza di tasti attuale.  Usare la proprietà <xref:System.Windows.Forms.KeyEventArgs.SuppressKeyPress%2A> per questo scopo.  
  
     L'esempio seguente è tratto da un'istruzione `switch` che esamina la proprietà <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> dell'oggetto <xref:System.Windows.Forms.KeyPressEventArgs> ricevuto da un gestore eventi <xref:System.Windows.Forms.Control.KeyPress>.  Questo codice usa i tasti corrispondenti ai caratteri 'A' e 'a'.  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#6](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#6)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#6](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#6)]  
  
### Per modificare un tasto carattere standard  
  
-   In un gestore eventi <xref:System.Windows.Forms.Control.KeyPress> impostare la proprietà <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> della classe <xref:System.Windows.Forms.KeyPressEventArgs> sul valore del nuovo tasto carattere.  
  
     L'esempio seguente è tratto da un'istruzione `switch` che modifica 'B' in 'A' e 'b' in 'a'.  Si noti che la proprietà <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> del parametro <xref:System.Windows.Forms.KeyPressEventArgs> è impostata su `false`, in modo che il nuovo valore del tasto venga propagato ad altri metodi ed eventi nella coda dei messaggi.  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#7](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#7)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#7](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#7)]  
  
### Per modificare un tasto non corrispondente a un carattere  
  
-   Eseguire l'override di un metodo <xref:System.Windows.Forms.Control> che elabora messaggi di Windows, individuare il messaggio WM\_KEYDOWN o WM\_SYSKEYDOWN e impostare la proprietà <xref:System.Windows.Forms.Message.WParam%2A> del parametro <xref:System.Windows.Forms.Message> sul valore <xref:System.Windows.Forms.Keys> che rappresenta il nuovo tasto non corrispondente a un carattere.  
  
     L'esempio di codice seguente illustra come eseguire l'override del metodo <xref:System.Windows.Forms.Control.PreProcessMessage%2A> di un controllo per individuare i tasti da F1 a F9 e modificare la funzione del tasto F3 in quella del tasto F1.  Per altre informazioni sui metodi <xref:System.Windows.Forms.Control> di cui è possibile eseguire l'override per intercettare i messaggi della tastiera, vedere [User Input in a Windows Forms Application](../../../docs/framework/winforms/user-input-in-a-windows-forms-application.md) e [How Keyboard Input Works](../../../docs/framework/winforms/how-keyboard-input-works.md).  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#12](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#12)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#12](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#12)]  
  
## Esempio  
 L'esempio di codice seguente è l'applicazione completa degli esempi di codice delle sezioni precedenti.  L'applicazione usa un controllo personalizzato derivato dalla classe <xref:System.Windows.Forms.TextBox> per usare e modificare gli input da tastiera.  
  
 [!code-csharp[System.Windows.Forms.KeyBoardInput#0](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.KeyBoardInput#0](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#0)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System, System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  Vedere anche [Procedura: Compilare ed eseguire un esempio di codice Windows Form completo tramite Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vedere anche  
 [Keyboard Input in a Windows Forms Application](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)   
 [User Input in a Windows Forms Application](../../../docs/framework/winforms/user-input-in-a-windows-forms-application.md)   
 [How Keyboard Input Works](../../../docs/framework/winforms/how-keyboard-input-works.md)