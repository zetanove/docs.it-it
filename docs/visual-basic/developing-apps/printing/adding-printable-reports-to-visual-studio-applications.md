---
title: "Adding Printable Reports to Visual Studio Applications | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "printing [Visual Studio], reports"
  - "reports, printing in Visual Studio"
ms.assetid: 93928405-ef41-495e-bce2-9d43d5a7080a
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Adding Printable Reports to Visual Studio Applications
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In Visual Studio vengono supportate diverse soluzioni di report per consentire di aggiungere funzionalità avanzate per il report di dati alle applicazioni Visual Basic.  È possibile creare e aggiungere report tramite controlli ReportViewer, Crystal Reports o SQL Server Reporting Services.  
  
> [!NOTE]
>  SQL Server Reporting Services fa parte di SQL Server 2005 anziché di Visual Studio.  Reporting Services è presente unicamente nei sistemi in cui è stato installato SQL Server 2005.  
  
## Cenni preliminari sulle tecnologie di generazione report Microsoft in applicazioni Visual Basic  
 Per utilizzare una tecnologia di generazione report Microsoft in un'applicazione, scegliere uno degli approcci seguenti:  
  
-   Aggiungere una o più istanze di un controllo ReportViewer a un'applicazione Windows Visual Basic.  
  
-   Integrare a livello di codice SQL Server Reporting Services tramite l'effettuazione di chiamate al servizio Web Report Server.  
  
-   Utilizzare il controllo ReportViewer e Microsoft SQL Server 2005 Reporting Services insieme, impiegando il controllo come visualizzatore di report e un server di report come elaboratore di report.  È importante precisare che per potere utilizzare insieme un server di report e il controllo ReportViewer è necessario disporre della versione SQL Server 2005 di Reporting Services.  
  
## Utilizzo dei controlli ReportViewer  
 Il modo più semplice di integrare la funzionalità di report in un'applicazione Windows Visual Basic è aggiungere il controllo ReportViewer a un form nell'applicazione.  Il controllo aggiunge direttamente all'applicazione funzionalità di elaborazione di report e fornisce una progettazione report integrata, in modo da consentire la compilazione di report utilizzando dati da qualsiasi oggetto dati ADO.NET.  Un'API completa fornisce accesso a livello di codice al controllo e ai report, per consentire la configurazione della funzionalità in fase di esecuzione.  
  
 ReportViewer fornisce funzionalità integrate di elaborazione e visualizzazione dei report in un unico controllo dati, liberamente distribuibile.  Scegliere i controlli ReportViewer se sono necessarie le seguenti funzionalità di report:  
  
-   Elaborazione di report nell'applicazione client.  Verrà visualizzato un report elaborato in un'area di visualizzazione fornita dal controllo.  
  
-   Associazione dati a tabelle dati ADO.NET.  È possibile creare report che utilizzano istanze <xref:System.Data.DataTable> fornite al controllo.  È inoltre possibile eseguire l'associazione diretta agli oggetti business.  
  
-   Controlli ridistribuibili che possono essere inclusi nell'applicazione.  
  
-   Funzionalità di runtime quali navigazione da una pagina all'altra, stampa, ricerca e formati di esportazione.  Una barra degli strumenti di ReportViewer fornisce supporto per tali operazioni.  
  
 Per utilizzare il controllo ReportViewer è possibile trascinarlo dalla sezione **Dati** della Casella degli strumenti di Visual Studio in un form dell'applicazione Windows Visual Basic.  
  
### Creazione di report in Visual Studio per controlli ReportViewer  
 Per compilare un report da eseguire in ReportViewer, aggiungere un modello **Report** al progetto.  In Visual Studio viene creato un file di definizione del report per il client \(con estensione rdlc\), viene aggiunto il file al progetto e viene aperta una progettazione report integrata nell'area di lavoro di Visual Studio.  
  
 La Progettazione report di Visual Studio si integra con la finestra **Origini dati**.  Quando si trascina un campo dalla finestra **Origini dati** in un report, la Progettazione report copia i metadati sull'origine dati nel file di definizione del report.  I metadati sono utilizzati dal controllo ReportViewer per generare automaticamente codice con associazione a dati.  
  
 In Progettazione report di Visual Studio non è inclusa la funzionalità di anteprima.  Per visualizzare in anteprima il report, eseguire l'applicazione e visualizzare in anteprima il report incorporato.  
  
||  
|-|  
|Per aggiungere all'applicazione funzionalità di report di base|  
|1.  Trascinare un controllo ReportViewer dalla scheda **Dati** della **Casella degli strumenti** nel form.<br />2.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  Nella finestra di dialogo **Aggiungi nuovo elemento** fare clic sull'icona **Report**, quindi scegliere **Aggiungi**.<br />     Verrà aperta la Progettazione report nell'ambiente di sviluppo e verrà aggiunto un file di report \(rdlc\) al progetto.<br />3.  Trascinare gli elementi del report dalla **Casella degli strumenti** al layout del report e disporli nel modo desiderato.<br />4.  Trascinare i campi dalla finestra **Origini dati** sugli elementi del report nel layout del report.|  
  
## Utilizzo di Reporting Services in applicazioni Visual Basic  
 Reporting Services è una tecnologia per la generazione di report basata su server, inclusa in SQL Server.  Reporting Services comprende funzionalità aggiuntive che non si trovano nei controlli ReportViewer.  Scegliere Reporting Services se sono necessarie le funzionalità seguenti:  
  
-   Distribuzione scalabile ed elaborazione di report sul lato server che forniscano prestazioni migliorate per report complessi o di lunga esecuzione e per attività di report con volumi elevati.  
  
-   Elaborazione dati e di report integrata, con supporto per controlli di report personalizzati e formati di output con rendering sofisticato.  
  
-   Elaborazione di report pianificata, con la possibilità di specificare il momento di esecuzione dei report.  
  
-   Distribuzione di report dietro sottoscrizione, tramite posta elettronica o in percorsi di condivisione file.  
  
-   Report ad\-hoc, che consente agli utenti la creazione di report in base alle esigenze.  
  
-   Sottoscrizioni basate su dati che indirizzano output di report personalizzati a un elenco dinamico di destinatari.  
  
-   Estensioni personalizzate per elaborazione dati, invio di report, autenticazione personalizzata e rendering di report.  
  
 Server di report implementato come servizio Web.  Il codice dell'applicazione deve includere chiamate al servizio Web, per accedere ai report e ad altri metadati.  Il servizio Web fornisce accesso completo a livello di codice a un'istanza del server di report.  
  
 Poiché Reporting Services è una tecnologia di generazione report basata su Web, nel visualizzatore in modalità predefinita vengono mostrati report il cui rendering è in formato HTML.  Se non si desidera utilizzare il formato HTML come formato predefinito di presentazione di report, è necessario scrivere un visualizzatore di report personalizzato per l'applicazione.  
  
### Creazione di report in Visual Studio per Reporting Services  
 Per compilare report da eseguire in un server di report, creare file di definizioni di applicazioni \(con estensione rdl\) in Visual Studio tramite Business Intelligence Development Studio, incluso in SQL Server 2005.  
  
> [!NOTE]
>  Per utilizzare SQL Server Reporting Services e Business Intelligence Development Studio è necessario che nel computer in uso sia installato SQL Server 2005.  
  
 Business Intelligence Development Studio aggiunge modelli di progetto specifici per i componenti di SQL Server.  Per creare report è possibile scegliere tra i modelli di **Progetto Report Server** o **Creazione guidata progetto Report Server**.  È possibile specificare connessioni a origini dati e query a diversi tipi di origini dati, tra cui SQL Server, Oracle, Analysis Services, XML e SQL Server Integration Services.  Una scheda **Dati**, una scheda **Layout** e una scheda **Anteprima** consentono di definire i dati, creare layout di report e visualizzare l'anteprima dei report nella stessa area di lavoro.  
  
 Le definizioni di report che vengono compilate per il controllo o per il server di report possono essere riutilizzate in entrambe le tecnologie.  
  
||  
|-|  
|Per creare un report da eseguire in un server di report|  
|1.  Scegliere **Nuovo** dal menu **File**.<br />     Verrà visualizzata la finestra di dialogo **Nuovo progetto**.<br />2.  Nel riquadro **Tipi progetto** fare clic su **Progetti Business Intelligence**.<br />3.  Nel riquadro Modelli fare clic su **Progetto Report Server** o su **Creazione guidata progetto Report Server**.|  
  
## Utilizzo simultaneo di controlli ReportViewer e di SQL Server Reporting Services  
 I controlli ReportViewer e SQL Server 2005 Reporting Services possono essere utilizzati insieme nella stessa applicazione.  
  
-   Il controllo ReportViewer fornisce un visualizzatore che viene utilizzato per visualizzare i report nell'applicazione.  
  
-   Tramite Reporting Services vengono invece forniti i report e viene eseguita l'elaborazione completa in un server remoto.  
  
 È possibile configurare il controllo ReportViewer per la visualizzazione di report che vengono archiviati ed elaborati in un server di report remoto di Reporting Services.  Questo tipo di configurazione viene chiamato *modalità di elaborazione remota*.  Nella modalità di elaborazione remota, il controllo richiede un report che è archiviato in un server di report remoto.  Nel server di report viene eseguita l'elaborazione completa del report, l'elaborazione dei dati e il rendering del report.  Viene quindi restituito al controllo e visualizzato nell'area di visualizzazione un report di cui è stato eseguito il rendering.  
  
 I report che vengono eseguiti in un server di report supportano formati di esportazione aggiuntivi, sono dotati di implementazione di parametrizzazione dei report differente, utilizzano i tipi di origini dati supportati dal server di report ed è possibile accedervi tramite il modello di autorizzazione basato sui ruoli nel server di report.  
  
 Per utilizzare la modalità di elaborazione remota, specificare l'URL e il percorso del report per server durante la configurazione del controllo ReportViewer.