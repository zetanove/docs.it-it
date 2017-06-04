---
title: "Compatibilit&#224; con la funzionalit&#224; di trust parziale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a36a540b-1606-4e63-88e0-b7c59e0e6ab7
caps.latest.revision: 75
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 74
---
# Compatibilit&#224; con la funzionalit&#224; di trust parziale
Se eseguito in ambiente parzialmente attendibile, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supporta un sottoinsieme limitato di funzionalità. Le funzionalità supportate in un contesto parzialmente attendibile sono progettate sulla base di uno specifico set di scenari, come descritto nell'argomento [Scenari di distribuzione supportati](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md).  
  
## Requisiti di autorizzazione minimi  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta un sottoinsieme di funzionalità in applicazioni in esecuzione con uno dei set di autorizzazioni denominati standard seguenti:  
  
-   Autorizzazioni Attendibilità media  
  
-   Autorizzazioni Area Internet  
  
 Il tentativo di utilizzare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in applicazioni in ambiente parzialmente attendibile con autorizzazioni più restrittive può generare eccezioni di sicurezza in fase di esecuzione.  
  
## Contratti  
 Se eseguiti in ambiente parzialmente attendibile, i contratti sono soggetti alle restrizioni seguenti:  
  
-   La classe del servizio che implementa l'interfaccia `[ServiceContract]` deve essere `public` e presentare un costruttore `public`. Se definisce metodi `[OperationContract]`, questi devono essere `public`. Se invece implementa un'interfaccia `[ServiceContract]`, le implementazioni dei metodi possono essere esplicite o `private`, purché l'interfaccia `[ServiceContract]` sia `public`.  
  
-   Quando si utilizza l'attributo `[ServiceKnownType]`, il metodo specificato deve essere `public`.  
  
-   Le classi `[MessageContract]` e i relativi membri possono essere `public`. Se la classe `[MessageContract]` viene definita nell'assembly dell'applicazione, può essere `internal` e disporre di membri `internal`.  
  
## Associazioni fornite dal sistema  
 Le classi <xref:System.ServiceModel.BasicHttpBinding> e <xref:System.ServiceModel.WebHttpBinding> sono completamente supportate in un ambiente di trust parziale. La classe <xref:System.ServiceModel.WSHttpBinding> è supportata solo per la modalità di sicurezza trasporto.  
  
 Le associazioni che utilizzano trasporti diversi da HTTP, quali <xref:System.ServiceModel.NetTcpBinding>, <xref:System.ServiceModel.NetNamedPipeBinding> o <xref:System.ServiceModel.NetMsmqBinding>, non sono supportate in un ambiente di trust parziale.  
  
## Associazioni personalizzate  
 Le associazioni personalizzate possono essere create e utilizzate in ambiente parzialmente attendibile, ma devono rispettare le restrizioni specificate in questa sezione.  
  
### Trasporti  
 Gli unici elementi di associazione di trasporto consentiti sono <xref:System.ServiceModel.Channels.HttpTransportBindingElement> e <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>.  
  
### Codificatori  
 Sono consentiti i codificatori seguenti:  
  
-   Codificatore di testo \(<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>\).  
  
-   Codificatore binario \(<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>\).  
  
-   Codificatore di messaggi Web \(<xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>\).  
  
 Non sono supportati codificatori MTOM \(Message Transmission Optimization Mechanism\).  
  
### Sicurezza  
 Le applicazioni in ambiente parzialmente attendibile possono utilizzare le funzionalità di sicurezza a livello di trasporto di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per proteggere la comunicazione. La sicurezza a livello di messaggio non è supportata. La configurazione di un'associazione per l'utilizzo della sicurezza a livello di messaggio genera un'eccezione in fase di esecuzione.  
  
### Associazioni non supportate  
 Le associazioni che utilizzano messaggistica affidabile, transazioni o sicurezza a livello di messaggio non sono supportate.  
  
## Serializzazione  
 Entrambe le classi <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Xml.Serialization.XmlSerializer> sono supportate in un ambiente di trust parziale. Tuttavia, l'utilizzo di <xref:System.Runtime.Serialization.DataContractSerializer> è soggetto alle condizioni seguenti:  
  
-   Tutti i tipi `[DataContract]` serializzabili devono essere `public`.  
  
-   Tutti i campi `[DataMember]` o le proprietà in un tipo `[DataContract]` devono essere pubblici e di lettura\/scrittura. La serializzazione e la deserializzazione di campi [di sola lettura](http://go.microsoft.com/fwlink/?LinkID=98854) non sono supportate quando si esegue [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in un'applicazione in ambiente parzialmente attendibile.  
  
-   Il modello di programmazione `[Serializable]`\/ISerializable non è supportato in ambiente parzialmente attendibile.  
  
-   I tipi noti devono essere specificati nel codice o nella configurazione a livello di computer \(machine.config\). I tipi noti non possono essere specificati nella configurazione a livello di applicazione per motivi di sicurezza.  
  
-   I tipi che implementano <xref:System.Runtime.Serialization.IObjectReference> generano un'eccezione in un ambiente parzialmente attendibile.  
  
 Per altre informazioni sulla sicurezza quando si usa <xref:System.Runtime.Serialization.DataContractSerializer> in modo sicuro in un'applicazione in ambiente parzialmente attendibile, vedere la sezione sulla serializzazione in [Procedure consigliate in ambienti parzialmente attendibili](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md).  
  
### Tipi di raccolta  
 Alcuni tipi di raccolta implementano sia <xref:System.Collections.Generic.IEnumerable%601> che <xref:System.Collections.IEnumerable>. Gli esempi includono tipi che implementano <xref:System.Collections.Generic.ICollection%601>. Tali tipi possono implementare un'implementazione `public` di `GetEnumerator()` e un'implementazione esplicita di `GetEnumerator()`. In questo caso, <xref:System.Runtime.Serialization.DataContractSerializer> richiama l'implementazione `public` di `GetEnumerator()` e non l'implementazione esplicita di `GetEnumerator()`. Se nessuna delle implementazioni di `GetEnumerator()` è `public` e tutte sono implementazioni esplicite, <xref:System.Runtime.Serialization.DataContractSerializer> richiama `IEnumerable.GetEnumerator()`.  
  
 Per i tipi di raccolta quando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene eseguito in un ambiente di trust parziale, se nessuna delle implementazioni di `GetEnumerator()` è `public` né è un'implementazione esplicita dell'interfaccia, viene generata un'eccezione di sicurezza.  
  
### NetDataContractSerializer  
 Molti tipi di raccolte .NET Framework come <xref:System.Collections.Generic.List%601>, <xref:System.Collections.ArrayList>, <xref:System.Collections.Generic.Dictionary%602> e <xref:System.Collections.Hashtable> non sono supportati da <xref:System.Runtime.Serialization.NetDataContractSerializer> in ambiente parzialmente attendibile. Per questi tipi è impostato l'attributo `[Serializable]` e, come indicato in precedenza nella sezione sulla serializzazione, questo attributo non è supportato in ambiente parzialmente attendibile.<xref:System.Runtime.Serialization.DataContractSerializer> considera le raccolte in modo particolare ed è pertanto in grado di ignorare questa restrizione, al contrario di <xref:System.Runtime.Serialization.NetDataContractSerializer> che non dispone di un meccanismo di questo tipo.  
  
 Il tipo <xref:System.DateTimeOffset> non è supportato da <xref:System.Runtime.Serialization.NetDataContractSerializer> in ambiente parzialmente attendibile.  
  
 Se l'esecuzione avviene in ambiente parzialmente attendibile, non è possibile utilizzare un surrogato con <xref:System.Runtime.Serialization.NetDataContractSerializer> \(tramite il meccanismo <xref:System.Runtime.Serialization.SurrogateSelector>\). Si noti che questa restrizione si applica all'utilizzo di un surrogato, non alla relativa serializzazione.  
  
## Abilitazione dell'esecuzione dei comportamenti comuni  
 I comportamenti del servizio o dell'endpoint non contrassegnati dall'attributo <xref:System.Security.AllowPartiallyTrustedCallersAttribute> \(APTCA\) aggiunti alla sezione [\<comportamentiComuni\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) di un file di configurazione non vengono eseguiti se l'applicazione è in esecuzione in un ambiente parzialmente attendibile. In tali circostanze non viene generata alcuna eccezione. Per imporre l'esecuzione di comportamenti comuni, è necessario eseguire una delle operazioni seguenti:  
  
-   Contrassegnare il comportamento comune con l'attributo <xref:System.Security.AllowPartiallyTrustedCallersAttribute> in modo tale che questo possa essere eseguito se distribuito come applicazione parzialmente attendibile. Si noti che una voce di registro può essere impostata nel computer per impedire l'esecuzione delle assembly APTCA. .  
  
-   Verificare che, se l'applicazione viene distribuita come completamente attendibile, gli utenti non possano modificare le impostazioni di sicurezza per l'accesso al codice per eseguire l'applicazione in ambiente parzialmente attendibile. In tal caso, il comportamento non viene eseguito e non viene generata alcuna eccezione. A tale scopo, vedere l'opzione **levelfinal** in [Caspol.exe \(Code Access Security Policy Tool\)](../../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md).  
  
 [!INCLUDE[crexample](../../../../includes/crexample-md.md)] di comportamento comune, vedere [Procedura: bloccare gli endpoint nell'organizzazione](../../../../docs/framework/wcf/extending/how-to-lock-down-endpoints-in-the-enterprise.md).  
  
## Configurazione  
 Con una sola eccezione, il codice in ambiente parzialmente attendibile può caricare sezioni di configurazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] solo nel file `app.config` locale. Per caricare sezioni di configurazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che fanno riferimento a sezioni di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in machine.config o in un file web.config radice è necessario ConfigurationPermission\(Unrestricted\). Senza questa autorizzazione, i riferimenti a sezioni di configurazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(comportamenti, associazioni\) esterni al file di configurazione locale generano un'eccezione al momento del caricamento della configurazione.  
  
 L'unica eccezione è data dalla configurazione del tipo noto per la serializzazione, come descritto nella sezione sulla serializzazione di questo argomento.  
  
> [!IMPORTANT]
>  Le estensioni di configurazione sono supportate solo quando in esecuzione sotto Attendibilità totale.  
  
## Diagnostica  
  
### Registrazione eventi  
 In ambiente parzialmente attendibile la registrazione eventi limitata è supportata. Solo gli errori relativi all'attivazione del servizio e alla registrazione dei messaggi\/traccia vengono registrati nel registro eventi. Per evitare che venga scritto un numero eccessivo di messaggi nel registro eventi, il numero massimo di eventi registrabili da un processo è stato impostato su 5.  
  
### Registrazione messaggi  
 La registrazione messaggi non funziona quando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene eseguito in un ambiente di trust parziale. In un trust parziale, l'attivazione del servizio ha esito positivo ma non viene registrato alcun messaggio.  
  
### Traccia  
 La funzionalità di traccia con restrizioni è disponibile quando l'applicazione viene eseguita in un ambiente di trust parziale. Nell'elemento \<`listeners`\> del file di configurazione, i soli tipi che è possibile aggiungere sono <xref:System.Diagnostics.TextWriterTraceListener> e il nuovo <xref:System.Diagnostics.EventSchemaTraceListener>. L'utilizzo della classe <xref:System.Diagnostics.XmlWriterTraceListener> standard può generare log incompleti o non corretti.  
  
 Le origini di traccia supportate sono:  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.Runtime.Serialization>  
  
-   <xref:System.IdentityModel.Claims>, <xref:System.IdentityModel.Policy>, <xref:System.IdentityModel.Selectors> e <xref:System.IdentityModel.Tokens>.  
  
 Le origini di traccia seguenti non sono supportate:  
  
-   CardSpace  
  
-   <xref:System.IO.Log>  
  
-   <xref:System.ServiceModel.Internal.TransactionBridge>  
  
 I membri seguenti dell'enumerazione <xref:System.Diagnostics.TraceOptions> non dovrebbero essere specificati:  
  
-   <xref:System.Diagnostics.TraceOptions>  
  
-   <xref:System.Diagnostics.TraceOptions.ProcessID>  
  
 Quando si utilizza la traccia in un ambiente di trust parziale, assicurare che l'applicazione disponga di autorizzazioni sufficienti per archiviare l'output del listener di traccia. Ad esempio, quando si utilizza <xref:System.Diagnostics.TextWriterTraceListener> per scrivere output di traccia in un file di testo, assicurare che l'applicazione disponga dell'autorizzazione FileIOPermission necessaria per scrivere correttamente nel file di traccia.  
  
> [!NOTE]
>  Per evitare il flooding dei file di traccia con errori duplicati, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] disabilita la traccia della risorsa o dell'azione dopo il primo errore di sicurezza. Viene generata una traccia di eccezione per ogni accesso alla risorsa non riuscito, la prima volta che viene eseguito il tentativo di accedere alla risorsa o eseguire l'azione.  
  
## Host servizio WCF  
 L'host del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta l'attendibilità parziale. Se si desidera utilizzare un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in attendibilità parziale, non utilizzare il modello Progetto Libreria di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] per compilare il servizio. Creare invece un nuovo sito Web in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] scegliendo il modello di sito Web del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in grado di ospitare il servizio in un server Web in cui è supportato l'attendibilità parziale di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Altre limitazioni  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è generalmente soggetto alle considerazioni di sicurezza imposte dall'applicazione host. Ad esempio, se [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è ospitato in un'applicazione browser XAML \(XBAP, XAML Browser Application\), è soggetto alle limitazioni XBAP, come descritto in [Sicurezza con attendibilità parziale in WPF](http://go.microsoft.com/fwlink/?LinkId=89138).  
  
 Se indigo2 viene eseguito in ambiente parzialmente attendibile, le funzionalità aggiuntive seguenti non vengono abilitate:  
  
-   Strumentazione gestione Windows \(WMI, Windows Management Instrumentation\)  
  
-   La registrazione eventi è abilitata solo parzialmente \(vedere la discussione nella sezione **Diagnostica**\).  
  
-   Contatori delle prestazioni  
  
 L'utilizzo di funzionalità [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono supportate in un ambiente di trust parziale può generare eccezioni in fase di esecuzione.  
  
## Funzionalità non elencate  
 Il modo migliore per individuare se un'informazione non è disponibile in modalità di esecuzione in un ambiente di trust parziale è tentare di accedere alla risorsa o di eseguire l'azione all'interno di un blocco `try` e quindi eseguire il `catch` dell'errore. Per evitare il flooding dei file di traccia con errori duplicati, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] disabilita la traccia della risorsa o dell'azione dopo il primo errore di sicurezza. Viene generata una traccia di eccezione per ogni accesso alla risorsa non riuscito, la prima volta che viene eseguito il tentativo di accedere alla risorsa o eseguire l'azione.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>   
 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>   
 <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>   
 [Scenari di distribuzione supportati](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md)   
 [Procedure consigliate in ambienti parzialmente attendibili](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md)