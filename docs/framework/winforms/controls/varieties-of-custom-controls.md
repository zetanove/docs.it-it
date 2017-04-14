---
title: "Tipi di controlli personalizzati | Microsoft Docs"
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
  - "controlli composti"
  - "controlli [Windows Form], composti"
  - "controlli [Windows Form], estese"
  - "controlli [Windows Form], tipi"
  - "controlli [Windows Form], controlli utente"
  - "controlli personalizzati [Windows Form]"
  - "controlli estesi"
  - "controlli utente [Windows Form]"
ms.assetid: 3cea09e5-4344-4ccb-9858-b66ccac210ff
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Tipi di controlli personalizzati
Con .NET Framework è possibile sviluppare e implementare nuovi controlli.  È possibile estendere la funzionalità dei controlli utente più comuni nonché dei controlli esistenti mediante ereditarietà.  È inoltre possibile scrivere controlli personalizzati che effettuano il proprio disegno.  
  
 Decidere quale tipo di controllo creare può generare una certa confusione.  In questo argomento vengono evidenziate le differenze tra i vari tipi di controllo da cui è possibile ereditare e fornite informazioni su come scegliere un tipo particolare di controllo per un progetto specifico.  
  
> [!NOTE]
>  Per ulteriori informazioni sulla modifica di un controllo da utilizzare in Web Form, vedere [Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md).  
  
## Classe base dei controlli  
 <xref:System.Windows.Forms.Control> è la classe base per i controlli di Windows Form  e fornisce l'infrastruttura necessaria per la visualizzazione nelle applicazioni Windows Form.  
  
 La classe <xref:System.Windows.Forms.Control> effettua le seguenti attività per fornire la visualizzazione nelle applicazioni Windows Form:  
  
-   Espone un handle di finestra.  
  
-   Gestisce il routing dei messaggi.  
  
-   Fornisce eventi di mouse e tastiera e molti altri eventi dell'interfaccia.  
  
-   Fornisce funzioni avanzate di layout.  
  
-   Contiene numerose proprietà specifiche per la visualizzazione, quali <xref:System.Windows.Forms.Control.ForeColor%2A>, <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.Height%2A> e<xref:System.Windows.Forms.Control.Width%2A>.  
  
-   Fornisce il supporto per sicurezza e threading necessario affinché un controllo di Windows Form funzioni come un controllo Microsoft® ActiveX®.  
  
 Dal momento che una parte così consistente dell'infrastruttura è fornita dalla classe base, è relativamente semplice sviluppare controlli Windows Form personalizzati.  
  
## Tipi di controllo  
 Windows Form supporta tre tipi di controllo definiti dall'utente: *composito*, *esteso* e *personalizzato*.  Nelle sezioni seguenti viene descritto ciascun tipo di controllo e vengono forniti suggerimenti per la scelta del tipo più adeguato a un progetto specifico.  
  
### Controlli compositi  
 Un controllo composito è una raccolta di controlli di Windows Form incapsulati in un contenitore comune.  Questo tipo di controllo viene talvolta definito *controllo utente*,  mentre i controlli contenuti vengono definiti *controlli costitutivi*.  
  
 Il controllo composito contiene tutta la funzionalità inerente associata a ciascuno dei controlli di Windows Form costitutivi e consente di esporre e associare le relative proprietà in modo selettivo.  Questo tipo di controllo offre inoltre una grande varietà di funzioni predefinite per la gestione della tastiera senza richiedere ulteriore intervento da parte dello sviluppatore.  
  
 Ad esempio, è possibile compilare un controllo composito per visualizzare i dati di indirizzo di un cliente contenuti in un database.  Il controllo può includere un controllo <xref:System.Windows.Forms.DataGridView> per la visualizzazione dei campi del database, un controllo <xref:System.Windows.Forms.BindingSource> per gestire l'associazione a un'origine dati e un controllo <xref:System.Windows.Forms.BindingNavigator> per lo spostamento tra i record.  È possibile esporre in modo selettivo le proprietà di associazione dei dati, creare un package e riutilizzare l'intero controllo in un'altra applicazione.  Per un esempio di questo tipo di controllo composito, vedere [Procedura: applicare attributi nei controlli Windows Form](../../../../docs/framework/winforms/controls/how-to-apply-attributes-in-windows-forms-controls.md).  
  
 Per modificare un controllo composito è necessario derivarlo dalla classe <xref:System.Windows.Forms.UserControl>.  La classe base <xref:System.Windows.Forms.UserControl> fornisce il routing da tastiera per i controlli figlio e consente il funzionamento di tali controlli come gruppo.  Per ulteriori informazioni, vedere [Sviluppo di un controllo Windows Form composto](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md).  
  
 **Consigli**  
  
 L'eredità dalla classe <xref:System.Windows.Forms.UserControl> risulta utile quando:  
  
-   Si desidera combinare la funzionalità di vari controlli Windows Form in una singola unità riutilizzabile.  
  
### Controlli estesi  
 È possibile derivare un controllo ereditato da qualsiasi controllo Windows Form esistente.  Questo meccanismo consente di mantenere tutta la funzionalità inerente a un controllo di Windows Form e di estenderla mediante l'aggiunta di proprietà, metodi o altre funzionalità personalizzate.  Mediante questa opzione è possibile eseguire l'override della logica di disegno del controllo di base ed estendere la relativa interfaccia utente modificandone l'aspetto.  
  
 È ad esempio possibile creare un controllo derivato dal controllo <xref:System.Windows.Forms.Button> che tenga traccia del numero di selezioni effettuate dall'utente.  
  
 Alcuni controlli consentono di aggiungere anche un aspetto personalizzato all'interfaccia utente grafica del controllo mediante l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base.  Nel caso di un pulsante esteso che tenga traccia delle selezioni effettuate, è possibile eseguire l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> per chiamare l'implementazione base di <xref:System.Windows.Forms.Control.OnPaint%2A> e quindi visualizzare il numero di clic in un angolo dell'area client del controllo <xref:System.Windows.Forms.Button>.  
  
 **Consigli**  
  
 L'eredità da un controllo Windows Form risulta utile quando:  
  
-   La maggior parte delle funzionalità necessarie sono identiche a un controllo Windows Form esistente.  
  
-   Non è necessario disporre di un'interfaccia utente grafica personalizzata o si desidera progettare una nuova interfaccia utente grafica per un controllo esistente.  
  
### Controlli personalizzati  
 Un altro metodo di creazione di un controllo consiste nel crearlo praticamente dal nulla ereditando dalla classe <xref:System.Windows.Forms.Control> che fornisce tutte le funzionalità di base richieste dai controlli, ad esempio gli eventi di gestione del mouse e della tastiera, ma non le funzionalità specifiche dei controlli o l'interfaccia grafica.  
  
 La creazione di un controllo mediante eredità dalla classe <xref:System.Windows.Forms.Control> richiede un lavoro più complesso rispetto all'eredità da <xref:System.Windows.Forms.UserControl> o da un controllo di Windows Form esistente.  Poiché l'implementazione è lasciata principalmente allo sviluppatore, il controllo offre una maggiore flessibilità rispetto a un controllo composito o esteso e può essere personalizzato in modo da soddisfare esigenze specifiche.  
  
 Per implementare un controllo personalizzato, è necessario scrivere il codice per l'evento <xref:System.Windows.Forms.Control.OnPaint%2A> del controllo nonché l'eventuale codice specifico richiesto da ogni funzionalità.  È inoltre possibile eseguire l'override del metodo <xref:System.Windows.Forms.Control.WndProc%2A> e gestire direttamente i messaggi Windows.  Questa è la tecnica più efficace per creare un controllo, ma per utilizzarla in modo adeguato è necessario avere familiarità con l'API Microsoft Win32®.  
  
 Un esempio di controllo personalizzato è dato da un controllo che duplica l'aspetto e il funzionamento di un orologio analogico.  Il richiamo del disegno personalizzato farà muovere le lancette dell'orologio in risposta agli eventi <xref:System.Windows.Forms.Timer.Tick> di un componente <xref:System.Windows.Forms.Timer> interno.  Per ulteriori informazioni, vedere [Procedura: sviluppare un controllo di Windows Form semplice](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md).  
  
 **Consigli**  
  
 L'eredità dalla classe <xref:System.Windows.Forms.Control> risulta utile quando:  
  
-   Si desidera fornire una rappresentazione grafica personalizzata del controllo.  
  
-   È necessario implementare funzionalità personalizzate che non sono disponibili nei controlli standard.  
  
### Controlli ActiveX  
 Sebbene l'infrastruttura Windows Form sia stata ottimizzata per contenere controlli di Windows Form, è comunque possibile utilizzare controlli ActiveX.  Questa attività è supportata in Visual Studio.  Per ulteriori informazioni, vedere la classe [Procedura: aggiungere i controlli ActiveX a Windows Form](../../../../docs/framework/winforms/controls/how-to-add-activex-controls-to-windows-forms.md).  
  
### Controlli privi di finestra  
 Le tecnologie Microsoft Visual Basic® 6.0 e ActiveX supportano i controlli *privi di finestra*.  I controlli privi di finestra non sono invece supportati in Windows Form.  
  
## Progettazione personalizzata  
 Se è necessario implementare una fase di progettazione personalizzata, è possibile modificare la finestra di progettazione.  Per i controlli compositi, derivare la classe della finestra di progettazione personalizzata dalla classe <xref:System.Windows.Forms.Design.ParentControlDesigner> o <xref:System.Windows.Forms.Design.DocumentDesigner>.  Per i controlli estesi e personalizzati, derivare la classe della finestra di progettazione personalizzata dalla classe <xref:System.Windows.Forms.Design.ControlDesigner>.  
  
 Utilizzare <xref:System.ComponentModel.DesignerAttribute> per associare il controllo alla finestra di progettazione.  Per ulteriori informazioni, vedere [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md) e [How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md).  
  
## Vedere anche  
 [Sviluppo di controlli Windows Form personalizzati con .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [Procedura: sviluppare un controllo di Windows Form semplice](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)   
 [Sviluppo di un controllo Windows Form composto](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md)   
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md)