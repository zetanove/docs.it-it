---
title: "Protocollo Reliable Messaging versione 1.1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0da47b82-f8eb-42da-8bfe-e56ce7ba6f59
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Protocollo Reliable Messaging versione 1.1
In questo argomento vengono illustrati i dettagli di implementazione di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per il protocollo WS\-ReliableMessaging di febbraio 2007 \(versione 1.1\) necessario per l'interazione con il trasporto HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] segue la specifica WS\-ReliableMessaging con i vincoli e i chiarimenti illustrati in questo argomento.Si noti che il protocollo WS\-Reliable Messaging versione 1.1 viene implementato a partire da [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)].  
  
 Il protocollo WS\-ReliableMessaging \(febbraio 2007\) viene implementato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] da <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>.  
  
 Per comodità, nell'argomento vengono utilizzati i ruoli seguenti:  
  
-   Iniziatore: il client che inizia la creazione della sequenza di WS\-Reliable Message.  
  
-   Risponditore: il servizio che riceve le richieste dell'iniziatore.  
  
 In questo documento vengono utilizzati i prefissi e gli spazi dei nomi riportati nella tabella seguente.  
  
|||  
|-|-|  
|Prefisso|Spazio dei nomi|  
|wsrm|http:\/\/docs.oasis\-open.org\/ws\-rx\/wsrm\/200702|  
|netrm|http:\/\/schemas.microsoft.com\/ws\/2006\/05\/rm|  
|s|http:\/\/www.w3.org\/2003\/05\/soap\-envelope|  
|wsa|http:\/\/schemas.xmlsoap.org\/ws\/2005\/08\/addressing|  
|wsse|http:\/\/docs.oasis\-open.org\/wss\/2004\/01\/oasis\-200401\-wssecurity\-secext\-1.0.xsd|  
|wsrmp|http:\/\/docs.oasis\-open.org\/ws\-rx\/wsrmp\/200702|  
|netrmp|http:\/\/schemas.microsoft.com\/ws\-rx\/wsrmp\/200702|  
|wsp|\(WS\-Policy 1.2 o WS\-Policy 1.5\)|  
  
## Messaggistica  
  
### Creazione sequenza  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa i messaggi `CreateSequence` e `CreateSequenceResponse` per stabilire una sequenza di messaggistica affidabile.Si applicano i vincoli seguenti:  
  
-   B1101: l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza lo stesso riferimento dell'endpoint di `ReplyTo`, `AcksTo` e `Offer/Endpoint` del messaggio `CreateSequence`.  
  
-   R1102: i riferimenti degli endpoint `AcksTo`, `ReplyTo` e `Offer/Endpoint` nel messaggio `CreateSequence` devono avere valori di indirizzo con rappresentazioni di stringa identiche in modo che corrispondano all'ottetto.  
  
    -   Prima di creare una sequenza , il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verifica che la parte URI dei riferimenti degli endpoint `AcksTo`, `ReplyTo` e `Endpoint` siano identiche.  
  
-   R1103: i riferimenti degli endpoint `AcksTo`, `ReplyTo` e `Offer/Endpoint` nel messaggio `CreateSequence` devono avere lo stesso set di parametri di riferimento.  
  
    -   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non impone, ma presuppone che i parametri di riferimento dei riferimenti degli endpoint `AcksTo`, `ReplyTo` e `Offer/Endpoint` in `CreateSequence` siano identici e utilizza i parametri di riferimento dal riferimento dell'endpoint `ReplyTo` per acknowledgement e messaggi in sequenza opposta.  
  
-   B1104: l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera l'elemento facoltativo `Expires` o `Offer/Expires` nel messaggio `CreateSequence`.  
  
-   B1105: quando si accede al messaggio `CreateSequence`, il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza il valore `Expires` dell'elemento `CreateSequence` come valore `Expires` dell'elemento `CreateSequenceResponse`.In caso contrario, il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] legge e ignora i valori `Expires` e `Offer/Expires`.  
  
-   B1106: quando si accede al messaggio `CreateSequenceResponse`, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] legge il valore facoltativo `Expires`, ma non lo utilizza.  
  
-   B1107: l'iniziatore e il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] generano sempre l'elemento facoltativo `IncompleteSequenceBehavior` negli elementi `CreateSequence/Offer` e `CreateSequenceResponse`.  
  
-   B1108: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza solo i valori `DiscardFollowingFirstGap` e `NoDiscard` nell'elemento `IncompleteSequenceBehavior`.  
  
    -   WS\-ReliableMessaging utilizza il meccanismo `Offer` per stabilire le due sequenze correlate opposte che formano una sessione.  
  
-   B1109: se `CreateSequence` contiene un elemento `Offer`, il risponditore unidirezionale [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] respinge la sequenza offerta rispondendo con un `CreateSequenceResponse` senza un elemento `Accept`.  
  
-   B1110: se un risponditore Reliable Messaging respinge la sequenza offerta, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera errori nella sequenza appena stabilita.  
  
-   B1111: se `CreateSequence` non contiene un elemento `Offer`, il risponditore bidirezionale [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] respinge la sequenza offerta rispondendo con un errore `CreateSequenceRefused`.  
  
-   R1112: quando vengono stabilite due sequenze opposte utilizzando il meccanismo `Offer`, la proprietà `[address]` del riferimento dell'endpoint `CreateSequenceResponse/Accept/AcksTo` deve corrispondere all'URI di destinazione del messaggio `CreateSequence`, byte per byte.  
  
-   R1113: quando vengono stabilite due sequenze opposte utilizzando il meccanismo `Offer`, tutti i messaggi su entrambe le sequenze dall'iniziatore al risponditore devono essere inviati allo stesso riferimento dell'endpoint.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza WS\-ReliableMessaging per stabilire sessioni affidabili tra l'iniziatore e il risponditore.L'implementazione di WS\-ReliableMessaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] offre una sessione affidabile per modelli di messaggistica unidirezionali, request\/reply e full duplex.Il meccanismo `Offer` di WS\-Reliable Messaging in `CreateSequence` e `CreateSequenceResponse` consente di stabilire due sequenze opposte correlate e fornisce un protocollo della sessione idoneo per tutti gli endpoint del messaggio.Dato che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce una garanzia di sicurezza per tale sessione, inclusa la protezione end\-to\-end per l'integrità della sessione, è consigliabile assicurarsi che i messaggi destinati alla stessa parte arrivino alla stessa destinazione.Ciò consente anche il "piggy\-backing" degli acknowledgement della sequenza sui messaggi dell'applicazione.A [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si applicano pertanto i vincoli R1102, R1112 e R1113.  
  
 Esempio di messaggio `CreateSequence`.  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:MessageID>  
    <wsa:ReplyTo>  
        <wsa:Address>http://Business456.com/clientA</wsa:Address>   
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequence>  
      <wsrm:AcksTo>  
        <wsa:Address>http://Business456.com/clientA</wsa:Address>  
      </wsrm:AcksTo>  
      <wsrm:Offer>  
        <wsrm:Identifier>urn:uuid:066b4730-fc82-458a-a5c1-210be4fb4e4e</wsrm:Identifier>  
        <wsrm:Endpoint>  
          <wsa:Address>http://Business456.com/clientA</wsa:Address>  
        </wsrm:Endpoint>  
        <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>  
      </wsrm:Offer>  
    </wsrm:CreateSequence>  
  </s:Body>  
</s:Envelope>  
```  
  
 Esempio di un messaggio `CreateSequenceResponse`.  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>  
      <wsrm:Accept>  
        <wsrm:AcksTo>  
          <wsa:Address>http://BusinessABC.com/serviceA</wsa:Address>  
        </wsrm:AcksTo>  
      </wsrm:Accept>  
    </wsrm:CreateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### Chiusura di una sequenza  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza i messaggi `CloseSequence` e `CloseSequenceResponse` per un arresto iniziato dall'origine di Reliable Messaging.La destinazione di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non inizia l'arresto e l'origine di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta un arresto iniziato dalla destinazione di Reliable Messaging.Si applicano i vincoli seguenti:  
  
-   B1201: l'origine di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] invia sempre un messaggio `CloseSequence` per chiudere la sequenza.  
  
-   B1202: l'origine di Reliable Messaging attende l'acknowledgment dell'intera serie di messaggi della sequenza prima di inviare il messaggio `CloseSequence`.  
  
-   B1203: l'origine di Reliable Messaging include sempre l'elemento facoltativo `LastMsgNumber`. Non lo include se la sequenza non contiene messaggi.  
  
-   R1204: la destinazione di Reliable Messaging non deve iniziare l'arresto inviando un messaggio `CloseSequence`.  
  
-   B1205: al ricevimento di un messaggio `CloseSequence`, l'origine di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] considera la sequenza incompleta e invia un errore.  
  
 Esempio di messaggio `CloseSequence`.  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:MessageID>  
    <wsa:ReplyTo>  
      <wsa:Address>http://Business456.com/clientA</wsa:Address>  
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CloseSequence>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>  
    </wsrm:CloseSequence>  
  </s:Body>  
</s:Envelope>  
Example CloseSequenceResponse message:  
<s:Envelope>  
  <s:Header>  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>  
      <wsrm:Final></wsrm:Final>  
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CloseSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
    </wsrm:CloseSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### Terminazione della sequenza  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza principalmente l'handshake `TerminateSequence/TerminateSequenceResponse` al completamento dell'handshake `CloseSequence/CloseSequenceResponse`.La destinazione di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non inizia la terminazione e l'origine di Reliable Messaging non supporta una terminazione iniziata dalla destinazione di Reliable Messaging.Si applicano i vincoli seguenti:  
  
-   B1301: l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] invia il messaggio `TerminateSequence` solo al completamento corretto dell'handshake `CloseSequence/CloseSequenceResponse`.  
  
-   R1302: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla che l'elemento `LastMsgNumber` sia coerente in tutti i messaggi `CloseSequence` e `TerminateSequence` per una data sequenza.Ciò significa che `LastMsgNumber` o non è presente in tutti i messaggi `CloseSequence` e `TerminateSequence`, o è presente e identico in tutti i messaggi `CloseSequence` e `TerminateSequence`.  
  
-   B1303: al ricevimento di un messaggio `TerminateSequence` dopo l'handshake `CloseSequence/CloseSequenceResponse`, la destinazione di Reliable Messaging risponde con un messaggio `TerminateSequenceResponse`.Poiché l'origine di Reliable Messaging dispone dell'acknowledgement finale prima dell'invio del messaggio `TerminateSequence`, la destinazione di Reliable Messaging è a conoscenza della fine della sequenza e richiede immediatamente le risorse.  
  
-   B1304: se viene ricevuto un messaggio `TerminateSequence` prima dell'handshake `CloseSequence/CloseSequenceResponse`, la destinazione di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] risponde con un messaggio `TerminateSequenceResponse`.Se la destinazione di Reliable Messaging stabilisce che non vi sono incoerenze nella sequenza, attende per il periodo di tempo specificato dalla destinazione dell'applicazione prima di richiedere le risorse, per offrire al client la possibilità di ricevere l'acknowledgement finale.In caso contrario, la destinazione di Reliable Messaging richiede immediatamente le risorse e indica alla destinazione dell'applicazione che la sequenza termina in modo dubbio generando l'evento `Faulted`.  
  
 Esempio di messaggio `TerminateSequence`.  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:MessageID>  
    <wsa:ReplyTo>  
      <wsa:Address>http://Business456.com/clientA</wsa:Address>  
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:TerminateSequence>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>  
      </wsrm:TerminateSequence>  
  </s:Body>  
</s:Envelope>  
Example TerminateSequenceResponse message:  
<s:Envelope>  
  <s:Header>  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>  
      <wsrm:Final></wsrm:Final>  
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:TerminateSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
    </wsrm:TerminateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### Sequenze  
 Di seguito è riportato un elenco di vincoli che si applicano alle sequenze:  
  
-   B1401:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera e accede a numeri di sequenza non superiori al valore massimo di `xs:long`, 9223372036854775807 incluso.  
  
 Esempio di intestazione `Sequence`.  
  
```  
<wsrm:Sequence s:mustUnderstand="1">  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
  <wsrm:MessageNumber>1</wsrm:MessageNumber>  
</wsrm:Sequence>  
```  
  
### Acknowledgement della richiesta  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'intestazione `AckRequested` come meccanismo keep\-alive.  
  
 Esempio di intestazione `AckRequested`.  
  
```  
<wsrm:AckRequested>  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
</wsrm:AckRequested>  
```  
  
### SequenceAcknowledgement  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza un meccanismo "piggy\-back" per gli acknowledgement di sequenza forniti in WS\-Reliable Messaging.Si applicano i vincoli seguenti:  
  
-   R1601: quando vengono stabilite due sequenze opposte utilizzando il meccanismo `Offer`, l'intestazione `SequenceAcknowledgement` può essere inclusa in qualsiasi messaggio dell'applicazione trasmesso al destinatario desiderato.L'endpoint remoto deve essere in grado di accedere a un'intestazione `SequenceAcknowledgement` sottoposta a piggyback.  
  
-   B1602: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera intestazioni `SequenceAcknowledgement` che contengono elementi `Nack`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verifica che ogni elemento `Nack` contenga un numero di sequenza, ma in caso contrario ignora il valore e l'elemento `Nack`.  
  
 Esempio di intestazione `SequenceAcknowledgement`.  
  
```  
<wsrm:SequenceAcknowledgement>  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
  <wsrm:AcknowledgementRange Lower="1" Upper="1"></wsrm:AcknowledgementRange>  
</wsrm:SequenceAcknowledgement>  
```  
  
### Errori WS\-ReliableMessaging  
 Di seguito è riportato un elenco di vincoli che si applicano all'implementazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di errori WS\-ReliableMessaging.Si applicano i vincoli seguenti:  
  
-   B1701: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera errori `MessageNumberRollover`.  
  
-   B1702: su SOAP 1.2 quando l'endpoint del servizio raggiunge il limite di connessione e non è in grado di elaborare nuove connessioni, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un codice secondario dell'errore `CreateSequenceRefused` annidato, `netrm:ConnectionLimitReached`, come illustrato nell'esempio seguente.  
  
```  
<s:Envelope>  
  <s:Header>  
    <wsa:Action>http://docs.oasis-open.org/ws-rx/wsrm/200702/fault</wsa:Action>  
  </s:Header>  
  <s:Body>  
    <s:Fault>  
      <s:Code>  
        <s:Value>s:Receiver</s:Value>  
        <s:Subcode>  
          <s:Value>wsrm:CreateSequenceRefused</s:Value>  
          <s:Subcode>  
            <s:Value>netrm:ConnectionLimitReached</s:Value>  
          </s:Subcode>  
        </s:Subcode>  
      </s:Code>  
      <s:Reason>  
        <s:Text xml:lang="en">Server 'http://BusinessABC.com/serviceA' is too busy to process this request. Try again later.</s:Text>  
      </s:Reason>  
    </s:Fault>  
  </s:Body>  
</s:Envelope>  
```  
  
### Errori WS\-Addressing  
 Dato che WS\-ReliableMessaging utilizza WS\-Addressing, l'implementazione WS\-ReliableMessaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] potrebbe generare e trasmettere errori WS\-Addressing.In questa sezione vengono illustrati gli errori WS\-Addressing generati e trasmessi in modo esplicito da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] a livello di WS\-ReliableMessaging:  
  
-   B1801:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera e trasmette l'errore `Message Addressing Header Required` quando si verifica una delle condizioni seguenti:  
  
    -   In un messaggio `CreateSequence`, `CloseSequence` o `TerminateSequence` manca un'intestazione `MessageId`.  
  
    -   In un messaggio `CreateSequence`, `CloseSequence` o `TerminateSequence` manca un'intestazione `ReplyTo`.  
  
    -   In un messaggio `CreateSequenceResponse`, `CloseSequenceResponse` o `TerminateSequenceResponse` manca un'intestazione `RelatesTo`.  
  
-   B1802:[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera e trasmette l'errore `Endpoint Unavailable` a indicare che nessun endpoint in ascolto è in grado di elaborare la sequenza in base all'esame delle intestazioni di indirizzamento nel messaggio `CreateSequence`.  
  
## Composizione del protocollo  
  
### Composizione con WS\-Addressing  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta due versioni di WS\-Addressing: WS\-Addressing 2004\/08 \[WS\-ADDR\] e W3C WS\-Addressing 1.0 Recommendation \[WS\-ADDR\-CORE\] e \[WS\-ADDR\-SOAP\].  
  
 Anche se la specifica WS\-ReliableMessaging menziona solo WS\-Addressing 2004\/08, non limita la versione WS\-Addressing da utilizzare.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   R2101: sia WS\-Addressing 2004\/08 che WS\-Addressing 1.0 possono essere utilizzati con WS\-Reliable Messaging.  
  
-   R2102: è necessario utilizzare una sola versione di WS\-Addressing in una data sequenza di WS\-Reliable Messaging o in una coppia di sequenze opposte correlate tramite il meccanismo `Offer`.  
  
### Composizione con SOAP  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta l'utilizzo sia di SOAP 1.1 che di SOAP 1.2 con WS\-Reliable Messaging.  
  
### Composizione con WS\-Security e WS\-SecureConversation  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce protezione per le sequenze di WS\-Reliable Messaging utilizzando trasporto protetto \(HTTPS\), composizione con WS\-Security e composizione con WS\-SecureConversation.Il protocollo WS\-Reliable Messaging 1.1, WS\-Security 1.1 e il protocollo WS\-SecureConversation 1.3 devono essere utilizzati insieme.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   R2301: per proteggere l'integrità di una sequenza di WS\-Reliable Messaging oltre all'integrità e alla riservatezza dei singoli messaggi, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede l'utilizzo di WS\-SecureConversation.  
  
-   R2302: prima di stabilire la\(e\) sequenza\(e\) di WS\-Reliable Messaging, è necessario stabilire una sessione WS\-SecureConversation.  
  
-   R2303: se la durata della sequenza di WS\-Reliable Messaging supera la durata della sessione WS\-SecureConversation, è necessario rinnovare il `SecurityContextToken` stabilito tramite WS\-SecureConversation utilizzando l'associazione WS\-Secure Conversation Renewal corrispondente.  
  
-   B2304: la sequenza WS\-ReliableMessaging o una coppia di sequenze opposte sono sempre associate a una singola sessione WS\-SecureConversation.  
  
-   R2305: in caso di composizione con WS\-SecureConversation, il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede che il messaggio `CreateSequence` contenga l'elemento `wsse:SecurityTokenReference` e l'intestazione `wsrm:UsesSequenceSTR`.  
  
 Esempio di intestazione `UsesSequenceSTR`.  
  
```  
<wsrm:UsesSequenceSTR></wsrm:UsesSequenceSTR>  
```  
  
### Composizione con sessioni SSL\/TLS  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta la composizione con sessioni SSL\/TLS:  
  
-   B2401: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera l'intestazione `wsrm:UsesSequenceSSL`.  
  
-   R2402: un iniziatore Reliable Messaging non deve inviare un messaggio `CreateSequence` con l'intestazione `wsrm:UsesSequenceSSL` a un risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
### Composizione con WS\-Policy  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta due versioni di WS\-Policy: WS\-Policy 1.2 e WS\-Policy 1.5.  
  
## Asserzione di WS\-Policy relativa a WS\-ReliableMessaging  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'asserzione di WS\-Policy `wsrm:RMAssertion` relativa a WS\-ReliableMessaging per descrivere le funzionalità degli endpoint.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   B3001: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] collega l'asserzione di WS\-Policy `wsrmn:RMAssertion` agli elementi `wsdl:binding`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta i collegamenti agli elementi `wsdl:binding` e `wsdl:port`.  
  
-   B3002: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non genera mai il tag `wsp:Optional`.  
  
-   B3003: quando si accede all'asserzione di WS\-Policy `wsrmp:RMAssertion`, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ignora il tag `wsp:Optional` e considera obbligatorio il criterio WS\-RM.  
  
-   R3004: poiché [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non esegue la composizione con sessioni SSL\/TLS, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non accetta il criterio che specifica `wsrmp:SequenceTransportSecurity`.  
  
-   B3005: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera sempre l'elemento `wsrmp:DeliveryAssurance`.  
  
-   B3006: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] specifica sempre la garanzia di recapito `wsrmp:ExactlyOnce`.  
  
-   B3007: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera e legge le proprietà seguenti dell'asserzione WS\-ReliableMessaging e fornisce un controllo su di esse in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]`ReliableSessionBindingElement`:  
  
    -   `netrmp:InactivityTimeout`  
  
    -   `netrmp:AcknowledgementInterval`  
  
     Esempio di `RMAssertion`.  
  
    ```  
    <wsrmp:RMAssertion>  
      <wsp:Policy>  
        <wsrmp:SequenceSTR/>  
        <wsrmp:DeliveryAssurance>  
          <wsp:Policy>  
            <wsrmp:ExactlyOnce/>  
            <wsrmp:InOrder/>  
          </wsp:Policy>  
        </wsrmp:DeliveryAssurance>  
      </wsp:Policy>  
      <netrmp:InactivityTimeout Milliseconds="600000"/>  
      <netrmp:AcknowledgementInterval Milliseconds="200"/>  
    </wsrmp:RMAssertion>  
    ```  
  
## Estensione di WS\-ReliableMessaging per il controllo del flusso  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'estendibilità di WS\-ReliableMessaging per offrire un controllo facoltativo aggiuntivo più rigido sul flusso di messaggi della sequenza.  
  
 Per attivare il controllo del flusso, impostare la proprietà `FlowControlEnabled``boolean` di `ReliableSessionBindingElement` su `true`.Di seguito è riportato un elenco di vincoli che si applicano a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   B4001: quando il controllo di flusso di Reliable Messaging è attivato, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera un elemento `netrm:BufferRemaining` nell'estendibilità dell'elemento dell'intestazione `SequenceAcknowledgement`, come illustrato nell'esempio seguente.  
  
    ```  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Upper="1" Lower="1"/>             
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    ```  
  
-   B4002: anche quando il controllo di flusso di Reliable Messaging è attivato, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non richiede un elemento `netrm:BufferRemaining` nell'intestazione `SequenceAcknowledgement`.  
  
-   B4003: la destinazione di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza `netrm:BufferRemaining` per indicare quanti messaggi nuovi è in grado di memorizzare nel buffer.  
  
-   B4004: quando il controllo di flusso di Reliable Messaging è attivato, l'origine di Reliable Messaging di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza il valore di `netrm:BufferRemaining` per limitare la trasmissione dei messaggi.  
  
-   B4005: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] genera valori integer `netrm:BufferRemaining` tra 0 e 4096 incluso e legge valori integer tra 0 e il valore `maxInclusive` di `xs:int`, 214748364 incluso.  
  
## Modelli di scambio dei messaggi  
 In questa sezione viene illustrato il comportamento di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando WS\-ReliableMessaging è utilizzato per modelli di scambio di messaggi diversi.Per ogni modello di scambio di messaggi, vengono presi in considerazione i due scenari di distribuzione seguenti:  
  
-   Iniziatore non indirizzabile: l'iniziatore si trova dietro a un firewall; il risponditore può recapitare messaggi all'iniziatore solo su risposte HTTP.  
  
-   Iniziatore indirizzabile: le richieste HTTP possono essere inviate sia all'iniziatore che al risponditore. In altre parole, è possibile stabilire due connessioni HTTP opposte.  
  
### Iniziatore unidirezionale, non indirizzabile  
  
#### Associazione  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello unidirezionale di scambio di messaggi utilizzando una sequenza in un canale HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi dall'iniziatore alle risposte del risponditore e di HTTP per trasmettere tutti i messaggi dal risponditore all'iniziatore.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `CreateSequence` senza alcun elemento `Offer` su una richiesta HTTP e attende il messaggio `CreateSequenceResponse` sulla risposta HTTP.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea una sequenza e trasmette il messaggio `CreateSequenceResponse` senza alcun elemento `Accept` sulla risposta HTTP.  
  
#### SequenceAcknowledgement  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] elabora gli acknowledgement sulla risposta di tutti i messaggi tranne il messaggio `CreateSequence` e i messaggi di errore.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette sempre un acknowledgement autonomo sulla risposta HTTP a tutte le sequenze e ai messaggi `AckRequested`.  
  
#### Scambio CloseSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `CloseSequence` su una richiesta HTTP e attende il messaggio `CreateSequenceResponse` sulla risposta HTTP.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette il messaggio `CloseSequenceResponse` sulla risposta HTTP.  
  
#### Scambio TerminateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `TerminateSequence` su una richiesta HTTP e attende il messaggio `TerminateSequenceResponse` sulla risposta HTTP.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette il messaggio `TerminateSequenceResponse` sulla risposta HTTP.  
  
### Iniziatore unidirezionale, indirizzabile  
  
#### Associazione  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di scambio di messaggi unidirezionale utilizzando una sequenza su un canale HTTP in ingresso e su uno in uscita.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi.Tutte le risposte HTTP hanno un corpo vuoto e un codice di stato HTTP 202.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `CreateSequence` senza alcun elemento `Offer` su una richiesta HTTP.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea una sequenza e trasmette il messaggio `CreateSequenceResponse` senza alcun elemento `Accept` su una richiesta HTTP.  
  
### Iniziatore duplex, indirizzabile  
  
#### Associazione  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di scambio di messaggi bidirezionale completamente asincrono utilizzando due sequenze su un canale HTTP in ingresso e su uno in uscita.Questo modello di scambio può essere combinato con il modello di scambio di messaggi `Request/Reply` dell'iniziatore `Addressable` in modo limitato.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza richieste HTTP per trasmettere tutti i messaggi.Tutte le risposte HTTP hanno un corpo vuoto e un codice di stato HTTP 202.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `CreateSequence` con un elemento `Offer` su una richiesta HTTP.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla che `CreateSequence` abbia un elemento `Offer`, quindi crea una sequenza e trasmette il messaggio `CreateSequenceResponse` con un elemento `Accept`.  
  
#### Durata della sequenza  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tratta le due sequenze come una sessione completamente duplex.  
  
 Dopo la generazione di un errore che origina errori in una sequenza, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si aspetta che l'endpoint crei errori in entrambe le sequenze.Dopo la lettura di un errore che origina errori in una sequenza, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea errori in entrambe le sequenze.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può chiudere la sequenza in uscita e continuare a elaborare i messaggi sulla sua sequenza in ingresso.Per contro, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può elaborare la chiusura della sequenza in ingresso e continuare a inviare i messaggi sulla sua sequenza in uscita.  
  
### Iniziatore request\/reply e unidirezionale, non indirizzabile  
  
#### Associazione  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di scambio di messaggi request\/reply e unidirezionale utilizzando due sequenze in un canale HTTP.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi dall'iniziatore alle risposte del risponditore e di HTTP per trasmettere tutti i messaggi dal risponditore all'iniziatore.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `CreateSequence` con un elemento `Offer` su una richiesta HTTP e attende il messaggio `CreateSequenceResponse` sulla risposta HTTP.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea una sequenza e trasmette il messaggio `CreateSequenceResponse` con un elemento `Accept` sulla risposta HTTP.  
  
#### Messaggio unidirezionale  
 Per completare correttamente uno scambio di messaggi unidirezionale, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio della sequenza di richiesta sulla richiesta HTTP e riceve un messaggio `SequenceAcknowledgement` autonomo sulla risposta HTTP.`SequenceAcknowledgement` deve riconoscere il messaggio trasmesso.  
  
 Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può rispondere alla richiesta con un acknowledgement, un errore o una risposta con un corpo vuoto e un codice di stato HTTP 202.  
  
#### Messaggi bidirezionali  
 Per completare correttamente un protocollo di scambio di messaggi bidirezionale, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio della sequenza di richiesta sulla richiesta HTTP e riceve un messaggio della sequenza di risposta sulla risposta HTTP.La risposta deve contenere un `SequenceAcknowledgement` che riconosce che il messaggio della sequenza di richiesta è stato trasmesso.  
  
 Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può rispondere alla richiesta con una risposta dell'applicazione, un errore o una risposta con un corpo vuoto e un codice di stato HTTP 202.  
  
 A causa della presenza di messaggi unidirezionali e del tempo delle risposte dell'applicazione, il numero di sequenza del messaggio della sequenza di richiesta e il numero di sequenza del messaggio di risposta non hanno alcuna correlazione.  
  
#### Nuovi tentativi di risposte  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si basa sulla correlazione request\/reply HTTP per la correlazione del protocollo di scambio di messaggi bidirezionali.Di conseguenza, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non smette di tentare un messaggio della sequenza di richiesta quando tale messaggio viene riconosciuto, ma piuttosto quando la risposta HTTP contiene un `SequenceAcknowledgement`, una risposta dell'applicazione o un errore.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ritenta le risposte sulla risposta HTTP della richiesta alla quale è correlata la risposta.  
  
#### Scambio CloseSequence  
 Dopo avere ricevuto tutti i messaggi della sequenza di risposta e gli acknowledgement per tutti i messaggi della sequenza di richiesta unidirezionali, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `CloseSequence` per la sequenza di richiesta su una richiesta HTTP e attende la `CloseSequenceResponse` sulla risposta HTTP.  
  
 Se la sequenza di richiesta viene chiusa in modo implicito, viene chiusa anche la sequenza di risposta.Ciò significa che l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] include il `SequenceAcknowledgement` finale della sequenza di risposta sul messaggio `CloseSequence` e che la sequenza di risposta non ha uno scambio `CloseSequence`.  
  
 Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assicura che tutte le risposte vengano riconosciute e trasmette il messaggio `CloseSequenceResponse` sulla risposta HTTP.  
  
#### Scambio TerminateSequence  
 Dopo la ricezione del messaggio `CloseSequenceResponse`, l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `TerminateSequence` per la sequenza di richiesta su una richiesta HTTP e attende la `TerminateSequenceResponse` sulla risposta HTTP.  
  
 Analogamente allo scambio `CloseSequence`, la terminazione della sequenza di richiesta in modo implicito termina la sequenza di risposta.Ciò significa che l'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] include il `SequenceAcknowledgement` finale della sequenza di risposta sul messaggio `TerminateSequence` e che la sequenza di risposta non ha uno scambio `TerminateSequence`.  
  
 Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette il messaggio `TerminateSequenceResponse` sulla risposta HTTP.  
  
### Iniziatore request\/reply, indirizzabile  
  
#### Associazione  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di scambio di messaggi request\/reply utilizzando due sequenze su un canale HTTP in ingresso e su uno in uscita.Questo modello di scambio può essere combinato con il modello di scambio di messaggi `Duplex, Addressable` in modo limitato.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le richieste HTTP per trasmettere tutti i messaggi.Tutte le risposte HTTP hanno un corpo vuoto e un codice di stato HTTP 202.  
  
#### Scambio CreateSequence  
 L'iniziatore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] trasmette un messaggio `CreateSequence` con un elemento `Offer` su una richiesta HTTP.Il risponditore [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla che `CreateSequence` abbia un elemento `Offer`, quindi crea una sequenza e trasmette il messaggio `CreateSequenceResponse` con un elemento `Accept`.  
  
#### Correlazione request\/reply  
 Quanto riportato di seguito si applica a tutte le richieste e le risposte correlate:  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla che tutti i messaggi di richiesta dell'applicazione contengano un riferimento all'endpoint `ReplyTo` e un `MessageId`.  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] applica il riferimento dell'endpoint locale come `ReplyTo` di ogni messaggio di richiesta dell'applicazione.Il riferimento dell'endpoint locale è `ReplyTo` del messaggio `CreateSequence` per l'iniziatore e `To` del messaggio `CreateSequence` per il risponditore.  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla che i messaggi di richiesta in entrata contengano un `MessageId` e un `ReplyTo`.  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla che l'URI di riferimento dell'endpoint `ReplyTo` di tutti i messaggi di richiesta dell'applicazione corrisponda al riferimento dell'endpoint locale come definito in precedenza.  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla che tutte le risposte contengano le intestazioni `RelatesTo` e `To`, in conformità con le regole di correlazione request\/reply di  `wsa`.