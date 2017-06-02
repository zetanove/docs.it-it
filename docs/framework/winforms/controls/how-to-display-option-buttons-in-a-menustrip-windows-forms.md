---
title: "Procedura: visualizzare pulsanti di opzione in un controllo MenuStrip (Windows Form) | Microsoft Docs"
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
  - "visualizzazione dei pulsanti di opzione, MenuStrip [Windows Form]"
  - "MenuStrip [Windows Form], visualizzazione dei pulsanti di opzione"
  - "pulsanti di opzione [Windows Form], visualizzazione in MenuStrip"
ms.assetid: 8b596af2-9ff8-4f7b-93d7-cba830e167f4
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: visualizzare pulsanti di opzione in un controllo MenuStrip (Windows Form)
I pulsanti di opzione sono simili alle caselle di controllo, tranne per il fatto che gli utenti possono selezionane solo uno alla volta.  Anche se per impostazione predefinita la classe <xref:System.Windows.Forms.ToolStripMenuItem> non fornisce il comportamento dei pulsanti di opzione, fornisce il comportamento delle caselle di controllo che è possibile personalizzare per implementare il comportamento dei pulsanti di opzione per le voci di menu in un controllo <xref:System.Windows.Forms.MenuStrip>.  
  
 Quando la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> di una voce di menu è `true`, gli utenti possono fare clic sull'elemento per visualizzare o nascondere un segno di spunta.  La proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> indica lo stato corrente dell'elemento.  Per implementare il comportamento di base dei pulsanti di opzione, è necessario assicurarsi che, quando un elemento viene selezionato, la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> dell'elemento selezionato in precedenza sia impostata su `false`.  
  
 Nelle procedure seguenti viene descritto come implementare questa e altre funzionalità in una classe che eredita la classe <xref:System.Windows.Forms.ToolStripMenuItem>.  La classe `ToolStripRadioButtonMenuItem` esegue l'override di membri quali <xref:System.Windows.Forms.ToolStripMenuItem.OnCheckedChanged%2A> e <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A> per fornire il comportamento di selezione e l'aspetto dei pulsanti di opzione.  Questa classe esegue inoltre l'override della proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> in modo che le opzioni di un sottomenu siano disabilitate a meno che non venga selezionato l'elemento padre.  
  
### Per implementare il comportamento di selezione dei pulsanti di opzione  
  
1.  Inizializzare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> su `true` per attivare la selezione di elementi.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#110)]
     [!code-vb[ToolStripRadioButtonMenuItem#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#110)]  
  
2.  Eseguire l'override del metodo <xref:System.Windows.Forms.ToolStripMenuItem.OnCheckedChanged%2A> per annullare la selezione dell'elemento selezionato in precedenza quando viene selezionato un nuovo elemento.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#120)]
     [!code-vb[ToolStripRadioButtonMenuItem#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#120)]  
  
3.  Eseguire l'override del metodo <xref:System.Windows.Forms.ToolStripMenuItem.OnClick%2A> per assicurarsi che un'azione di clic su un elemento già selezionato non annulli la selezione.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#130](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#130)]
     [!code-vb[ToolStripRadioButtonMenuItem#130](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#130)]  
  
### Per modificare l'aspetto degli elementi dei pulsanti di opzione  
  
1.  Eseguire l'override del metodo <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A> per sostituire il segno di spunta predefinito con un pulsante di opzione utilizzando la classe <xref:System.Windows.Forms.RadioButtonRenderer>.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#140)]
     [!code-vb[ToolStripRadioButtonMenuItem#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#140)]  
  
2.  Eseguire l'override dei metodi <xref:System.Windows.Forms.ToolStripMenuItem.OnMouseEnter%2A>, <xref:System.Windows.Forms.ToolStripMenuItem.OnMouseLeave%2A>, <xref:System.Windows.Forms.ToolStripMenuItem.OnMouseDown%2A> e <xref:System.Windows.Forms.ToolStripMenuItem.OnMouseUp%2A> per registrare lo stato del mouse e assicurarsi che il metodo <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A> disegni lo stato corretto del pulsante di opzione.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#150](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#150)]
     [!code-vb[ToolStripRadioButtonMenuItem#150](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#150)]  
  
### Per disabilitare le opzioni di un sottomenu quando l'elemento padre non è selezionato  
  
1.  Eseguire l'override della proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> in modo che l'elemento venga disabilitato se dispone di un elemento padre con la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> impostata su `true` e la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> impostata su `false`.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#160](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#160)]
     [!code-vb[ToolStripRadioButtonMenuItem#160](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#160)]  
  
2.  Eseguire l'override del metodo <xref:System.Windows.Forms.ToolStripMenuItem.OnOwnerChanged%2A> per sottoscrivere l'evento <xref:System.Windows.Forms.ToolStripMenuItem.CheckedChanged> dell'elemento padre.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#170](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#170)]
     [!code-vb[ToolStripRadioButtonMenuItem#170](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#170)]  
  
3.  Nel gestore dell'evento <xref:System.Windows.Forms.ToolStripMenuItem.CheckedChanged> dell'elemento padre invalidare l'elemento per aggiornare la visualizzazione con il nuovo stato attivato.  
  
     [!code-csharp[ToolStripRadioButtonMenuItem#180](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#180)]
     [!code-vb[ToolStripRadioButtonMenuItem#180](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#180)]  
  
## Esempio  
 Nell'esempio di codice seguente vengono fornite la classe `ToolStripRadioButtonMenuItem` completa, una classe <xref:System.Windows.Forms.Form> e una classe `Program` per illustrare il comportamento dei pulsanti di opzione.  
  
 [!code-csharp[ToolStripRadioButtonMenuItem#000](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/cs/ToolStripRadioButtonMenuItem.cs#000)]
 [!code-vb[ToolStripRadioButtonMenuItem#000](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripRadioButtonMenuItem/vb/ToolStripRadioButtonMenuItem.vb#000)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Riferimenti agli assembly System, System.Drawing e System.Windows.Forms.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.OnCheckedChanged%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.OnPaint%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.RadioButtonRenderer>   
 [Controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)   
 [Procedura: implementare un oggetto ToolStripRenderer personalizzato](../../../../docs/framework/winforms/controls/how-to-implement-a-custom-toolstriprenderer.md)