---
title: "Protocolli di messaggistica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5b20bca7-87b3-4c8f-811b-f215b5987104
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Protocolli di messaggistica
Lo stack di canali di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilizza canali di codifica e di trasporto per trasformare le rappresentazioni interne dei messaggi nel relativo formato di trasmissione e quindi per inviare i dati così ottenuti mediante un trasporto specifico.Il trasporto più comunemente utilizzato per garantire l'interoperabilità dei servizi Web è il protocollo HTTP, mentre le codifiche utilizzate dai servizi Web sono in genere SOAP 1.1 basato su XML, SOAP 1.2 e il protocollo MTOM \(Message Transmission Optimization Mechanism, meccanismo di ottimizzazione della trasmissione dei messaggi\).  
  
 Questo argomento descrive i dettagli di implementazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] relativi ai protocolli elencati di seguito utilizzati dalla classe <xref:System.ServiceModel.Channels.HttpTransportBindingElement>. Nota: la documentazione seguente potrebbe essere in inglese.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|HTTP 1.1|http:\/\/www.ietf.org\/rfc\/rfc2616.txt|  
|Associazione SOAP 1.1 HTTP|http:\/\/www.w3.org\/TR\/2000\/NOTE\-SOAP\-20000508\/, sezione 7|  
|Associazione SOAP 1.2 HTTP|http:\/\/www.w3.org\/TR\/soap12\-part2\/, sezione 7|  
  
 Questo argomento descrive i dettagli di implementazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] relativi ai protocolli elencati di seguito utilizzati dalle classi <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> e <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>. Nota: la documentazione seguente potrebbe essere in inglese.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|XML|http:\/\/www.w3.org\/TR\/REC\-xml|  
|SOAP 1.1|http:\/\/www.w3.org\/TR\/2000\/NOTE\-SOAP\-20000508\/|  
|Specifica di base di SOAP 1.2|http:\/\/www.w3.org\/TR\/soap12\-part1\/|  
|WS\-Addressing 2004\/08|http:\/\/www.w3.org\/Submission\/2004\/SUBM\-ws\-addressing\-20040810\/|  
|Specifica di base di W3C Web Services Addressing 1.0|http:\/\/www.w3.org\/TR\/2006\/REC\-ws\-addr\-core\-20060509|  
|W3C Web Services Addressing 1.0 con associazione SOAP|http:\/\/www.w3.org\/TR\/2006\/REC\-ws\-addr\-soap\-20060509|  
|W3C Web Services Addressing 1.0 con associazione WSDL|http:\/\/www.w3.org\/TR\/2006\/CR\-ws\-addr\-wsdl\-20060529\/|  
|W3C Web Services Addressing 1.0 \- Metadata|http:\/\/www.w3.org\/TR\/ws\-addr\-metadata\/|  
|WSDL SOAP1.1 Binding|http:\/\/www.w3.org\/TR\/wsdl\/|  
|WSDL SOAP1.2 Binding|http:\/\/www.w3.org\/Submission\/wsdl11soap12\/|  
  
 Questo argomento descrive i dettagli di implementazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] relativi ai protocolli elencati di seguito utilizzati dalla classe <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>. Nota: la documentazione seguente potrebbe essere in inglese.  
  
|Specifica\/documento|Collegamento|  
|--------------------------|------------------|  
|XOP|http:\/\/www.w3.org\/TR\/xop10\/|  
|Associazione MTOM SOAP 1.2|http:\/\/www.w3.org\/TR\/soap12\-mtom\/|  
|Associazione MTOM SOAP 1.1|http:\/\/www.w3.org\/Submission\/soap11mtom10\/|  
|Asserzione di WS\-Policy relativa a MTOM|http:\/\/www.w3.org\/Submission\/2006\/SUBM\-WS\-MTOMPolicy\-20061101\/.|  
  
 In questo argomento vengono utilizzati gli spazi dei nomi XML e i relativi prefissi associati seguenti.  
  
|Prefisso|URI \(Uniform Resource Identifier\) dello spazio dei nomi|  
|--------------|---------------------------------------------------------------|  
|s11|http:\/\/schemas.xmlsoap.org\/soap\/envelope|  
|s12|http:\/\/www.w3.org\/2003\/05\/soap\-envelope|  
|wsa|http:\/\/www.w3.org\/2004\/08\/addressing|  
|wsam|http:\/\/www.w3.org\/2007\/05\/addressing\/metadata|  
|wsap|http:\/\/schemas.xmlsoap.org\/ws\/2004\/09\/policy\/addressing|  
|wsa10|http:\/\/www.w3.org\/2005\/08\/addressing|  
|wsaw10|http:\/\/www.w3.org\/2006\/05\/addressing\/wsdl|  
|xop|http:\/\/www.w3.org\/2004\/08\/xop\/include|  
|xmime|http:\/\/www.w3.org\/2004\/06\/xmlmime<br /><br /> http:\/\/www.w3.org\/2005\/05\/xmlmime|  
|cdp|http:\/\/schemas.microsoft.com\/net\/2006\/06\/duplex|  
  
## SOAP 1.1 e SOAP 1.2  
  
### Modello di elaborazione della envelope  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa l'elaborazione della SOAP 1.1 envelope attenendosi alle specifiche Basic Profile 1.1 \(BP11\) e Basic Profile 1.0 \(SSBP10\).L'elaborazione della SOAP 1.2 envelope viene implementata attenendosi alla specifica SOAP12\-Part1.  
  
 In questa sezione vengono descritte alcune scelte di implementazione previste in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] relativamente alle specifiche BP11 e SOAP12\-Part1.  
  
#### Elaborazione obbligatoria delle intestazioni  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] elabora le intestazioni `mustUnderstand` attenendosi alle regole descritte nelle specifiche SOAP 1.1 e SOAP 1.2, con le variazioni seguenti.  
  
 Un messaggio che viene inserito nello stack di canali di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene elaborato da canali specifici configurati in base ai relativi elementi di associazione, ad esempio gli elementi relativi alla codifica dei messaggi di testo, alla sicurezza, alla messaggistica affidabile e alle transazioni.Ogni canale riconosce le intestazioni dallo spazio dei nomi associato e le contrassegna come riconosciute.Dopo l'inserimento di un messaggio nel dispatcher, il formattatore dell'operazione legge le intestazioni previste dal contratto di messaggio\/operazione corrispondente e le contrassegna come riconosciute.Quindi, il dispatcher verifica se esistono intestazioni non riconosciute ma la cui intestazione `mustUnderstand` richiede il riconoscimento e, in tal caso, genera un'eccezione.I messaggi che contengono intestazioni `mustUnderstand` indirizzate al destinatario non vengono elaborati dal codice dell'applicazione di destinazione.  
  
 Questo tipo di elaborazione a livelli consente la separazione fra i livelli di infrastruttura e livelli di applicazione del nodo SOAP:  
  
-   B1111: le intestazioni non riconosciute vengono rilevate dopo l'elaborazione del messaggio da parte dello stack di canali dell'infrastruttura di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ma prima dell'elaborazione del messaggio da parte dell'applicazione  
  
     Il valore dell'intestazione `mustUnderstand` differisce tra SOAP 1.1 e SOAP 1.2.Basic Profile 1.1 richiede che il valore di `mustUnderstand` sia 0 o 1 per i messaggi SOAP 1.1.La specifica di SOAP 1.2, oltre ai valori 0 e 1, prevede inoltre i valori `false` e `true`. Tuttavia, tale specifica consiglia di applicare una rappresentazione canonica dei valori `xs:boolean`, ovvero `false` e `true`.  
  
-   B1112: in entrambe le versioni 1.1 e 1.2 della SOAP envelope, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] prevede i valori 0 e 1 per `mustUnderstand`.Inoltre, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] accetta l'intero spazio dei valori `xs:boolean` per l'intestazione `mustUnderstand`, ovvero, 0, 1, `false` e `true`.  
  
#### Errori SOAP  
 L'elenco seguente contiene le implementazioni degli errori SOAP specifiche di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   B2121: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] restituisce i codici di errore SOAP 1.1 seguenti: `s11:mustUnderstand`, `s11:Client`e `s11:Server`.  
  
-   B2122: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] restituisce i codici di errore SOAP 1.2 seguenti: `s12:MustUnderstand`, `s12:Sender`e `s12:Receiver`.  
  
### Associazione HTTP  
  
#### Associazione SOAP 1.1 HTTP  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa l'associazione SOAP 1.1 HTTP attenendosi alla sezione 3.4 della specifica Basic Profile 1.1, con le precisazioni seguenti:  
  
-   B2211: il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non implementa il reindirizzamento di richieste HTTP POST.  
  
-   B2212: i client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supportano i cookie HTTP in conformità alla sezione 3.4.8.  
  
#### Associazione SOAP 1.2 HTTP  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa l'associazione SOAP 1.2 HTTP attenendosi alla specifica SOAP 1.2\-part 2 \(SOAP12Part2\), con le precisazioni seguenti:  
  
 SOAP 1.2 introduce un nuovo parametro Action facoltativo per il tipo di supporto `application/soap+xml`.Questo parametro è utile per ottimizzare l'invio dei messaggi in quanto elimina l'esigenza di analizzare il corpo del messaggio SOAP quando non si utilizza la specifica WS\-Addressing.  
  
-   R2221: il parametro Action `application/soap+xml`, quando presente in una richiesta SOAP 1.2, deve corrispondere all'attributo `soapAction` dell'elemento `wsoap12:operation` contenuto nell'associazione WSDL corrispondente.  
  
-   R2222: il parametro Action `application/soap+xml`, quando presente in un messaggio SOAP 1.2, deve corrispondere all'elemento `wsa:Action` quando si utilizza la specifica WS\-Addressing 2004\/08 o la specifica WS\-Addressing 1.0.  
  
 Quando la specifica WS\-Addressing è disabilitata e in una richiesta in ingresso non è incluso alcun parametro Action, il parametro `Action` del messaggio viene considerato come non specificato.  
  
## WS\-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di implementare 3 versioni di WS\-Addressing:  
  
-   WS\-Addressing 2004\/08  
  
-   Specifica di base di W3C Web Services Addressing 1.0 \(ADDR10\-CORE\) e associazione SOAP \(ADDR10\-SOAP\)  
  
-   WS\-Addressing 1.0 \- Metadata  
  
### Riferimenti a endpoint  
 In tutte le versioni di WS\-Addressing implementate da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono utilizzati i riferimenti a endpoint per descrivere gli endpoint.  
  
#### Utilizzo dei riferimenti a endpoint con le versioni di WS\-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa diversi protocolli di infrastruttura \(ad esempio WS\-ReliableMessaging, WS\-SecureConversation e WS\-Trust\) che utilizzano WS\-Addressing e in particolare l'elemento `EndpointReference` e la classe `W3C.WsAddressing.EndpointReferenceType`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta l'utilizzo di una delle due versioni di WS\-Addressing con gli altri protocolli di infrastruttura.Per ogni endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è consentito utilizzare una sola versione di WS\-Addressing.  
  
 R3111: lo spazio dei nomi dell'elemento `EndpointReference` o del tipo utilizzato nei messaggi scambiati con un endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] deve corrispondere alla versione di WS\-Addressing implementata da tale endpoint.  
  
 Ad esempio, se un endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa il protocollo WS\-ReliableMessaging, l'intestazione `AcksTo` restituita da tale endpoint nella risposta `CreateSequenceResponse` utilizza la versione di WS\-Addressing specificata dall'associazione `EncodingBinding` per tale endpoint.  
  
#### Utilizzo dei riferimenti a endpoint con i metadati  
 Diversi scenari richiedono la comunicazione di metadati o di riferimenti a metadati relativi a un dato endpoint.  
  
 B3121: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza i meccanismi descritti nella sezione 6 della specifica MEX \(WS\-MetadataExchange\) per includere metadati associati a riferimenti per valore o per riferimento a un determinato endpoint.  
  
 Si consideri lo scenario in cui un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede l'autenticazione tramite un token SAML \(Security Assertions Markup Language\) emesso dall'emittente di token all'indirizzo http:\/\/sts.fabrikam123.com.L'endpoint [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] descrive questo requisito di autenticazione utilizzando un'asserzione `sp:IssuedToken` avente un'asserzione `sp:Issuer` annidata che punta all'emittente di token.Le applicazioni client che accedono all'asserzione `sp:Issuer` devono conoscere la modalità di comunicazione con l'endpoint dell'emittente di token.In particolare, il client deve conoscere i metadati relativi all'emittente di token.Utilizzando le estensioni di metadati di riferimento a endpoint definite in MEX, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un riferimento ai metadati del mittente di token.  
  
```  
<sp:IssuedToken>  
  <sp:Issuer>  
    <wsa10:Address>  
      http://sts.fabrikam123.com  
    </wsa10:Address>  
    <wsa10:Metadata>  
      <mex:Metadata>  
        <mex:MetadataSection>  
          <mex:MetadataReference>  
            <wsa10:Address>  
              http://sts.fabrikam123.com/mex  
            </wsa10:Address>  
          </mex:MetadataReference>  
        </mex:MetadataSection>  
      </mex:Metadata>  
    </wsa10:Metadata>  
  </sp:Issuer>  
</sp:IssuedToken>  
  
```  
  
### Intestazioni di indirizzamento dei messaggi  
  
#### Intestazioni del messaggio  
 Per entrambe le versioni di WS\-Addressing, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono utilizzate le intestazioni di messaggio elencate di seguito come previsto dalle specifiche `wsa:To`, `wsa:ReplyTo`, `wsa:Action`, `wsa:MessageID`,e `wsa:RelatesTo`.  
  
 B3211: per tutte le versioni di WS\-Addressing, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono rispettate, senza tuttavia crearle da zero, le intestazioni di messaggio di WS\-Addressing `wsa:FaultTo` e `wsa:From`.  
  
 Le applicazioni che interagiscono con le applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possono aggiungere queste intestazioni di messaggio, che quindi verranno elaborate di conseguenza da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
#### Parametri e proprietà dei riferimenti  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa l'elaborazione dei parametri e delle proprietà dei riferimenti a endpoint  
  
 in conformità alle rispettive specifiche.  
  
 B3221: quando configurati per utilizzare la specifica WS\-Addressing 2004\/08, gli endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] elaborano le proprietà dei riferimenti e i parametri dei riferimenti allo stesso modo.  
  
### Modelli di scambio dei messaggi  
 La sequenza dei messaggi coinvolti nella chiamata all'operazione del servizio Web è detta *modello di scambio dei messaggi*.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta i modelli di scambio dei messaggi unidirezionale, richiesta\-risposta e duplex.Questa sezione descrive i requisiti della specifica WS\-Addressing che definiscono il modo in cui il modello di scambio dei messaggi utilizzato influisce sull'elaborazione dei messaggi.  
  
 In questa sezione, il richiedente invia il primo messaggio e il risponditore riceve il primo messaggio.  
  
#### Modello unidirezionale  
 Quando un endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene configurato per supportare messaggi aventi un determinato parametro `Action` in modo da applicare un modello unidirezionale, tale endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si attiene ai comportamenti e ai requisiti elencati di seguito.A meno che non vengano specificati diversamente, i comportamenti e le regole riguardano entrambe le versioni di WS\-Addressing supportate in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   R3311: il richiedente deve includere gli elementi `wsa:To` e `wsa:Action` nonché le intestazioni di tutti i parametri specificati nel riferimento a endpoint.Quando si utilizza la specifica WS\-Addressing 2004\/08 e il riferimento a endpoint specifica le proprietà di riferimento \[reference properties\], occorre aggiungere al messaggio anche le intestazioni corrispondenti.  
  
-   B3312: il richiedente può includere le intestazioni `MessageID` e `ReplyTo` e `FaultTo`.Dopo essere stati ignorati dall'infrastruttura del destinatario, questi elementi vengono passati all'applicazione.  
  
-   R3313: quando si utilizza il protocollo HTTP e non viene inviato alcun messaggio sul canale di risposta HTTP, il risponditore deve inviare una risposta HTTP contenente un corpo vuoto e un codice di stato HTTP 202.  
  
     Quando si utilizza il trasporto HTTP e il contratto dell'operazione dichiara un messaggio unidirezionale, la risposta HTTP può comunque essere utilizzata per l'invio di messaggi di infrastruttura. Ad esempio, la funzionalità di messaggistica affidabile può inviare un messaggio `SequenceAcknowledgement` in una risposta HTTP.  
  
-   B3314: il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non invia alcun messaggio di errore in risposta a un messaggio unidirezionale.  
  
#### Modello richiesta\-risposta  
 Quando un endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene configurato per supportare messaggi aventi un determinato parametro `Action` in modo da applicare un modello richiesta\-risposta, tale endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si attiene ai comportamenti e ai requisiti elencati di seguito.A meno che non vengano specificati diversamente, i comportamenti e le regole riguardano entrambe le versioni di WS\-Addressing supportate in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   R3321: il richiedente deve includere nella richiesta gli elementi `wsa:To`, `wsa:Action` e `wsa:MessageID` nonché le intestazioni di tutti i \[parametri di riferimento\] o le \[proprietà di riferimento\] \(o entrambi\) specificati nel riferimento a endpoint.  
  
-   R3322: quando si utilizza la specifica WS\-Addressing 2004\/08, nella richiesta deve essere incluso anche l'elemento `ReplyTo`.  
  
-   R3323: se quando si utilizza la specifica WS\-Addressing 1.0 la richiesta non contiene alcun elemento `ReplyTo`, tale elemento viene impostato su un riferimento a endpoint predefinito in cui la proprietà \[address\] è uguale a "http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous".  
  
-   R3321: il richiedente deve includere nel messaggio di risposta le intestazioni `wsa:To`, `wsa:Action` e `wsa:RelatesTo` nonché le intestazioni di tutti i parametri di riferimento \[reference parameters\] o di tutte le proprietà di riferimento \[reference properties\] \(o entrambi\) specificati nel riferimento a endpoint `ReplyTo` contenuto nella richiesta.  
  
### Errori di indirizzamento dei servizi Web  
 R3411: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera gli errori seguenti definiti nella specifica WS\-Addressing 2004\/08.  
  
|Codice|Causa|  
|------------|-----------|  
|wsa:DestinationUnreachable|Il messaggio in ingresso presenta un riferimento `ReplyTo` diverso dall'indirizzo per risposte definito per questo canale. Non esiste alcun endpoint in attesa presso l'indirizzo specificato nell'intestazione di destinazione.|  
|wsa:ActionNotSupported|I canali dell'infrastruttura o il dispatcher associato all'endpoint non riconoscono l'azione specificata nell'intestazione `Action`.|  
  
 R3412: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera gli errori seguenti definiti nella specifica WS\-Addressing 1.0.  
  
|Codice|Causa|  
|------------|-----------|  
|wsa10:InvalidAddressingHeader|Elemento `wsa:To`, `wsa:ReplyTo`, `wsa:From` o `wsa:MessageID` duplicato.Elemento `wsa:RelatesTo`  duplicato avente lo stesso tipo `RelationshipType`.|  
|wsa10:MessageAddressingHeaderRequired|L'intestazione obbligatoria di indirizzamento è mancante.|  
|wsa10:DestinationUnreachable|Il messaggio in ingresso presenta un riferimento `ReplyTo` diverso dall'indirizzo per risposte definito per questo canale.Non esiste alcun endpoint in attesa presso l'indirizzo specificato nell'intestazione di destinazione.|  
|wsa10:ActionNotSupported|I canali dell'infrastruttura o il dispatcher associato all'endpoint non riconoscono l'azione specificata nell'intestazione `Action`.|  
|wsa10:EndpointUnavailable|Il canale RM restituisce questo errore per indicare che l'endpoint non elaborerà la sequenza basata sull'esame delle intestazioni di indirizzamento del messaggio `CreateSequence`.|  
  
 Il codice delle tabelle precedenti viene mappato al codice `FaultCode` in SOAP 1.1 e al codice `SubCode` \(in cui il codice corrisponde al mittente\) in SOAP 1.2.  
  
### Utilizzo di associazioni WSDL 1.1 con le asserzioni di WS\-Policy  
  
#### Definizione dell'uso di WS\-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le asserzioni di criteri per indicare il supporto di endpoint relativamente a una determinata versione di WS\-Addressing.  
  
 L'asserzione di criteri seguente contiene il soggetto dei criteri di endpoint \[WS\-PA\] e indica che i messaggi scambiati con l'endpoint devono utilizzare la specifica WS\-Addressing 2004\/08.  
  
```  
<wsap:UsingAddressing />  
```  
  
 Questa asserzione di criteri si aggiunge alla specifica WS\-Addressing 2004\/08.  
  
 Tramite l'asserzione di criteri seguente viene indicato che nei messaggi inviati\/ricevuti deve essere utilizzato WS\-Addressing 1.0.  
  
```vb  
<wsam:Addressing/>   
```  
  
 Nell'asserzione di criteri seguente è incluso un soggetto dei criteri di endpoint \[WS\-PA\] e viene indicato che nei messaggi scambiati con l'endpoint deve essere utilizzata la specifica WS\-Addressing 2004\/08.  
  
```  
<wsaw10:UsingAddressing />  
```  
  
 L'elemento `wsaw10:UsingAddressing` è preso in prestito da \[WS\-Addressing\-WSDL\] e viene utilizzato nel contesto di WS\-Policy in conformità alla sezione 3.1.2 di tale specifica.  
  
 L'utilizzo dell'intestazione di indirizzamento non modifica la semantica delle associazioni WSDL 1.1 HTTP, SOAP 1.1 HTTP e SOAP 1.2 HTTP.Ad esempio, se si prevede una risposta a una richiesta inviata a un endpoint in cui vengono utilizzati WS\-Addressing e l'associazione WSDL SOAP 1.x HTTP, la risposta deve essere inviata tramite la risposta HTTP.  
  
 Per le risposte inviate tramite la risposta http, l'asserzione WS\-AM è:  
  
```xml  
<wsam:AnonymousResponses/>  
```  
  
 L'asserzione di criteri completa potrebbe essere simile alla seguente:  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
        <wsam:AnonymousResponses />   
    </wsp:Policy>  
</wsam:Addressing>  
```  
  
 Tuttavia, sono presenti modelli di scambio dei messaggi che traggono profitto dalla presenza di due connessioni HTTP opposte indipendenti stabilite tra il richiedente e il risponditore, ad esempio i messaggi unidirezionali non richiesti inviati dal risponditore.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è disponibile una funzionalità grazie alle quale due canali di trasporto sottostanti possono formare un canale duplex composito in cui un canale viene utilizzato per i messaggi di input e l'altro per quelli di output.Nel caso del trasporto HTTP, il modello duplex composito offre due connessioni HTTP opposte.Il richiedente utilizza una connessione per inviare i messaggi al risponditore, mentre quest'ultimo utilizza l'altra connessione per inviare i messaggi di risposta al richiedente.  
  
 Per le risposte inviate tramite richieste http distinte, l'asserzione ws\-am è:  
  
```xml  
<wsam:NonAnonymousResponses/>  
```  
  
 L'asserzione di criteri completa potrebbe essere simile alla seguente:  
  
```xml  
<wsam:Addressing>  
    <wsp:Policy>  
      <wsam:NonAnonymousResponses />   
   </wsp:Policy>  
  </wsam:Addressing>  
```  
  
 Per l'utilizzo dell'asserzione seguente che presenta il soggetto dei criteri di endpoint \[WS\-PA\] negli endpoint in cui vengono utilizzate le associazioni SOAP 1.x HTTP WSDL 1.1 sono richieste due connessioni HTTP opposte e distinte da utilizzare rispettivamente per i messaggi dal richiedente al risponditore e dal risponditore al richiedente.  
  
```  
<cdp:CompositeDuplex/>  
```  
  
 L'istruzione precedente comporta i requisiti seguenti per l'intestazione `wsa:ReplyTo` dei messaggi di richiesta:  
  
-   R3514: se l'endpoint utilizza un'associazione WSDL 1.1 SOAP 1.x HTTP e dispone di un'alternativa criteri avente un'asserzione `wsap10:UsingAddressing` o un'asserzione `wsap:UsingAddressing` associata a un elemento `cdp:CompositeDuplex`, i messaggi di richiesta inviati a un endpoint devono presentare un'intestazione `ReplyTo` in cui la proprietà `[address]` sia diversa da "http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous".  
  
-   R3515: se l'endpoint utilizza un'associazione WSDL 1.1 SOAP 1.x HTTP e dispone di un'alternativa criteri avente un'asserzione `wsap10:UsingAddressing` senza alcuna asserzione `cdp:CompositeDuplex` associata, i messaggi di richiesta inviati a un endpoint non devono presentare alcuna intestazione `ReplyTo` oppure devono presentare un'intestazione `ReplyTo` in cui la proprietà `[address]` sia uguale a "http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous".  
  
-   R3516: se l'endpoint utilizza un'associazione WSDL 1.1 SOAP 1.x HTTP e dispone di un'alternativa criteri avente un'asserzione `wsap:UsingAddressing` e nessun elemento `cdp:CompositeDuplex` associato, i messaggi di richiesta inviati a un endpoint devono presentare un'intestazione `ReplyTo` in cui la proprietà `[address]` sia uguale a "http:\/\/www.w3.org\/2005\/08\/addressing\/anonymous".  
  
 La specifica WS\-Addressing WSDL tenta di descrivere associazioni del protocollo simili introducendo un elemento `<wsaw:Anonymous/>` con tre valori testuali \(obbligatorio, facoltativo e proibito\) per indicare requisiti nell'intestazione `wsa:ReplyTo` \(sezione 3.2\).Sfortunatamente, tale definizione dell'elemento non è utilizzabile in modo specifico nel contesto di WS\-Policy, perché richiede estensioni specifiche di dominio per supportare l'intersezione di alternative che utilizzano tale elemento come asserzione.A differenza del comportamento di endpoint in transito, che rende il valore dell'intestazione `ReplyTo` specifico del trasporto HTTP, il suddetto elemento indica questo valore senza associarlo a un determinato protocollo.  
  
#### Definizione dell'attributo Action  
 La specifica WS\-Addressing 2004\/08 definisce un attributo `wsa:Action` per gli elementi `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]`.L'associazione WS\-Addressing 1.0 WSDL \(WS\-ADDR10\-WSDL\) definisce un attributo simile, ovvero `wsaw10:Action`.  
  
 L'unica differenza consiste nella semantica del modello Action predefinito, descritta rispettivamente nella sezione 3.3.2 della specifica WS\-ADDR e nella sezione 4.4.4 della specifica WS\-ADDR10\-WSDL.  
  
 È ammissibile avere due endpoint aventi lo stesso attributo `portType` \(ossia lo stesso contratto, usando la terminologia di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\) ma versioni diverse di WS\-Addressing.Tuttavia, se l'attributo Action è definito dall'attributo `portType` e deve essere condiviso da tutti gli endpoint che implementano l'attributo `portType`, risulta impossibile supportare entrambi i modelli Action predefiniti.  
  
 Per risolvere questa problematica, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta una sola versione dell'attributo `Action`.  
  
 B3521: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'attributo `wsaw10:Action` degli elementi `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` in conformità alla specifica WS\-ADDR10\-WSDL per determinare l'URI dell'attributo `Action` relativo ai messaggi corrispondenti indipendentemente dalla versione di WS\-Addressing utilizzata dall'endpoint.  
  
#### Utilizzare il riferimento a endpoint nell'elemento wsdl:port  
 La sezione 4.1 di WS\-ADDR10\-WSDL estende l'elemento `wsdl:port` per includere l'elemento figlio `<wsa10:EndpointReference…/>` allo scopo di descrivere l'endpoint in termini di WS\-Addressing.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] estende questa utilità in WS\-Addressing 2004\/08, consentendo di visualizzare `<wsa:EndpointReference…/>` come elemento figlio di `wsdl:port`.  
  
-   R3531: se a un endpoint è associata un'alternativa criteri avente un'asserzione di criteri `<wsaw10:UsingAddressing/>``wsdl:port, l'elemento` `<wsa10:EndpointReference …/> corrispondente può contenere un elemento figlio` .  
  
-   R3532: se un elemento `wsdl:port` contiene un elemento figlio `<wsa10:EndpointReference …/>``wsa10:EndpointReference/wsa10:Address, il valore dell'elemento figlio` `@address deve corrispondere al valore dell'attributo` `wsdl:port dell'elemento` `wsdl:location/` di pari livello.  
  
-   R3533: se a un endpoint è associata un'alternativa criteri avente un'asserzione di criteri `<wsap:UsingAddressing/>``wsdl:port, l'elemento` `<wsa:EndpointReference …/> corrispondente può contenere un elemento figlio` .  
  
-   R3534: se un elemento `wsdl:port` contiene un elemento figlio `<wsa:EndpointReference …/>``wsa:EndpointReference/wsa:Address, il valore dell'elemento figlio` `@address deve corrispondere al valore dell'attributo` `wsdl:port dell'elemento` `wsdl:location/` di pari livello.  
  
### Integrazione con WS\-Security  
 Secondo le sezioni di WS\-ADDR e WS\-ADDR10 relative alle considerazioni sulla sicurezza, è consigliabile firmare tutte le intestazioni dei messaggi di indirizzamento insieme al corpo del messaggio, in modo da associarli fra loro.  
  
 Quando si utilizza WS\-Security per garantire l'integrità dei messaggi, le intestazioni dei messaggi di WS\-Addressing nonché le intestazioni ottenute dai parametri o dalle proprietà del riferimento \(o da entrambi\) devono essere firmate insieme al corpo del messaggio.  
  
### Esempi  
  
#### Modello unidirezionale  
 In questo scenario, il mittente invia un messaggio unidirezionale al destinatario.Vengono utilizzate le specifiche SOAP 1.2, HTTP 1.1 e W3C WS\-Addressing 1.0.  
  
 Struttura dei messaggi di richiesta: le intestazioni dei messaggi includono gli elementi `wsa10:To` e `wsa10:Action`.Il corpo dei messaggi include un elemento `<app:Ping>` specifico dello spazio dei nomi dell'applicazione.  
  
 Intestazioni HTTP: la destinazione indicata in POST corrisponde all'URI specificato nell'elemento `wsa10:To` .  
  
 L'intestazione Content\-Type dispone del valore di `application/soap+xml` come richiesto da SOAP 1.2.I parametri `charset` e `action` sono inclusi.Il parametro `action` dell'intestazione Content\-Type corrisponde al valore dell'intestazione dei messaggi `wsa10:Action`.  
  
```  
POST http://fabrikam123.com/Service HTTP/1.1  
Content-Type: application/soap+xml; charset=utf-8;    
              action="http://fabrikam123.com/Service/OneWay"  
Host: 131.107.72.15  
Content-Length: 1501  
Expect: 100-continue  
Proxy-Connection: Keep-Alive  
<s12:Envelope>  
  <s12:Header>  
    <wsa10:To s12:mustUnderstand="1">  
        http://fabrikam123.com/Service  
    </wsa10:To>  
    <wsa10:Action s12:mustUnderstand="1">  
        http://fabrikam123.com/Service/OneWay   
    </wsa10:Action>  
  </s12:Header>  
  <s12:Body>  
    <Ping xmlns="http://fabrikam123.com/Service/">  
      <Text>Hello World</Text>  
    </Ping>  
  </s12:Body>  
</s12:Envelope>  
```  
  
 Il destinatario fornisce con una risposta HTTP vuota e lo stato 202.Un esempio della risposta HTTP:  
  
```  
HTTP/1.1 202 Accepted  
Date: Fri, 15 Jul 2005 08:56:07 GMT  
Server: Microsoft-IIS/6.0  
MicrosoftOfficeWebServer: 5.0_Pub  
X-Powered-By: ASP.NET  
X-AspNet-Version: 2.0.50215  
Cache-Control: private  
Content-Length: 0  
```  
  
## SOAP MTOM  
 In questa sezione vengono forniti i dettagli di implementazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] relativi al meccanismo HTTP SOAP MTOM.La tecnologia MTOM è un meccanismo di codifica dei messaggi SOAP analogo ai meccanismi tradizionali di codifica text\/XML o di codifica binaria di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Il meccanismo MTOM prevede le funzionalità seguenti:  
  
-   Meccanismo di codifica e assemblaggio di pacchetti XML descritto da \[XOP\] che ottimizza le voci di informazioni XML contenenti dati binari con codifica in base 64 suddividendoli in parti binarie distinte.  
  
-   Incapsulamento MIME del pacchetto XOP che serializza l'InfoSet XML e ogni parte binaria del pacchetto XOP in una parte MIME distinta.  
  
-   Codifica MIME XOP applicata alla SOAP 1.x envelope.  
  
-   Associazione di trasporto HTTP.  
  
 Benché in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sia possibile utilizzare il meccanismo MTOM con trasporti diversi da HTTP,quanto descritto in questo argomento si basa sul protocollo HTTP.  
  
 Il formato MTOM sfrutta un numeroso set di specifiche relative al meccanismo MTOM stesso, a XOP e a MIME.La modularità di questo set di specifiche rende piuttosto difficile ricavare in modo esatto i requisiti relativi alla semantica di formato ed elaborazione.Questa sezione descrive i requisiti di formato ed elaborazione dell'associazione MTOM HTTP.  
  
### Codifica dei messaggi MTOM  
  
#### Generazione di messaggi MTOM  
 La sezione 3.1 di \[XOP\] descrive il processo di codifica di elementi XML aventi voci di informazioni sugli elementi contenenti valori in base 64 in un pacchetto XOP definito in modo astratto.  
  
 La sequenza di passaggi seguente descrive il processo di codifica specifico del meccanismo MTOM:  
  
1.  Verificare che la SOAP envelope da codificare non contenga alcuna voce di informazioni sugli elementi il cui attributo `[namespace name]` sia "http:\/\/www.w3.org\/2004\/08\/xop\/include" e il cui attributo `[local name]` sia `Include`.  
  
2.  Creare un pacchetto MIME vuoto.  
  
3.  Identificare all'interno dell'InfoSet XML originale le voci di informazioni sugli elementi da ottimizzare.Affinché gli elementi vengano ottimizzati, i caratteri che costituiscono l'attributo `[children]` della voce di informazioni sugli elementi devono presentare la forma canonica di `xs:base64Binary` \(vedere XSD\-2, 3.2.16 base64Binary\) e non devono contenere spazi vuoti nella stessa riga contenente i caratteri diversi da spazio vuoto, né nella riga precedente o successiva.  
  
4.  Creare una XOP SOAP envelope uguale alla SOAP envelope originale, sostituendo tuttavia al figlio di ogni voce di informazioni sugli elementi identificato nel passaggio precedente una voce di informazioni sugli elementi `xop:Include` costruito come segue:  
  
    1.  Trasformare i caratteri sostituiti in dati binari elaborandoli come dati codificati in base 64.  
  
    2.  Generare un valore univoco di intestazione Content\-ID che soddisfi i requisiti R3133 e R3134.  
  
    3.  Generare un'intestazione MIME Content\-Transfer\-Encoding con il valore in binario.  
  
    4.  Se la voce di informazioni sugli elementi da ottimizzare \(ovvero il padre \[parent\] della voce di informazioni sugli elementi `xop:Include` appena aggiunto\) contiene una voce di informazioni sugli attributi `xmime:contentType`, generare un'intestazione Content\-Type MIME con il valore dell'attributo `xmime:contentType`.  
  
    5.  Generare una nuova parte MIME binaria avente un contenuto formato dagli elementi seguenti: dati binari decodificati a partire dai caratteri sostituiti elaborati come dati in base 64, intestazione Content\-ID come da passaggio 4b, intestazione Content\- Transfer\-Encoding come da passaggio 4c e intestazione Content\-Type come da passaggio 4d, se presente.  
  
    6.  Aggiungere un attributo `href` all'elemento `xop:Include` con il valore cid: uri derivato dal valore dell'intestazione Content\-ID generato nel passaggio 4b.Rimuovere i caratteri "\<" e "\>", applicare il flag Escape\-URL alla stringa restante e aggiungere il prefisso `cid:`.La suddetta conversione, da eseguire in base ai documenti RFC1738 e RFC2396, deve riguardare almeno il set di caratteri seguente,ma può essere applicata anche ad altri caratteri.  
  
        ```  
        Hexadecimal 00-1F , 7F, 20, "<" | ">" | "#" | "%" | <">  
        "{" | "}" | "|" | "\" | "^" | "[" | "]" | "`" | "~" | "^"  
        ```  
  
5.  Creare una parte MIME radice contenente la XOP SOAP envelope ottenuta nel passaggio 4.  
  
6.  Scrivere le intestazioni HTTP, compresa l'intestazione Content\-Type HTTP.  
  
7.  Scrivere il pacchetto MIME.  
  
#### Elaborazione di messaggi MTOM  
 L'elaborazione di un messaggio MTOM è l'esatto contrario del processo descritto nella sezione precedente "Generazione di messaggi MTOM":  
  
1.  Verificare che la parte MIME radice contenga l'elemento Content\-Type `application/xop+xml`.  
  
2.  Costruire una SOAP envelope analizzando la parte MIME radice del pacchetto come documento XML.La codifica dei caratteri viene determinata in base al parametro `charset` del Content\-Type della parte MIME radice.  
  
3.  Per ogni voce di informazioni sugli elementi della SOAP envelope costruita, che come unico membro della proprietà dei relativi figli \[children\] presenta una voce di informazioni sugli elementi `xop:Include`, eseguire quanto segue:  
  
    1.  Rimuovere il prefisso `cid:` ed eseguire la conversione URI inversa di tutte le sequenze escape \(RFC 2396\) contenute nel valore dell'attributo `@href` dell'elemento `xop:Include`.Racchiudere la stringa così ottenuta fra i caratteri "\<" e "\>".  
  
    2.  Individuare la parte MIME contenente il valore dell'intestazione Content\-ID corrispondente alla stringa ottenuta nel passaggio 3a.  
  
    3.  Sostituire la voce di informazioni sugli elementi `xop:Include` contenuto nella proprietà `children` di ogni elemento contenente le voci di informazioni sugli elementi che rappresentano la codifica canonica in base 64 \(vedere XSD\-2, 3.2.16 base64Binary\) del corpo dell'entità della parte MIME identificato nel passaggio 3b. In pratica, sostituire la voce di informazioni sugli elementi `xop:Include` con i dati ricostruiti a partire dalla parte di pacchetto.  
  
#### Intestazione Content\-Type HTTP  
 Segue un elenco di precisazioni in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] relative al formato dell'intestazione Content\-Type HTTP di un messaggio con codifica SOAP 1.x MTOM ottenuto a partire dai requisiti dichiarati nella specifica di MTOM nonché dal meccanismo MTOM e dal documento RFC 2387.  
  
-   R4131: un'intestazione Content\-Type HTTP deve contenere il valore multipart\/related \(che non fa distinzione fra maiuscole e minuscole\) e i relativi parametri.Anche i nomi dei parametri non fanno distinzione tra maiuscole e minuscole.Inoltre, l'ordine dei parametri è irrilevante.  
  
-   Il formato BNF \(Backus\-Naur Form\) completo dell'intestazione Content\-Type dei messaggi MIME è riportato nella sezione 5.1 del documento RFC 2045.  
  
-   R4132: un'intestazione Content\-Type HTTP deve contenere un parametro di tipo avente il valore `application/xop+xml` compreso fra virgolette doppie.  
  
 Benché il requisito di utilizzo delle virgolette doppie non venga evidenziato esplicitamente nel documento RFC 2387, in questo documento viene fatto notare che nella maggior parte dei casi tutti i parametri di tipo di supporto multipart\/related contengono caratteri riservati, ad esempio "@" o "\/", il che comporta l'esigenza di utilizzare le virgolette doppie.  
  
-   R4133: un'intestazione Content\-Type HTTP deve presentare un parametro start con il valore dell'intestazione Content\-ID della parte MIME contenente l'elemento SOAP 1.x Envelope, racchiuso fra virgolette doppie.Se tale parametro viene omesso, la SOAP 1.x envelope deve essere inclusa nella prima parte MIME.  
  
-   R4134: un'intestazione Content\-Type HTTP di un messaggio con codifica SOAP 1.1 MTOM deve includere il parametro start\-info con il valore text\/xml racchiuso fra virgolette doppie.  
  
-   R4135: un'intestazione Content\-Type HTTP di un messaggio con codifica SOAP 1.2 MTOM deve includere il parametro start\-info con il valore `application/soap+xml` racchiuso fra virgolette doppie.  
  
-   R4136: un'intestazione Content\-Type HTTP di un messaggio con codifica SOAP 1.x MTOM deve contenere un parametro boundary il cui valore \(racchiuso fra virgolette doppie\) corrisponda al formato BNF del limite MIME definito nella sezione 5.1.1 del documento RFC 2046.  
  
    ```  
    boundary := 0*69<bchars> bcharsnospace   
    bchars := bcharsnospace / " "   
    bcharsnospace :=    DIGIT / ALPHA / "'" / "(" / ")" / "+"   
                        / "_" / "," / "-" / "." / "/" / ":" / "=" / "?"  
    ```  
  
     Esempi:  
  
     CORRETTO  
  
    ```  
    Content-Type: multipart/related; type="application/xop+xml";start=" <part0@tempuri.org>";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1";start-info="text/xml"  
  
    ```  
  
     CORRETTO  
  
    ```  
    Content-Type: Multipart/Related; type="application/xop+xml";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
  
    ```  
  
     NON CORRETTO  
  
    ```  
    Content-Type: Multipart/Related; type=application/xop+xml;start=" <part0@tempuri.org>";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"   
    ```  
  
#### Parte MIME InfoSet  
 La SOAP 1.x envelope è incapsulata come parte radice del pacchetto XOP MIME e spesso viene detta "parte `infoset`".  
  
-   R4141: la SOAP 1.x envelope deve essere incapsulata come parte radice del pacchetto XOP MIME, detto "parte `infoset`", a cui si fa riferimento nell'intestazione Content\-Type HTTP.  
  
-   R4142: la parte `Infoset` SOAP deve contenere le intestazioni MIME seguenti: `Content-ID`, `Content-Transfer-Encoding` e `Content-Type`.  
  
 Il formato dell'intestazione Content\-ID è definito nel documento RFC 2045 come  
  
```  
"Content-ID" ":" msg-id  
```  
  
 in cui l'elemento `msg-id` è definito nel documento RFC 2822 \(che sostituisce il documento RFC 822, a cui si fa riferimento nel documento RFC 2045\) come:  
  
```  
msg-id    =       [CFWS] "<" id-left "@" id-right ">" [CFWS]  
```  
  
 e che in effetti è un indirizzo di posta elettronica compreso fra "\<" e "\>".Il prefisso e il suffisso `[CFWS]` sono stati aggiunti nel documento RFC 2822 per contenere commenti e non devono essere utilizzati per mantenere l'interoperabilità.  
  
 R4143: il valore dell'intestazione Content\-ID della parte MIME InfoSet deve attenersi alle regole di definizione dell'elemento `msg-id` indicate nel documento RFC 2822, omettendo le parti `[CFWS]` di prefisso e suffisso.  
  
 In alcune implementazioni del protocollo MIME sono stati ridotti i requisiti relativi all'esigenza che il valore compreso fra "\<" e "\>" corrisponda a un indirizzo di posta elettronica. In tali implementazioni, oltre all'indirizzo di posta elettronica, si utilizza un elemento `absoluteURI` racchiuso fra "\<" e ",\>".Questa versione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] prevede che i valori dell'intestazione MIME Content\-ID presentino il formato:  
  
```  
Content-ID: <http://tempuri.org/0>   
```  
  
 R4144: i processori MTOM devono accettare valori di intestazione Content\-ID corrispondenti all'elemento `msg-id` con requisiti ridotti riportato di seguito.  
  
```  
msg-id-relaxed =     [CFWS] "<" (absoluteURI | mail-address) ">" [CFWS]  
mail-address   =     id-left "@" id-right  
```  
  
 Il protocollo MIME \(RFC 2045\) fornisce l'intestazione Content\-Transfer\-Encoding per comunicare la codifica del contenuto della parte MIME.L'impostazione predefinita dell'intestazione Content\-Transfer\-Encoding è una codifica a 7 bit, che tuttavia per la maggior parte dei messaggi SOAP risulta inadatta. Pertanto, tale intestazione è necessaria per garantire una maggiore interoperabilità:  
  
-   R4145: la parte SOAP InfoSet deve contenere l'intestazione Content\-Transfer\-Encoding.  
  
-   R4146: se la codifica dei caratteri della SOAP envelope è UTF\-8, il valore dell'intestazione Content\-Transfer\-Encoding deve corrispondere a una codifica a 8 bit.  
  
-   R4147: se la codifica dei caratteri della SOAP envelope è UTF\-16, il valore dell'intestazione Content\-Transfer\-Encoding deve corrispondere a una codifica binaria.  
  
-   Secondo quanto indicato nella sezione 5 di \[XOP\]:  
  
-   R4148: la parte SOAP1.1 InfoSet deve contenere un'intestazione Content\-Type avente tipo di supporto "application\/xop\+xml", tipo di parametri "text\/xml" e charset "utf\-8".  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="text/xml"  
    ```  
  
-   R4149: nella parte SOAP 1.2 InfoSet deve essere inclusa un'intestazione Content\-Type con tipo di supporto "`application/xop+xml`" e tipo di parametri "`application/soap+xml`" e `charset`.  
  
    ```  
    Content-Type: application/xop+xml;  
                  charset=utf-8;type="application/soap+xml"  
    ```  
  
     Benché XOP consenta di definire il parametro `charset` di `application/xop+xml` come facoltativo, tale parametro è necessario per l'interoperabilità, analogamente al requisito di BP 1.1 relativo al parametro `charset` del tipo di supporto `text/xml`.  
  
-   R41410: i parametri `type` e `charset` devono essere presenti nell'intestazione Content\-Type della parte SOAP 1.x InfoSet.  
  
#### Supporto degli endpoint WCF per MTOM  
 Lo scopo del meccanismo MTOM è codificare un messaggio SOAP allo scopo di ottimizzare i dati codificati in base 64.Segue un elenco di vincoli:  
  
-   R4151: qualsiasi voce di informazioni sugli elementi contenente dati con codifica in base 64 può essere ottimizzata.  
  
-   B4152: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ottimizza le voci di informazioni sugli elementi contenenti dati con codifica in base 64 e aventi una lunghezza superiore a 1024 byte.  
  
 Un endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] configurato per utilizzare il meccanismo MTOM invia sempre messaggi con codifica MTOM.Anche se nessuna parte soddisfa i criteri previsti, il messaggio viene comunque considerato come messaggio con codifica MTOM, serializzato come pacchetto MIME e avente una sola parte MIME contenente la SOAP envelope.  
  
### Asserzione di WS\-Policy relativa a MTOM  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'asserzione di criteri seguente per indicare l'utilizzo del meccanismo MTOM in base all'endpoint:  
  
```  
<wsoma:OptimizedMimeSerialization ... />  
```  
  
-   R4211: l'asserzione di criteri precedente contiene un soggetto dei criteri di endpoint e impone che tutti i messaggi inviati all'endpoint e provenienti da quest'ultimo vengano ottimizzati tramite il meccanismo MTOM.  
  
-   B4212: quando configurato per utilizzare l'ottimizzazione MTOM, un endpoint di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] aggiunge un'asserzione di criteri MTOM al criterio associato all'elemento `wsdl:binding` corrispondente.  
  
### Integrazione con WS\-Security  
 MTOM è un meccanismo di codifica simile ai meccanismi di codifica `text/xml` e di codifica binaria XML di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Il meccanismo MTOM può integrarsi perfettamente con il protocollo WS\-Security e gli altri protocolli WS \- \*: un messaggio protetto mediante il protocollo WS\-Security può infatti essere ottimizzato tramite MTOM.  
  
### Esempi  
  
#### Esempio di messaggio WCF SOAP 1.1 codificato tramite MTOM  
  
```  
POST http://131.107.72.15/Mtom/svc/service.svc/Soap11MtomUTF8 HTTP/1.1  
SOAPAction: "http://xmlsoap.org/echoBinaryAsString"  
Content-Type: multipart/related;type="application/xop+xml";  
              start="<http://tempuri.org/0>";start-info="text/xml";  
       boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"  
Host: 131.107.72.15  
Content-Length: 1501  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="text/xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Body>  
    <EchoBinaryAsString xmlns="http://xmlsoap.org/Ping">  
      <array>  
        <xop:Include   
         href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206521093670"   
         xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </array>  
    </EchoBinaryAsString>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
Content-ID: <http://tempuri.org/1/632618206521093670>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
…Binary Content..  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1  
```  
  
#### Esempio di messaggio WCF Secure SOAP 1.2 codificato tramite MTOM  
 Questo esempio illustra la codifica tramite MTOM e SOAP 1.2 di un messaggio protetto mediante WS\-Security.Le parti binarie identificate per la codifica sono il contenuto del token `BinarySecurityToken`, il valore `CipherValue` dell'elemento `EncryptedData` che corrisponde alla firma crittografata e il corpo crittografato.Si noti che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non considera il valore `CipherValue` della chiave `EncryptedKey` come ottimizzabile, in quanto la relativa lunghezza è inferiore a 1024 byte.  
  
```  
POST http://131.107.72.15/Mtom/service.svc/Soap12MtomSecureSignEncrypt HTTP/1.1  
Content-Type: multipart/related; type="application/xop+xml";  
              start="<http://tempuri.org/0>";  
            boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3";  
              start-info="application/soap+xml";   
              action="http://xmlsoap.org/echoBinaryAsString"  
Host: 131.107.72.15  
Content-Length: 1941  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/0>  
Content-Transfer-Encoding: 8bit  
Content-Type: application/xop+xml;charset=utf-8;type="application/soap+xml"  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" xmlns:u="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
  <s:Header>  
    <o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
      <u:Timestamp u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-5">  
        <u:Created>2005-09-09T06:57:32.488Z</u:Created>  
        <u:Expires>2005-09-09T07:02:32.488Z</u:Expires>  
      </u:Timestamp>  
      <o:BinarySecurityToken u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-2" ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509v3" EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">  
        <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
      </o:BinarySecurityToken>  
      <e:EncryptedKey Id="_1" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#rsa-oaep-mgf1p"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:KeyIdentifier ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509SubjectKeyIdentifier">Xeg55vRyK3ZhAEhEf+YT0z986L0=</o:KeyIdentifier>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>          <e:CipherValue>oQfpxwT8/SAGyZQzKE2b4yO6dXuQj7pwJ+5CGL3Rf7C06bQ5ttMoQ9GLJcQYkXTzin+WwHEgs5bj5ml9HKTW9QAU5JJ6lksdymmQvWP5ZtGPBVchO4sofEGoCKmBiZL/DYS/cnbzgnc/3a6NYnc10y2fWGaGLiqa00zijAw7o0Y=</e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedKey>  
      <c:DerivedKeyToken u:Id="_2" xmlns:c="http://schemas.xmlsoap.org/ws/2005/02/sc">  
        <o:SecurityTokenReference>  
          <o:Reference URI="#_1"/>  
        </o:SecurityTokenReference>  
        <c:Nonce>OrEPRX7fISIS4sXYWPMv3g==</c:Nonce>  
      </c:DerivedKeyToken>  
      <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:DataReference URI="#_3"/>  
        <e:DataReference URI="#_4"/>  
      </e:ReferenceList>  
      <e:EncryptedData Id="_4" Type="http://www.w3.org/2001/04/xmlenc#Element" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
          <o:SecurityTokenReference>  
            <o:Reference URI="#_2"/>  
          </o:SecurityTokenReference>  
        </KeyInfo>  
        <e:CipherData>  
          <e:CipherValue>  
            <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F2%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
          </e:CipherValue>  
        </e:CipherData>  
      </e:EncryptedData>  
    </o:Security>  
  </s:Header>  
  <s:Body u:Id="_0">  
    <e:EncryptedData Id="_3" Type="http://www.w3.org/2001/04/xmlenc#Content" xmlns:e="http://www.w3.org/2001/04/xmlenc#">  
      <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>  
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">  
        <o:SecurityTokenReference xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">  
          <o:Reference URI="#_2"/>  
        </o:SecurityTokenReference>  
      </KeyInfo>  
      <e:CipherData>  
        <e:CipherValue>  
          <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F3%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>  
        </e:CipherValue>  
      </e:CipherData>  
    </e:EncryptedData>  
  </s:Body>  
</s:Envelope>  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/1/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary content of BinarySecurityToken - X509 Certificate...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/2/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted primary signature...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3  
Content-ID: <http://tempuri.org/3/632618206525089430>  
Content-Transfer-Encoding: binary  
Content-Type: application/octet-stream  
...Binary serialization of the encrypted Body...  
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3--  
```