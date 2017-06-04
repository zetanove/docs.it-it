---
title: "Derivazione da WebRequest | Microsoft Docs"
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
  - "WebRequest (classe), protocolli di collegamento"
  - "gestore richieste specifico del protocollo"
  - "invio di dati, protocolli di collegamento"
  - "protocolli di collegamento, criteri di classe"
  - "Internet, protocolli di collegamento"
  - "ricezione di dati, protocolli di collegamento"
  - "collegamento, protocolli"
ms.assetid: 9810c177-973e-43d7-823c-14960bd625ea
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Derivazione da WebRequest
La classe <xref:System.Net.WebRequest> è una classe base astratta che fornisce metodi e proprietà di base per creare un gestore di richieste protocollo specifico che estende il modello di protocollo di .NET Framework.  Le applicazioni che utilizzano la classe **WebRequest** possono dati della richiesta utilizzando qualsiasi protocollo supportato senza la necessità di specificare il protocollo utilizzato.  
  
 Due modelli devono essere soddisfatti in modo che una classe protocollo specifica da utilizzare come protocollo innestabile: la classe deve implementare l'interfaccia <xref:System.Net.IWebRequestCreate> e deve registrare con il metodo <xref:System.Net.WebRequest.RegisterPrefix%2A?displayProperty=fullName>.  La classe deve eseguire l'override dei metodi e proprietà astratti **WebRequest** per fornire l'interfaccia di collegamento.  
  
 Le istanze di**WebRequest** è previsto l'utilizzo di una volta; se si desidera eseguire un'altra richiesta, creare un nuovo **WebRequest**.  **WebRequest** supporta l'interfaccia <xref:System.Runtime.Serialization.ISerializable> per consentire agli sviluppatori di serializzare un modello **WebRequest** quindi per ricostruire il modello per le richieste aggiuntive.  
  
## IWebRequest crea il metodo  
 Il metodo <xref:System.Net.IWebRequestCreate.Create%2A> è responsabile di inizializzare una nuova istanza della classe protocollo specifica.  Quando nuovo **WebRequest** viene creato, il metodo <xref:System.Net.WebRequest.Create%2A?displayProperty=fullName> corrisponde all'URI obbligatorio con i prefissi URI registrati con il metodo **RegisterPrefix**.  Il metodo **Create** discendente protocollo specifico appropriato deve restituire un'istanza inizializzata discendenti in grado di eseguire una transazione standard\/risposta della richiesta per il protocollo senza la necessità di alcuni campi specifici protocollo modificati.  
  
## Proprietà di ConnectionGroupName  
 La proprietà <xref:System.Net.WebRequest.ConnectionGroupName%2A> viene utilizzata per assegnare un nome a un gruppo di connessioni a una risorsa in modo da poter eseguire più richieste da una sola connessione.  Per implementare connessione\- condividere, è necessario utilizzare un metodo specifico protocollo pool di connessioni e assegnare.  Ad esempio, la classe fornita <xref:System.Net.ServicePointManager> implementa la connessione che condivide per la classe <xref:System.Net.HttpWebRequest>.  La classe **ServicePointManager** crea <xref:System.Net.ServicePoint> che fornisce una connessione a un server specifico per ciascun gruppo di connessioni.  
  
## Proprietà di ContentLength  
 La proprietà <xref:System.Net.WebRequest.ContentLength%2A> specifica il numero di byte dei dati che verranno inviati al server quando carica i dati.  
  
 In genere la proprietà <xref:System.Net.WebRequest.Method%2A> deve essere impostata per indicare che un carico è in esecuzione verificano quando la proprietà **ContentLength** è impostata su un valore maggiore di zero.  
  
## Proprietà di Tipocontenuto  
 La proprietà <xref:System.Net.WebRequest.ContentType%2A> fornisce tutte le informazioni specifiche del protocollo è necessario inviare al server per identificare il tipo di contenuto che si inviano.  In genere questo è il tipo di contenuto MIME di tutti i dati caricati.  
  
## Proprietà delle credenziali  
 La proprietà <xref:System.Net.WebRequest.Credentials%2A> contiene informazioni necessarie per autenticare la richiesta al server.  È necessario distribuire i dettagli del processo di autenticazione per il protocollo.  La classe <xref:System.Net.AuthenticationManager> è responsabile di autenticare le richieste e della disponibilità del token di autenticazione.  La classe che fornisce le credenziali utilizzate dal protocollo deve implementare l'interfaccia <xref:System.Net.ICredentials>.  
  
## Proprietà delle intestazioni  
 La proprietà <xref:System.Net.WebRequest.Headers%2A> contiene una raccolta arbitraria di coppie nome\/valore dei metadati associati alla richiesta.  Tutti i metadati necessari dal protocollo che può essere espresso come coppia nome\/valore possono essere inclusi nella proprietà **Headers**.  In genere queste informazioni devono essere incluse chiamare i metodi <xref:System.Net.WebRequest.GetResponse%2A> o <xref:System.Net.WebRequest.GetRequestStream%2A> ; è stata eseguita la richiesta una volta, i metadati viene considerata come di sola lettura.  
  
 Non è necessario utilizzare la proprietà **Headers** per utilizzare i metadati dell'intestazione.  i metadati protocollo specifici possono essere esposti come proprietà; ad esempio, la proprietà <xref:System.Net.HttpWebRequest.UserAgent%2A?displayProperty=fullName> espone l'intestazione HTTP **User\-Agent** .  Quando si espone i metadati dell'intestazione come proprietà, non è necessario consentire la stessa proprietà da impostare utilizzando la proprietà **Headers**.  
  
## Proprietà di metodo  
 La proprietà <xref:System.Net.WebRequest.Method%2A> contiene il verbo o l'azione che la richiesta viene richiesto il server di eseguire.  L'impostazione predefinita per la proprietà **Method** necessario attivare un'azione standard\/risposta delle richieste senza richiedere alcuna proprietà specifiche del protocollo di essere impostato.  Ad esempio, le impostazioni predefinite GET del metodo [HttpWebResponse](frlrfSystemNetHttpWebResponseClassMethodTopic), che richiedono una risorsa da un server Web e restituisce la risposta.  
  
 In genere la proprietà **ContentLength** deve essere impostata su un valore maggiore di zero quando la proprietà **Method** è impostata su un verbo o a un'azione che indica che un carico è in esecuzione volta.  
  
## Proprietà di PreAuthenticate  
 Le applicazioni impostare la proprietà <xref:System.Net.WebRequest.PreAuthenticate%2A> per indicare che le informazioni di autenticazione devono essere inviati con la richiesta iniziale anziché aspettare una sfida di autenticazione.  La proprietà **PreAuthenticate** è significativa solo se le credenziali di autenticazione dei supporti dei protocolli inviate con la richiesta iniziale.  
  
## Proprietà del proxy  
 La proprietà <xref:System.Net.WebRequest.Proxy%2A> contiene un'interfaccia <xref:System.Net.IWebProxy> utilizzata per accedere alla risorsa richiesta.  La proprietà **Proxy** è significativa solo se i supporti dei protocolli proxied le richieste.  Impostare il proxy predefinito se un oggetto è richiesto dal protocollo.  
  
 In alcuni ambienti, ad esempio protetto da un firewall aziendale, il protocollo potrebbe essere necessario utilizzare un proxy.  In tal caso, è necessario implementare l'interfaccia **IWebProxy** per creare una classe proxy che verrà eseguito per il protocollo.  
  
## Proprietà di RequestUri  
 La proprietà <xref:System.Net.WebRequest.RequestUri%2A> contiene l'uri passato al metodo **WebRequest.Create**.  È di sola lettura e non può essere modificato dopo **WebRequest** è stato creato.  Se il reindirizzamento dei supporti dei protocolli, la risposta può derivare da una risorsa identificata da un URI diverso.  Se è necessario fornire l'accesso all'URI che ha risposto, è necessario fornire una proprietà aggiuntiva che contiene tale URI.  
  
## Proprietà interval  
 La proprietà <xref:System.Net.WebRequest.Timeout%2A> contiene la durata, in millisecondi, attendere prima della richiesta scade e genera un'eccezione.  **Timeout** si applica solo alle chiamate sincrone effettuate dal metodo <xref:System.Net.WebRequest.GetResponse%2A> ; le richieste asincrone devono utilizzare il metodo <xref:System.Net.WebRequest.Abort%2A> per annullare di una richiesta in attesa.  
  
 Impostare la proprietà **Timeout** è significativo solo se la classe implementa protocollo specifica un processo di timeout.  
  
## Metodo di interruzione  
 Il metodo <xref:System.Net.WebRequest.Abort%2A> annulla di una richiesta asincrona in attesa in un server.  Dopo che la richiesta è stata annullata, chiamando **GetResponse**, **BeginGetResponse**, **EndGetResponse**, **GetRequestStream**, **BeginGetRequestStream**, o **EndGetRequestStream** genereranno <xref:System.Net.WebException> con la proprietà <xref:System.Net.WebException.Status%2A> a [RequestCanceled](frlrfSystemNetWebExceptionStatusClassTopic).  
  
## Metodi di EndGetRequestStream e di BeginGetRequestStream  
 Il metodo <xref:System.Net.WebRequest.BeginGetRequestStream%2A> avvia una richiesta asincrona del flusso utilizzato per caricare i dati nel server.  Il metodo <xref:System.Net.WebRequest.EndGetRequestStream%2A> completa la richiesta asincrona e restituisce il flusso richiesto.  Questi metodi implementano il metodo **GetRequestStream** utilizzando il modello asincrono.NET Framework standard.  
  
## Metodi di EndGetResponse e di BeginGetResponse  
 Il metodo <xref:System.Net.WebRequest.BeginGetResponse%2A> avvia una richiesta asincrona in un server.  Il metodo <xref:System.Net.WebRequest.EndGetResponse%2A> completa la richiesta asincrona e restituisce la risposta richiesta.  Questi metodi implementano il metodo **GetResponse** utilizzando il modello asincrono.NET Framework standard.  
  
## Metodo di GetRequestStream  
 Il metodo <xref:System.Net.WebRequest.GetRequestStream%2A> restituisce un flusso utilizzato per scrivere i dati nel server.  Il flusso restituito deve essere un flusso di sola scrittura non viene trovato, è progettato come flusso di dati unidirezionale che vengono scritti sul server.  Il flusso restituisce false per le proprietà <xref:System.IO.Stream.CanSeek%2A> e <xref:System.IO.Stream.CanRead%2A> le righe per la proprietà <xref:System.IO.Stream.CanWrite%2A>.  
  
 Il metodo **GetRequestStream** in genere visualizzata una connessione al server e, prima di restituire il flusso, invia le informazioni di intestazione che indicano che i dati vengono inviandi al server.  Poiché **GetRequestStream** avvia la richiesta, impostare alcune proprietà **Header** o la proprietà **ContentLength** in genere non è consentito dopo aver chiamato **GetRequestStream**.  
  
## Metodo di GetResponse  
 Il metodo <xref:System.Net.WebRequest.GetResponse%2A> restituisce un discendente protocollo specifico della classe <xref:System.Net.WebResponse> che rappresenta la risposta dal server.  A meno che la richiesta è già stata avviata dal metodo **GetRequestStream**, il metodo **GetResponse** crea una connessione alla risorsa identificata da **RequestUri**, invia le informazioni di intestazione che indicano il tipo di richiesta inviata e riceve una risposta dalla risorsa.  
  
 Una volta che il metodo **GetResponse** viene chiamato, tutte le proprietà devono essere considerate di sola lettura.  Le istanze di**WebRequest** è previsto l'utilizzo di una volta; se si desidera eseguire un'altra richiesta, è necessario creare un nuovo **WebRequest**.  
  
 Il metodo **GetResponse** è necessario creare un discendente appropriato **WebResponse** per contenere la risposta in ingresso.  
  
## Vedere anche  
 <xref:System.Net.WebRequest>   
 <xref:System.Net.HttpWebRequest>   
 <xref:System.Net.FileWebRequest>   
 [Programmazione di protocolli di collegamento](../../../docs/framework/network-programming/programming-pluggable-protocols.md)   
 [Derivazione da WebResponse](../../../docs/framework/network-programming/deriving-from-webresponse.md)