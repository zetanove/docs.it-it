---
title: "How to: Determine Which Modifier Key Was Pressed | Microsoft Docs"
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
  - "keyboard input"
  - "shift keys"
  - "events [Windows Forms], mouse"
  - "Keys.ControlKey enumeration member"
  - "keys, control keys"
  - "user input, checking for keyboard"
  - "keys, determining last pressed"
  - "keys, shift keys"
  - "keys, modifier keys"
  - "control keys"
  - "keys, alt keys"
  - "alt keys"
  - "Keys.Shift enumeration member"
  - "events [Windows Forms], keyboard"
  - "keyboards, keyboard input"
  - "Keys.Alt enumeration member"
  - "modifier keys"
ms.assetid: 1e184048-0ae3-4067-a200-d4ba31dbc2cb
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Determine Which Modifier Key Was Pressed
Quando si crea un'applicazione che accetta la pressione dei tasti da parte dell'utente, può rivelarsi necessario monitorare i tasti di modifica, quali MAIUSC, ALT e CTRL.  Quando un tasto di modifica viene premuto in combinazione con altri tasti o con un clic del mouse, l'applicazione sarà in grado di rispondere in modo appropriato.  Se ad esempio si preme la lettera S, verrà semplicemente visualizzata una "S" sullo schermo, mentre se si preme CTRL\+S si potrebbe determinare il salvataggio del documento corrente.  Se si gestisce l'evento <xref:System.Windows.Forms.Control.KeyDown>, la proprietà <xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> della classe <xref:System.Windows.Forms.KeyEventArgs> ricevuta dal gestore eventi specifica i tasti di modifica premuti.  In alternativa la proprietà <xref:System.Windows.Forms.KeyEventArgs.KeyData%2A> della classe <xref:System.Windows.Forms.KeyEventArgs> specifica il carattere premuto nonché i tasti di modifica associati a un operatore OR bit per bit.  Se tuttavia si gestisce l'evento <xref:System.Windows.Forms.Control.KeyPress> o un evento mouse, il gestore eventi non riceverà tali informazioni.  In tal caso è necessario utilizzare la proprietà <xref:System.Windows.Forms.Control.ModifierKeys%2A> della classe <xref:System.Windows.Forms.Control>.  Sia nell'uno che nell'altro caso è necessario eseguire un'operazione AND bit per bit del valore di <xref:System.Windows.Forms.Keys> appropriato e del valore che si sottopone a verifica.  L'enumerazione <xref:System.Windows.Forms.Keys> offre variazioni di ogni tasto di modifica pertanto è importante eseguire l'operazione AND bit per bit con il valore corretto.  Il tasto MAIUSC, ad esempio, è rappresentato da <xref:System.Windows.Forms.Keys>, <xref:System.Windows.Forms.Keys>, <xref:System.Windows.Forms.Keys> e <xref:System.Windows.Forms.Keys>. Il valore corretto per verificare MAIUSC come tasto di modifica è <xref:System.Windows.Forms.Keys>.  Analogamente, per verificare CTRL e ALT come tasti di modifica è necessario utilizzare rispettivamente i valori <xref:System.Windows.Forms.Keys> e <xref:System.Windows.Forms.Keys>.  
  
> [!NOTE]
>  I programmatori Visual Basic possono inoltre accedere a informazioni sui tasti mediante la proprietà <xref:Microsoft.VisualBasic.Devices.Computer.Keyboard%2A>.  
  
### Per individuare il tasto di modifica premuto  
  
-   Per stabilire se è premuto un particolare tasto di modifica, utilizzare l'operatore `AND` bit per bit con la proprietà <xref:System.Windows.Forms.Control.ModifierKeys%2A> e un valore dell'enumerazione <xref:System.Windows.Forms.Keys>.  Nell'esempio di codice seguente viene illustrato come determinare se il tasto MAIUSC è premuto nell'ambito di un gestore di eventi <xref:System.Windows.Forms.Control.KeyPress>.  
  
     [!code-cpp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/cpp/form1.cpp#5)]
     [!code-csharp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/VB/form1.vb#5)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.Keys>   
 <xref:System.Windows.Forms.Control.ModifierKeys%2A>   
 [Keyboard Input in a Windows Forms Application](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)   
 [How to: Determine If CapsLock is On in Visual Basic](http://msdn.microsoft.com/it-it/91e60f5c-dd61-4222-ba5f-39af803afd8c)