---
title: "Selezione di un tipo di credenziale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf707063-3f30-4304-ab53-0e63413728a8
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Selezione di un tipo di credenziale
Le *credenziali* sono i dati usati da [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per attestare un'identità o alcune funzionalità.  Ad esempio, un passaporto è una credenziale rilasciata da un'autorità dello Stato per provare la cittadinanza in un paese o una regione.  In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], le credenziali possono essere di vario tipo, ad esempio token del nome utente e certificati X.509.  In questo argomento vengono esaminate le credenziali, come vengono usate in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e come selezionare la credenziale appropriata per l'applicazione.  
  
 In molti paesi e regioni, la patente di guida costituisce un esempio di credenziale.  Oltre a contenere dati che descrivono l'identità e le capacità di un individuo,  una patente contiene una prova di possesso, ovvero la foto del titolare.  La patente viene inoltre rilasciata da un'autorità attendibile, in genere un apposito ente governativo  e, allo scopo di impedire manomissioni e falsificazioni, viene sigillata ed eventualmente corredata di ologramma.  
  
 Quando si presenta una credenziale, è necessario presentare sia i dati sia la prova di possesso dei dati.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta vari tipi di credenziali, basati su sistemi di sicurezza sia a livello di trasporto sia a livello di messaggio.  Si considerino ad esempio due tipi di credenziali supportati in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]: nome utente e certificati \(X.509\).  
  
 Nel primo tipo di credenziale, il nome utente rappresenta l'attestazione di identità e la password rappresenta la prova di possesso.  In questo caso l'autorità attendibile è il sistema che convalida nome utente e password.  
  
 Se la credenziale è un certificato X.509, il nome del soggetto, il nome alternativo del soggetto o i campi specifici del certificato possono essere usati come attestazioni di identità, mentre gli altri campi, ad esempio i campi `Valid From` e `Valid To`, specificano la validità del certificato.  
  
## Tipi di credenziali a livello di trasporto  
 Nella tabella seguente vengono illustrati i tipi di credenziali client che possono essere usati da un'associazione nella modalità di sicurezza del trasporto.  Quando si crea un servizio, impostare la proprietà `ClientCredentialType` su uno di questi valori per specificare il tipo di credenziale che il client deve fornire per comunicare con il servizio.  È possibile impostare i tipi nel codice o nei file di configurazione.  
  
|Impostazione|Descrizione|  
|------------------|-----------------|  
|None|Specifica che il client non deve presentare alcuna credenziale.  Il client viene pertanto autenticato come anonimo.|  
|Di base|Specifica l'autenticazione di base per il client.  Per altre informazioni, vedere il documento RFC2617 [HTTP Authentication: Basic and Digest Authentication](http://go.microsoft.com/fwlink/?LinkID=88313).|  
|Digest|Specifica l'autenticazione digest per il client.  Per altre informazioni, vedere il documento RFC2617 [HTTP Authentication: Basic and Digest Authentication](http://go.microsoft.com/fwlink/?LinkID=88313).|  
|Ntlm|Specifica l'autenticazione NT LAN Manager \(NTLM\).  Viene usato quando non è possibile usare l'autenticazione Kerberos per qualche motivo.  È inoltre possibile disabilitarne l'uso come fallback impostando la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> su `false`, affinché [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] effettui tutti i tentativi possibili per generare un'eccezione se viene usata l'autenticazione NTLM.  Si noti che l'impostazione di questa proprietà su `false` potrebbe non impedire l'invio di credenziali NTLM nella rete.|  
|Windows|Specifica l'autenticazione Windows.  Per specificare solo il protocollo Kerberos in un dominio Windows, impostare la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> su `false` \(l'impostazione predefinita è `true`\).|  
|Certificato|Esegue l'autenticazione client mediante un certificato X.509.|  
|Password|L'utente deve specificare un nome utente e una password.  Convalidare la coppia di nome utente\/password usando l'autenticazione di Windows o un'altra soluzione personalizzata.|  
  
### Tipi di credenziale usati nella sicurezza client a livello di messaggio  
 La tabella seguente mostra i tipi di credenziali usabili quando si crea un'applicazione che usa la sicurezza a livello di messaggio.  I valori riportati possono essere usati nel codice o nei file di configurazione.  
  
|Impostazione|Descrizione|  
|------------------|-----------------|  
|None|Specifica che il client non deve presentare una credenziale.  Il client viene pertanto autenticato come anonimo.|  
|Windows|Consente lo scambio di messaggi SOAP all'interno di un contesto di sicurezza stabilito mediante una credenziale Windows.|  
|Nome utente|Consente al servizio di richiedere che l'autenticazione del client si basi su una credenziale di tipo nome utente.  Si noti che in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] i nomi utente non possono essere usati in nessuna operazione di crittografia, come la generazione di una firma o la crittografia di dati.  Quando si usano credenziali di tipo nome utente, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che il trasporto sia protetto.|  
|Certificato|Consente al servizio di richiedere che il client venga autenticato tramite un certificato X.509.|  
|Token emesso|Un tipo di token personalizzato, configurato in base a un criterio di sicurezza.  Il tipo di token predefinito è Security Assertions Markup Language \(SAML\).  Il token viene emesso da un servizio token di sicurezza.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Federazione e token emessi](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).|  
  
### Modello di negoziazione delle credenziali del servizio  
 La *negoziazione* è il processo in base al quale si stabilisce l'attendibilità tra un client e un servizio mediante lo scambio di credenziali.  Il processo viene eseguito in maniera iterativa tra il client e il servizio in modo da divulgare solo le informazioni necessarie per il passaggio successivo nel processo di negoziazione.  In pratica, il risultato finale è il recapito della credenziale di un servizio al client da usare nelle operazioni successive.  
  
 Con una sola eccezione, le associazioni fornite dal sistema in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per impostazione predefinita negoziano automaticamente la credenziale del servizio quando si usa la sicurezza a livello di messaggio  \(l'eccezione è <xref:System.ServiceModel.BasicHttpBinding>, che non consente la sicurezza per impostazione predefinita\). Per disabilitare questo comportamento, vedere le proprietà <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> e <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.NegotiateServiceCredential%2A>.  
  
> [!NOTE]
>  Quando viene usata la sicurezza SSL con .NET Framework 3.5 e versioni successive, un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa sia i certificati intermedi nel proprio archivio certificati sia i certificati intermedi ricevuti durante la negoziazione SSL per eseguire la convalida della catena di certificati sul certificato del servizio.  In .NET Framework 3.0 vengono usati solo i certificati intermedi installati nell'archivio certificati locale.  
  
#### Negoziazione fuori banda  
 Se la negoziazione automatica è disabilitata, la credenziale del servizio deve essere fornita al client prima di inviare qualsiasi messaggio al servizio.  Questa operazione è anche nota come provisioning *fuori banda*.  Ad esempio, se il tipo di credenziale specificato è un certificato e la negoziazione automatica è disabilitata, il client deve contattare il proprietario del servizio per ricevere e installare il certificato nel computer che esegue l'applicazione client.  Questa operazione può essere eseguita, ad esempio, quando si desidera controllare accuratamente i client che possono accedere a un servizio in uno scenario business\-to\-business.  La negoziazione fuori banda può essere eseguita tramite posta elettronica e il certificato X.509 può essere archiviato nell'archivio certificati di Windows, mediante uno strumento come lo snap\-in Certificati di Microsoft Management Console \(MMC\).  
  
> [!NOTE]
>  La proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> viene usata per fornire al servizio un certificato ottenuto tramite la negoziazione fuori banda.  Questa proprietà è necessaria quando si usa la classe <xref:System.ServiceModel.BasicHttpBinding> poiché l'associazione non consente la negoziazione automatica.  La proprietà viene usata anche in uno scenario duplex non correlato.  Si tratta di un scenario in cui un server invia un messaggio al client senza richiedere prima al client l'invio di una richiesta al server.  Poiché il server non riceve una richiesta dal client, deve usare il certificato del client per crittografare il messaggio per il client.  
  
## Impostazione dei valori di credenziale  
 Dopo aver selezionato una modalità di sicurezza, è necessario specificare le effettive credenziali.  Ad esempio, se il tipo di credenziale è impostato su "certificato", è necessario associare una credenziale specifica \(ad esempio un certificato X.509 specifico\) al servizio o client.  
  
 Il metodo per l'impostazione del valore della credenziale differisce leggermente se si programma un servizio o un client.  
  
### Impostazione delle credenziali del servizio  
 Se si sta usando la modalità di trasporto e si usa HTTP come trasporto, è necessario usare Internet Information Services \(IIS\) o configurare la porta con un certificato.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Panoramica sulla sicurezza del trasporto](../../../../docs/framework/wcf/feature-details/transport-security-overview.md) e [Protezione del trasporto HTTP](../../../../docs/framework/wcf/feature-details/http-transport-security.md).  
  
 Per fornire le credenziali a un servizio tramite il codice, creare un'istanza della classe <xref:System.ServiceModel.ServiceHost> e specificare la credenziale appropriata usando la classe <xref:System.ServiceModel.Description.ServiceCredentials>, a cui si accede tramite la proprietà <xref:System.ServiceModel.ServiceHostBase.Credentials%2A>.  
  
#### Impostazione di un certificato  
 Per fornire a un servizio un certificato X.509 da usare per autenticare il servizio nei client, usare il metodo <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A> della classe <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>.  
  
 Per fornire a un servizio un certificato client, usare il metodo <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> della classe <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential>.  
  
#### Impostazione delle credenziali di Windows  
 Se il client specifica un nome utente e una password validi, tali credenziali vengono usate per autenticare client.  In caso contrario, vengono usate le credenziali dell'utente connesso.  
  
### Impostazione delle credenziali del client  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], le applicazioni client usano un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per connettersi ai servizi.  Ogni client deriva dalla classe <xref:System.ServiceModel.ClientBase%601> e la proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> sul client consente alla specifica di vari valori delle credenziali client.  
  
#### Impostazione di un certificato  
 Per fornire a un servizio un certificato X.509 usato per autenticare il client per un servizio, usare il metodo <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> della classe <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>.  
  
## Come usare le credenziali client per autenticare il client per il servizio  
 Le informazioni sulla credenziale client richieste per comunicare con un servizio vengono fornite mediante la proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> o la proprietà <xref:System.ServiceModel.ChannelFactory.Credentials%2A>.  Il canale di sicurezza usa queste informazioni per autenticare il client per il servizio.  L'autenticazione viene eseguita tramite una delle due modalità seguenti:  
  
-   Le credenziali client vengono usate una volta prima che il primo messaggio venga inviato, usando l'istanza client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per stabilire un contesto di sicurezza.  Tutti i messaggi dell'applicazione vengono quindi protetti tramite il contesto di sicurezza.  
  
-   Le credenziali client vengono usate per autenticare ogni messaggio dell'applicazione inviato al servizio.  In questo caso, nessun contesto viene stabilito tra il client e il servizio.  
  
### Non è possibile modificare le identità stabilite  
 Quando si usa il primo metodo, il contesto stabilito viene associato permanentemente all'identità del client.  Pertanto, quando il contesto di sicurezza è stato stabilito, l'identità associata al client non può essere modificata.  
  
> [!IMPORTANT]
>  È necessario tenere presente un aspetto legato all'impossibilità di cambiare identità \(quando viene stabilito il contesto di sicurezza, ovvero il comportamento predefinito\).  Se si crea un servizio che comunica con un secondo servizio, l'identità usata per aprire il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] al secondo servizio non può essere modificata.  Questo diventa un problema se più client possono usare il primo servizio e il servizio rappresenta i client nell'accesso al secondo servizio.  Se il servizio riusa lo stesso client per tutti i chiamanti, tutte le chiamate al secondo servizio vengono eseguite con l'identità del primo chiamante usato per aprire il client al secondo servizio.  In altre parole, il servizio usa l'identità del primo client per tutti i client che vogliono comunicare con il secondo servizio.  Ciò può causare un'elevazione di privilegi.  Se questo non è il comportamento desiderato del servizio, è necessario registrare ogni chiamante e creare un nuovo client per il secondo servizio per ogni singolo chiamante e verificare che il servizio usi solo il client corretto per consentire ai diversi chiamanti la comunicazione con il secondo servizio.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] credenziali e sessioni protette, vedere [Considerazioni sulla protezione per le sessioni protette](../../../../docs/framework/wcf/feature-details/security-considerations-for-secure-sessions.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.ClientBase%601?displayProperty=fullName>   
 <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.BasicHttpMessageSecurity.ClientCredentialType%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.MessageSecurityOverMsmq.ClientCredentialType%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.MessageSecurityOverTcp.ClientCredentialType%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A?displayProperty=fullName>   
 [Concetti sulla protezione](../../../../docs/framework/wcf/feature-details/security-concepts.md)   
 [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Programmazione delle funzionalità di sicurezza di WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)   
 [Protezione del trasporto HTTP](../../../../docs/framework/wcf/feature-details/http-transport-security.md)