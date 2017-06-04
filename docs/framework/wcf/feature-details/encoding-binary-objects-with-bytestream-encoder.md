---
title: "Codifica di oggetti binari con il codificatore ByteStream | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 020ee981-c889-4b12-a3ea-91823ef46444
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Codifica di oggetti binari con il codificatore ByteStream
L'invio e la ricezione di dati binari non elaborati con [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] vengono configurati utilizzando <xref:System.ServiceModel.Channels.ByteStreamMessageEncodingBindingElement>.  
  
## Architettura del codificatore di messaggi del flusso di byte  
 Il codificatore di messaggi binario utilizzato da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non dispone di funzionalità per l'elaborazione, la convalida o l'identificazione dei dati binari sottostanti nel messaggio.Il pacchetto dei dati viene codificato in XML, inviato, ricevuto e decodificato.Il codificatore elabora i dati dopo essere passati al trasporto e prima che il messaggio venga inviato alla coda di messaggi.A livello funzionale, il codificatore binario esegue il wrapping dei dati del messaggio negli elementi `<binary>` per l'invio e rimuove gli elementi in seguito alla ricezione del messaggio.  
  
## Utilizzo del codificatore di messaggi del flusso di byte  
 Nell'esempio seguente viene mostrato un contratto di servizio che implementa il codificatore di messaggi del flusso di byte.  
  
```csharp  
[OperationContract]  
Void Myfunction(Stream stream);  
```  
  
 Nell'esempio riportato di seguito viene illustrato il servizio richiamato.  
  
```csharp  
proxy.MyFunction(stream);  
```  
  
 In caso di utilizzo di un servizio che implementa un'infrastruttura di messaggi \(ad esempio, un router\), il messaggio viene elaborato senza controllo, convalida o interazione con il messaggio, come mostrato nell'esempio seguente.  
  
```csharp  
[OperationContract]  
void ProcessMessage(Message message) ;  
```  
  
## Scenari  
 Il codificatore del flusso di byte è utile negli scenari seguenti.  
  
-   Trasferimento di un'immagine JPEG tra computer mediante [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].In questo scenario l'immagine arriva tramite il trasporto da un'origine esterna e i dati inviati saranno i byte non elaborati che costituiscono l'immagine.Un servizio riceverà i dati binari e visualizzerà l'immagine.  
  
-   Lettura delle informazioni al di fuori di una coda di messaggi ed elaborazione delle informazioni.Il messaggio verrà letto da un gestore delle code di messaggi e verrà passato al canale della coda di messaggi per essere gestito.Il canale della coda di messaggi fungerà da gestore delle code nello stack di canali di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 In caso di invio di un messaggio tramite un canale della coda di messaggi, il mittente non avrà alcun controllo sui byte ricevuti dal gestore delle code.Se il processo di ricezione non è in grado di leggere i byte non elaborati, il messaggio verrà ricevuto in un formato non corretto e non verrà elaborato. Si presuppone che il processo di ricezione sia in grado di convertire i byte ricevuti in un formato utilizzabile.