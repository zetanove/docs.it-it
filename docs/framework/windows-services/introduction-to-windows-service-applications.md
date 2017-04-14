---
title: "Introduction to Windows Service Applications | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ServiceController"
helpviewer_keywords: 
  - "Windows Service applications, deploying"
  - "OnStop method"
  - "OnPause method"
  - "services, about services"
  - "Service class, Windows Service applications"
  - "framework services, creating services"
  - "ServiceController components, about Windows services"
  - "Win32OwnProcess service type"
  - "services, lifetime"
  - "OnContinue method"
  - "Windows Service applications, about Windows Service applications"
  - "services, states"
  - "service states"
  - "WaitForStatus method"
  - "Win32ShareProcess service type"
  - "Windows Service applications, lifetime"
ms.assetid: 1b1b5e67-3ff3-40c0-8154-322cfd6ef0ae
caps.latest.revision: 17
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 17
---
# Introduction to Windows Service Applications
I servizi di Microsoft Windows, noti in precedenza come servizi NT, consentono di creare applicazioni eseguibili di lunga durata eseguite nelle proprie sessioni Windows.  Questi servizi possono essere avviati automaticamente all'avvio del computer, sospesi e riavviati e non mostrare alcuna interfaccia utente.  Grazie a queste caratteristiche, i servizi Windows sono perfetti per essere utilizzati su un server o quando si desidera una funzionalità a esecuzione prolungata che non interferisca con altri utenti che utilizzano lo stesso computer.  È anche possibile eseguire servizi nel contesto di sicurezza di uno specifico account utente diverso dall'utente connesso o dall'account del computer predefinito.  Per ulteriori informazioni sui servizi e sulle sessioni Windows, vedere la documentazione su Windows SDK in MSDN Library.  
  
 È possibile creare servizi con facilità creando un'applicazione che viene installata come servizio.  Si supponga, ad esempio, di dover monitorare i dati dei contatori prestazioni e reagire ai valori di soglia.  È possibile compilare un'applicazione di servizio Windows in grado di recepire i dati del contatore prestazioni, distribuire l'applicazione e iniziare la raccolta e l'analisi dei dati.  
  
 Il servizio viene creato come progetto di Microsoft Visual Studio, definendo il codice interno che controlla quali comandi possono essere inviati al servizio e quali operazioni devono essere eseguite quando si ricevono tali comandi.  A un servizio è possibile inviare i comandi di avvio, sospensione, ripresa, interruzione ed esecuzione di comandi personalizzati.  
  
 Dopo avere creato e compilato l'applicazione, è possibile installarla mediante l'utilità della riga di comando InstallUtil.exe, a cui è necessario passare il percorso del file eseguibile del servizio.  È possibile quindi utilizzare **Gestione controllo servizi** per avviare, interrompere, sospendere, riprendere e configurare il servizio.  È inoltre possibile eseguire molte di queste attività nel nodo **Servizi** di **Esplora server** oppure mediante la classe <xref:System.ServiceProcess.ServiceController>.  
  
## Confronto tra applicazioni di servizio e altre applicazioni di Visual Studio  
 Le applicazioni di servizio funzionano in modo diverso rispetto a molti altri tipi di progetti, come illustrato di seguito.  
  
-   Il file eseguibile compilato che viene creato da un progetto di applicazione di servizio deve essere installato sul server prima che il progetto possa funzionare in modo significativo.  Non è possibile eseguire un servizio o eseguirne il debug premendo F5 o F11. Inoltre, non è possibile eseguire un servizio immediatamente o effettuando un'istruzione alla volta.  È invece necessario installare e avviare il servizio, quindi associare un debugger al processo del servizio.  Per ulteriori informazioni, vedere [How to: Debug Windows Service Applications](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md).  
  
-   A differenza di alcuni tipi di progetti, è necessario creare componenti di installazione per applicazioni di servizio.  I componenti di installazione installano e registrano il servizio sul server e creano una voce per il servizio con **Gestione controllo servizi** di Windows.  Per ulteriori informazioni, vedere [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
-   Il metodo `Main` per l'applicazione di servizio deve eseguire il comando Run per i servizi contenuti nel progetto.  Il metodo `Run` carica i servizi in **Gestione controllo servizi** sul server appropriato.  Se si utilizza il modello di progetto **Servizio Windows**, questo metodo viene creato automaticamente.  Notare che il caricamento di un servizio è un'operazione diversa rispetto all'avvio.  Per ulteriori informazioni, vedere di seguito la sezione "Durata del servizio".  
  
-   Le applicazioni di servizio Windows vengono eseguite in un oggetto finestra diverso dall'oggetto finestra interattivo dell'utente che ha effettuato l'accesso.  Un oggetto finestra è un oggetto protetto che contiene gli Appunti, un set di atomi globali e un gruppo di oggetti desktop.  Poiché l'oggetto finestra del servizio Windows non è interattivo, le finestre di dialogo generate da un'applicazione di servizio Windows non verranno visualizzate e potranno comportare l'arresto del programma.  Allo stesso modo, è necessario che i messaggi di errore vengano registrati nel log eventi di Windows piuttosto che essere visualizzati nell'interfaccia utente.  
  
     Le classi del servizio Windows supportate da .NET Framework non supportano l'interazione con oggetti finestra interattivi, ovvero con l'utente che ha effettuato l'accesso.  .NET Framework, inoltre, non include classi che rappresentino oggetti finestra e desktop.  Se il servizio Windows deve interagire con altri oggetti finestra, sarà necessario accedere alle API non gestite di Windows.  Per ulteriori informazioni, vedere la documentazione su Windows SDK.  
  
     L'interazione del servizio Windows con l'utente o con altri oggetti finestra deve essere progettata con accortezza considerando scenari in cui, ad esempio, non vi siano utenti connessi o l'utente disponga di un set di oggetti desktop non previsto.  In alcuni casi può essere più indicato scrivere un'applicazione Windows che viene eseguita sotto il controllo dell'utente.  
  
-   Le applicazioni di servizio Windows vengono eseguite nel proprio contesto di sicurezza e vengono avviate prima che l'utente si connetta al computer Windows sul quale sono installate.  Occorre stabilire attentamente con quale account utente eseguire il servizio, in quanto un servizio eseguito con l'account di sistema dispone di più autorizzazioni e privilegi rispetto a un account utente.  
  
## Durata del servizio  
 Un servizio attraversa diversi stati interni nel corso della sua durata.  Per prima cosa, il servizio è installato sul sistema sul quale viene eseguito.  Questo processo esegue i programmi di installazione per il progetto del servizio e carica il servizio in **Gestione controllo servizi** su tale computer.  **Gestione controllo servizi** è l'utilità centrale fornita da Windows per l'amministrazione dei servizi.  
  
 Una volta caricato, è necessario avviare il servizio  per consentirne il funzionamento.  Un servizio può essere avviato da **Gestione controllo servizi**, da **Esplora server** o dal codice chiamando il metodo <xref:System.ServiceProcess.ServiceController.Start%2A>.  Il metodo <xref:System.ServiceProcess.ServiceController.Start%2A> passa l'elaborazione al metodo <xref:System.ServiceProcess.ServiceBase.OnStart%2A> dell'applicazione ed elabora qualsiasi codice che vi è stato definito.  
  
 Un servizio in esecuzione può rimanere in questo stato in modo indefinito finché non viene interrotto o sospeso o finché il computer non viene spento.  Un servizio può rimanere in uno dei tre stati fondamentali seguenti: <xref:System.ServiceProcess.ServiceControllerStatus>, <xref:System.ServiceProcess.ServiceControllerStatus> o <xref:System.ServiceProcess.ServiceControllerStatus>.  Può inoltre fornire informazioni sullo stato di un comando in sospeso: <xref:System.ServiceProcess.ServiceControllerStatus>, <xref:System.ServiceProcess.ServiceControllerStatus>, <xref:System.ServiceProcess.ServiceControllerStatus> o <xref:System.ServiceProcess.ServiceControllerStatus>.  Questi stati indicano che un comando è stato emesso, ad esempio un comando per sospendere un servizio in esecuzione, ma non è ancora stato terminato.  È possibile eseguire una query sulla proprietà <xref:System.ServiceProcess.ServiceController.Status%2A> per stabilire in quale stato si trova il servizio o utilizzare <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A> per effettuare un'operazione quando si verifica uno di questi stati.  
  
 È possibile sospendere, interrompere o riprendere un servizio da **Gestione controllo servizi**, da **Esplora server** o chiamando i metodi nel codice.  Ciascuna di queste operazioni può chiamare una routine associata al servizio \(<xref:System.ServiceProcess.ServiceBase.OnStop%2A>, <xref:System.ServiceProcess.ServiceBase.OnPause%2A> o <xref:System.ServiceProcess.ServiceBase.OnContinue%2A>\) nella quale è possibile definire un'ulteriore elaborazione da eseguire quando il servizio cambia stato.  
  
## Tipi di servizi  
 In Visual Studio è possibile creare due tipi di servizi mediante .NET Framework.  Ai servizi che vengono eseguiti da soli in un processo viene assegnato il tipo <xref:System.ServiceProcess.ServiceType>,  mentre ai servizi che condividono un processo con un altro servizio viene assegnato il tipo <xref:System.ServiceProcess.ServiceType>.  È possibile recuperare il tipo di servizio eseguendo una query sulla proprietà <xref:System.ServiceProcess.ServiceController.ServiceType%2A>.  
  
 Talvolta è possibile individuare altri tipi di servizi eseguendo una query relativa ai servizi esistenti non creati in Visual Studio.  Per ulteriori informazioni, vedere <xref:System.ServiceProcess.ServiceType>.  
  
## Servizi e il componente ServiceController  
 Il componente <xref:System.ServiceProcess.ServiceController> viene utilizzato per connettersi a un servizio installato e per modificarne lo stato. Mediante il componente <xref:System.ServiceProcess.ServiceController>, inoltre, è possibile avviare e interrompere un servizio, sospenderlo e riprenderne l'esecuzione, nonché inviare comandi personalizzati al servizio stesso.  Quando si crea un'applicazione di servizio, tuttavia, non è necessario utilizzare un componente <xref:System.ServiceProcess.ServiceController>.  Nella maggior parte dei casi, infatti, il componente <xref:System.ServiceProcess.ServiceController> deve essere presente in un'applicazione diversa dall'applicazione di servizio Windows che definisce il servizio dell'utente.  
  
 Per ulteriori informazioni, vedere <xref:System.ServiceProcess.ServiceController>.  
  
## Requisiti  
  
-   I servizi devono essere creati in un progetto di applicazione **Servizio Windows** o in un altro progetto supportato da .NET Framework che crea un file EXE al momento della compilazione ed eredita dalla classe <xref:System.ServiceProcess.ServiceBase>.  
  
-   I progetti contenenti servizi Windows devono disporre di componenti di installazione per il progetto e i servizi relativi.  A tale scopo, è possibile utilizzare la finestra **Proprietà**.  Per ulteriori informazioni, vedere [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
## Vedere anche  
 [Windows Service Applications](../../../docs/framework/windows-services/index.md)   
 [Service Application Programming Architecture](../../../docs/framework/windows-services/service-application-programming-architecture.md)   
 [How to: Create Windows Services](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)   
 [How to: Start Services](../../../docs/framework/windows-services/how-to-start-services.md)   
 [How to: Debug Windows Service Applications](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)   
 [Walkthrough: Creating a Windows Service Application in the Component Designer](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)   
 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)