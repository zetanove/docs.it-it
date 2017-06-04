---
title: "Denial of Service (Negazione del servizio) | Microsoft Docs"
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
  - "Denial of Service (Negazione del servizio) [WCF]"
ms.assetid: dfb150f3-d598-4697-a5e6-6779e4f9b600
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Denial of Service (Negazione del servizio)
Si verifica un attacco Denial of Service quando un sistema viene sommerso da una quantità di messaggi tale da non poter essere elaborata o da poter essere elaborata solo molto lentamente.  
  
## Eccessivo consumo di memoria  
 Quando viene letto un documento XML con un numero elevato di nomi locali, spazi dei nomi o prefissi univoci, può verificarsi un problema.  Se si usa una classe che deriva da <xref:System.Xml.XmlReader> e si chiama la proprietà <xref:System.Xml.XmlReader.LocalName%2A>, <xref:System.Xml.XmlReader.Prefix%2A> o <xref:System.Xml.XmlReader.NamespaceUri%2A> per ogni elemento, la stringa restituita viene aggiunta a una classe <xref:System.Xml.NameTable>.  Le dimensioni della raccolta contenuta nella classe <xref:System.Xml.NameTable> non diminuiscono mai, creando una "perdita di memoria" virtuale degli handle di stringa.  
  
 Le prevenzioni includono:  
  
-   Derivare dalla classe <xref:System.Xml.NameTable> e imporre una quota della dimensione massima.  Non è possibile impedire l'uso di una classe <xref:System.Xml.NameTable> o cambiare la classe <xref:System.Xml.NameTable> quando è completa.  
  
-   Evitare di usare le proprietà citate e impiegare invece il metodo <xref:System.Xml.XmlReader.MoveToAttribute%2A> con il metodo <xref:System.Xml.XmlReader.IsStartElement%2A> quando possibile; questi metodi non restituiscono stringhe e non provocano quindi problemi di superamento della capacità della raccolta <xref:System.Xml.NameTable>.  
  
## Il client dannoso invia un numero eccessivo di richieste di licenza al servizio  
 Se un client dannoso bombarda un servizio con un numero eccessivo di richieste di licenza, può costringere il server a usare troppa memoria.  
  
 Prevenzione: usare le proprietà seguenti della classe <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>:  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxCachedCookies%2A>: controlla il numero massimo di classi `SecurityContextToken` temporali memorizzate nella cache dal server dopo la negoziazione `SPNego` o `SSL`.  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.IssuedCookieLifetime%2A>: controlla la durata della classe `SecurityContextTokens` rilasciata dal server in seguito alla negoziazione `SPNego` o `SSL`.  Il server memorizza nella cache la classe `SecurityContextToken` per questo periodo di tempo.  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxPendingSessions%2A>: controlla il numero massimo di conversazioni protette stabilite nel server, per cui però non sono stati elaborati messaggi dell'applicazione.  Questa quota impedisce ai client di stabilire conversazioni protette nel servizio, facendo così in modo che il servizio mantenga lo stato per client, senza mai usare i client.  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.InactivityTimeout%2A>: controlla il tempo massimo in cui il servizio mantiene attiva una conversazione protetta senza ricevere un messaggio dell'applicazione dal client per la conversazione.  Questa quota impedisce ai client di stabilire conversazioni protette nel servizio, facendo così in modo che il servizio mantenga lo stato per client, senza mai usare i client.  
  
## Necessità dell'autenticazione client per WSDualHttpBinding o per le doppie associazioni personalizzate  
 Per impostazione predefinita, <xref:System.ServiceModel.WSDualHttpBinding> ha la sicurezza abilitata.  È tuttavia possibile che, se l'autenticazione client viene disattivata impostando la proprietà <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> su <xref:System.ServiceModel.MessageCredentialType>, un utente malintenzionato provochi un attacco Denial of Service in un terzo servizio.  Ciò può verificarsi perché un client dannoso può indicare al servizio di inviare un flusso di messaggi a un terzo servizio.  
  
 Per prevenire il problema, non impostare la proprietà su `None`.  Occorre essere consapevoli di questa possibilità quando si crea un'associazione personalizzata con un modello di messaggio doppio.  
  
## Possibilità di riempimento del registro eventi di controllo  
 Se un utente malintenzionato comprende che è attivato il controllo, può inviare messaggi non validi che causano la scrittura di voci di controllo.  Ciò comporta a sua volta la generazione di errori nel sistema di controllo.  
  
 Per ridurre questo problema, impostare la proprietà <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> su `true` e usare le proprietà del Visualizzatore eventi per controllare il comportamento di controllo.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'uso e del Visualizzatore eventi per visualizzare e gestire i log eventi, vedere [Visualizzatore eventi](http://go.microsoft.com/fwlink/?LinkId=186123).  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
## Possibili blocchi del servizio causati da implementazioni non valide di IAuthorizationPolicy  
 La chiamata del metodo <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> su un'implementazione non valida dell'interfaccia <xref:System.IdentityModel.Policy.IAuthorizationPolicy> può causare il blocco del servizio.  
  
 Prevenzione: usare solo codice attendibile.  In altre parole, usare solo codice scritto e verificato o proveniente da un provider attendibile.  Non consentire l'aggiunta nel codice di estensioni non attendibili di <xref:System.IdentityModel.Policy.IAuthorizationPolicy> senza la dovuta considerazione.  Questo vale per tutte le estensioni usate in un'implementazione del servizio.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non fa distinzioni tra codice dell'applicazione e codice esterno aggiunto usando punti di estendibilità.  
  
## Possibile necessità di ridimensionamento per la dimensione massima dei token Kerberos  
 Se un client appartiene a un gran numero di gruppi \(circa 900, anche se il numero effettivo varia a seconda dei gruppi\), può verificarsi un problema quando il blocco dell'intestazione di un messaggio supera i 64 kilobyte.  In questo caso, è possibile aumentare la dimensione massima dei token Kerberos, come descritto nell'articolo del Supporto Tecnico Microsoft sul [malfunzionamento dell'autenticazione Kerberos di Internet Explorer dovuto alla connessione a IIS con un buffer insufficiente](http://go.microsoft.com/fwlink/?LinkId=89176). Può inoltre essere necessario aumentare la dimensione massima dei messaggi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per adattarla al più ampio token Kerberos.  
  
## Generazione da parte della registrazione automatica di più certificati per computer con lo stesso nome di soggetto  
 La *registrazione automatica* è la funzionalità di [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] per registrare automaticamente certificati per utenti e computer.  Quando un computer si trova in un dominio con questa funzionalità attivata, viene automaticamente creato un certificato X.509 con l'obiettivo di eseguire l'autenticazione client, tale certificato viene quindi inserito nell'archivio dei certificati personali del computer locale ogni qualvolta un nuovo computer viene associato alla rete.  Tuttavia, la registrazione automatica usa lo stesso nome di soggetto per tutti i certificati creati nella cache.  
  
 Può quindi accadere che l'apertura dei servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] abbia esito negativo nei domini con la registrazione automatica.  Ciò si verifica perché i criteri predefiniti per la ricerca delle credenziali X.509 del servizio potrebbero essere ambigui, dal momento che esistono più certificati con il nome DNS \(Domain Name System\) completo del computer.  Un certificato ha origine dalla registrazione automatica, l'altro potrebbe invece essere un certificato autorilasciato.  
  
 Per prevenire il problema, fare riferimento al certificato esatto da usare specificando un criterio di ricerca più preciso nell'[\<credenzialiServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md).  Usare, ad esempio, l'opzione <xref:System.Security.Cryptography.X509Certificates.X509FindType> e specificare il certificato in base all'identificazione personale univoca \(hash\).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla funzionalità di registrazione automatica, vedere la pagina relativa alla [registrazione automatica di certificati in Windows Server 2003](http://go.microsoft.com/fwlink/?LinkId=95166).  
  
## Uso per l'autorizzazione dell'ultimo dei diversi nomi di soggetto alternativi  
 Nel raro caso che un certificato X.509 contenga più nomi di soggetto alternativi e si esegua l'autorizzazione usando il nome di soggetto alternativo, l'autorizzazione potrebbe avere esito negativo.  
  
## Protezione dei file di configurazione con elenchi di controllo di accesso \(ACL\)  
 È possibile specificare attestazioni obbligatorie e facoltative nel codice e nei file di configurazione per i token rilasciati da [!INCLUDE[infocard](../../../../includes/infocard-md.md)].  Ciò comporta l'emissione di elementi corrispondenti nei messaggi `RequestSecurityToken` inviati al servizio token di sicurezza.  L'autore di un attacco può modificare il codice o la configurazione per rimuovere attestazioni obbligatorie o facoltative, facendo in modo che il servizio token di sicurezza rilasci un token che non consente l'accesso al servizio di destinazione.  
  
 Per prevenire il problema: richiedere l'accesso al computer per modificare il file di configurazione.  Usare elenchi di controllo di accesso \(ACL\) per proteggere i file di configurazione.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede che il codice si trovi nella directory dell'applicazione o nella Global Assembly Cache prima di consentirne il caricamento dalla configurazione.  Usare elenchi di controllo di accesso alle directory per proteggere le directory.  
  
## Raggiunto il numero massimo di sessioni protette per un servizio  
 Quando un client viene correttamente autenticato da un servizio e viene stabilita una sessione protetta con il servizio, il servizio tiene traccia della sessione fino a quando il client non la annulla o la sessione non scade.  Ogni sessione stabilita viene conteggiata a fronte del numero massimo consentito di sessioni attive simultanee con un servizio.  Quando viene raggiunto questo limite, i client che tentano di creare una nuova sessione con il servizio in questione vengono rifiutati fino a quando una o più sessioni attive non scadono o non vengono annullate da un client.  Un client può avere più sessioni con un servizio e ognuna di esse viene conteggiata per il raggiungimento del limite.  
  
> [!NOTE]
>  Se si usano sessioni con stato, non vale quanto detto nel paragrafo precedente.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle sessioni con stato, vedere [Procedura: creare un token di contesto di sicurezza per una sessione sicura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
 Per prevenire il problema, impostare il limite per il numero massimo di sessioni attive e la durata massima di una sessione impostando la proprietà <xref:System.ServiceModel.Channels.SecurityBindingElement> della classe <xref:System.ServiceModel.Channels.SecurityBindingElement>.  
  
## Vedere anche  
 [Considerazioni sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [Diffusione di informazioni](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [Elevazione dei privilegi](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [Denial of Service](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [Attacchi di tipo replay](../../../../docs/framework/wcf/feature-details/replay-attacks.md)   
 [Manomissioni](../../../../docs/framework/wcf/feature-details/tampering.md)   
 [Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)