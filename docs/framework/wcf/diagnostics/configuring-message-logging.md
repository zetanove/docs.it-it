---
title: "Configurazione della registrazione dei messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "registrazione dei messaggi [WCF]"
ms.assetid: 0ff4c857-8f09-4b85-9dc0-89084706e4c9
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Configurazione della registrazione dei messaggi
In questo argomento viene illustrato come configurare la registrazione dei messaggi per scenari differenti.  
  
## Attivazione della registrazione dei messaggi  
 Per impostazione predefinita, in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] non viene eseguita la registrazione dei messaggi.Per attivarla, è necessario aggiungere un listener di traccia all'origine di traccia `System.ServiceModel.MessageLogging` e impostare gli attributi relativi all'elemento `<messagelogging>` nel file di configurazione.  
  
 Nell'esempio seguente viene illustrato come abilitare la registrazione e specificare opzioni aggiuntive.  
  
```  
<system.diagnostics>  
  <sources>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
                 <add name="messages"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\logs\messages.svclog" />  
          </listeners>  
      </source>  
    </sources>  
</system.diagnostics>  
  
<system.serviceModel>  
  <diagnostics>  
    <messageLogging   
         logEntireMessage="true"   
         logMalformedMessages="false"  
         logMessagesAtServiceLevel="true"   
         logMessagesAtTransportLevel="false"  
         maxMessagesToLog="3000"  
         maxSizeOfMessageToLog="2000"/>  
  </diagnostics>  
</system.serviceModel>  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] impostazioni di registrazione dei messaggi, vedere [Impostazioni consigliate per la traccia e la registrazione dei messaggi](../../../../docs/framework/wcf/diagnostics/tracing/recommended-settings-for-tracing-and-message-logging.md).  
  
 Per specificare il nome e il tipo del listener di traccia che si desidera utilizzare, è possibile utilizzare l'istruzione `add`.Nella configurazione dell'esempio, il listener viene denominato "messages" e come tipo da utilizzare viene aggiunto il listener di traccia standard di .NET Framework, ovvero `System.Diagnostics.XmlWriterTraceListener`.Se si utilizza `System.Diagnostics.XmlWriterTraceListener`, è necessario specificare il percorso e il nome del file di output nel file di configurazione.A tal fine impostare `initializeData` sul nome del file di log.In caso contrario, il sistema genererà un'eccezione.È inoltre possibile implementare un listener personalizzato che genera log in un file predefinito.  
  
> [!NOTE]
>  Poiché la registrazione dei messaggi occupa spazio su disco, è necessario limitare il numero dei messaggi che vengono scritti su disco per un particolare servizio.Una volta raggiunto il limite dei messaggi, viene generata una traccia a livello Informazioni e tutte le attività di registrazione dei messaggi vengono interrotte.  
  
 Il livello di registrazione e le opzioni aggiuntive vengono illustrate nella sezione Livelli di registrazione e opzioni.  
  
 L'attributo `switchValue` di una `source` è valido solo per la traccia.Se si specifica un attributo `switchValue` per l'origine di traccia `System.ServiceModel.MessageLogging` come illustrato di seguito, non si ottiene alcun effetto.  
  
```  
<source name="System.ServiceModel.MessageLogging" switchValue="Verbose">  
```  
  
 Se si desidera disattivare l'origine di traccia, è invece necessario utilizzare gli attributi `logMessagesAtServiceLevel`, `logMalformedMessages` e `logMessagesAtTransportLevel` dell'elemento `messageLogging`.Tali attributi devono essere impostati su `false`.È possibile ottenere questo risultato utilizzando il file di configurazione dell'esempio di codice precedente, attraverso l'interfaccia utente dell'Editor di configurazione o utilizzando WMI.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] strumento Editor di configurazione, vedere [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] WMI, vedere [Utilizzo di Strumentazione gestione Windows \(WMI\) per la diagnostica](../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
## Livelli di registrazione e opzioni  
 Per i messaggi in ingresso, la registrazione avviene immediatamente dopo che il messaggio è stato formato, immediatamente prima che il messaggio raggiunga il codice utente nel livello di servizio e quando vengono rilevati messaggi in formato non valido.  
  
 Per i messaggi in uscita, la registrazione avviene immediatamente dopo che il messaggio esce dal codice utente e immediatamente prima che il messaggio vada in transito.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] i messaggi vengono registrati a due livelli differenti, ovvero a livello di servizio e a livello di trasporto.Vengono inoltre registrati i messaggi in formato non valido.Le tre categorie sono indipendenti l'una dall'altra e possono essere attivate separatamente nella configurazione.  
  
 È possibile controllare il livello di registrazione impostando gli attributi `logMessagesAtServiceLevel`, `logMalformedMessages` e `logMessagesAtTransportLevel` dell'elemento `messageLogging`.  
  
### Livello di servizio  
 I messaggi registrati a questo livello stanno per entrare \(sul lato di ricezione\) o per uscire \(sul lato di invio\) dal codice utente.Se sono stati definiti dei filtri, vengono registrati solo i messaggi che corrispondono a tali filtri.In caso contrario, vengono registrati tutti i messaggi a livello di servizio.A questo livello vengono inoltre registrati i messaggi dell'infrastruttura \(transazioni, canale peer e protezione\), ad eccezione dei messaggi di messaggistica affidabile.Per i messaggi trasmessi come flusso, vengono registrate solo le intestazioni.Inoltre, a questo livello i messaggi protetti vengono registrati in forma decrittografata.  
  
### Livello di trasporto  
 I messaggi registrati a questo livello sono pronti per essere codificati o decodificati prima o dopo il trasporto in transito.Se sono stati definiti dei filtri, vengono registrati solo i messaggi che corrispondono a tali filtri.In caso contrario, vengono registrati tutti i messaggi al livello di trasporto.A questo livello vengono registrati tutti i messaggi dell'infrastruttura, compresi i messaggi di messaggistica affidabile.Per i messaggi trasmessi come flusso, vengono registrate solo le intestazioni.Inoltre, a questo livello i messaggi protetti vengono registrati come crittografati, a meno che non si utilizzi un trasporto protetto come HTTPS.  
  
### Livello dei messaggi in formato non valido  
 I messaggi in formato non valido sono messaggi rifiutati dallo stack [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in qualsiasi fase dell'elaborazione.I messaggi in formato non valido vengono registrati così come sono, vale a dire crittografati se lo sono, con XML non corretto e così via.`maxSizeOfMessageToLog` definisce le dimensioni del messaggio da registrare come CDATA.Per impostazione predefinita, la proprietà `maxSizeOfMessageToLog` è uguale a 256 K.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] questo attributo, vedere la sezione Altre opzioni.  
  
### Altre opzioni  
 Oltre ai livelli di registrazione, l'utente può specificare le opzioni seguenti:  
  
-   Registrazione dell'intero messaggio \(attributo `logEntireMessage`\): questo valore specifica se viene registrato l'intero messaggio \(intestazione e corpo del messaggio\).Il valore predefinito è `false`, ovvero viene registrata solo l'intestazione del messaggio.Questa impostazione influisce sui livelli di registrazione dei messaggi di servizio e di trasporto.  
  
-   Numero massimo di messaggi da registrare \(attributo `maxMessagesToLog`\): questo valore specifica il numero massimo di messaggi da registrare.Tutti i messaggi \(servizio, trasporto e messaggi in formato non valido\) vengono conteggiati fino a tale quota.Una volta raggiunta la quota, viene generata una traccia e non vengono registrati ulteriori messaggi.Il valore predefinito è 10000.  
  
-   Dimensione massima del messaggio da registrare \(attributo `maxSizeOfMessageToLog`\): questo valore specifica la dimensione massima, in byte, dei messaggi da registrare.I messaggi la cui dimensione supera il limite non vengono registrati e per essi non vengono eseguite altre attività.Questa impostazione influisce su tutti i livelli di traccia.Se la traccia del modello di servizio è attiva, viene generata una traccia a livello Avviso al primo punto di registrazione \(ServiceModelSend\* o TransportReceive\) per informarne l'utente.Il valore predefinito per i messaggi a livello di servizio e di trasporto è 256 K, mentre il valore predefinito per i messaggi in formato non valido è 4 K.  
  
    > [!CAUTION]
    >  La dimensione del messaggio calcolata per eseguire il confronto con `maxSizeOfMessageToLog` corrisponde alla dimensione del messaggio in memoria prima della serializzazione.Questa dimensione può essere diversa dalla lunghezza effettiva della stringa di messaggio da registrare e in molti casi è maggiore della dimensione effettiva.Di conseguenza, dei messaggi potrebbero non essere registrati.Per intervenire su tale situazione, è possibile specificare per l'attributo `maxSizeOfMessageToLog` un valore del 10% maggiore rispetto alla dimensione prevista dei messaggi.Inoltre, se si registrano messaggi in formato non valido, lo spazio su disco effettivo utilizzato dai log dei messaggi può essere fino a 5 volte maggiore della dimensione del valore specificato da `maxSizeOfMessageToLog`.  
  
 Se non si definisce alcun listener di traccia nel file di configurazione, non viene generato alcun output di registrazione, indipendentemente dal livello di registrazione specificato.  
  
 Le opzioni di registrazione dei messaggi, ad esempio gli attributi descritti in questa sezione, possono essere modificati a runtime utilizzando Strumentazione gestione Windows \(WMI, Windows Management Instrumentation\).Tale operazione può essere eseguita accedendo all'istanza [AppDomainInfo](../../../../docs/framework/wcf/diagnostics/wmi/appdomaininfo.md), che espone le proprietà booleane `LogMessagesAtServiceLevel`, `LogMessagesAtTransportLevel` e `LogMalformedMessages`.Pertanto, se si configura un listener di traccia per la registrazione dei messaggi, ma si impostano queste opzioni su `false` nella configurazione, è possibile in seguito modificarle in `true` quando l'applicazione è in esecuzione.In questo modo viene abilitata la registrazione dei messaggi al runtime.Analogamente, se si abilita la registrazione dei messaggi nel file di configurazione, è possibile disabilitarla al runtime utilizzando WMI.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Utilizzo di Strumentazione gestione Windows \(WMI\) per la diagnostica](../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
 Nel campo `source` di un log di messaggi viene specificato il contesto in cui il messaggio viene registrato: durante l'invio\/ricezione di un messaggio di richiesta, per una request\-reply o una richiesta unidirezionale, a livello di modello di servizio o di trasporto o in caso di messaggio in formato non valido.  
  
 Per i messaggi in formato non valido, `source`  corrisponde a `Malformed`.In caso contrario, l'origine ha i valori seguenti in base al contesto.  
  
 Per request\/reply  
  
||Invio richiesta|Ricezione richiesta|Invio risposta|Ricezione risposta|  
|-|---------------------|-------------------------|--------------------|------------------------|  
|Livello del modello di servizio|Servizio<br /><br /> Livello<br /><br /> Invia<br /><br /> Richiesta|Servizio<br /><br /> Livello<br /><br /> Receive<br /><br /> Richiesta|Servizio<br /><br /> Livello<br /><br /> Invia<br /><br /> Reply|Servizio<br /><br /> Livello<br /><br /> Receive<br /><br /> Reply|  
|Livello di trasporto|Transport<br /><br /> Invia|Transport<br /><br /> Receive|Transport<br /><br /> Invia|Transport<br /><br /> Receive|  
  
 Per richiesta unidirezionale  
  
||Invio richiesta|Ricezione richiesta|  
|-|---------------------|-------------------------|  
|Livello del modello di servizio|Servizio<br /><br /> Livello<br /><br /> Invia<br /><br /> Datagram|Servizio<br /><br /> Livello<br /><br /> Receive<br /><br /> Datagram|  
|Livello di trasporto|Transport<br /><br /> Send|Transport<br /><br /> Receive|  
  
## Filtri messaggi  
 I filtri dei messaggi vengono definiti nell'elemento di configurazione `messageLogging` della sezione di configurazione `diagnostics`.Essi vengono applicati a livello di servizio e di trasporto.Quando sono definiti uno o più filtri, solo i messaggi che corrispondono almeno a uno dei filtri vengono registrati.Se non è definito alcun filtro, passeranno tutti i messaggi.  
  
 I filtri supportano la sintassi Xpath completa e sono applicati nell'ordine in cui vengono visualizzati nel file di configurazione.Un filtro sintatticamente errato determina un'eccezione di configurazione.  
  
 I filtri forniscono anche una funzionalità di sicurezza mediante l'attributo `nodeQuota`, che limita il numero massimo di nodi nel DOM XPath che possono essere esaminati per la corrispondenza al filtro.  
  
 Nell'esempio seguente viene illustrato come configurare un filtro che registra solo messaggi con una sezione intestazione SOAP.  
  
```  
<messageLogging logEntireMessage="true"  
    logMalformedMessages="true"   
    logMessagesAtServiceLevel="true"  
    logMessagesAtTransportLevel="true"  
    maxMessagesToLog="420">  
    <filters>  
        <add nodeQuota="10" xmlns:soap="http://www.w3.org/2003/05/soap-envelope">  
                 /soap:Envelope/soap:Header  
        </add>  
     </filters>  
</messageLogging>  
```  
  
 Non è possibile applicare filtri al corpo di un messaggio.I filtri che tentano di manipolare il corpo di un messaggio vengono rimossi dall'elenco dei filtri.In questo caso verrà anche generato un evento.Ad esempio, il filtro seguente verrebbe rimosso dalla tabella dei filtri.  
  
```  
<add xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">/s:Envelope/s:Body[contains(text(), "Hello")]</add>  
```  
  
## Configurazione di un listener personalizzato  
 È possibile configurare un listener personalizzato con opzioni aggiuntive.Un listener personalizzato può essere utile per filtrare informazioni personali specifiche dell'applicazione dai messaggi prima della registrazione.Nell'esempio seguente viene illustrata la configurazione di un listener personalizzato.  
  
```  
<system.diagnostics>  
   <sources>  
     <source name="System.ServiceModel.MessageLogging">  
           <listeners>  
             <add name="MyListener"   
                    type="YourCustomListener"  
                    initializeData="c:\logs\messages.svclog"  
                    maxDiskSpace="1000"/>  
           </listeners>  
     </source>  
   </sources>  
</system.diagnostics>  
```  
  
 È necessario tenere presente che l'attributo `type` deve essere impostato su un nome di assembly completo del tipo.  
  
## Vedere anche  
 [\<messageLogging\>](../../../../docs/framework/configure-apps/file-schema/wcf/messagelogging.md)   
 [Registrazione messaggi](../../../../docs/framework/wcf/diagnostics/message-logging.md)   
 [Impostazioni consigliate per la traccia e la registrazione dei messaggi](../../../../docs/framework/wcf/diagnostics/tracing/recommended-settings-for-tracing-and-message-logging.md)