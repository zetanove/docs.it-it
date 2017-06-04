---
title: "Procedura: impostare l&#39;ordine di tabulazione in Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "TabStop"
  - "TabIndex"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "controlli [Windows Form], impostazione dell'ordine delle schede"
  - "ordine di tabulazione, controlli su Windows Form"
  - "controlli Windows Form, impostazione dell'ordine delle schede"
  - "Windows Form, impostazione dell'ordine delle schede"
ms.assetid: 71fa8e76-0472-414b-ad3c-0f90166e0ad7
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: impostare l&#39;ordine di tabulazione in Windows Form
L'ordine di tabulazione è l'ordine in cui un utente sposta lo stato attivo da un controllo a un altro premendo il tasto TAB.  Ogni form presenta un proprio ordine di tabulazione.  In base all'impostazione predefinita, l'ordine di tabulazione rispetta l'ordine in cui vengono creati i controlli.  La numerazione dell'ordine di tabulazione inizia da zero.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per impostare l'ordine di tabulazione di un controllo  
  
1.  Scegliere **Ordine di tabulazione** dal menu **Visualizza**.  
  
     In questo modo viene attivata la modalità di selezione dell'ordine di tabulazione nel form.  Viene visualizzato un numero, che rappresenta la proprietà <xref:System.Windows.Forms.Control.TabIndex%2A>, nell'angolo superiore sinistro di ciascun controllo.  
  
2.  Fare clic sui controlli in ordine sequenziale per stabilire l'ordine di tabulazione desiderato.  
  
    > [!NOTE]
    >  La posizione di un controllo all'interno dell'ordine di tabulazione può essere impostata su qualsiasi valore maggiore o uguale a 0.  In caso di duplicazione, viene valutato l'ordine Z dei due controlli e al controllo in primo piano viene assegnata la precedenza nell'ordine di tabulazione.  Si definisce ordine Z la disposizione visiva dei controlli su più livelli all'interno di un form, lungo l'asse z dello stesso form \(profondità\).  L'ordine Z stabilisce quali controlli sono in primo piano rispetto ad altri. Per ulteriori informazioni sull'ordine Z, vedere [Disposizione di oggetti su più livelli in Windows Form](../../../../docs/framework/winforms/controls/how-to-layer-objects-on-windows-forms.md).  
  
3.  Al termine scegliere nuovamente **Ordine di tabulazione** dal menu **Visualizza** per uscire dalla modalità ordine di tabulazione.  
  
    > [!NOTE]
    >  I controlli che non possono diventare attivi, i controlli disabilitati e quelli non visibili non dispongono di una proprietà <xref:System.Windows.Forms.Control.TabIndex%2A> e non vengono inclusi nell'ordine di tabulazione.  Tali controlli vengono ignorati quando l'utente preme il tasto TAB.  
  
 In alternativa, l'ordine di tabulazione può essere impostato nella finestra Proprietà utilizzando la proprietà <xref:System.Windows.Forms.Control.TabIndex%2A>.  La proprietà <xref:System.Windows.Forms.Control.TabIndex%2A> di un controllo determina la posizione del controllo nell'ordine di tabulazione.  Per impostazione predefinita, il primo controllo creato ha un valore <xref:System.Windows.Forms.Control.TabIndex%2A> pari a 0, il secondo ha un valore <xref:System.Windows.Forms.Control.TabIndex%2A> pari a 1 e così via.  
  
 Inoltre, sempre per impostazione predefinita, un controllo <xref:System.Windows.Forms.GroupBox> presenta un valore <xref:System.Windows.Forms.Control.TabIndex%2A> rappresentato da un numero intero.  Il singolo controllo <xref:System.Windows.Forms.GroupBox> non può diventare attivo in fase di esecuzione.  Ciascun controllo all'interno di un <xref:System.Windows.Forms.GroupBox> dispone quindi del proprio valore <xref:System.Windows.Forms.Control.TabIndex%2A> decimale, che inizia con ,0.   Man mano che il valore <xref:System.Windows.Forms.Control.TabIndex%2A> del controllo <xref:System.Windows.Forms.GroupBox> viene incrementato, naturalmente, i controlli all'interno verranno incrementati di conseguenza.  Se si modifica un valore <xref:System.Windows.Forms.Control.TabIndex%2A> da 5 a 6, il valore <xref:System.Windows.Forms.Control.TabIndex%2A> del primo controllo nel gruppo passerà automaticamente a 6,0 e così via.  
  
 Ogni controllo presente sul form può essere ignorato nell'ordine di tabulazione.  In genere, pressioni successive del tasto TAB in fase di esecuzione consentono la selezione successiva di ciascun controllo nell'ordine di tabulazione.  Disattivando la proprietà <xref:System.Windows.Forms.Control.TabStop%2A> è possibile ignorare un controllo nell'ordine di tabulazione del form.  
  
#### Per rimuovere un controllo dall'ordine di tabulazione  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.Control.TabStop%2A> del controllo su `false` nella finestra Proprietà.  
  
     Un controllo, la cui proprietà <xref:System.Windows.Forms.Control.TabStop%2A> sia stata impostata su `false`, mantiene comunque la propria posizione nell'ordine di tabulazione, anche se il controllo viene ignorato quando si passano in rassegna i controlli mediante la pressione del tasto TAB.  
  
    > [!NOTE]
    >  Un gruppo di pulsanti di opzione presenta un unico punto di tabulazione in fase di esecuzione.  Per il pulsante selezionato, ovvero quello avente proprietà <xref:System.Windows.Forms.RadioButton.Checked%2A> impostata su `true`, la proprietà <xref:System.Windows.Forms.Control.TabStop%2A> viene impostata automaticamente su `true`, mentre per gli altri pulsanti è impostata su `false`.  Per ulteriori informazioni sul raggruppamento di controlli <xref:System.Windows.Forms.RadioButton>, vedere [Raggruppamento di controlli RadioButton di Windows Form in modo che funzionino come un gruppo](../../../../docs/framework/winforms/controls/how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md).  
  
## Vedere anche  
 [Controlli per Windows Form](../../../../docs/framework/winforms/controls/index.md)   
 [Disposizione di controlli in Windows Form](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Controlli Windows Form per funzione](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)