---
title: "Introduzione ai protocolli di collegamento | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "richieste di dati, protocolli di collegamento"
  - "WebRequest (classe), protocolli di collegamento"
  - "risposta a una richiesta Internet, protocolli di collegamento"
  - "URI"
  - "Windows Sockets"
  - "modello di richiesta/risposta"
  - "invio di dati, protocolli di collegamento"
  - "protocolli di collegamento"
  - "WebClient (classe), informazioni"
  - "protocolli di collegamento, informazioni sui protocolli di collegamento"
  - "Internet, protocolli di collegamento"
  - "identificatori del percorso"
  - "URI (Uniform Resource Identifier)"
  - "sviluppo di applicazioni [.NET Framework], protocolli di collegamento"
  - "richiesta di dati da Internet, protocolli di collegamento"
  - "ricezione di dati, protocolli di collegamento"
  - "collegamento, protocolli"
  - "identificatori del server"
  - "identificatori schema"
ms.assetid: 4b48e22d-e4e5-48f0-be80-d549bda97415
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Introduzione ai protocolli di collegamento
Microsoft .NET Framework fornisce un'implementazione a più livelli, estendibile e gestita di servizi Internet che possono essere integrati rapidamente e facilmente nelle applicazioni.  Le classi di accesso a Internet in <xref:System.Net> e gli spazi dei nomi <xref:System.Net.Sockets> possono essere utilizzati per implementare sia le applicazioni basate su web che basate su Internet.  
  
## Applicazioni Internet  
 Le applicazioni Internet possono essere classificate largamente in due tipi: applicazioni client che richiedono le informazioni e le applicazioni server che soddisfano le richieste di informazioni da client.  L'applicazione classica client\-server Internet è il web, in cui gli utenti vengono utilizzati i browser per accedere a documenti e altri dati archiviati nei server Web in.  
  
 Le applicazioni non sono limitate a una sola di questi ruoli, ad esempio, i server applicazioni di livello intermedio comuni soddisfano le richieste dei client richieste di dati da un altro server, nel qual caso viene utilizzato sia come server che client.  
  
 L'applicazione client effettua una richiesta identificando la risorsa Internet richiesta e il protocollo di comunicazione da utilizzare per la richiesta e risposta.  Se necessario, il client sono inoltre disponibili i dati aggiuntivi necessari per completare la richiesta, ad esempio la posizione del proxy o informazioni di autenticazione \(nome utente, password, e così via\).  La richiesta viene formata una volta, tale richiesta può essere inviata al server.  
  
## Identificazione delle risorse  
 .NET Framework utilizza Uniform Resource Identifier \(URI\) per identificare la risorsa Internet e il protocollo di comunicazione necessari.  L'uri consiste almeno di tre ed eventualmente di quattro, frammenti: l'identificatore di schema, che identifica il protocollo di comunicazione per la richiesta e risposta, l'identificatore server, costituito da un nome host di \(DNS\) DNS \(Domain Name System o di un indirizzo TCP che identifica in modo univoco il server Internet, identificatore del percorso, per trovare le informazioni necessarie sul server; e una stringa di query facoltativa, che comunica informazioni dal client al server.  Ad esempio, l'uri “http:\/\/www.contoso.com\/whatsnew.aspx?date\=today„ è “HTTP„ identificatore di schema, l'identificatore server “www.contoso.com„, il percorso “\/whatsnew.aspx„ e la stringa di query “? date\=today„.  
  
 Dopo che il server ha ricevuto la richiesta e ha elaborato la risposta, restituisce la risposta all'applicazione client.  La risposta include informazioni aggiuntive, ad esempio il tipo di contenuto \(testo non elaborato o dati XML, ad esempio\).  
  
## Richieste e risposte in .NET Framework  
 Le classi specifiche di.NET Framework utilizza per fornire le informazioni necessarie per accedere alle risorse Internet tramite un modello\/risposta della richiesta: la classe <xref:System.Uri>, che contiene l'uri della risorsa Internet si cercano; la classe <xref:System.Net.WebRequest>, che contiene una richiesta per la risorsa, e la classe <xref:System.Net.WebResponse>, che fornisce un contenitore per la risposta in ingresso.  
  
 Le applicazioni client crea le istanze `WebRequest` passando l'uri della risorsa di rete al metodo <xref:System.Net.WebRequest.Create%2A>.  Questo metodo statico crea `WebRequest` per un protocollo specifico, ad esempio HTTP.  `WebRequest` restituito fornisce accesso alle proprietà che controllano la richiesta al server che accedono al flusso di dati che viene inviato alla richiesta.  Il metodo <xref:System.Net.WebRequest.GetResponse%2A> su `WebRequest` invia la richiesta dell'applicazione client al server identificato nell'URI.  Nei casi in cui la risposta venga ritardata, tale richiesta può essere eseguita in modo asincrono utilizzando il metodo <xref:System.Net.WebRequest.BeginGetResponse%2A> su **WebRequest**e risposta può essere restituita in un secondo momento utilizzando il metodo <xref:System.Net.WebRequest.EndGetResponse%2A>.  
  
 I metodi **EndGetResponse** e **GetResponse** restituiscono **WebResponse** che fornisce l'accesso ai dati restituiti dal server.  Poiché questi dati vengono forniti all'applicazione di richiesta come flusso con il metodo <xref:System.Net.WebResponse.GetResponseStream%2A>, possono essere utilizzati nei flussi di dati di un'applicazione in qualsiasi punto vengono utilizzati.  
  
 Le classi **WebResponse** e **WebRequest** rappresentano la base dei protocolli innestabili — un'implementazione dei servizi di rete che consente di compilare applicazioni che utilizzano le risorse Internet senza preoccupare per i dettagli specifici del protocollo gli utilizzi di tali ogni risorsa.  Le classi derivate **WebRequest** registrati con la classe **WebRequest** per gestire i dettagli di creazione di connessioni effettive alle risorse Internet.  
  
 Ad esempio, la classe <xref:System.Net.HttpWebRequest> gestisce i dettagli della connessione a una risorsa Internet tramite HTTP.  Per impostazione predefinita, quando il metodo **WebRequest.Create** rileva un URI che inizia con “HTTP: „ o “HTTPS: „ \(identificatori di protocollo per HTTP e HTTP sicuro\), **WebRequest** restituito può essere utilizzato come è, o è possibile eseguire su di essi un cast a **HttpWebRequest** per accedere alle proprietà specifiche del protocollo.  Nella maggior parte dei casi, **WebRequest** fornisce tutte le informazioni necessarie per la creazione della richiesta.  
  
 Qualsiasi protocollo che può essere rappresentato come transazione\/risposta richiedente può essere utilizzato in **WebRequest**.  È possibile derivare classi specifiche del protocollo da **WebRequest** e da **WebResponse** quindi registrarli dall'applicazione dal metodo statico <xref:System.Net.WebRequest.RegisterPrefix%2A?displayProperty=fullName>.  
  
 Quando l'autorizzazione client per le richieste Internet viene richiesta, la proprietà <xref:System.Net.WebRequest.Credentials%2A>**WebRequest** specifica credenziali necessarie.  Queste credenziali possono essere una coppia\/password del nome semplice per HTTP base o l'autenticazione del digest, o un nome\/\/password dominio impostato per la sicurezza NTLM o l'autenticazione Kerberos.  Un set di credenziali può essere memorizzato in un'istanza [NetworkCredentials](frlrfsystemnetnetworkcredentialclasstopic), o più insiemi possono essere archiviate contemporaneamente in un'istanza <xref:System.Net.CredentialCache>.  **CredentialCache** utilizza l'uri della richiesta e dello schema di autenticazione supportati dal server di determinare quali credenziali da inviare al server.  
  
## Richieste semplici con il WebClient  
 Per applicazioni che devono effettuare richieste semplici per le risorse Internet, la classe <xref:System.Net.WebClient> vengono forniti metodi comuni per caricare i dati o scaricare i dati da un server Internet.  **WebClient** si basa sulla classe **WebRequest** per fornire l'accesso alle risorse Internet, pertanto, la classe **WebClient** può utilizzare qualsiasi protocollo innestabile registrato.  
  
 Per le applicazioni che non possono utilizzare il modello\/risposta di richiesta, o di applicazioni che devono rimanere in ascolto sulla rete e inviare richieste, lo spazio dei nomi **System.Net.Sockets** fornisce le classi [TCPClient](frlrfsystemnetsocketstcpclientclasstopic), [TCPListener](frlrfsystemnetsocketstcplistenerclasstopic)e [UDPClient](frlrfsystemnetsocketsudpclientclasstopic).  Tali classi, in cui è possibile utilizzare diversi protocolli di trasporto, consentono di gestire i dettagli delle connessioni di rete. Le connessioni verranno poi esposte all'applicazione come un flusso.  
  
 Gli sviluppatori che hanno familiarità con Windows Sockets collegamento o coloro che richiede il controllo fornito dalla programmazione a livello di socket cercheranno che le classi **System.Net.Sockets** soddisfano le proprie esigenze.  Le classi **System.Net.Sockets** sono un punto di transizione da codice gestito a codice nativo nelle classi **System.Net**.  Nella maggior parte dei casi, le classi **System.Net.Sockets** effettua il marshalling dei dati nelle rispettive controparti a 32 bit di Windows e gestisce tutti i controlli di sicurezza necessarie.  
  
## Vedere anche  
 [Programmazione di protocolli di collegamento](../../../docs/framework/network-programming/programming-pluggable-protocols.md)   
 [Programmazione di rete in .NET Framework](../../../docs/framework/network-programming/index.md)   
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)   
 [Esempi di rete per.NET in MSDN Code Gallery](http://code.msdn.microsoft.com/Wiki/View.aspx?ProjectName=nclsamples)