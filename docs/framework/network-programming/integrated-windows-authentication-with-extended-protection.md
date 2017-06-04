---
title: "Autenticazione di Windows integrata con Protezione estesa | Microsoft Docs"
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
ms.assetid: 81731998-d5e7-49e4-ad38-c8e6d01689d0
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Autenticazione di Windows integrata con Protezione estesa
I miglioramenti sono stati apportati a che influenzano l'autenticazione integrata di Windows è gestita da <xref:System.Net.HttpWebRequest>, <xref:System.Net.HttpListener>, <xref:System.Net.Mail.SmtpClient>, <xref:System.Net.Security.SslStream>, <xref:System.Net.Security.NegotiateStream>e le classi correlate in <xref:System.Net> e gli spazi dei nomi correlati.  Il supporto è stato aggiunto per la protezione estesa migliorano la sicurezza.  
  
 Tali modifiche possono influire sulle applicazioni che utilizzano queste classi per effettuare richieste Web e ricevere le risposte in cui l'autenticazione integrata di Windows viene utilizzata.  Questa modifica può inoltre comportare i server web e applicazioni client configurati per utilizzare l'autenticazione integrata di Windows.  
  
 Tali modifiche possono inoltre possibile modificare le applicazioni che utilizzano queste classi per creare altri tipi di richieste e ricevere le risposte in cui l'autenticazione integrata di Windows viene utilizzata.  
  
 Le modifiche per supportare la protezione estesa sono disponibili solo per le applicazioni in Windows 7 e Windows Server 2008 R2.  Le funzionalità di protezione estese non sono disponibili nelle versioni precedenti di Windows.  
  
## Panoramica  
 La progettazione dell'autenticazione integrata di Windows consente ad alcune richieste di verifica\/risposta delle credenziali di essere universali, il che vuol dire che possono essere utilizzate nuovamente o inoltrate.  Le risposte alla richiesta devono essere generate al minimo le informazioni specifiche di destinazione e possibilmente anche con informazioni specifiche del canale.  I servizi possono quindi garantire la protezione estesa per assicurarsi che le richieste In attesa\/Risposta di credenziali contengono informazioni specifiche del servizio come un nome principale \(SPN\) di servizio.  Con queste informazioni negli scambi credenziali, i servizi possono proteggere consigliabile utilizzare dannoso di richieste In attesa\/Risposta di credenziali che potrebbe erroneamente essere utilizzate.  
  
 La progettazione estensiva di sicurezza è un miglioramento ai protocolli di autenticazione progettati per proteggersi dagli attacchi di inoltro di autenticazione.  Si basa sul concetto di informazioni di associazione di servizi e del canale.  
  
 Gli oggetti globali sono i seguenti:  
  
1.  Se il client è aggiornato per supportare la protezione estesa, le applicazioni devono fornire le informazioni di associazione di servizio e dell'associazione di canale a tutti i protocolli di autenticazione supportati.  Informazioni di associazione di canale possono essere fornite solo quando esiste un canale \(TLS\) da associare a.  Le informazioni di associazione di servizio deve essere fornita sempre.  
  
2.  I server aggiornati che vengono configurati correttamente possono testare le informazioni di associazione di servizi e del canale quando sono presenti nel token di autenticazione client e rifiutare il tentativo di autenticazione se le associazioni di canale non corrispondono.  A seconda dello scenario di distribuzione, i server possono testare l'associazione di canale, l'associazione del servizio o entrambe.  
  
3.  I server aggiornati in grado di accettare o rifiutare le richieste del client fino a che non contengono informazioni di associazione di canale in base a criteri.  
  
 Le informazioni utilizzate da protezione estesa sono costituite da una o entrambe le seguenti due parti:  
  
1.  Un token di associazione di canale o un CBT.  
  
2.  Informazioni di associazione di servizio sotto forma di nome principale del servizio o di SPN.  
  
 Le informazioni di associazione del servizio sono un'indicazione di scopo di un client di autenticare un endpoint particolare servizio.  Vengono passate dal client al server con le proprietà seguenti:  
  
-   Il valore di SPN deve essere disponibile all'autenticazione del client nel server in forma di testo non crittografato.  
  
-   Il valore di SPN è pubblico.  
  
-   Lo SPN deve a crittografia essere protetto in transito in modo che un attacco di tipo man\-in\-the\-middle non può inserire, rimuovere o modificare il valore.  
  
 Un CBT è una proprietà del canale sicuro esterno \(come TLS\) utilizzato per legarla \(associazione\) a una conversazione tramite un canale interno e client autenticato.  Il CBT deve disporre di proprietà \(anche definite da IETF RFC 5056\):  
  
-   Quando un canale esterno esiste, il valore di CBT deve essere una proprietà che identifica uno il canale esterno o l'endpoint server, in modo indipendente da entrambi i lati del client e server di una conversazione.  
  
-   Il valore di CBT inviato dal client non deve essere un'operazione che un utente malintenzionato possa influire su.  
  
-   Alcuna garanzia viene eseguita sulla privacy del valore di CBT.  Ciò non significa tuttavia che il valore delle informazioni di associazione nonché di associazione di canale di servizio può essere esaminato sempre come qualsiasi altro ma il server che esegue l'autenticazione, ad esempio il protocollo che fornisce il CBT può crittografarla.  
  
-   Il CBT sia a livello di crittografia integrità protetta in transito in modo che un utente malintenzionato non può inserire, rimuovere o modificare il valore.  
  
 L'associazione di canale viene soddisfatta da client che trasferisce lo SPN e il CBT al server in modo sia protetta da eventuali alterazioni.  Il server convalida informazioni di associazione di canale in base ai criteri e tenta di autenticazione di rifiuta per il quale non si ritiene che diventerà il database di destinazione desiderato.  In questo modo, i due canali a livello di crittografia associata.  
  
 Per mantenano la compatibilità con i client esistenti e le applicazioni, un server sia configurato per consentire ai tentativi di autenticazione dai client che non supportano la protezione estesa.  In tal caso si parla di configurazione “parzialmente indurita„, a differenza di una configurazione “completamente indurita„.  
  
 Più componenti in <xref:System.Net> e gli spazi dei nomi <xref:System.Net.Security> eseguono l'autenticazione integrata di Windows per un'applicazione chiamante.  Questa sezione descrive le modifiche ai componenti di System.Net per aggiungere la protezione estesa nel relativo utilizzo di autenticazione integrata di Windows.  
  
 La protezione estesa attualmente supportato in Windows 7.  Un meccanismo viene fornito in modo da un'applicazione può determinare se i il sistema operativo supporta estendessero la sicurezza.  
  
## Modifiche per supportare protezione estesa  
 Il processo di autenticazione utilizzato con l'autenticazione integrata di Windows, come il protocollo di autenticazione utilizzato, comporta spesso una sfida pubblicata dal computer di destinazione e rinviata al computer client.  La protezione estesa aggiunte nuove funzionalità per il processo di autenticazione  
  
 Lo spazio dei nomi <xref:System.Security.Authentication.ExtendedProtection> fornisce supporto per l'autenticazione utilizzando la protezione estesa per le applicazioni.  La classe <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding> in questo spazio dei nomi rappresenta l'associazione di canale.  La classe <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> in questo spazio dei nomi rappresenta i criteri di protezione estesa utilizzato dal server per convalidare le connessioni client in arrivo.  Altri membri della classe vengono utilizzati con protezione estesa.  
  
 Per le applicazioni server, tali classi includono:  
  
 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> che presenta gli elementi seguenti:  
  
-   Una proprietà <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy.OSSupportsExtendedProtection%2A> che indica se i il sistema operativo supporta integrati l'autenticazione di Windows con protezione estesa.  
  
-   Valore di <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> che indica quando applicare i criteri di protezione estesa.  
  
-   Un valore <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario> che indica lo scenario di distribuzione.  Ciò influisce sulla protezione estesa è selezionata.  
  
-   <xref:System.Security.Authentication.ExtendedProtection.ServiceNameCollection> facoltativo che contiene l'elenco di SPN personalizzato utilizzato per trovare una corrispondenza con lo SPN fornito dal client come destinazione desiderato di autenticazione.  
  
-   <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding> facoltativo che contiene un'associazione di canale personalizzata da utilizzare per la convalida.  Questo scenario non è un caso comune  
  
 Lo spazio dei nomi <xref:System.Security.Authentication.ExtendedProtection.Configuration> fornisce supporto per la configurazione dell'autenticazione utilizzando la protezione estesa per le applicazioni.  
  
 Una serie di modifiche della funzionalità sono state apportate per supportare la protezione estesa nello spazio dei nomi esistente <xref:System.Net>.  Tali modifiche includono:  
  
-   Una nuova classe <xref:System.Net.TransportContext> aggiunta allo spazio dei nomi <xref:System.Net> che rappresenta un contesto di trasporto.  
  
-   Nuovo <xref:System.Net.HttpWebRequest.EndGetRequestStream%2A> e i metodi di overload <xref:System.Net.HttpWebRequest.GetRequestStream%2A> in <xref:System.Net.HttpWebRequest> classe che consentono di recuperare <xref:System.Net.TransportContext> per supportare la protezione estesa per le applicazioni client.  
  
-   Aggiunte alle classi <xref:System.Net.HttpListenerRequest> e <xref:System.Net.HttpListener> per supportare le applicazioni server.  
  
 Una modifica della funzionalità è stata eseguita per supportare la protezione estesa per le applicazioni client SMTP nello spazio dei nomi esistente <xref:System.Net.Mail> :  
  
-   Una proprietà <xref:System.Net.Mail.SmtpClient.TargetName%2A> nella classe <xref:System.Net.Mail.SmtpClient> che rappresenta lo SPN da utilizzare per l'autenticazione quando si utilizza ha esteso la sicurezza delle applicazioni client SMTP.  
  
 Una serie di modifiche della funzionalità sono state apportate per supportare la protezione estesa nello spazio dei nomi esistente <xref:System.Net.Security>.  Tali modifiche includono:  
  
-   Nuovo <xref:System.Net.Security.NegotiateStream.BeginAuthenticateAsClient%2A> e i metodi di overload <xref:System.Net.Security.NegotiateStream.AuthenticateAsClient%2A> in <xref:System.Net.Security.NegotiateStream> classe che consentono di passare un CBT per supportare la protezione estesa per le applicazioni client.  
  
-   Nuovo <xref:System.Net.Security.NegotiateStream.BeginAuthenticateAsServer%2A> e i metodi di overload <xref:System.Net.Security.NegotiateStream.AuthenticateAsServer%2A> in <xref:System.Net.Security.NegotiateStream> classe che consentono di passare <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> per supportare la protezione estesa per le applicazioni server.  
  
-   Una nuova proprietà <xref:System.Net.Security.SslStream.TransportContext%2A> nella classe <xref:System.Net.Security.SslStream> per supportare protezione estesa per le applicazioni client e server.  
  
 Una proprietà <xref:System.Net.Configuration.SmtpNetworkElement> è stata aggiunta alla configurazione di supporto di protezione estesa per i client SMTP nello spazio dei nomi <xref:System.Net.Security>.  
  
## Protezione estesa per le applicazioni client  
 Supporto esteso di sicurezza nella maggior parte delle applicazioni client viene eseguito automaticamente.  Il supporto delle classi <xref:System.Net.Mail.SmtpClient> e <xref:System.Net.HttpWebRequest> ha esteso la protezione ogni volta che la versione sottostante dei supporti di Windows ha esteso la sicurezza.  Un'istanza <xref:System.Net.HttpWebRequest> invia una SPN costruito da <xref:System.Uri>.  Per impostazione predefinita, un'istanza <xref:System.Net.Mail.SmtpClient> invia una SPN costruito dal nome host del server di posta elettronica SMTP.  
  
 Per l'autenticazione personalizzata, le applicazioni client possono utilizzare <xref:System.Net.HttpWebRequest.EndGetRequestStream%28System.IAsyncResult%2CSystem.Net.TransportContext%40%29?displayProperty=fullName> o <xref:System.Net.HttpWebRequest.GetRequestStream%28System.Net.TransportContext%40%29?displayProperty=fullName> in <xref:System.Net.HttpWebRequest> classe che consentono di recuperare <xref:System.Net.TransportContext> e il CBT utilizzando il metodo <xref:System.Net.TransportContext.GetChannelBinding%2A>.  
  
 Lo SPN da utilizzare per l'autenticazione integrata di Windows inviata da un'istanza <xref:System.Net.HttpWebRequest> a un servizio specificato può essere modificato impostando la proprietà <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A>.  
  
 La proprietà <xref:System.Net.Mail.SmtpClient.TargetName%2A> può essere utilizzata per impostare un oggetto personalizzato SPN da utilizzare per l'autenticazione integrata di Windows per la connessione SMTP.  
  
## Protezione estesa per le applicazioni server  
 <xref:System.Net.HttpListener> automaticamente i meccanismi forniti per convalidare le associazioni di servizio durante l'autenticazione HTTP.  
  
 Il meglio scenario sicuro è di consentire la protezione estesa per i prefissi di HTTPS:\/\/.  In questo caso, impostare <xref:System.Net.HttpListener.ExtendedProtectionPolicy%2A?displayProperty=fullName> a <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> con <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> impostato su <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> o a <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement>e <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario> impostata sul valore <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario> A <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> inserisce <xref:System.Net.HttpListener> in modalità parzialmente indurita, mentre <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> corrisponde alla modalità completamente indurita.  
  
 In questa configurazione quando viene effettuata una richiesta al server tramite un canale sicuro esterno, il canale esterno viene eseguita una query per l'associazione di canale.  Questa associazione di canale viene passata alle chiamate di autenticazione SSPI, che verificano che l'associazione di canale l'autenticazione BLOB corrisponde a.  Esistono tre possibili risultati:  
  
1.  Il sistema operativo sottostante del server non supporta la protezione estesa.  La richiesta non verrà esposta all'applicazione e \(401\) una risposta non autorizzata verrà restituita al client.  Un messaggio verrà registrato nell'origine di analisi <xref:System.Net.HttpListener> che specifica il motivo dell'errore.  
  
2.  La chiamata di SSPI non riesce a indicare che il client ha specificato un'associazione di canale che non corrisponde al valore previsto recuperato dal canale esterno o di non riuscita per fornire un'associazione di canale quando i criteri di protezione estesa nel server è stato configurato per <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement>.  In entrambi i casi, la richiesta non verrà esposta all'applicazione e \(401\) una risposta non autorizzata verrà restituita al client.  Un messaggio verrà registrato nell'origine di analisi <xref:System.Net.HttpListener> che specifica il motivo dell'errore.  
  
3.  Il client specifica l'associazione di canale corretta o è consentito per la connessione senza specificare un'associazione di canale poiché i criteri di protezione estesa nel server è configurato con <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> che la richiesta viene restituita alla domanda di elaborare.  Nessun controllo del nome del servizio viene eseguito automaticamente.  Un'applicazione può scegliere di eseguire una convalida del nome del servizio utilizzando la proprietà <xref:System.Net.HttpListenerRequest.ServiceName%2A>, ma in queste circostanze è ridondante.  
  
 Se un'applicazione è le chiamate a SSPI eseguire l'autenticazione basata sui BLOB passati avanti e indietro nel corpo di una richiesta HTTP e desidera supportare l'associazione di canale, deve recuperare l'associazione di canale prevista dal canale sicuro esterno utilizzando <xref:System.Net.HttpListener> per visualizzarne la funzione Win32 [AcceptSecurityContext](http://go.microsoft.com/fwlink/?LinkId=147021) nativa.  A tale scopo, utilizzare la proprietà <xref:System.Net.HttpListenerRequest.TransportContext%2A> e chiamare il metodo <xref:System.Net.TransportContext.GetChannelBinding%2A> per recuperare il CBT.  Solo le associazioni di endpoint sono supportate.  Anziché l'altro <xref:System.Security.Authentication.ExtendedProtection.ChannelBindingKind> è specificato, <xref:System.NotSupportedException> verrà generata un'eccezione.  Se l'associazione di canale sottostante del sistema operativo supporta, il metodo <xref:System.Net.TransportContext.GetChannelBinding%2A> restituirà <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding><xref:System.Runtime.InteropServices.SafeHandle> che esegue il wrapping di un puntatore a un'associazione di canale appropriata per il [AcceptSecurityContext](http://go.microsoft.com/fwlink/?LinkId=147021) passaggio alla funzione del membro del pvBuffer di una struttura di SecBuffer passata al parametro `pInput`.  La proprietà <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding.Size%2A> contiene la lunghezza, in byte, dell'associazione di canale.  Se il sistema operativo sottostante non supporta le associazioni di canale, la funzione restituirà `null`.  
  
 Un altro scenario consiste nel consentire la protezione estesa per i prefissi di HTTP:\/\/ quando i proxy non vengono utilizzati.  In questo caso, impostare <xref:System.Net.HttpListener.ExtendedProtectionPolicy%2A?displayProperty=fullName> a <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> con <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> impostato su <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> o a <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement>e <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario> impostata sul valore <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario> A <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> inserisce <xref:System.Net.HttpListener> in modalità parzialmente indurita, mentre <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> corrisponde alla modalità completamente indurita.  
  
 Un elenco predefinito dei nomi del servizio per viene creato in base ai prefissi registrati con <xref:System.Net.HttpListener>.  Questo elenco predefinito può essere esaminato mediante la proprietà <xref:System.Net.HttpListener.DefaultServiceNames%2A>.  Se l'elenco non è completo, un'applicazione può specificare una raccolta di nome al servizio personalizzata nel costruttore della classe <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> che verrà utilizzata al posto dell'elenco nome del servizio predefinito.  
  
 In questa configurazione, quando viene effettuata una richiesta al server senza procedere all'esterno dell'autenticazione di canale sicuro in genere senza un controllo dell'associazione di canale.  Se l'autenticazione viene eseguita correttamente, il contesto è possibile eseguire una query per il nome del servizio che il client ha fornito da e convalidato rispetto all'elenco di nomi del servizio validi.  Esistono quattro risultati possibili:  
  
1.  Il sistema operativo sottostante del server non supporta la protezione estesa.  La richiesta non verrà esposta all'applicazione e \(401\) una risposta non autorizzata verrà restituita al client.  Un messaggio verrà registrato nell'origine di analisi <xref:System.Net.HttpListener> che specifica il motivo dell'errore.  
  
2.  Il sistema operativo sottostante del client non supporta la protezione estesa.  Nella configurazione <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement>, il tentativo di autenticazione riuscirà e la richiesta verrà restituita all'applicazione.  Nella configurazione <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement>, di autenticazione non riuscirà.  La richiesta non verrà esposta all'applicazione e \(401\) una risposta non autorizzata verrà restituita al client.  Un messaggio verrà registrato nell'origine di analisi <xref:System.Net.HttpListener> che specifica il motivo dell'errore.  
  
3.  Supporta il sistema operativo sottostante del client hanno esteso la sicurezza, ma non è stata specificata un'associazione al servizio.  La richiesta non verrà esposta all'applicazione e \(401\) una risposta non autorizzata verrà restituita al client.  Un messaggio verrà registrato nell'origine di analisi <xref:System.Net.HttpListener> che specifica il motivo dell'errore.  
  
4.  Il client ha specificato un'associazione al servizio.  L'associazione del servizio viene confrontata con elenco di associazioni concedere di servizio.  Se corrisponde, la richiesta viene restituita all'applicazione.  In caso contrario, la richiesta non verrà esposta all'applicazione e \(401\) una risposta non autorizzata automaticamente verrà restituita al client.  Un messaggio verrà registrato nell'origine di analisi <xref:System.Net.HttpListener> che specifica il motivo dell'errore.  
  
 Se questo approccio semplice utilizzando un elenco concessione dei nomi del servizio accettabili è insufficiente, un'applicazione può fornire la propria convalida del nome del servizio eseguire una query sulla proprietà <xref:System.Net.HttpListenerRequest.ServiceName%2A>.  In casi 1 e 2 precedente, la proprietà restituirà `null`.  Nel caso 3, restituiranno una stringa vuota.  Nel caso 4, il nome del servizio specificato dal client vengono restituiti.  
  
 Queste funzionalità di sicurezza estese possono essere utilizzate da applicazioni server per l'autenticazione con altri tipi di richieste e quando i proxy attendibili utilizzati.  
  
## Vedere anche  
 <xref:System.Security.Authentication.ExtendedProtection>   
 <xref:System.Security.Authentication.ExtendedProtection.Configuration>