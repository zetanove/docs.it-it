---
title: "How Mouse Input Works in Windows Forms | Microsoft Docs"
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
  - "Windows Forms, mouse input"
  - "mouse, input"
ms.assetid: 48fc5240-75a6-44bf-9fce-6aa21b49705a
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# How Mouse Input Works in Windows Forms
La ricezione e la gestione dell'input del mouse costituiscono un elemento importante di ogni applicazione Windows.  È possibile gestire eventi del mouse per eseguire un'azione nell'applicazione oppure utilizzare le informazioni sulla posizione del mouse per eseguire un'operazione di hit testing o altre azioni.  È inoltre possibile modificare la modalità con cui l'input del mouse viene gestito dai controlli dell'applicazione.  In questo argomento sono descritti dettagliatamente gli eventi del mouse e viene illustrato come ottenere e modificare le impostazioni di sistema per il mouse.  Per ulteriori informazioni sui dati forniti con gli eventi del mouse e l'ordine in cui gli eventi click del mouse sono generati, vedere [Mouse Events in Windows Forms](../../../docs/framework/winforms/mouse-events-in-windows-forms.md).  
  
## Posizione del mouse e operazione di hit testing  
 Quando l'utente sposta il mouse, il sistema operativo sposta il puntatore del mouse.  Il puntatore del mouse contiene un unico pixel, detto area sensibile, che viene registrato e riconosciuto come posizione del puntatore.  Quando l'utente sposta il mouse o preme un pulsante, la classe <xref:System.Windows.Forms.Control> contenente la proprietà <xref:System.Windows.Forms.Cursor.HotSpot%2A> genera l'evento del mouse appropriato.  Per ottenere la posizione corrente del mouse, è possibile utilizzare la proprietà <xref:System.Windows.Forms.MouseEventArgs.Location%2A> della classe <xref:System.Windows.Forms.MouseEventArgs> durante la gestione di un evento del mouse oppure la proprietà <xref:System.Windows.Forms.Cursor.Position%2A> della classe <xref:System.Windows.Forms.Cursor>.  Le informazioni sulla posizione del mouse possono quindi essere utilizzate per operazioni di hit testing e in seguito per l'esecuzione di un'azione basata sulla posizione del mouse.  La funzione di hit testing è incorporata in vari controlli in Windows Form, ad esempio i controlli <xref:System.Windows.Forms.ListView>, <xref:System.Windows.Forms.TreeView>, <xref:System.Windows.Forms.MonthCalendar> e <xref:System.Windows.Forms.DataGridView>.  Se utilizzata con l'evento del mouse appropriato, ad esempio con <xref:System.Windows.Forms.Control.MouseHover>, l'operazione di hit testing è molto utile per determinare il momento in cui nell'applicazione deve essere eseguita una determinata azione.  
  
## Eventi del mouse  
 Il modo principale per rispondere all'input del mouse consiste nel gestire gli eventi del mouse.  Nella tabella seguente sono indicati gli eventi del mouse e descritti i momenti in cui vengono generati.  
  
|Evento del mouse|Descrizione|  
|----------------------|-----------------|  
|<xref:System.Windows.Forms.Control.Click>|Si verifica quando il pulsante del mouse viene rilasciato, solitamente prima dell'evento <xref:System.Windows.Forms.Control.MouseUp>.  Il gestore di questo evento riceve un argomento di tipo <xref:System.EventArgs>.  Gestire l'evento quando è sufficiente determinare il momento in cui si verifica un clic.|  
|<xref:System.Windows.Forms.Control.MouseClick>|Si verifica quando l'utente fa clic sul controllo con il mouse.  Il gestore di questo evento riceve un argomento di tipo <xref:System.Windows.Forms.MouseEventArgs>.  Gestire l'evento quando è necessario reperire informazioni sul mouse nel momento in cui si verifica un clic.|  
|<xref:System.Windows.Forms.Control.DoubleClick>|Si verifica quando viene fatto doppio clic sul controllo.  Il gestore di questo evento riceve un argomento di tipo <xref:System.EventArgs>.  Gestire l'evento quando è sufficiente determinare il momento in cui si verifica un doppio clic.|  
|<xref:System.Windows.Forms.Control.MouseDoubleClick>|Si verifica quando l'utente fa doppio clic sul controllo con il mouse.  Il gestore di questo evento riceve un argomento di tipo <xref:System.Windows.Forms.MouseEventArgs>.  Gestire l'evento quando è necessario reperire informazioni sul mouse nel momento in cui si verifica un doppio clic.|  
|<xref:System.Windows.Forms.Control.MouseDown>|Si verifica quando il puntatore del mouse è sopra il controllo e l'utente preme un pulsante del mouse.  Il gestore di questo evento riceve un argomento di tipo <xref:System.Windows.Forms.MouseEventArgs>.|  
|<xref:System.Windows.Forms.Control.MouseEnter>|Si verifica quando il puntatore del mouse si sposta all'interno del bordo o dell'area client del controllo, a seconda del tipo di controllo.  Il gestore di questo evento riceve un argomento di tipo <xref:System.EventArgs>.|  
|<xref:System.Windows.Forms.Control.MouseHover>|Si verifica quando il puntatore del mouse si ferma sul controllo.  Il gestore di questo evento riceve un argomento di tipo <xref:System.EventArgs>.|  
|<xref:System.Windows.Forms.Control.MouseLeave>|Si verifica quando il puntatore del mouse si sposta all'esterno del bordo o dell'area client del controllo, a seconda del tipo di controllo.  Il gestore di questo evento riceve un argomento di tipo <xref:System.EventArgs>.|  
|<xref:System.Windows.Forms.Control.MouseMove>|Si verifica quando il puntatore del mouse si sposta mentre è su un controllo.  Il gestore di questo evento riceve un argomento di tipo <xref:System.Windows.Forms.MouseEventArgs>.|  
|<xref:System.Windows.Forms.Control.MouseUp>|Si verifica quando il puntatore del mouse è sopra il controllo e l'utente rilascia un pulsante del mouse.  Il gestore di questo evento riceve un argomento di tipo <xref:System.Windows.Forms.MouseEventArgs>.|  
|<xref:System.Windows.Forms.Control.MouseWheel>|Si verifica quando l'utente muove la rotellina del mouse mentre il controllo è attivo.  Il gestore di questo evento riceve un argomento di tipo <xref:System.Windows.Forms.MouseEventArgs>.  Per determinare l'entità dello scorrimento del mouse, utilizzare la proprietà <xref:System.Windows.Forms.MouseEventArgs.Delta%2A> di <xref:System.Windows.Forms.MouseEventArgs>.|  
  
## Modifica dell'input del mouse e rilevazione delle impostazioni di sistema  
 È possibile rilevare e modificare la modalità con cui un controllo gestisce l'input del mouse mediante la derivazione del controllo e l'utilizzo dei metodi <xref:System.Windows.Forms.Control.GetStyle%2A> e <xref:System.Windows.Forms.Control.SetStyle%2A>.  Il metodo <xref:System.Windows.Forms.Control.SetStyle%2A> utilizza una combinazione bit per bit dei valori di <xref:System.Windows.Forms.ControlStyles> per determinare se il controllo avrà un comportamento standard di un solo clic o di un doppio clic oppure se gestirà direttamente l'elaborazione del mouse.  La classe <xref:System.Windows.Forms.SystemInformation>, inoltre, comprende proprietà che descrivono le funzioni del mouse e specificano la modalità di interazione del mouse con il sistema operativo.  Tali proprietà sono riepilogate nella tabella che segue.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Windows.Forms.SystemInformation.DoubleClickSize%2A>|Ottiene le dimensioni, in pixel, dell'area in cui l'utente deve fare clic due volte affinché il sistema operativo consideri i due clic come un doppio clic.|  
|<xref:System.Windows.Forms.SystemInformation.DoubleClickTime%2A>|Ottiene il numero massimo di millisecondi consentiti tra il primo e il secondo clic affinché il sistema operativo consideri l'azione del mouse come un doppio clic.|  
|<xref:System.Windows.Forms.SystemInformation.MouseButtons%2A>|Ottiene il numero di pulsanti del mouse.|  
|<xref:System.Windows.Forms.SystemInformation.MouseButtonsSwapped%2A>|Ottiene un valore che indica se le funzioni dei pulsanti sinistro e destro sono state invertite.|  
|<xref:System.Windows.Forms.SystemInformation.MouseHoverSize%2A>|Ottiene le dimensioni, in pixel, del rettangolo entro il quale il puntatore del mouse deve soffermarsi per la durata necessaria prima che venga generato un messaggio visualizzato al passaggio del mouse.|  
|<xref:System.Windows.Forms.SystemInformation.MouseHoverTime%2A>|Ottiene il tempo, in millisecondi, per il quale il puntatore del mouse deve soffermarsi sul rettangolo prima che venga generato un messaggio visualizzato al passaggio del mouse.|  
|<xref:System.Windows.Forms.SystemInformation.MousePresent%2A>|Ottiene un valore indicante se è installato un mouse.|  
|<xref:System.Windows.Forms.SystemInformation.MouseSpeed%2A>|Ottiene un valore indicante la velocità corrente del mouse, da 1 a 20.|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelPresent%2A>|Ottiene un valore indicante se è installato un mouse dotato di rotellina.|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelScrollDelta%2A>|Ottiene il valore delta dell'incremento di una singola rotazione della rotellina del mouse.|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelScrollLines%2A>|Ottiene il numero di righe da far scorrere quando viene ruotata la rotellina del mouse.|  
  
## Vedere anche  
 [Mouse Input in a Windows Forms Application](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)   
 [Mouse Capture in Windows Forms](../../../docs/framework/winforms/mouse-capture-in-windows-forms.md)   
 [Mouse Pointers in Windows Forms](../../../docs/framework/winforms/mouse-pointers-in-windows-forms.md)