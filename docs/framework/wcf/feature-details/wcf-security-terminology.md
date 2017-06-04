---
title: "Terminologia di sicurezza di WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sicurezza [WCF], terminologia"
  - "glossario di sicurezza [WCF]"
  - "termini di sicurezza [WCF]"
ms.assetid: 68dde024-8e51-40ba-804f-ec52d85e9ca9
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# Terminologia di sicurezza di WCF
Alcuni termini utilizzati nelle descrizioni delle funzionalità di sicurezza possono risultare poco chiari.Questo argomento fornisce brevi spiegazioni di alcuni termini di sicurezza, senza tuttavia offrire una descrizione dettagliata per ognuno degli argomenti correlati.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] termini utilizzati nella documentazione di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], vedere [Concetti fondamentali di Windows Communication Foundation](../../../../docs/framework/wcf/fundamental-concepts.md).  
  
 elenco di controllo di accesso \(ACL, Access Control List\)  
 Elenco di protezioni applicate a un oggetto,che può essere un file, un processo, un evento o un qualsiasi altro elemento a cui è associato un descrittore di sicurezza. Una voce appartenente a un ACL è detta voce di controllo di accesso \(ACE, Access Control Entry\).Esistono due tipi di ACL: discrezionale e di sistema.  
  
 autenticazione  
 Processo di verifica dell'attestazione di identità di un utente, un computer, un servizio o un processo.  
  
 autorizzazione  
 Controllo dell'accesso e dei diritti di accesso a una determinata risorsa.È ad esempio possibile autorizzare i membri di un gruppo a leggere un file, ma consentire esclusivamente ai membri di un altro gruppo di modificare tale file.  
  
 Certificato dell'autorità di certificazione \(CA, Certificate Authority\)  
 Indica la CA che rilascia i certificati di autenticazione server e client ai server e ai client che li richiedono.Poiché contiene una chiave pubblica utilizzata nelle firme digitali, tale certificato è anche detto *certificato di firma*.Se la CA è un'autorità radice, il certificato CA può anche essere detto *certificato radice*.Infine, tale certificato viene talvolta indicato con il termine *certificato di sito*.  
  
 Gerarchia di CA  
 Una gerarchia di CA contiene più CA,ognuna delle quali è certificata da un'altra CA appartenente a un livello gerarchicamente più elevato. Questa catena di certificazioni si estende verso livelli sempre più elevati, fino a raggiungere il livello massimo della gerarchia, ovvero l'*autorità radice*.  
  
 certificato  
 Attestato dotato di firma digitale contenente informazioni su un'entità e sulla relativa chiave pubblica. Un certificato consente quindi di associare fra loro questi due dati.I certificati vengono rilasciati da un'organizzazione \(o da un'entità\) attendibile, detta autorità di certificazione, dopo che quest'ultima ha verificato l'attestazione di identità dell'entità che richiede il certificato.  
  
 I certificati possono contenere vari tipi di dati.Ad esempio, un certificato X.509 contiene il formato del certificato, il numero di serie del certificato, l'algoritmo utilizzato per firmare il certificato, il nome della CA che ha rilasciato il certificato, il nome e la chiave pubblica dell'entità che richiede il certificato e la firma della CA.  
  
 archivio certificati  
 Un archivio certificati è in genere un archivio permanente in cui vengono memorizzati i certificati, gli elenchi di revoche di certificati \(CRL, Certificate Revocation List\) e gli elenchi di certificati attendibili \(CTL, Certificate Trust List\).Quando si utilizzano certificati che non richiedono un'archiviazione permanente è tuttavia possibile creare e aprire un archivio certificati che risiede soltanto in memoria.  
  
 attestazioni  
 Informazioni passate da un'entità a un'altra per verificare l'identità del mittente.Un token nome utente\/password e un certificato X.509 sono esempi di attestazioni.  
  
 certificato client  
 Certificato utilizzato per l'autenticazione del client, ad esempio durante l'autenticazione di un browser Web da parte di un server Web.Quando un client tenta di utilizzare un browser Web per accedere a un server Web protetto, il client invia il proprio certificato al server per consentire a quest'ultimo di verificare l'identità del client.  
  
 credenziali  
 Dati di accesso precedentemente autenticati utilizzati da un'entità di sicurezza per stabilire la propria identità, ad esempio una password o un ticket del protocollo Kerberos.Le credenziali vengono utilizzate per controllare l'accesso alle risorse.  
  
 Dati digest  
 Tipo di contenuto di dati definito nello standard PKCS \(Public Key Cryptographic Standard\) \#7, costituito da un tipo generico di dati e da un hash \(ovvero un digest\) dei messaggi del contenuto.  
  
 firma digitale  
 Dati che associano l'identità di un mittente alle informazioni inviate.Una firma digitale può essere inviata come entità a parte oppure insieme a un messaggio, un file o un qualsiasi altro contenuto con codifica digitale.Le firme digitali vengono utilizzate negli ambienti a chiave pubblica e forniscono servizi di autenticazione e integrità.  
  
 codifica  
 Modalità di conversione dei dati in flussi di bit.La codifica è una parte del processo di serializzazione che converte i dati in un flusso di zero e uno.  
  
 coppia di chiavi di scambio  
 Coppia di chiavi pubblica\/privata utilizzata per crittografare le chiavi di sessione affinché possano essere archiviate e scambiate in modo sicuro con altri utenti.  
  
 hash  
 Valore numerico di dimensioni costanti ottenuto applicando una funzione matematica \(vedere il termine "algoritmo di hash"\) a un quantità arbitraria di dati.I dati in genere contengono dati casuali, noti come *parametro nonce*.Sia il servizio sia il client contribuiscono con parametri nonce di scambio per aumentare la complessità del risultato.Il risultato è anche noto come *digest del messaggio*.L'invio di un valore hash è più sicuro rispetto all'invio di dati riservati, ad esempio una password, anche se quest'ultima è crittografata.Affinché sia possibile verificare il valore hash ricevuto, il mittente e il destinatario dell'hash devono utilizzare lo stesso algoritmo di hash e gli stessi parametri nonce.  
  
 algoritmo di hash  
 Algoritmo utilizzato per generare un valore hash relativo a un dato, ad esempio un messaggio o una chiave di sessione.Alcuni esempi tipici di algoritmi di hash sono MD2, MD4, MD5 e SHA\-1.  
  
 Protocollo Kerberos  
 Protocollo che definisce la modalità di interazione fra i client e il servizio di autenticazione di rete.I client ottengono ticket dal centro di distribuzione chiave Kerberos \(KDC, Kerberos Key Distribution Center\) e quindi presentano questi ticket ai server durante la procedura di connessione.I ticket Kerberos rappresentano le credenziali di rete del client.  
  
 autorità di sicurezza locale \(LSA, Local Security Authority\)  
 Sottosistema protetto che autentica gli utenti e consente loro di accedere al sistema locale.La LSA gestisce inoltre informazioni relative a tutti gli aspetti della protezione locale di un sistema, complessivamente noti come criteri locali di sicurezza del sistema.  
  
 Negotiate  
 Provider SSP \(Security Support Provider\) che funziona da livello applicazione tra l'interfaccia SSPI \(Security Support Provider Interface\) e gli altri provider SSP.Un'applicazione che chiama l'interfaccia SSPI per accedere a una rete può specificare un provider SSP per l'elaborazione della richiesta.Se l'applicazione specifica l'elemento `Negotiate`, il provider `Negotiate` analizza la richiesta e sceglie il miglior provider SSP per gestire la richiesta in base ai criteri di sicurezza configurati dall'utente.  
  
 parametro nonce  
 Valore generato casualmente utilizzato per respingere gli attacchi di tipo "replay".  
  
 non ripudio  
 Capacità di identificare gli utenti che hanno eseguito determinate azioni. Tale capacità consente pertanto di impedire che un utente declini la propria responsabilità relativamente alle azioni che ha eseguito.Ad esempio, un sistema può registrare l'ID di un utente ogni volta che quest'ultimo elimina un file.  
  
 Public Key Cryptography Standard \(PKCS\)  
 Specifiche prodotte da RSA Data Security, Inc.in collaborazione con gli sviluppatori di sistemi protetti di tutto il mondo finalizzate ad accelerare la distribuzione della crittografia a chiave pubblica.  
  
 PKCS \#7  
 Standard della sintassi dei messaggi crittografati.Si tratta di una sintassi generale per dati crittografabili, come firme digitali e crittografia,che inoltre fornisce una sintassi per distribuire al messaggio certificati o elenchi di revoche di certificati e altri attributi dei messaggi, ad esempio un timestamp.  
  
 testo non crittografato  
 Messaggiodi *testo non crittografato*.  
  
 privilegio  
 Diritto di un utente a eseguire varie operazioni di sistema, come l'arresto del sistema, il caricamento dei driver di periferica o la modifica dell'ora del sistema.Il token di accesso di un utente contiene l'elenco dei privilegi assegnati a tale utente o ai gruppi di appartenenza di tale utente.  
  
 chiave privata  
 Metà segreta di una coppia di chiavi utilizzata in un algoritmo a chiave pubblica.Le chiavi private vengono in genere utilizzate per crittografare una chiave di sessione simmetrica, includere una firma digitale in un messaggio o decrittografare un messaggio crittografato con la chiave pubblica corrispondente.Vedere anche il termine "chiave pubblica".  
  
 processo  
 Contesto di sicurezza in cui un'applicazione viene eseguita.In genere, il contesto di sicurezza è associato a un utente, pertanto tutte le applicazioni che sono in esecuzione all'interno di un dato processo ereditano le autorizzazioni e i privilegi dell'utente che le possiede.  
  
 coppia di chiavi pubblica\/privata  
 Coppia di chiavi di crittografia utilizzata nella crittografia a chiave pubblica.Un provider del servizio di crittografia \(CSP, Cryptographic Service Provider\) in genere gestisce per ogni utente due coppie di chiavi pubblica\/privata: una coppia di chiavi di scambio e una coppia di chiavi di firma digitale.Entrambe le coppie di chiavi vengono mantenute di sessione in sessione.  
  
 chiave pubblica  
 Chiave di crittografia in genere utilizzata per decrittografare una chiave di sessione o una firma digitale.La chiave pubblica può inoltre essere utilizzata per crittografare un messaggio in modo che possa essere decrittografato soltanto tramite la chiave privata corrispondente.  
  
 crittografia a chiave pubblica  
 Crittografia basata su una coppia di chiavi, una per crittografare i dati e l'altra per decrittografarli.Gli algoritmi di crittografia simmetrica utilizzano invece un'unica chiave sia per crittografare sia per decrittografare i dati.In pratica, la crittografia a chiave pubblica in genere si utilizza per proteggere la chiave di sessione utilizzata da un algoritmo di crittografia simmetrica.In questo caso, la chiave pubblica viene utilizzata per crittografare la chiave di sessione che a sua volta è stata utilizzata per crittografare i dati, mentre la chiave privata viene utilizzata per la decrittografia.Oltre a proteggere le chiavi di sessione, la crittografia a chiave pubblica può essere utilizzata per includere una firma digitale in un messaggio \(tramite la chiave privata\) e convalidare tale firma \(tramite la chiave pubblica\).  
  
 infrastruttura a chiave pubblica \(PKI, Public Key Infrastructure\)  
 Infrastruttura che fornisce un set integrato di servizi e strumenti amministrativi per la creazione, la distribuzione e la gestione di applicazioni a chiave pubblica.  
  
 ripudio  
 Capacità di un utente di negare di aver eseguito una determinata azione in casi in cui risulta impossibile provare il contrario.Si consideri ad esempio il caso di un utente che, dopo aver eliminato un file, riesce a dimostrare di non aver eseguito questa azione.  
  
 autorità radice  
 CA al livello più elevato della gerarchia di CA.L'autorità radice certifica le CA del livello immediatamente inferiore della gerarchia.  
  
 Secure Hash Algorithm \(SHA\)  
 Algoritmo di hash che genera un digest del messaggio.SHA è utilizzato insieme a molte tecnologie, fra cui l'algoritmo Digital Signature Algorithm \(DSA\) dello standard Digital Signature Standard \(DSS\).Esistono quattro versioni di SHA: SHA\-1, SHA\-256, SHA\-384 e SHA\-512.SHA\-1 genera un digest del messaggio a 160 bit.SHA\-256, SHA\-384 e SHA\-512 generano rispettivamente un digest del messaggio a 256, 384 e 512 bit.SHA è stato sviluppato dall'istituto National Institute of Standards and Technology \(NIST\) e dall'agenzia National Security Agency \(NSA\).  
  
 Secure Sockets Layer \(SSL\)  
 Protocollo di sicurezza delle comunicazioni di rete basato su una combinazione di tecnologie a chiave pubblica e a chiave privata.  
  
 contesto di sicurezza  
 Attributi o regole di sicurezza correntemente applicati.Esempi di contesti di sicurezza sono l'utente connesso correntemente al computer o il codice PIN immesso da un utente di smart card.Per l'interfaccia SSPI, un contesto di sicurezza è una struttura non trasparente di dati che contiene dati di sicurezza relativi a una connessione, ad esempio una chiave di sessione o un'indicazione della durata della sessione.  
  
 entità di sicurezza  
 Entità riconosciuta dal sistema di sicurezza.Le entità di sicurezza possono essere utenti o processi autonomi.  
  
 Provider SSP \(Security Support Provider\)  
 Libreria a collegamento dinamico \(DLL, Dynamic Link Library\) che implementa l'interfaccia SSPI rendendo disponibili per le applicazioni uno o più pacchetti di sicurezza.Ogni pacchetto di sicurezza fornisce associazioni tra le chiamate di funzione dell'interfaccia SSPI di un'applicazione e le funzioni di un modello di sicurezza effettivo.I pacchetti di sicurezza supportano diversi protocolli di sicurezza, fra cui l'autenticazione Kerberos e Microsoft LAN Manager \(LanMan\).  
  
 Security Support Provider Interface \(SSPI\)  
 Interfaccia comune tra applicazioni a livello di trasporto, ad esempio RPC \(Remote Procedure Call\), e provider di sicurezza, ad esempio Windows Distributed Security.L'interfaccia SSPI consente a un'applicazione a livello di trasporto di chiamare uno dei diversi provider di sicurezza per ottenere una connessione autenticata.Queste chiamate non richiedono una conoscenza approfondita dei dettagli del protocollo di sicurezza.  
  
 servizio token di sicurezza  
 Servizio progettato per emettere e gestire token di sicurezza personalizzati \(token emessi\) in uno scenario multiservizio.I token personalizzati sono in generale token SAML \(Security Assertions Markup Language\) contenenti una credenziale personalizzata.  
  
 certificato server  
 Certificato utilizzato per l'autenticazione del server, ad esempio durante l'autenticazione di un server Web da parte di un browser Web.Quando un client tenta di utilizzare un browser Web per accedere a un server Web protetto, il server invia il proprio certificato al browser per consentire a quest'ultimo di verificare l'identità del server.  
  
 sessione  
 Scambio di messaggi protetto mediante un solo elemento di materiale per le chiavi.Ad esempio, le sessioni SSL utilizzano un'unica chiave per proteggere lo scambio di più messaggi.  
  
 chiave di sessione  
 Chiave a generazione casuale che, dopo essere stata utilizzata una volta, viene eliminata.Le chiavi di sessione sono simmetriche, ovvero vengono utilizzate sia per la crittografia sia per la decrittografia.Tali chiavi vengono inoltre inviate insieme al messaggio e crittografate mediante una chiave pubblica ottenuta dal destinatario previsto.Una chiave di sessione è costituita da un numero casuale di bit compreso approssimativamente fra 40 e 2.000.  
  
 credenziali supplementari  
 Credenziali da utilizzare per l'autenticazione di un'entità principale di sicurezza presso domini di sicurezza esterni.  
  
 crittografia simmetrica  
 Crittografia che utilizza un'unica chiave sia per la crittografia sia per la decrittografia.La crittografia simmetrica è preferibile quando si esegue la crittografia di notevoli quantità di dati.Alcuni degli algoritmi di crittografia simmetrici più comuni sono RC2, RC4 e Data Encryption Standard \(DES\).  
  
 Vedere anche il termine "crittografia a chiave pubblica".  
  
 chiave simmetrica  
 Chiave utilizzata sia per la crittografia sia per la decrittografia.In genere le chiavi di sessione sono simmetriche.  
  
 token \(token di accesso\)  
 Un token di accesso contiene le informazioni sulla protezione relative a una sessione di accesso.Il sistema crea un token di accesso quando un utente esegue l'accesso e quindi assegna una copia del token a ogni processo eseguito per conto di tale utente.Il token identifica l'utente nonché i relativi gruppi e privilegi.Il sistema utilizza il token per controllare l'accesso agli oggetti a protezione diretta e per autorizzare o impedire nell'ambito del computer locale l'esecuzione di varie operazioni di sistema.Esistono due tipi di token di accesso: primario e di rappresentazione.  
  
 livello di trasporto  
 Livello di rete responsabile sia per la qualità del servizio sia per l'affidabilità di recapito delle informazioni.Fra le attività eseguite in questo livello vi sono il rilevamento e la correzione degli errori.  
  
 elenco di attendibilità o elenco di certificati attendibili \(CTL, Certificate Trust List\)  
 Elenco predefinito di elementi firmati da un'entità attendibile.Un CTL può presentarsi in varie forme, ad esempio un elenco di hash di certificati o un elenco di nomi di file.Tutti gli elementi dell'elenco sono autenticati \(ovvero approvati\) dall'entità che li ha firmati.  
  
 provider attendibilità  
 Software che decide se un determinato file è attendibile.La decisione si basa sul certificato associato al file.  
  
 nome UPN \(User Principal Name\)  
 Nome costituito dal nome dell'account utente \(talvolta detto *nome di accesso utente*\) e dal nome del dominio in cui tale account si trova.Questo nome rappresenta il formato standard dei nomi di accesso a un dominio Windows.Analogamente a un indirizzo di posta elettronica, il formato è: utente@esempio.com.  
  
> [!NOTE]
>  Oltre al formato standard UPN, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] accetta nomi UPN in formato di livello inferiore, ad esempio cohowinery.com\\utente.  
  
 X.509  
 Standard riconosciuto a livello internazionale che definisce le parti obbligatorie dei certificati.  
  
## Vedere anche  
 [Concetti fondamentali di Windows Communication Foundation](../../../../docs/framework/wcf/fundamental-concepts.md)   
 [Concetti sulla protezione](../../../../docs/framework/wcf/feature-details/security-concepts.md)   
 [Sicurezza e protezione](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)