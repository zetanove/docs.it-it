---
title: "Concetti fondamentali di Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "concetti [WCF]"
  - "nozioni fondamentali [WCF]"
  - "WCF [WCF], concetti"
  - "Windows Communication Foundation [WCF], concetti"
ms.assetid: 3e7e0afd-7913-499d-bafb-eac7caacbc7a
caps.latest.revision: 39
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 39
---
# Concetti fondamentali di Windows Communication Foundation
In questo documento viene fornita una panoramica dettagliata dell'architettura [!INCLUDE[indigo1](../../../includes/indigo1-md.md)].Il documento è concepito per spiegare i concetti principali e le modalità di interazione.Per un'esercitazione sulla creazione della versione più semplice di un servizio e di un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md).Per informazioni sulla programmazione [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md).  
  
## Nozioni fondamentali su WCF  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è uno strumento runtime e un set di API per la creazione di sistemi che inviano messaggi tra servizi e client.La stessa infrastruttura e le stesse API vengono utilizzate per creare applicazioni che comunicano con le altre applicazioni nello stesso computer o su un sistema di un'altra società accessibile tramite Internet.  
  
### Messaggistica ed endpoint  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è basato sulla nozione di comunicazione che utilizza messaggi e qualsiasi elemento che può essere modellato come messaggio, ad esempio una richiesta HTTP o una richiesta di accodamento messaggi, nota come messaggio MSMQ, può essere rappresentato in modo uniforme nel modello di programmazione.Questo consente un'API unificata su meccanismi di trasporto differenti.  
  
 Il modello distingue tra *client*, ovvero applicazioni che iniziano la comunicazione, e *servizi*, ovvero applicazioni che attendono la comunicazione dei client e rispondono a tale richiesta.Una singola applicazione può comportarsi sia come client che come servizio.Per alcuni esempi, vedere [Servizi duplex](../../../docs/framework/wcf/feature-details/duplex-services.md) e [Rete peer\-to\-peer](../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
 I messaggi vengono inviati tra endpoint.Gli *endpoint* sono punti in cui i messaggi vengono inviati o ricevuti \(o entrambe le operazioni\) e definiscono tutte le informazioni necessarie per lo scambio di messaggi.Un servizio espone uno o più endpoint dell'applicazione \(così come zero o più endpoint dell'infrastruttura\) e il client genera un endpoint che è compatibile con uno degli endpoint del servizio.  
  
 Un *endpoint* descrive in modo standard dove i messaggi devono essere inviati, come devono essere inviati e come devono apparire.Un servizio può esporre queste informazioni come metadati che possono essere elaborati dai client per generare client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] appropriati e *stack* di comunicazione.  
  
### Protocolli di comunicazione  
 Un elemento obbligatorio dello stack di comunicazione è il *protocollo di trasporto*.I messaggi possono essere inviati tramite Intranet e Internet utilizzando trasporti comuni, ad esempio HTTP e TCP.Sono inclusi altri trasporti che supportano la comunicazione con applicazioni di Accodamento messaggi e nodi su una rete peer.Ulteriori meccanismi di trasporto possono essere aggiunti utilizzando i punti di estensione incorporati di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 Un altro elemento obbligatorio nello stack di comunicazione è la codifica che specifica come ogni messaggio viene formattato.[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] fornisce le codifiche seguenti:  
  
-   Codifica testo, una codifica interoperativa.  
  
-   Codifica Message Transmission Optimization Mechanism \(MTOM\), una modalità interoperativa per l'invio efficiente di dati binari non strutturati a e da un servizio.  
  
-   Codifica binaria per trasferimenti efficienti.  
  
 Ulteriori meccanismi di codifica \(ad esempio, una codifica di compressione\) possono essere aggiunti utilizzando i punti di estensione incorporati di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
### Modelli dei messaggi  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] supporta numerosi modelli di messaggistica, inclusa la comunicazione request\/reply, unidirezionale e duplex.Trasporti differenti supportano modelli di messaggistica differenti e in questo modo influenzano i tipi di interazioni supportati.Il runtime e le API [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] consentono inoltre di inviare messaggi in modo protetto e affidabile.  
  
## Termini WCF  
 Altri concetti e termini utilizzati nella documentazione [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] includono gli elementi seguenti.  
  
 messaggio  
 Unità autonoma di dati che può essere costituita da varie parti, incluso corpo e intestazioni.  
  
 servizio  
 Costrutto che espone uno o più endpoint che a loro volta espongono una o più operazioni del servizio.  
  
 endpoint  
 Costrutto a cui vengono inviati o da cui vengono ricevuti \(o entrambe le operazioni\) i messaggi.Comprende un percorso \(indirizzo\) che definisce dove i messaggi possono essere inviati, una specifica del meccanismo di comunicazione \(associazione\) che descrive come i messaggi devono essere inviati e una definizione per un set di messaggi che possono essere inviati o ricevuti \(o entrambe le operazioni\) da quel percorso \(contratto di servizio\) che descrive quale messaggio può essere inviato.  
  
 Un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene esposto come una raccolta di endpoint.  
  
 endpoint applicazione  
 Endpoint esposto dall'applicazione che corrisponde a un contratto di servizio implementato dall'applicazione.  
  
 endpoint infrastruttura  
 Endpoint esposto dall'infrastruttura per agevolare la funzionalità necessaria o fornita dal servizio che non è correlata a un contratto di servizio.Un servizio, ad esempio, potrebbe avere un endpoint dell'infrastruttura che fornisce informazioni sui metadati.  
  
 indirizzo  
 Specifica il percorso in cui vengono ricevuti i messaggi.Viene specificato sotto forma di URI \(Uniform Resource Identifier\).La parte relativa allo schema URI denomina il meccanismo di trasporto da utilizzare per raggiungere l'indirizzo, ad esempio HTTP e TCP.La parte gerarchica dell'URI contiene un percorso univoco il cui formato dipende dal meccanismo di trasporto.  
  
 L'indirizzo endpoint consente di creare indirizzi endpoint univoci per ogni endpoint in un servizio o, a determinate condizioni, di condividere un indirizzo tra gli endpoint.Nell'esempio seguente viene illustrato un indirizzo che utilizza il protocollo HTTPS con una porta non predefinita:  
  
```  
HTTPS://cohowinery:8005/ServiceModelSamples/CalculatorService  
```  
  
 associazione  
 Definisce le modalità di comunicazione tra un endpoint e gli elementi rimanenti.È costituita da un set di componenti chiamati elementi di associazione posizionati uno sopra l'altro in uno stack per creare l'infrastruttura della comunicazione.Un'associazione definisce almeno il trasporto \(ad esempio HTTP o TCP\) e la codifica \(ad esempio testo o binaria\) utilizzati.Un'associazione può contenere elementi di associazione che specificano dettagli come i meccanismi di sicurezza utilizzati per proteggere i messaggi o il modello del messaggio utilizzato da un endpoint.Per ulteriori informazioni, vedere [Configurazione dei servizi](../../../docs/framework/wcf/configuring-services.md).  
  
 elemento di associazione  
 Rappresenta una particolare parte dell'associazione, ad esempio un trasporto, una codifica, un'implementazione di un protocollo a livello di infrastruttura \(ad esempio WS\-ReliableMessaging\) o qualsiasi altro componente dello stack di comunicazione.  
  
 comportamenti  
 Componente che controlla vari aspetti in fase di esecuzione di un servizio, di un endpoint, di una particolare operazione o di un client.I comportamenti sono raggruppati in base allo scopo. I comportamenti comuni influiscono globalmente su tutti gli endpoint, i comportamenti del servizio influiscono solo sugli aspetti relativi al servizio, i comportamenti dell'endpoint influiscono solo sulle proprietà relative all'endpoint e i comportamenti a livello di operazione influiscono su particolari operazioni.Un comportamento del servizio, ad esempio, l'azione di limitazione che specifica come un servizio reagisce quando un eccesso di messaggi minaccia di sovraccaricarne le funzionalità di gestione.Un comportamento dell'endpoint, invece, controlla solo gli aspetti pertinenti agli endpoint, ad esempio come e dove trovare una credenziale di sicurezza.  
  
 associazioni fornite dal sistema  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] include numerose associazioni fornite dal sistema.Si tratta di raccolte di elementi di associazione ottimizzati per scenari specifici.<xref:System.ServiceModel.WSHttpBinding> è progettata, ad esempio, per l'interoperabilità con servizi che implementano varie specifiche WS\-\*.Le associazioni predefinite consentono di risparmiare tempo presentando solo quelle opzioni che possono essere applicate correttamente allo scenario specifico.Se un'associazione predefinita non soddisfa i requisiti, è possibile crearne una personalizzata.  
  
 configurazione e codifica  
 Il controllo di un'applicazione può essere eseguito tramite codifica, tramite configurazione o tramite una combinazione di entrambe.La configurazione presenta il vantaggio di consentire a qualcun altro oltre allo sviluppatore, ad esempio a un amministratore di rete, di impostare parametri del client e del servizio dopo che il codice è stato scritto e senza doverlo ricompilare.La configurazione non solo consente di impostare valori come gli indirizzi endpoint ma fornisce anche un maggior controllo consentendo di aggiungere endpoint, associazioni e comportamenti.La codifica consente allo sviluppatore di mantenere uno stretto controllo su tutti i componenti del servizio o del client ed eventuali impostazioni eseguite tramite la configurazione possono essere controllate e se necessario sottoposte a override dal codice.  
  
 operazione del servizio  
 Procedura definita nel codice di un servizio che implementa la funzionalità per un'operazione.Questa operazione viene esposta ai client come metodi in un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Il metodo può restituire un valore e può accettare zero, uno o più argomenti e può non restituire alcuna risposta.Un'operazione, ad esempio, che funziona come un semplice "Hello" può essere utilizzata come notifica della presenza di un client e per iniziare una serie di operazioni.  
  
 contratto di servizio  
 Collega più operazioni correlate in una sola unità funzionale.Il contratto può definire impostazioni a livello di servizio, ad esempio lo spazio dei nomi del servizio, un contratto callback corrispondente e altre impostazioni simili.Nella maggior parte dei casi, il contratto viene definito creando un'interfaccia nel linguaggio di programmazione selezionato e applicando l'attributo <xref:System.ServiceModel.ServiceContractAttribute> all'interfaccia.Il codice del servizio effettivo viene determinato implementando l'interfaccia.  
  
 contratto dell'operazione  
 Un contratto dell'operazione definisce i parametri e il tipo restituito di un'operazione.Quando si crea un'interfaccia che definisce il contratto di servizio, si indica un contratto dell'operazione applicando l'attributo <xref:System.ServiceModel.OperationContractAttribute> a ogni definizione del metodo che fa parte del contratto.Le operazioni possono essere modellate in modo da accettare un solo messaggio e restituire un solo messaggio o in modo da accettare un set di tipi e restituire un tipo.Nel secondo caso, il sistema determinerà il formato per i messaggi che devono essere scambiati per quell'operazione.  
  
 contratto di messaggio  
 Descrive il formato di un messaggio.Un contratto di messaggio dichiara, ad esempio, se gli elementi del messaggio devono essere inseriti nelle intestazioni invece che nel corpo, quale livello di sicurezza deve essere applicato e a quali elementi del messaggio e così via.  
  
 contratto di errore  
 Può essere associato a un'operazione del servizio per individuare errori che possono essere restituiti al chiamante.Un'operazione può avere zero o più errori associati.Si tratta di errori SOAP modellati come eccezioni nel modello di programmazione.  
  
 contratto dati  
 Descrizioni nei metadati dei tipi di dati utilizzati da un servizio.In questo modo è consentito ad altri elementi di interoperare con il servizio.I tipi di dati possono essere utilizzati in qualsiasi parte di un messaggio, come parametri o tipi restituiti.Se il servizio utilizza solo tipi semplici, non è necessario utilizzare esplicitamente i contratti dati.  
  
 hosting  
 Un servizio deve essere ospitato in un processo.Un *host* è un'applicazione che controlla la durata del servizio.I servizi possono essere indipendenti o gestiti da un processo di hosting esistente.  
  
 servizio indipendente  
 Servizio in esecuzione all'interno di un'applicazione di processo creata dallo sviluppatore.Lo sviluppatore ne controlla la durata, imposta le proprietà del servizio, apre il servizio \(impostandolo in modalità di ascolto\) e chiude il servizio.  
  
 processo di hosting  
 Applicazione progettata per ospitare servizi,inclusi Internet Information Services \(IIS\), Windows Activation Services \(WAS\) e servizi per Windows.In questi scenari di hosting, l'host controlla la durata del servizio.Ad esempio, tramite IIS è possibile configurare una directory virtuale che contiene l'assembly del servizio e il file di configurazione.Quando un messaggio viene ricevuto, IIS avvia il servizio e ne controlla la durata.  
  
 istanze  
 Un servizio è dotato di un modello di istanze.Sono presenti tre modelli di istanze, ovvero singolo, nel quale un solo oggetto CLR provvede a tutti i client, per chiamata, nel quale viene creato un nuovo oggetto CLR per gestire ogni chiamata del client, e per sessione, nel quale viene creato un set di oggetti CLR, uno per ogni sessione separata.La scelta di un modello di istanze dipende dai requisiti dell'applicazione e dal modello di utilizzo previsto del servizio.  
  
 applicazione client  
 Programma che scambia messaggi con uno o più endpoint.L'applicazione client inizia creando un'istanza di un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e chiamando metodi del client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].È importante notare che una stessa applicazione può essere sia un client che un servizio.  
  
 canale  
 Implementazione concreta di un elemento di associazione.L'associazione rappresenta la configurazione e il canale è l'implementazione associata a tale configurazione.Per ogni elemento di associazione è pertanto presente un canale associato.I canali si dispongono uno sopra l'altro per creare l'implementazione concreta dell'associazione, ovvero lo stack dei canali.  
  
 client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]  
 Costrutto dell'applicazione client che espone le operazioni del servizio come metodi nel linguaggio di programmazione [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] scelto, ad esempio Visual Basic o Visual C\#.Qualsiasi applicazione può ospitare un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], inclusa un'applicazione che ospita un servizio.È pertanto possibile creare un servizio che include client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] di altri servizi.  
  
 Un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] può essere generato automaticamente utilizzando [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) e puntandolo a un servizio in esecuzione che pubblica metadati.  
  
 metadati  
 In un servizio, i metadati descrivono le caratteristiche del servizio che un'entità esterna deve comprendere per comunicare con il servizio.I metadati possono essere utilizzati da [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per generare un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e una configurazione abbinata, che possono essere utilizzati da un'applicazione client per interagire con il servizio.  
  
 I metadati esposti dal servizio includono documenti di XML Schema che definiscono il contratto di dati del servizio e documenti WSDL che descrivono i metodi del servizio.  
  
 Se abilitati, i metadati per il servizio vengono generati automaticamente da [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] tramite il controllo del servizio e dei relativi endpoint.Per pubblicare i metadati associati a un servizio occorre abilitarne esplicitamente il comportamento.  
  
 sicurezza  
 In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] include la riservatezza \(crittografia dei messaggi per impedire l'intercettazione\), integrità \(mezzi per il rilevamento di manomissioni del messaggio\), autenticazione \(mezzi per la convalida di server e client\) e autorizzazione \(controllo di accesso alle risorse\).Queste funzioni vengono fornite basandosi sui meccanismi di sicurezza esistenti, ad esempio TLS su HTTP \(anche noto come HTTPS\) o implementando una o più delle varie specifiche di sicurezza WS\-\*.  
  
 modalità di sicurezza del trasporto  
 Specifica che la riservatezza, l'integrità e l'autenticazione vengono fornite da meccanismi a livello del trasporto, ad esempio HTTPS.In caso di utilizzo di un trasporto come HTTPS, questa modalità presenta il vantaggio di essere efficiente in termini di prestazioni e di essere ben compresa grazie alla sua prevalenza su Internet.Lo svantaggio consiste nel fatto che questo tipo di sicurezza viene applicato separatamente su ogni hop nel percorso di comunicazione, rendendo quest'ultima vulnerabile a un attacco di tipo " man in the middle".  
  
 modalità di sicurezza a livello di messaggio  
 Specifica che la sicurezza viene fornita implementando una o più delle relative specifiche, ad esempio la specifica denominata [Web Services Security: SOAP Message Security](http://go.microsoft.com/fwlink/?LinkId=94684) \(la pagina potrebbe essere in inglese\).Ogni messaggio contiene i meccanismi necessari a fornire sicurezza durante il transito e a consentire ai destinatari di rilevare manomissioni e decrittografare i messaggi.A tale scopo, la sicurezza viene incapsulata all'interno di ogni messaggio, fornendo sicurezza end\-to\-end tra più hop.Poiché le informazioni sulla sicurezza diventano parte del messaggio, è inoltre possibile includere più tipi di credenziali nel messaggio, denominati *attestazioni*.Questo approccio presenta inoltre il vantaggio di consentire al messaggio di viaggiare in modo protetto su qualsiasi trasporto, anche se tra l'origine e la destinazione ne esistono diversi.Lo svantaggio di questo approccio consiste nella complessità dei meccanismi di crittografia adottati, con conseguenti implicazioni sulle prestazioni.  
  
 modalità di sicurezza Trasporto con credenziale a livello di messaggio  
 Specifica l'utilizzo del livello trasporto per fornire riservatezza, autenticazione e integrità dei messaggi, mentre ogni messaggio può contenere più credenziali \(attestazioni\) richieste dai destinatari del messaggio.  
  
 WS\-\*  
 Abbreviazione per il set crescente di specifiche Web Service \(WS\), ad esempio WS\-Security, WS\-ReliableMessaging e così via, che sono implementate in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
## Vedere anche  
 [Informazioni su Windows Communication Foundation](../../../docs/framework/wcf/whats-wcf.md)   
 [Architettura di Windows Communication Foundation](../../../docs/framework/wcf/architecture.md)   
 [Security Architecture](http://msdn.microsoft.com/it-it/16593476-d36a-408d-808c-ae6fd483e28f)