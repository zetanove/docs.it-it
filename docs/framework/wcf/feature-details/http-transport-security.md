---
title: "Protezione del trasporto HTTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d3439262-c58e-4d30-9f2b-a160170582bb
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# Protezione del trasporto HTTP
Quando si usa HTTP come trasporto, la protezione viene fornita da un'implementazione SSL \(Secure Sockets Layer\).  SSL viene ampiamente usato in Internet per autenticare un servizio presso un client e quindi garantire la riservatezza \(crittografia\) sul canale.  In questo argomento viene illustrato come funziona SSL e come viene implementato in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## SSL di base  
 Per illustrare la modalità di funzionamento di SSL è preferibile usare uno scenario tipico, in questo caso il sito Web di una banca.  Il sito consente a un cliente di accedere al sistema con un nome utente e una password.  Dopo l'autenticazione, l'utente può eseguire transazioni, come, ad esempio, visualizzare i saldi dei conti, pagare bollette e spostare denaro da un conto all'altro.  
  
 Quando un utente visita per la prima volta il sito, il meccanismo SSL avvia una serie di negoziazioni, chiamate *handshake*, con il client dell'utente, in questo caso Internet Explorer.  SSL prima autentica il sito della banca presso il cliente.  Questo è un passaggio essenziale, perché i clienti devono innanzitutto sapere che stanno comunicando con il sito effettivo e non sono invece vittime di una truffa mirata far digitare loro nome utente e password.  SSL esegue questa autenticazione usando un certificato SSL fornito da un'autorità attendibile, ad esempio VeriSign.  La logica è la seguente: VeriSign attesta l'identità del sito della banca.  Poiché Internet Explorer considera VeriSign attendibile, il sito viene a sua volta considerato attendibile.  Se si desidera eseguire il controllo con VeriSign, è possibile fare clic sul logo VeriSign.  Verrà visualizzata una dichiarazione di autenticità con la data di scadenza e il nome dell'organizzazione a cui è stato rilasciato il certificato, ovvero il sito della banca.  
  
 Per avviare una sessione protetta, il client invia l'equivalente di un "ciao" al server, insieme a un elenco di algoritmi di crittografia usabili per apporre firme, generare hash e procedere a operazioni di crittografia e decrittografia.  In risposta, il sito restituisce un riconoscimento e indica la suite di algoritmi scelta.  Durante questo handshake iniziale, entrambe le parti inviano e ricevono parametri nonce.  Un *parametro nonce* è un dato generato in modo casuale che viene usato, in combinazione con la chiave pubblica del sito, per creare un hash.  Un *hash* è un nuovo numero derivato dai due numeri tramite un algoritmo standard quale SHA1.  Il client e il sito si scambiano anche messaggi, per concordare l'algoritmo hash da usare. L'hash è univoco e viene usato solo per la sessione tra il client e il sito, per crittografare e decrittografare messaggi.  Sia il client che il servizio dispongono del parametro nonce originale e della chiave pubblica del certificato, pertanto entrambi i lati possono generare lo stesso hash.  Il client convalida quindi l'hash inviato dal servizio \(a\) usando l'algoritmo concordato per calcolare l'hash dai dati e \(b\) confrontandolo con l'hash inviato dal servizio; se i due numeri corrispondono, il client ha la garanzia che l'hash non è stato manomesso.  Il client può quindi usare l'hash come chiave per crittografare un messaggio che contiene ancora un altro hash nuovo.  Il servizio può decrittografare il messaggio usando l'hash e recuperare questo terzultimo hash.  Le informazioni accumulate \(parametri nonce, chiave pubblica e altri dati\) sono ora conosciute su entrambi i lati e può essere creato un hash finale \(o chiave master\).  Questa chiave finale viene inviata in forma crittografata usando il penultimo hash.  La chiave master viene quindi usata per crittografare e decrittografare messaggi, per la reimpostazione della sessione.  Poiché sia il client che il servizio usando la stessa chiave, quest'ultima viene chiamata anche *chiave di sessione*.  
  
 La chiave di sessione viene definita anche chiave simmetrica o "segreto condiviso". Disporre di una chiave simmetrica è importante perché riduce i calcoli richiesti da entrambi lati della transazione.  Se ogni messaggio richiedesse un nuovo scambio di parametri nonce e hash, le prestazioni peggiorerebbero.  L'obiettivo finale di SSL è pertanto quello di usare una chiave simmetrica che consenta ai messaggi di passare liberamente da un lato all'altro con un maggiore grado di sicurezza ed efficienza.  
  
 La descrizione precedente è una versione semplificata di ciò che accade, poiché il protocollo può variare da sito a sito.  È inoltre possibile che sia il client che il sito generino parametri nonce non combinati in modo algoritmico durante l'handshake, per aggiungere maggiore complessità, e di conseguenza protezione, al processo di scambio dei dati.  
  
### Certificati e infrastruttura a chiave pubblica  
 Durante l'handshake, il servizio invia anche il proprio certificato SSL al client.  Il certificato contiene informazioni quali la data di scadenza, l'autorità emittente e l'URI \(Uniform Resource Identifier\) del sito.  Il client confronta questo URI con l'URI che aveva originariamente contattato, per assicurarsi che corrispondano, e controlla anche la data e l'autorità emittente.  
  
 Ogni certificato ha due chiavi, una privata e una pubblica, che insieme sono note come *coppia di chiavi di scambio*.  In breve, la chiave privata è nota solo al proprietario del certificato, mentre quella pubblica è leggibile dal certificato.  Ognuna delle due chiavi può essere usata per crittografare o decrittografare digest, hash o altre chiavi, ma solo in operazioni contrarie.  Ad esempio, se il client esegue la crittografia con la chiave pubblica, solo il sito può decrittografare il messaggio usando la chiave privata.  Allo stesso modo, se il sito esegue la crittografia con la chiave privata, il client può procedere alla decrittografia con la chiave pubblica.  Questo fornisce al client l'assicurazione che i messaggi vengono scambiati solo con il possessore della chiave privata, poiché solo i messaggi crittografati con la chiave privata possono essere decrittografati con la chiave pubblica.  Il sito riceve l'assicurazione che sta scambiando messaggi con un client che ha eseguito la crittografia usando la chiave pubblica.  Tuttavia, questo scambio è protetto solo per un handshake iniziale, motivo per cui è essenziale creare l'effettiva chiave simmetrica.  Ciononostante, tutte le comunicazioni dipendono dal servizio che dispone di un certificato SSL valido.  
  
## Implementazione di SSL con WCF  
 La protezione del trasporto HTTP \(o SSL\) viene fornita esternamente a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  È possibile implementare SSL in due modi; il fattore decisivo dipende dalla modalità di host dell'applicazione:  
  
-   Se si usa Internet Information Services \(IIS\) come host [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], usare l'infrastruttura IIS per configurare un servizio SSL.  
  
-   Se si sta creando un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] indipendente, è possibile associare un certificato SSL all'indirizzo usando lo strumento HttpCfg.exe.  
  
### Uso di IIS per la protezione del trasporto  
  
#### IIS 7.0  
 Per configurare [!INCLUDE[iisver](../../../../includes/iisver-md.md)] come host sicuro, usando SSL, vedere [Configurazione di Secure Sockets Layer in IIS 7](http://go.microsoft.com/fwlink/?LinkId=88600).  
  
 Per configurare i certificati da usare con [!INCLUDE[iisver](../../../../includes/iisver-md.md)], vedere [Configurazione dei certificati del server in IIS 7](http://go.microsoft.com/fwlink/?LinkID=88595).  
  
#### IIS 6.0  
 Per configurare [!INCLUDE[iis601](../../../../includes/iis601-md.md)] come host sicuro, usando SSL, vedere[Configurazione di SSL \(Secure Sockets Layer\)](http://go.microsoft.com/fwlink/?LinkId=88601).  
  
 Per configurare i certificati da usare con [!INCLUDE[iis601](../../../../includes/iis601-md.md)], vedere [Certificates\_IIS\_SP1\_Ops](http://go.microsoft.com/fwlink/?LinkId=88602).  
  
### Uso di HttpCfg per SSL  
 Se si sta creando un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] indipendente, scaricare lo strumento HttpCfg.exe disponibile nella pagina [Strumenti di supporto per Windows XP Service Pack 2](http://go.microsoft.com/fwlink/?LinkId=29002).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sull'uso dello strumento HttpCfg.exe per configurare una porta con un certificato X.509, vedere [Procedura: configurare una porta con un certificato SSL](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md).  
  
## Vedere anche  
 [Protezione del trasporto](../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [Protezione dei messaggi](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)