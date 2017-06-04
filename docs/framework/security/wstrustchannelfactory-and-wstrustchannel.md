---
title: "WSTrustChannelFactory e WSTrustChannel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96cec467-e963-4132-b18b-7d0b3a2e979f
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# WSTrustChannelFactory e WSTrustChannel
Se si conosce già con Windows Communication Foundation \(WCF\), sapere che un client WCF è già federazione ricezione.  Configurando un client WCF con <xref:System.ServiceModel.WSFederationHttpBinding> o simile associazione personalizzata, è possibile abilitare l'autenticazione organizzata in modo federativo un servizio.  
  
 Il WCF ottiene il token che viene generato dal servizio token di sicurezza \(STS\) in background e utilizza questo token per autenticare il servizio.  La limitazione principale di questo approccio è che non esiste visibilità nelle comunicazioni client al server.  Il WCF genera automaticamente il token di sicurezza \(RST\) di richiesta al servizio token di sicurezza in base ai parametri simbolici pubblicati nell'associazione.  Ciò significa che il client non può variare i parametri di RST di richiesta, controllare la risposta \(RSTR\) del token di sicurezza di richiesta per ottenere informazioni quali richieste di visualizzazione, oppure memorizzare il token per un utilizzo futuro.  
  
 Attualmente, il client WCF è adatto a scenari di base di federazione.  Tuttavia, uno degli scenari principali che costituiscono la base \(WIF\)identità Windows supporta richiede il RST a un livello che il WCF facilmente non consente.  Di conseguenza, WIF aggiunge funzionalità che consentono un controllo sulla comunicazione con il servizio token di sicurezza.  
  
 WIF supporta i seguenti scenari di federazione:  
  
-   Utilizzando un client WCF senza dipendenze di WIF da autenticare a un servizio organizzato in modo federativo  
  
-   Abilitare WIF su un client WCF per inserire un elemento di OnBehalfOf o di ActAs in RST al servizio token di sicurezza  
  
-   Utilizzando WIF da solo per ottenere un token dal servizio token di sicurezza per poi consentire a un client WCF per eseguire l'autenticazione con questo token.  Per [ClaimsAwareWebService](http://go.microsoft.com/fwlink/?LinkID=248406) ulteriori informazioni, vedere l'esempio.  
  
 Il primo scenario è evidente: I client WCF esistenti continueranno a funzionare con componenti di WIF e il servizio token di sicurezza.  In questo argomento vengono illustrati i due scenari rimanenti.  
  
## Aggiornamento di un client WCF esistente con ActAs\/OnBehalfOf  
 In uno scenario tipico di delega di identità, un client chiama un servizio di livello intermedio, quindi chiama un servizio back\-end.  Il servizio di livello intermedio funge da, o opera per conto di, il client.  
  
> [!TIP]
>  Qual è la differenza tra ActAs e OnBehalfOf?  
>   
>  Dal punto di vista di procotol di WS\- attendibilità:  
>   
>  1.  Un elemento di ActAs RST indica che il richiedente desidera un token che contiene le richieste su due entità distinte: il richiedente e un'entità esterna rappresentata dal token dell'elemento di ActAs.  
> 2.  Un elemento di OnBehalfOf RST indica che il richiedente desidera un token che contiene le richieste solo su un'entità: l'entità esterna rappresentata dal token dell'elemento di OnBehalfOf.  
>   
>  La funzionalità di ActAs in genere utilizzata negli scenari che richiedono la delega composta, in cui il destinatario finale del token generato può controllare l'intera catena di delega e visualizzare appena il client, ma qualsiasi intermediari.  In questo modo la possibile eseguire il controllo di accesso, il controllo e altre attività correlate in base all'intera catena di delega di identità.  La funzionalità di ActAs viene utilizzata in sistemi a più livelli l'autenticazione e comunicare le informazioni sulle identità tra livelli senza dover comunicare le informazioni all'applicazione\/livello di logica di business.  
>   
>  La funzionalità di OnBehalfOf viene utilizzata negli scenari in cui solo all'identità del client originale è importante e viene efficacemente la stessa funzionalità di rappresentazione di identità disponibile in Windows.  Quando OnBehalfOf viene utilizzato, il destinatario finale del token generato può visualizzare solo le richieste sul client originale e informazioni sugli intermediari non vengono mantenute.  Un modello comune in cui la funzionalità di OnBehalfOf viene utilizzata è il modello di dominio in cui il client non può accedere al servizio token di sicurezza direttamente bensì comunica tramite un protocollo del proxy.  Il gateway del proxy autentica il chiamante e inserisce le informazioni sul chiamante nell'elemento di OnBehalfOf del messaggio di RST che invia al servizio token di sicurezza reale per l'elaborazione.  Il token risultante contiene solo le richieste relative al client del proxy, cedendo il proxy completamente trasparente al ricevitore del token pubblicato. Si noti che WIF non supporta \<wsse:SecurityTokenReference\> o \<wsa:EndpointReferences\> come figlio \<wst:OnBehalfOf\>.  La specifica di WS\- attendibilità consente l'invio di tre modi per identificare il richiedente originale \(per conto del proxy viene utilizzato\).  Tali valori sono:  
>   
>  -   Riferimento del token di sicurezza.  Un riferimento a un token, nel messaggio, o eventualmente recuperato dalla banda\).  
> -   Riferimento dell'endpoint.  Utilizzato come chiave per cercare dati, nuovamente la banda.  
> -   Token di sicurezza.  Identifica direttamente il richiedente originale.  
>   
>  WIF supporta solo i token di sicurezza, crittografati o non crittografati, come elemento figlio diretto \<wst:OnBehalfOf\>.  
  
 Queste informazioni vengono trasferite a un autorità di WS\- attendibilità utilizzando gli elementi di OnBehalfOf simbolici e di ActAs in RST.  
  
 Il WCF espone un punto di estensibilità sull'associazione che consente agli elementi XML arbitrari da aggiungere al RST.  Tuttavia, poiché il punto di estensibilità è associato all'associazione, gli scenari che richiedono il RST soddisfa per variare di chiamata è necessario ricreare il client per ogni chiamata, che riduce le prestazioni.  WIF utilizza i metodi di estensione nella classe `ChannelFactory` per consentire agli sviluppatori possa connettersi qualsiasi token che si ottiene dalla banda al RST.  Nell'esempio di codice seguente viene illustrato come creare un token che rappresenta il client \(ad esempio uno X.509, un nome utente, o un token di \(SAML\) di linguaggio markup delle asserzioni di sicurezza\) e lo associa al RST inviata all'autorità.  
  
```  
IHelloService serviceChannel = channelFactory.CreateChannelActingAs<IHelloService>( clientSamlToken );  
serviceChannel.Hello(“Hi!”);  
```  
  
 WIF offre i vantaggi seguenti:  
  
-   Il RST può essere modificato per canale; pertanto, i servizi di livello intermedio non è necessario ricreare il channel factory per ciascun client, che consente di migliorare le prestazioni.  
  
-   Questo funziona con i client esistenti WCF, che consente un percorso di aggiornamento semplice per i servizi di livello intermedio esistenti WCF che desiderano abilitare la semantica di delega di identità.  
  
 Tuttavia, non è ancora visibilità nella comunicazione del client al servizio token di sicurezza.  La trattazione nel terzo scenario.  
  
## Comunicare direttamente con un autorità e utilizzando il token generato per autenticare  
 Per alcuni scenari avanzati, aggiornare un client WCF non è sufficiente.  Sviluppatori che utilizzano solo il messaggio di utilizzare WCF in genere in\/contratti del messaggio estrazione e gestiscono l'analisi lato client di risposta dell'autorità manualmente.  
  
 WIF vengono introdotte le classi <xref:System.ServiceModel.Security.WSTrustChannel> e <xref:System.ServiceModel.Security.WSTrustChannelFactory> per consentire il client comunicare direttamente con un autorità di WS\- attendibilità.  Le classi <xref:System.ServiceModel.Security.WSTrustChannel> e <xref:System.ServiceModel.Security.WSTrustChannelFactory> consentono agli oggetti fortemente tipizzati di RSTR e di RST al flusso tra il client e autorità emittente, come illustrato nell'esempio di codice.  
  
```  
WSTrustChannelFactory trustChannelFactory = new WSTrustChannelFactory( stsBinding, stsAddress );  
WSTrustChannel channel = (WSTrustChannel) trustChannelFactory.CreateChannel();  
RequestSecurityToken rst = new RequestSecurityToken(RequestTypes.Issue);  
rst.AppliesTo = new EndpointAddress(serviceAddress);  
RequestSecurityTokenResponse rstr = null;  
SecurityToken token = channel.Issue(rst, out rstr);  
```  
  
 Si noti che il parametro `out` nel metodo <xref:System.ServiceModel.Security.WSTrustChannel.Issue%2A> consente l'accesso a RSTR per l'ispezione lato client.  
  
 Finora, illustrato in precedenza solo come ottenere un token.  Il token restituito dall'oggetto <xref:System.ServiceModel.Security.WSTrustChannel> è `GenericXmlSecurityToken` che contiene tutte le informazioni necessarie per l'autenticazione a un componente.  Nell'esempio di codice seguente viene illustrato come utilizzare il token.  
  
```  
IHelloService serviceChannel = channelFactory.CreateChannelWithIssuedToken<IHelloService>( token ); serviceChannel.Hello(“Hi!”);  
```  
  
 Il metodo di estensione <xref:System.ServiceModel.ChannelFactory%601.CreateChannelWithIssuedToken%2A> sull'oggetto `ChannelFactory` indica a WIF ottenuto un token dalla banda che deve interrompere la chiamata normale WCF all'autorità e utilizzare il token che si è verificato per autenticare al componente.  Ciò comporta i vantaggi seguenti:  
  
-   Fornisce controllo completo sul processo token di emissione.  
  
-   Supporta scenari OnBehalfOf\/ActAs direttamente l'impostazione di queste proprietà su RST in uscita.  
  
-   Attiva le decisioni sul lato client dinamiche di essere eseguito in base al contenuto del RSTR.  
  
-   Consente di memorizzare nella cache e riutilizzare il token restituito dal metodo <xref:System.ServiceModel.Security.WSTrustChannel.Issue%2A>.  
  
-   <xref:System.ServiceModel.Security.WSTrustChannelFactory> e <xref:System.ServiceModel.Security.WSTrustChannel> consentono un controllo della memorizzazione nella cache del canale, errore e la semantica di recupero in base alle procedure consigliate WCF.  
  
## Vedere anche  
 [Funzionalità di WIF](../../../docs/framework/security/wif-features.md)