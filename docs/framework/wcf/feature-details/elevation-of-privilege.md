---
title: "Elevazione dei privilegi | Microsoft Docs"
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
  - "Elevazione dei privilegi [WCF]"
  - "sicurezza [WCF], elevazione dei privilegi"
ms.assetid: 146e1c66-2a76-4ed3-98a5-fd77851a06d9
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Elevazione dei privilegi
L'*elevazione dei privilegi* si verifica quando all'autore di un attacco vengono concesse autorizzazioni superiori a quelle iniziali.L'autore di un attacco con, ad esempio, un set di privilegi di autorizzazioni "di sola lettura" eleva il set per includere "lettura e scrittura".  
  
## Un servizio token di sicurezza affidabile deve firmare le attestazioni del token SAML  
 Un token SAML \(Security Assertions Markup Language\) è un token XML generico che è il tipo predefinito per i token emessi.Un token SAML può essere costruito da un servizio token di sicurezza \(STS, Security Token Service\) ritenuto affidabile dal servizio Web finale in uno scambio tipico.Nelle istruzioni, i token SAML contengono attestazioni.L'autore di un attacco può copiare le attestazioni da un token valido, creare un nuovo token SAML e firmarlo con un emittente diverso.Lo scopo è quello di determinare se il server sta convalidando gli emittenti e, in caso negativo, utilizzare la debolezza per costruire token SAML che consentano privilegi oltre quelli previsti da un servizio token di sicurezza.  
  
 La classe <xref:System.IdentityModel.Tokens.SamlAssertion> verifica la firma digitale contenuta in un token SAML e l'oggetto <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> predefinito richiede che i token SAML siano firmati da un certificato X.509 che sia valido quando la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> della classe <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> è impostata sul campo <xref:System.ServiceModel.Security.X509CertificateValidationMode>.La sola modalità `ChainTrust` non è sufficiente per stabilire se l'emittente del token SAML è affidabile.I servizi che richiedono un modello di affidabilità più granulare possono utilizzare i criteri di autorizzazione e di imposizione per controllare l'emittente dei set di attestazioni prodotti dall'autenticazione del token emesso oppure utilizzare le impostazioni di convalida X.509 in <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> per limitare il set di certificati di firma consentiti.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Gestione di attestazioni e autorizzazioni con il modello di identità](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md) e [Federazione e token emessi](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).  
  
## Cambio di identità senza un contesto di sicurezza  
 Quando segue si applica solo a [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)].  
  
 Quando viene stabilita una connessione tra un client e un server, l'identità del client non cambia, tranne che in una situazione: dopo l'apertura del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], se si verificano tutte le condizioni seguenti:  
  
-   Le procedure per stabilire un contesto di sicurezza \(utilizzando una sessione di sicurezza del trasporto o una sessione di sicurezza del messaggio\) sono disattivate. La proprietà <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> è impostata su `false` nel caso della protezione del messaggio oppure, nel caso della protezione del trasporto, è utilizzato un trasporto che non è in grado di stabilire sessioni di sicurezza.HTTPS è un esempio di questo tipo di trasporto.  
  
-   Viene utilizzata l'autenticazione di Windows.  
  
-   La credenziale non è impostata in modo esplicito.  
  
-   Il servizio viene chiamato nel contesto di sicurezza rappresentato.  
  
 In presenza di queste condizioni, l'identità utilizzata per autenticare il client nei confronti del servizio potrebbe cambiare \(potrebbe non essere l'identità rappresentata ma l'identità del processo\) dopo l'apertura del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Ciò accade perché la credenziale di Windows utilizzata per autenticare il client al servizio viene trasmessa con ogni messaggio e la credenziale utilizzata per l'autenticazione viene ottenuta dall'identità di Windows del thread corrente.Se l'identità di Windows del thread corrente cambia \(ad esempio, rappresentando un chiamante diverso\), potrebbe cambiare anche la credenziale allegata al messaggio e utilizzata per autenticare il client al servizio.  
  
 Se si desidera ottenere un comportamento deterministico quando si utilizza l'autenticazione di Windows assieme alla rappresentazione, è necessario impostare in modo esplicito la credenziale di Windows oppure stabilire un contesto di sicurezza con il servizio.A tale scopo, utilizzare una sessione di sicurezza del messaggio o una sessione di sicurezza del trasporto.Il trasporto net.tcp, ad esempio, può fornire una sessione di sicurezza del trasporto.Quando si chiama il servizio , è inoltre necessario utilizzare solo una versione sincrona delle operazioni client.Se si stabilisce un contesto di sicurezza del messaggio, non mantenere aperta la connessione al servizio oltre il periodo di rinnovo della sessione configurato, perché l'identità può cambiare anche durante il processo di rinnovo della sessione.  
  
### Acquisizione delle credenziali  
 Quanto segue si applica a [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] e versioni successive.  
  
 Le credenziali utilizzate dal client o dal servizio sono basate sul thread del contesto corrente.Le credenziali vengono ottenute quando si chiama il metodo `Open` \(o `BeginOpen`, per le chiamate asincrone\) del client o del servizio.Per entrambe le classi <xref:System.ServiceModel.ServiceHost> e <xref:System.ServiceModel.ClientBase%601>, i metodi `Open` e `BeginOpen` ereditano dai metodi <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> e <xref:System.ServiceModel.Channels.CommunicationObject.BeginOpen%2A> della classe <xref:System.ServiceModel.Channels.CommunicationObject>.  
  
> [!NOTE]
>  Quando si utilizza il metodo `BeginOpen`, non è possibile garantire che le credenziali acquisite siano quelle del processo che chiama il metodo.  
  
## I token memorizzati nella cache consentono la riproduzione utilizzando dati obsoleti  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza la funzione `LogonUser` dell'autorità di sicurezza locale \(LSA, Local Security Authority\) per autenticare gli utenti tramite nome utente e password.Dato che la funzione di accesso è un'operazione che consuma molte risorse, per aumentare le prestazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di memorizzare nella cache i token che rappresentano gli utenti autenticati.Il meccanismo di memorizzazione nella cache salva i risultati ottenuti da `LogonUser` per utilizzi successivi.Per impostazione predefinita, questo meccanismo è disattivato. Per attivarlo, impostare la proprietà <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CacheLogonTokens%2A> su `true` o utilizzare l'attributo `cacheLogonTokens` di [\<autenticazioneNomeUtente\>](../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md).  
  
 È possibile impostare la durata \(TTL\) per i token memorizzati nella cache, impostando la proprietà <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.CachedLogonTokenLifetime%2A> su un <xref:System.TimeSpan>, oppure utilizzare l'attributo `cachedLogonTokenLifetime` dell'elemento `userNameAuthentication`. L'impostazione predefinita è 15 minuti.Si noti che quando un token è memorizzato nella cache, può essere utilizzato da qualsiasi client che presenti lo stesso nome utente e la stessa password, anche se l'account utente viene eliminato da Windows o se la sua password è stata modificata.Fino alla scadenza del TTL e finché il token non viene rimosso dalla cache, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente all'utente \(forse malintenzionato\) di autenticarsi.  
  
 Per limitare questo problema, ridurre il tempo a disposizione dell'attacco impostando il valore `cachedLogonTokenLifetime` sull'intervallo di tempo più breve necessario per gli utenti.  
  
## Autorizzazione del token emesso: scadenza reimpostata su un valore grande  
 In certe condizioni, la proprietà <xref:System.IdentityModel.Policy.AuthorizationContext.ExpirationTime%2A> di <xref:System.IdentityModel.Policy.AuthorizationContext> può essere impostata su un valore inaspettatamente superiore \(il valore del campo <xref:System.DateTime.MaxValue> meno un giorno, o 20 dicembre 9999\).  
  
 Ciò si verifica quando si utilizza <xref:System.ServiceModel.WSFederationHttpBinding> e una qualsiasi delle associazioni fornite dal sistema che ha un token emesso come tipo di credenziale client.  
  
 Lo stesso accade anche quando si creano associazioni personalizzate utilizzando uno dei metodi seguenti:  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenBindingElement%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenForSslBindingElement%2A>  
  
-   <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateIssuedTokenOverTransportBindingElement%2A>  
  
 Per limitare questo problema, il criterio di autorizzazione deve controllare l'azione e la data di scadenza di ogni criterio di autorizzazione.  
  
## Il servizio utilizza un certificato diverso da quello previsto dal client  
 In certe condizioni, un client può firmare digitalmente un messaggio con un certificato X.509 e far sì che il servizio recuperi un certificato diverso da quello previsto.  
  
 Ciò può verificarsi nelle circostanze seguenti:  
  
-   Il client firma digitalmente un messaggio utilizzando un certificato X.509 e non allega il certificato X.509 al messaggio, ma fa semplicemente riferimento al certificato utilizzando il suo identificatore chiave del soggetto.  
  
-   Il computer del servizio contiene due o più certificati con la stessa chiave pubblica, ma tali certificati contengono informazioni diverse.  
  
-   Il servizio recupera un certificato che corrisponde all'identificatore chiave del soggetto, ma non è quello che il client doveva utilizzare.Quando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] riceve il messaggio e verifica la firma, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] esegue il mapping delle informazioni nel certificato X.509 non previsto a un set di attestazioni che sono diverse e potenzialmente con privilegi più elevi rispetto a quelli previsti dal client.  
  
 Per limitare questo problema, fare riferimento al certificato X.509 in un altro modo, ad esempio utilizzando <xref:System.ServiceModel.Security.Tokens.X509KeyIdentifierClauseType>.  
  
## Vedere anche  
 [Considerazioni sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [Diffusione di informazioni](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [Denial of Service \(Negazione del servizio\)](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [Attacchi di tipo replay](../../../../docs/framework/wcf/feature-details/replay-attacks.md)   
 [Manomissioni](../../../../docs/framework/wcf/feature-details/tampering.md)   
 [Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)