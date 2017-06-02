---
title: "Cenni preliminari sui controlli HScrollBar e VScrollBar (Windows Form) | Microsoft Docs"
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
  - "HScrollBar"
  - "VScrollBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "HScrollBar (controllo) [Windows Form], informazioni"
  - "barre di scorrimento, informazioni"
  - "ScrollBar (controllo) [Windows Form]"
  - "ScrollBar (controllo) [Windows Form], informazioni sul controllo ScrollBar"
  - "VScrollBar (controllo) [Windows Form], informazioni sul controllo VScrollBar"
ms.assetid: 8b307679-1cae-41d8-99aa-3d1efd207cd6
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Cenni preliminari sui controlli HScrollBar e VScrollBar (Windows Form)
I controlli <xref:System.Windows.Forms.ScrollBar> Windows Form vengono utilizzati per semplificare la navigazione di lunghi elenchi di elementi o di grandi quantità di dati mediante lo scorrimento orizzontale o verticale all'interno di un'applicazione o di un controllo.  Le barre di scorrimento rappresentano un elemento comune dell'interfaccia Windows, quindi il controllo <xref:System.Windows.Forms.ScrollBar> viene utilizzato spesso con controlli che non derivano dalla classe <xref:System.Windows.Forms.ScrollableControl>.  Analogamente, molti sviluppatori scelgono di incorporare il controllo <xref:System.Windows.Forms.ScrollBar> durante la creazione di controlli utente personalizzati.  
  
 I controlli <xref:System.Windows.Forms.HScrollBar> \(orizzontale\) e <xref:System.Windows.Forms.VScrollBar> \(verticale\) funzionano in modo indipendente da altri controlli e dispongono di propri set di eventi, proprietà e metodi.   I controlli <xref:System.Windows.Forms.ScrollBar> non corrispondono alle barre di scorrimento incorporate, collegate a caselle di testo, caselle di riepilogo e caselle combinate, oppure ai form MDI. Il controllo <xref:System.Windows.Forms.TextBox>, ad esempio, dispone di una proprietà <xref:System.Windows.Forms.TextBox.ScrollBars%2A>per mostrare o nascondere le barre di scorrimento collegate al controllo.  
  
 I controlli <xref:System.Windows.Forms.ScrollBar> utilizzano l'evento <xref:System.Windows.Forms.ScrollBar.Scroll> per monitorare il movimento della casella di scorrimento, talvolta denominata semplicemente casella, lungo la barra di scorrimento.  L'evento <xref:System.Windows.Forms.ScrollBar.Scroll> consente di accedere al valore della barra di scorrimento durante il trascinamento.  
  
## Proprietà Value  
 La proprietà <xref:System.Windows.Forms.ScrollBar.Value%2A>, che per impostazione predefinita ha un valore pari a 0, è un valore `integer` che corrisponde alla posizione della casella di scorrimento nella barra di scorrimento.  Quando la posizione della casella di scorrimento è al valore minimo, la casella si sposta verso la posizione più a sinistra, per le barre di scorrimento orizzontale, oppure verso la posizione più in alto, per le barre di scorrimento verticale.  Quando la posizione della casella di scorrimento è al valore massimo, la casella si sposta verso la posizione più a destra o in basso.  Analogamente, impostando un valore intermedio tra la posizione inferiore e superiore, il bordo iniziale della casella di scorrimento viene posizionato al centro della barra di scorrimento.  
  
 Per modificare il valore della barra di scorrimento, oltre a utilizzare il mouse, è possibile trascinare la casella di scorrimento su qualsiasi punto lungo la barra.  Il valore ottenuto dipende dalla posizione della casella di scorrimento, ma rientra sempre nell'intervallo compreso tra la proprietà <xref:System.Windows.Forms.ScrollBar.Minimum%2A> e la proprietà <xref:System.Windows.Forms.ScrollBar.Maximum%2A> impostate dall'utente.  
  
## Proprietà LargeChange e SmallChange  
 Quando l'utente preme il tasto PGSU o PGGIÙ oppure fa clic sull'indicatore di avanzamento della barra di scorrimento su uno dei due lati della casella di scorrimento, la proprietà <xref:System.Windows.Forms.ScrollBar.Value%2A> viene modificata in base al valore impostato nella proprietà <xref:System.Windows.Forms.ScrollBar.LargeChange%2A>.  
  
 Quando l'utente preme uno dei tasti di direzione oppure fa clic su uno dei pulsanti della barra di scorrimento, la proprietà <xref:System.Windows.Forms.ScrollBar.Value%2A> viene modificata in base al valore impostato nella proprietà <xref:System.Windows.Forms.ScrollBar.SmallChange%2A>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.HScrollBar>   
 <xref:System.Windows.Forms.VScrollBar>   
 [Additions to Windows Forms for the .NET Framework 2.0](http://msdn.microsoft.com/it-it/c61a923d-3d6a-4c8c-820c-e94c83f3f9a8)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)