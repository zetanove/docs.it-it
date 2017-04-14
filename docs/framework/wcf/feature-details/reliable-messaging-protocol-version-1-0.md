---
title: "Protocollo Reliable Messaging versione 1.0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5509a5c-de24-4bc2-9a48-19138055dcce
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Protocollo Reliable Messaging versione 1.0
In questo argomento vengono illustrati i dettagli di implementazione di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per il protocollo WS\-Reliable Messaging di febbraio 2005 \(versione 1.0\) necessario per l'interazione con il trasporto HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] segue la specifica WS\-Reliable Messaging con i vincoli e i chiarimenti illustrati in questo argomento.Si noti che il protocollo WS\-Reliable Messaging versione 1.0 viene implementato a partire da [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)].  
  
 Il protocollo WS\-Reliable Messaging \(febbraio 2005\) viene implementato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] da <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>.  
  
 Per comodità, nell'argomento vengono utilizzati i ruoli seguenti:  
  
-   Iniziatore: il client che avvia la creazione della sequenza di WS\-Reliable Message.  
  
-   Risponditore: il servizio che riceve le richieste dell'iniziatore.  
  
 In questo documento vengono utilizzati i prefissi e gli spazi dei nomi riportati nella tabella seguente.  
  
|Prefisso|Spazio dei nomi|  
|--------------|---------------------|  
|wsrm|http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm|  
|netrm|http:\/\/schemas.microsoft.com\/ws\/2006\/05\/rm|  
|s|http:\/\/www.w3.org\/2003\/05\/soap\-envelope|  
|wsa|http:\/\/schemas.xmlsoap.org\/ws\/2005\/08\/addressing|  
|wsse|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wssecurity\-secext\-1.0.xsd|  
  
## Messaggistica  
  
### Messaggi di definizione sequenza  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa messaggi `CreateSequence` e `CreateSequenceResponse` per stabilire una sequenza di messaggi affidabile.Si applicano i vincoli seguenti:  
  
-   B1101: l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera l'elemento Expires facoltativo nel messaggio `CreateSequence` o, nei casi in cui il messaggio `CreateSequence` contiene un elemento `Offer`, l'elemento `Expires` facoltativo nell'elemento `Offer`.  
  
-   B1102: durante l'accesso al messaggio `CreateSequence`, il `Responder`[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] invia e riceve entrambi gli elementi `Expires`, se esistenti, ma non ne utilizza i valori.  
  
 Con il protocollo WS\-ReliableMessaging viene introdotto il meccanismo `Offer` che consente di stabilire le due sequenze correlate opposte che formano una sessione.  
  
-   R1103: se `CreateSequence` contiene un elemento `Offer`, il risponditore Reliable Messaging deve accettare la sequenza e rispondere con `CreateSequenceResponse` contenente un elemento `wsrm:Accept`, formando due sequenze correlate opposte, oppure rifiutare la richiesta `CreateSequence`.  
  
-   R1104: i messaggi `SequenceAcknowledgement` e dell'applicazione in transito sulla sequenza opposta devono essere inviati al riferimento endpoint `ReplyTo` di `CreateSequence`.  
  
-   R1105: i riferimenti endpoint `AcksTo` e `ReplyTo` in `CreateSequence` devono presentare valori indirizzo che corrispondano all'ottetto.  
  
     Prima di creare una sequenza , il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verifica che le parti URI dei riferimenti endpoint `AcksTo` e`ReplyTo` siano identiche.  
  
-   R1106: i riferimenti endpoint `AcksTo`e `ReplyTo` in `CreateSequence` devono avere lo stesso set di parametri di riferimento.  
  
     [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non impone, ma presuppone che i parametri di riferimento dei riferimenti endpoint `AcksTo` e `ReplyTo` in `CreateSequence` siano identici e utilizza i parametri di riferimento dal riferimento endpoint `ReplyTo` per acknowledgement e messaggi della sequenza opposta.  
  
-   R1107: quando vengono stabilite due sequenze opposte tramite il meccanismo `Offer`, i messaggi dell'applicazione e `SequenceAcknowledgement` in transito sulle sequenze opposte devono essere inviati al riferimento all'endpoint `ReplyTo` di `CreateSequence`.  
  
-   R1108: quando vengono stabilite due sequenze opposte mediante il meccanismo Offer, la proprietà `[address]` dell'elemento figlio del riferimento endpoint `wsrm:AcksTo` dell'elemento `wsrm:Accept` di `CreateSequenceResponse` deve corrispondere per numero di byte all'URI di destinazione di `CreateSequence`.  
  
-   R1109: quando vengono stabilite due sequenze opposte tramite il meccanismo `Offer`, i messaggi inviati dall'iniziatore e gli acknowledgement a tali messaggi da parte del risponditore devono essere inviati allo stesso riferimento all'endpoint.  
  
     [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza WS\-Reliable Messaging per stabilire sessioni affidabili tra l'iniziatore e il risponditore.L'implementazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di WS\-ReliableMessaging offre una sessione affidabile per modelli di messaggistica unidirezionali, request\/reply e full duplex.Il meccanismo `Offer` del protocollo WS\-Reliable Messaging in `CreateSequence`\/`CreateSequenceResponse` consente di stabilire due sequenze opposte correlate e fornisce un protocollo della sessione idoneo per tutti gli endpoint del messaggio.Dato che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce una garanzia di sicurezza per tale sessione, inclusa la protezione end\-to\-end per l'integrità della sessione, è consigliabile assicurarsi che i messaggi destinati alla stessa parte arrivino alla stessa destinazione.Ciò consente anche il "piggy\-backing" degli acknowledgement della sequenza sui messaggi dell'applicazione.A [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si applicano pertanto i vincoli R1104, R1105 e R1108.  
  
 Esempio di un messaggio `CreateSequence`.  
  
```  
<s:Envelope>  
  <s:Header>  
    <a:Action s:mustUnderstand="1">  
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequence  
    </a:Action>  
    <a:ReplyTo>  
      <a:Address>          
         http://Business456.com/clientA        
      </a:Address>  
    </a:ReplyTo>  
    <a:MessageID>  
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
    </a:MessageID>  
    <a:To s:mustUnderstand="1">  
      http://Business456.com/clientA  
    </a:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequence>  
      <wsrm:AcksTo>  
       <wsa:Address>  
         http://Business456.com/clientA  
       </wsa:Address>  
     </wsrm:AcksTo>  
     <wsrm:Offer>  
      <wsrm:Identifier>  
        urn:uuid:0afb8d36-bf26-4776-b8cf-8c91fddb5496  
      </wsrm:Identifier>  
     </wsrm:Offer>  
   </wsrm:CreateSequence>  
  </s:Body>  
</s:Envelope>  
```  
  
 Esempio di un messaggio `CreateSequenceResponse`.  
  
```  
<s:Envelope>  
  <s:Header>  
    <a:Action s:mustUnderstand="1">  
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequenceResponse  
    </a:Action>  
    <a:RelatesTo>  
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
    </a:RelatesTo>  
    <a:To s:mustUnderstand="1">  
      http://Business456.com/clientA  
    </a:To>  
  </s:Header>  
  <s:Body>  
   <wsrm:CreateSequenceResponse>  
    <Identifier>  
     urn:uuid:eea0a36c-b38a-43e8-8c76-2fabe2d76386  
    </Identifier>  
    <Accept>  
    <AcksTo>  
      <a:Address>  
        http://BusinessABC.com/serviceA  
      </a:Address>  
    </AcksTo>  
    </Accept>  
   </wsrm:CreateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### Sequenza  
 Di seguito è riportato un elenco di vincoli che si applicano alle sequenze:  
  
-   B1201:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera e accede a numeri di sequenza non superiori al valore massimo di `xs:long`, 9223372036854775807 incluso.  
  
-   B1202:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera sempre un ultimo messaggio con corpo vuoto con l'URI di azione http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm\/LastMessage.  
  
-   B1203: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] riceve e recapita un messaggio con un'intestazione di sequenza contenente un elemento `LastMessage`, a condizione che l'URI dell'azione non sia http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm\/LastMessage.  
  
 Esempio di intestazione di sequenza.  
  
```  
<wsrm:Sequence>  
  <wsrm:Identifier>  
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
  </wsrm:Identifier>  
  <wsrm:MessageNumber>  
    10  
  </wsrm:MessageNumber>  
  <wsrm:LastMessage/>  
 </wsrm:Sequence>  
```  
  
### Intestazione AckRequested  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'intestazione `AckRequested` come meccanismo keep\-alive.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera l'elemento `MessageNumber` facoltativo.Quando viene ricevuto un messaggio con un'intestazione `AckRequested` contenente l'elemento `MessageNumber`, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ignora il valore dell'elemento `MessageNumber`, come illustrato nell'esempio seguente.  
  
```  
<wsrm:AckRequested>  
  <wsrm:Identifier>  
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
  </wsrm:Identifier>  
</wsrm:AckRequested>  
```  
  
### Intestazione SequenceAcknowledgement  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza un meccanismo "piggy\-back" per gli acknowledgement di sequenza disponibile nel protocollo WS\-Reliable Messaging.  
  
-   R1401: quando vengono stabilite due sequenze opposte utilizzando il meccanismo `Offer`, l'intestazione `SequenceAcknowledgement` può essere inclusa in qualsiasi messaggio dell'applicazione trasmesso al destinatario desiderato.  
  
-   B1402: quando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] deve generare un acknowledgement prima di ricevere qualsiasi messaggio di sequenza, ad esempio per soddisfare un messaggio `AckRequested`, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un'intestazione `SequenceAcknowledgement` che contiene l'intervallo 0\-0, come illustrato nell'esempio seguente.  
  
    ```  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>  
        urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36  
      </wsrm:Identifier>  
      <wsrm:AcknowledgementRange Upper="0" Lower="0"/>  
    </wsrm:SequenceAcknowledgement>  
    ```  
  
-   B1403: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera intestazioni `SequenceAcknowledgement` che contengono un elemento `Nack`, ma supporta elementi `Nack`.  
  
### Errori WS\-ReliableMessaging  
 Di seguito è riportato un elenco di vincoli applicabili all'implementazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] degli errori di WS\-Reliable Messaging:  
  
-   B1501: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera errori `MessageNumberRollover`.  
  
-   B1502:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] l'endpoint può generare errori `CreateSequenceRefused`, come descritto nella specifica.  
  
-   B1503: quando l'endpoint del servizio raggiunge il limite di connessione e non è in grado di elaborare nuove connessioni, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un ulteriore codice secondario di errore `CreateSequenceRefused`, `netrm:ConnectionLimitReached`, come illustrato nell'esempio seguente.  
  
    ```  
    <s:Envelope>  
      <s:Header>  
        <wsa:Action>  
          http://schemas.xmlsoap.org/ws/2005/08/addressing/fault  
        </wsa:Action>  
      </s:Header>  
      <s:Body>  
        <s:Fault>  
          <s:Code>  
            <s:Value>  
              s:Receiver  
            </s:Value>  
            <s:Subcode>  
              <s:Value>  
                wsrm:CreateSequenceRefused  
              </s:Value>  
              <s:Subcode>  
                <s:Value>  
                  netrm:ConnectionLimitReached  
                </s:Value>  
              </s:Subcode>  
            </s:Subcode>  
          </s:Code>  
          <s:Reason>  
            <s:Text xml:lang="en">  
              [Reason]  
            </s:Text>  
          </s:Reason>  
        </s:Fault>  
      </s:Body>  
    </s:Envelope>  
    ```  
  
### Errori WS\-Addressing  
 Dato che WS\-Reliable Messaging utilizza WS\-Addressing, l'implementazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di WS\-Reliable Messaging potrebbe generare errori WS\-Addressing.In questa sezione vengono illustrati gli errori WS\-Addressing generati in modo esplicito da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] a livello di WS\-ReliableMessaging:  
  
-   B1601:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera l'errore Message Addressing Header Required quando si verifica una delle condizioni seguenti:  
  
    -   In un messaggio mancano un'intestazione `Sequence` e un'intestazione `Action`.  
  
    -   In un messaggio `CreateSequence` manca un'intestazione `MessageId`.  
  
    -   In un messaggio `CreateSequence` manca un'intestazione `ReplyTo`.  
  
-   B1602:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera l'errore del tipo Operazione non supportata in risposta a un messaggio privo di un'intestazione `Sequence`, ma con un'intestazione `Action` non riconosciuta nella specifica del protocollo WS\-Reliable Messaging.  
  
-   B1603:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera l'errore del tipo Endpoint non disponibile per indicare che l'endpoint non elabora la sequenza in base all'esame delle intestazioni di indirizzamento del messaggio `CreateSequence`.  
  
## Composizione del protocollo  
  
### Composizione con WS\-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta due versioni di WS\-Addressing: WS\-Addressing 2004\/08 \[WS\-ADDR\] e W3C WS\-Addressing 1.0 Recommendation \[WS\-ADDR\-CORE\] e \[WS\-ADDR\-SOAP\].  
  
 Anche se la specifica WS\-Reliable Messaging menziona solo WS\-Addressing 2004\/08, non limita la versione WS\-Addressing da utilizzare.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   R2101:sia WS\-Addressing 2004\/08 che WS\-Addressing 1.0 possono essere utilizzati con WS\-Reliable Messaging.  
  
-   R2102:è necessario utilizzare una sola versione di WS\-Addressing in una data sequenza di WS\-Reliable Messaging o in una coppia di sequenze opposte correlate tramite il meccanismo `wsrm:Offer`.  
  
### Composizione con SOAP  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta l'utilizzo sia di SOAP 1.1 che di SOAP 1.2 con WS\-Reliable Messaging.  
  
### Composizione con WS\-Security e WS\-SecureConversation  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce protezione per le sequenze di WS\-Reliable Messaging utilizzando trasporto protetto \(HTTPS\), composizione con WS\-Security e composizione con WS\-SecureConversation.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   R2301:per proteggere l'integrità di una sequenza di WS\-Reliable Messaging oltre all'integrità e alla riservatezza dei singoli messaggi, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede l'utilizzo di WS\-SecureConversation.  
  
-   R2302:prima di stabilire la\/e sequenza\/e di WS\-Reliable Messaging, è necessario stabilire una sessione WS\-SecureConversation.  
  
-   R2303: se la durata della sequenza di WS\-Reliable Messaging supera la durata della sessione WS\-SecureConversation, è necessario rinnovare il `SecurityContextToken` stabilito tramite WS\-SecureConversation utilizzando l'associazione WS\-Secure Conversation Renewal corrispondente.  
  
-   B2304: la sequenza WS\-ReliableMessaging o una coppia di sequenze opposte è sempre associata a una singola sessione WS\-SecureConversation.  
  
     L'origine [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera l'elemento `wsse:SecurityTokenReference` nella sezione di estendibilità degli elementi del messaggio `CreateSequence`.  
  
-   R2305:in caso di composizione con WS\-SecureConversation, un messaggio `CreateSequence` deve contenere l'elemento `wsse:SecurityTokenReference`.  
  
## Asserzione di WS\-Policy relativa a WS\-Reliable Messaging  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'asserzione di WS\-Policy `wsrm:RMAssertion` relativa a WS\-Reliable Messaging per descrivere le funzionalità degli endpoint.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   B3001: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] collega l'asserzione di WS\-Policy `wsrm:RMAssertion` agli elementi `wsdl:binding`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta i collegamenti agli elementi `wsdl:binding` e `wsdl:port`.  
  
-   B3002: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta le proprietà facoltative seguenti dell'asserzione di WS\-Reliable Messaging e ne assicura il controllo sull'elemento [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]`ReliableMessagingBindingElement`:  
  
    -   `wsrm:InactivityTimeout`  
  
    -   `wsrm:AcknowledgementInterval`  
  
     Di seguito è riportato un esempio.  
  
    ```  
    <wsrm:RMAssertion>  
      <wsrm:InactivityTimeout Milliseconds="600000" />  
      <wsrm:AcknowledgementInterval Milliseconds="200" />  
    </wsrm:RMAssertion>  
    ```  
  
## Estensione di WS\-Reliable Messaging per il controllo del flusso  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'estendibilità di WS\-Reliable Messaging per offrire un controllo facoltativo aggiuntivo più rigido sul flusso di messaggi della sequenza.  
  
 Per attivare il controllo del flusso, impostare la proprietà `FlowControlEnabled``bool` di `ReliableSessionBindingElement` su `true`.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   B4001: quando viene attivato il controllo del flusso di Reliable Messaging, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un elemento `netrm:BufferRemaining` nell'estendibilità dell'elemento dell'intestazione `SequenceAcknowledgement`.  
  
-   B4002: quando il controllo di flusso di Reliable Messaging è attivato, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non richiede la presenza di un elemento `netrm:BufferRemaining` nell'intestazione `SequenceAcknowledgement`, come illustrato nell'esempio seguente.  
  
    ```  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>  
        http://fabrikam123.com/abc  
      </wsrm:Identifier>  
      <wsrm:AcknowledgementRange Upper="1" Lower="1"/>             
      <netrm:BufferRemaining>  
        8  
      </netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
  
    ```  
  
-   B4003: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza `netrm:BufferRemaining` per indicare quanti nuovi messaggi la destinazione di Reliable Messaging è in grado di memorizzare nel buffer.  
  
-   B4004:il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Reliable Messaging limita il numero di messaggi trasmessi quando l'applicazione di destinazione Reliable Messaging non può ricevere messaggi rapidamente.La destinazione Reliable Messaging memorizza nel buffer messaggi e il valore dell'elemento scende a 0.  
  
-   B4005: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera valori integer `netrm:BufferRemaining` tra 0 e 4096 incluso e legge valori integer tra 0 e il valore `maxInclusive` di `xs:int`, 214748364 incluso.  
  
## Modelli di scambio dei messaggi  
 In questa sezione viene illustrato il comportamento di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando WS\-Reliable Messaging viene utilizzato per modelli di scambio di messaggi diversi.Per ogni modello di scambio di messaggi, vengono presi in considerazione i due scenari di distribuzione seguenti:  
  
-   Iniziatore non indirizzabile: l'iniziatore si trova dietro a un firewall; il risponditore può recapitare messaggi all'iniziatore solo su risposte HTTP.  
  
-   Iniziatore indirizzabile: le richieste HTTP possono essere inviate sia all'iniziatore che al risponditore. In altre parole, è possibile stabilire due connessioni HTTP opposte.  
  
### Iniziatore unidirezionale, non indirizzabile  
  
#### Associazione  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello unidirezionale di scambio di messaggi utilizzando una sequenza in un canale HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi da RMS a RMD e la risposta HTTP per trasmettere tutti i messaggi da RMD a RMS.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un messaggio `CreateSequence` senza offerta.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che `CreateSequence` non abbia alcuna offerta prima di creare una sequenza.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] risponde alla richiesta `CreateSequence` con un messaggio `CreateSequenceResponse`.  
  
#### SequenceAcknowledgement  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] elabora gli acknowledgement sulla risposta di tutti i messaggi tranne il messaggio `CreateSequence` e i messaggi di errore.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera sempre un acknowledgement autonomo in risposta alla sequenza e ai messaggi `AckRequested`.  
  
#### Messaggio TerminateSequence  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] considera `TerminateSequence` come un'operazione unidirezionale, in cui cioè la risposta HTTP ha un corpo vuoto e il codice di stato HTTP 202.  
  
### Iniziatore unidirezionale, indirizzabile  
  
#### Binding  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello unidirezionale di scambio di messaggi utilizzando una sequenza in un canale HTTP in ingresso e in uscita.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi.Tutte le risposte HTTP hanno un corpo vuoto e un codice di stato HTTP 202.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un messaggio `CreateSequence` senza offerta.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che `CreateSequence` non abbia alcuna offerta prima di creare una sequenza.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette il messaggio `CreateSequenceResponse` su una richiesta HTTP indirizzata con il riferimento endpoint `ReplyTo`.  
  
### Iniziatore duplex, indirizzabile  
  
#### Binding  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di scambio di messaggi bidirezionale completamente asincrono utilizzando due sequenze in un canale HTTP in ingresso e in uscita.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi.Tutte le risposte HTTP hanno un corpo vuoto e un codice di stato HTTP 202.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un messaggio `CreateSequence` con un'offerta.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che `CreateSequence` abbia un'offerta prima di creare una sequenza.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] invia `CreateSequenceResponse` sulla richiesta HTTP indirizzata al riferimento dell'endpoint `ReplyTo` di `CreateSequence`.  
  
#### Durata della sequenza  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tratta le due sequenze come una sessione completamente duplex.  
  
 Dopo la generazione di un errore che origina errori in una sequenza, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si aspetta che l'endpoint crei errori in entrambe le sequenze.Dopo la lettura di un errore che origina errori in una sequenza, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea errori in entrambe le sequenze.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può chiudere la sequenza in uscita e continuare a elaborare i messaggi sulla sua sequenza in ingresso.Per contro, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può elaborare la chiusura della sequenza in ingresso e continuare a inviare i messaggi sulla sua sequenza in uscita.  
  
### Iniziatore request\/reply non indirizzabile  
  
#### Binding  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di scambio di messaggi request\/reply e unidirezionale utilizzando due sequenze in un canale HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere i messaggi della sequenza di richiesta e utilizza le risposte HTTP per trasmettere i messaggi della sequenza di risposte.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un messaggio `CreateSequence` con un'offerta.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che `CreateSequence` abbia un'offerta prima di creare una sequenza.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] risponde alla richiesta `CreateSequence` con un messaggio `CreateSequenceResponse`.  
  
#### Messaggio unidirezionale  
 Per completare correttamente un protocollo di scambio di messaggi unidirezionale, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio della sequenza di richiesta sulla richiesta HTTP e riceve un messaggio `SequenceAcknowledgement` autonomo sulla risposta HTTP.`SequenceAcknowledgement` deve riconoscere il messaggio trasmesso.  
  
 Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può rispondere alla richiesta con un acknowledgement, un errore o una risposta con un corpo vuoto e un codice di stato HTTP 202.  
  
#### Messaggi bidirezionali  
 Per completare correttamente un protocollo di scambio di messaggi bidirezionale, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio della sequenza di richiesta sulla richiesta HTTP e riceve un messaggio della sequenza di risposta sulla risposta HTTP.La risposta deve contenere un `SequenceAcknowledgement` che riconosce che il messaggio della sequenza di richiesta è stato trasmesso.  
  
 Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può rispondere alla richiesta con una risposta dell'applicazione, un errore o una risposta con un corpo vuoto e un codice di stato HTTP 202.  
  
 A causa della presenza di messaggi unidirezionali e del tempo delle risposte dell'applicazione, il numero di sequenza del messaggio della sequenza di richiesta e il numero di sequenza del messaggio di risposta non hanno alcuna correlazione.  
  
#### Nuovi tentativi di risposte  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si basa sulla correlazione request\/reply HTTP per la correlazione del protocollo di scambio di messaggi bidirezionali.Di conseguenza, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non smette di tentare un messaggio della sequenza di richiesta quando tale messaggio viene riconosciuto, ma piuttosto quando la risposta HTTP contiene un acknowledgement, un messaggio dell'utente o un errore.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ritenta le risposte sulla parte della richiesta HTTP della richiesta a cui è correlata la risposta.  
  
#### Scambio LastMessage  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera e trasmette un ultimo messaggio con corpo vuoto sulla parte della richiesta HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede una risposta, ma ignora il messaggio di risposta effettivo.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] risponde all'ultimo messaggio con corpo vuoto della sequenza di richiesta con un ultimo messaggio con corpo vuoto della sequenza di risposta.  
  
 Se il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] riceve un ultimo messaggio in cui l'URI di azione non è http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/rm\/LastMessage, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] risponde con un ultimo messaggio.Nel caso di un protocollo di scambio di messaggi bidirezionale, l'ultimo messaggio contiene il messaggio dell'applicazione; nel caso, invece, di un protocollo di scambio di messaggi unidirezionale, l'ultimo messaggio è vuoto.  
  
 Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non richiede un acknowledgement per l'ultimo messaggio con corpo vuoto della sequenza di risposta.  
  
#### Scambio TerminateSequence  
 Quando tutte le richieste hanno ricevuto una risposta valida, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera e trasmette il messaggio `TerminateSequence` della sequenza di richieste sulla parte della richiesta HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede una risposta, ma ignora il messaggio di risposta effettivo.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] risponde al messaggio `TerminateSequence` della sequenza di richiesta con un messaggio `TerminateSequence` della sequenza di risposta.  
  
 In una sequenza di arresto normale, entrambi i messaggi `TerminateSequence` contengono un intervallo completo `SequenceAcknowledgement`.  
  
### Iniziatore request\/reply, indirizzabile  
  
#### Binding  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di scambio di messaggi request\/reply utilizzando due sequenze in un canale HTTP in ingresso e in uscita.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi.Tutte le risposte HTTP hanno un corpo vuoto e un codice di stato HTTP 202.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un messaggio `CreateSequence` con un'offerta.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che `CreateSequence` abbia un'offerta prima di creare una sequenza.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] invia `CreateSequenceResponse` sulla richiesta HTTP indirizzata al riferimento dell'endpoint `ReplyTo` di `CreateSequence`.  
  
#### Correlazione request\/reply  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che tutti i messaggi di richiesta dell'applicazione presentino un `MessageId` e un riferimento all'endpoint `ReplyTo`.L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] applica il riferimento endpoint `ReplyTo` del messaggio `CreateSequence` a ogni messaggio di richiesta dell'applicazione.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede che i messaggi di richiesta in ingresso presentino un `MessageId` e `ReplyTo`.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che gli URI dei riferimenti endpoint di `CreateSequence` e di tutti i messaggi di richiesta dell'applicazione siano identici.