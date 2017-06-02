---
title: "Consigli sui tipi di controlli | Microsoft Docs"
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
  - "controlli [Windows Form], creazione"
  - "controlli personalizzati [Windows Form], tipi"
  - "ereditarietà, Windows Form (controlli personalizzati)"
  - "controlli utente [Windows Form], quando utilizzare"
ms.assetid: 5235fe9d-c36a-4c08-ae76-6cb90b50085e
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Consigli sui tipi di controlli
.NET Framework offre funzionalità per sviluppare e implementare nuovi controlli.  Oltre al tradizionale controllo utente, ora è possibile scrivere controlli personalizzati che eseguono il proprio disegno e possono anche estendere le funzionalità dei controlli esistenti tramite l'ereditarietà.  Decidere quale tipo di controllo creare può generare confusione.  Questa sezione evidenzia le differenze tra i vari tipi di controlli che offrono opzioni di ereditarietà e fornisce considerazioni sul tipo da scegliere per il progetto.  
  
> [!NOTE]
>  Per creare un controllo da usare nei Web Form, vedere [Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md).  
  
## Eredità da un controllo di Windows Form  
 È possibile derivare un controllo ereditato da un controllo di Windows Form esistente.  Questo approccio consente di mantenere tutte le funzionalità intrinseche di un controllo di Windows Form ed estenderle mediante l'aggiunta di proprietà personalizzate, metodi o altre funzionalità.  Ad esempio, è possibile creare un controllo derivato da <xref:System.Windows.Forms.TextBox> che accetta solo numeri e converte automaticamente l'input in un valore.  Un controllo di questo tipo potrebbe contenere un codice di convalida chiamato a ogni modifica del testo nella casella di testo e potrebbe avere una proprietà aggiuntiva, Valore.  In alcuni controlli è possibile aggiungere anche un aspetto personalizzato per l'interfaccia grafica del controllo eseguendo l'override del metodo <xref:System.Windows.Forms.Control.OnPaint%2A> della classe base.  
  
 Ereditare da un controllo di Windows Form se:  
  
-   Molte delle funzionalità necessarie sono identiche a quelle incluse in un controllo di Windows Form esistente.  
  
-   Non è necessaria un'interfaccia grafica personalizzata oppure si vuole progettare un nuovo front\-end grafico per un controllo esistente.  
  
## Eredità dalla classe UserControl  
 Un controllo utente è una raccolta di controlli di Windows Form incapsulata in un contenitore comune.  Il contenitore include tutte le funzionalità intrinseche associate a ciascun controllo di Windows Form e consente di esporre e associare in modo selettivo le relative proprietà.  Un esempio di controllo utente potrebbe essere un controllo compilato per la visualizzazione dei dati dell'indirizzo del cliente da un database.  Questo controllo include diverse caselle di testo per visualizzare tutti i campi e diversi pulsanti per spostarsi tra i record.  Le proprietà di data binding possono essere esposte in modo selettivo e l'intero controllo può essere incluso in un pacchetto e riusato nelle diverse applicazioni.  
  
 Ereditare dalla classe <xref:System.Windows.Forms.UserControl> per:  
  
-   Combinare le funzionalità di vari controlli di Windows Form in una singola unità riusabile.  
  
## Eredità dalla classe Control  
 Un altro metodo per creare un controllo consiste nel crearne uno praticamente dal nulla mediante eredità da <xref:System.Windows.Forms.Control>.  La classe <xref:System.Windows.Forms.Control> fornisce tutte le funzionalità di base richieste dai controlli \(ad esempio, gli eventi\), ma nessuna funzionalità specifica del controllo o interfacce grafiche.  La creazione di un controllo mediante eredità dalla classe <xref:System.Windows.Forms.Control> è molto più complesso in termini di elaborazione e di passaggi da eseguire rispetto a un controllo ereditato da un controllo utente o da un controllo di Windows Form esistente.  L'autore deve scrivere un codice per l'evento <xref:System.Windows.Forms.Control.OnPaint%2A> del controllo, nonché altri codici specifici per le funzionalità necessarie.  Tuttavia, questo metodo permette una maggiore flessibilità e la possibilità di personalizzare il controllo per soddisfare completamente le esigenze dell'utente.  Un esempio di controllo personalizzato è un controllo clock che duplica l'aspetto e il funzionamento di un orologio analogico.  Viene richiamato un disegno personalizzato che causa il movimento delle lancette dell'orologio in risposta ad eventi <xref:System.Windows.Forms.Timer.Tick> provenienti da un componente timer interno.  
  
 Ereditare dalla classe <xref:System.Windows.Forms.Control> per:  
  
-   Fornire una rappresentazione grafica personalizzata del controllo.  
  
-   È necessario implementare una funzionalità personalizzata non disponibile tramite i controlli standard.  
  
-   [Procedura: Visualizzare un controllo nella finestra di dialogo Scegli elementi della Casella degli strumenti](http://msdn.microsoft.com/library/9yxtkx75\(v=vs.110\))  
  
-   [Procedura dettagliata: Serializzazione di raccolte di tipi standard tramite DesignerSerializationVisibilityAttribute](http://msdn.microsoft.com/library/ms171731\(v=vs.110\))  
  
-   [Procedura dettagliata: Eredità da un controllo di Windows Form con Visual C\#](http://msdn.microsoft.com/library/5h0k2e6x\(v=vs.110\))  
  
-   [Procedura: Specificare una bitmap nella casella degli strumenti per un controllo](http://msdn.microsoft.com/library/4wk1wc0a\(v=vs.110\))  
  
-   [Procedura: Ereditare da controlli di Windows Form esistenti](http://msdn.microsoft.com/library/7h62478z\(v=vs.110\))  
  
-   [Procedura dettagliata: Debug di controlli di Windows Form personalizzati in fase di progettazione](http://msdn.microsoft.com/library/5ytx0z24\(v=vs.110\))  
  
-   [Procedura: Ereditare dalla classe Control](http://msdn.microsoft.com/library/skcysbt2\(v=vs.110\))  
  
-   [Procedura: Eseguire il test del comportamento in fase di esecuzione di UserControl](http://msdn.microsoft.com/library/ms171738\(v=vs.110\))  
  
-   [Procedura: Allineare un controllo ai bordi dei form in fase di progettazione](http://msdn.microsoft.com/library/1fxyb15b\(v=vs.110\))  
  
-   [Procedura: Ereditare dalla classe UserControl](http://msdn.microsoft.com/library/00ctb4z0\(v=vs.110\))  
  
-   [Procedura: Creare controlli per Windows Form](http://msdn.microsoft.com/library/bs3yhkh7\(v=vs.110\))  
  
-   [Procedura: Modificare controlli compositi](http://msdn.microsoft.com/library/3sf86w5h\(v=vs.110\))  
  
-   [Procedura dettagliata: Modifica di un controllo composito con Visual Basic](http://msdn.microsoft.com/library/c316f119\(v=vs.110\))  
  
-   [Procedura dettagliata: Modifica di un controllo composito con Visual C\#](http://msdn.microsoft.com/library/a6h7e207\(v=vs.110\))  
  
-   [Procedura dettagliata: Eredità da un controllo di Windows Form con Visual Basic](http://msdn.microsoft.com/library/w2a8y03d\(v=vs.110\))  
  
-   [Procedura: Creare un controllo Windows Form che usa le funzionalità di progettazione](http://msdn.microsoft.com/library/307hck25\(v=vs.110\))  
  
-   [Procedura: Creare un controllo Windows Form che usa le funzionalità di progettazione](http://msdn.microsoft.com/library/307hck25\(v=vs.120\))  
  
## Vedere anche  
 [Procedura: sviluppare un controllo di Windows Form semplice](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)   
 [Tipi di controlli personalizzati](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)