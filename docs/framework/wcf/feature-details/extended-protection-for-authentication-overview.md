---
title: "Panoramica sulla protezione estesa per l&#39;autenticazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d2ceffe-a7bf-4bd9-a5a2-9406423bd7f8
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# Panoramica sulla protezione estesa per l&#39;autenticazione
La protezione estesa per l'autenticazione consente di impedire attacchi man\-in\-the\-middle \(MITM\) in cui l'autore di un attacco intercetta le credenziali del client e le inoltra a un server.  
  
 Si consideri ad esempio uno scenario in cui sono presenti un client, un server e l'autore di un attacco.Gli URL del server e dell'autore dell'attacco sono, rispettivamente, `https://server` e `https://attacker`.L'autore dell'attacco induce il client ad accedere all'autore stesso come se fosse il server,quindi invia una richiesta al server.Se l'autore dell'attacco sta tentando di accedere a una risorsa protetta, il server risponde con un'intestazione WWW\-Authenticate.Poiché l'autore dell'attacco non dispone delle informazioni di autenticazione, invia l'intestazione WWW\-Authenticate al client.A questo punto il client invia l'intestazione Authorization all'autore dell'attacco che a sua volta la inoltra al server e ottiene l'accesso alle risorse protette utilizzando le credenziali del client.  
  
 Attualmente, quando un'applicazione client si autentica nel server con i metodi Kerberos, Digest o NTLM utilizzando il protocollo HTTPS, viene innanzitutto stabilito un canale TLS \(Transport Level Security\) mediante il quale viene eseguita l'autenticazione.Poiché non esiste alcuna associazione tra la chiave di sessione generata dal protocollo SSL \(Secure Sockets Layer\) e quella generata durante l'autenticazione,se nello scenario precedente la comunicazione viene eseguita tramite un canale TLS, ad esempio un canale HTTPS, sono presenti due canali SSL, uno tra il client e l'autore dell'attacco e un altro tra l'autore dell'attacco e il server.Le credenziali del client vengono inviate dal client al server prima sul canale SSL tra il client e l'autore dell'attacco e successivamente sul canale tra l'autore dell'attacco e il server.Dopo che ha ricevuto le credenziali del client, il server le verifica senza rilevare che il canale su cui sono state inviate è stato originato con l'autore dell'attacco e non con il client.  
  
 La soluzione prevede l'utilizzo di un canale esterno protetto da TLS e di un canale interno autenticato dal client nonché il passaggio di un token di associazione del canale al server.Tale token rappresenta una proprietà del canale esterno protetto da TLS e viene utilizzato per associare il canale esterno a una conversazione sul canale interno autenticato dal client.  
  
 Nello scenario precedente il token di associazione del canale TLS tra l'autore dell'attacco e il client viene unito con le informazioni di autorizzazione inviate al server.Un server abilitato al riconoscimento del token confronta il token ricevuto con le informazioni di autenticazione del client, che corrisponde al canale tra l'autore del canale e il client, con quello collegato al canale tra il server e l'autore dell'attacco.Poiché un token di associazione del canale è specifico di un canale di destinazione, il token relativo al canale tra l'autore dell'attacco e il client non corrisponde a quello relativo al canale tra l'autore dell'attacco e il server.Il questo modo il server è in grado di rilevare l'attacco man\-in\-the\-middle e di rifiutare la richiesta di autenticazione.  
  
 Nel lato client non è necessaria alcuna impostazione di configurazione.Una volta che è stato aggiornato per passare il token di associazione del canale al server, il client esegue sempre questa operazione.Se anche il server è stato aggiornato, può essere configurato per utilizzare il token o per ignorarlo.In caso contrario, il server ignora il token.  
  
 Nel server possono essere implementati i livelli di protezione seguenti:  
  
-   Nessuno.Non viene eseguita alcuna convalida dell'associazione di canale.Questo comportamento è tipico di tutti i server che non sono stati aggiornati.  
  
-   Parziale.Tutti i client che sono stati aggiornati devono inviare informazioni di associazione del canale al server,a differenza di quelli che non sono stati aggiornati.Questa è un'opzione di protezione intermedia che consente la compatibilità tra le applicazioni.  
  
-   Completa.Tutti i client devono inviare informazioni di associazione del canale al server,Il server rifiuterà le richiese di autenticazione ai client che non eseguono questa operazione.  
  
 Per ulteriori informazioni, vedere l'esempio Win7 CBT\/Extended Protection.  
  
## Vedere anche  
 [Sicurezza e protezione](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)