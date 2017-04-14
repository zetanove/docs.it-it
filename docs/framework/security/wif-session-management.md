---
title: "Gestione delle sessioni WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 98bce126-18a9-401b-b20d-67ee462a5f8a
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# Gestione delle sessioni WIF
Quando un client prima tenta di accedere a una risorsa protetta ospitata da un componente, il client deve innanzitutto autenticarsi a un servizio token di sicurezza \(STS\) considerato attendibile dal componente.  Il servizio token di sicurezza quindi pubblica un token di sicurezza sul client.  Il client richiede questo token al componente, che quindi concedere l'accesso client alla risorsa protetta.  Tuttavia, non si desidera che il client per essere nuovamente l'autenticazione al servizio token di sicurezza per ogni richiesta, soprattutto perché potrebbe non essere lo stesso computer o nello stesso dominio del componente.  Invece, communications foundation \(WIF\) l'identità di Windows al client e stabilire al componente una sessione in cui il client viene utilizzato un token di sicurezza della sessione per autenticarsi al componente per tutte le richieste dopo la prima richiesta.  Il componente può utilizzare questo token di sicurezza della sessione, che viene archiviato in un cookie, per ricostruire <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>client.  
  
 Il servizio token di sicurezza che definisce autenticazione del client deve fornire.  Tuttavia, il client potrebbe disporre di credenziali con cui può autenticarsi al servizio token di sicurezza.  Ad esempio, potrebbe avere un token da Windows attivo, un nome utente e una password, un certificato e uno smartkey.  In tal caso, il servizio token di sicurezza consente al client diverse identità, con ogni identità che corrisponde a una delle credenziali che il client richiede.  Il componente può utilizzare uno o più di queste identità per stabilire quale livello di accesso per concedere il client.  
  
 <xref:System.IdentityModel.Tokens.SessionSecurityToken?displayProperty=fullName> viene utilizzato per ricostruire <xref:System.Security.Claims.ClaimsPrincipal?displayProperty=fullName>client, contenente le identità del client in <xref:System.Security.Claims.ClaimsPrincipal.Identities%2A>.  Ogni <xref:System.Security.Claims.ClaimsIdentity?displayProperty=fullName> nella raccolta contiene i token del caricatore bootstrap associati a tale identità.  
  
 Se un token della sessione viene generato con ID sessione del token della sessione, <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler?displayProperty=fullName> non aggiorna il token della sessione nella cache dei token.  È necessario creare un'istanza sempre un token della sessione con un ID univoco della sessione  
  
> [!NOTE]
>  Session.SecurityTokenHandler.ReadToken genera un'eccezione <xref:System.Xml.XmlException> se riceve l'input non valido; ad esempio, se il cookie contenenti il token di sessione sono danneggiate.  È consigliabile intercettare questa eccezione e fornire il comportamento specifico dell'applicazione.  
  
 Se una pagina Web protetta contiene molte delle risorse \(come piccoli elementi grafici\) che sono anche nel dominio protetto, il client necessario sottoporre autenticarsi al componente per scaricare ognuna delle risorse.  L'utilizzo di un token di autenticazione della sessione non sia necessario autenticare al servizio token di sicurezza per ogni richiesta, pur significa che molti cookie vengono inviati più.  È possibile configurare la pagina Web in modo che i dati e risorse importanti nel dominio protetto mentre i materiali minuti vengono archiviati in un dominio non protetto e collegati dalla pagina Web principale.  Inoltre, impostare il percorso del cookie per fare riferimento solo il dominio protetto.  
  
 Per l'esecuzione in modalità di riferimento, Si consiglia di fornire un gestore per l'evento <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.SessionSecurityTokenCreated> nel file **global.asax.cs** e impostare la proprietà **IsReferenceMode** il token passato nella proprietà <xref:System.IdentityModel.Services.SessionSecurityTokenCreatedEventArgs.SessionToken%2A>.  Questi aggiornamenti garantirà che il token della sessione esecuzione in modalità di riferimento per ogni richiesta e sia selezionato su solo impostare la proprietà <xref:System.IdentityModel.Services.SessionAuthenticationModule.IsReferenceMode%2A> nel modulo di autenticazione della sessione.  
  
## Estensibilità  
 È possibile estendere il meccanismo di gestione della sessione.  Un motivo per questa sequenza di migliorare le prestazioni.  Ad esempio, è possibile creare un gestore personalizzato di un cookie che trasforma o ottimizza il token di sicurezza della sessione tra il relativo stato in memoria e cosa rientra in un cookie.  A tale scopo, è possibile configurare la proprietà <xref:System.IdentityModel.Services.SessionAuthenticationModule.CookieHandler%2A?displayProperty=fullName><xref:System.IdentityModel.Services.SessionAuthenticationModule?displayProperty=fullName> per utilizzare un gestore personalizzato di un cookie che deriva da <xref:System.IdentityModel.Services.CookieHandler?displayProperty=fullName>.  <xref:System.IdentityModel.Services.ChunkedCookieHandler?displayProperty=fullName> è il gestore predefinito del cookie poiché il cookie supera la dimensione valida per il protocollo HTTP \(HTTP\); se si utilizza un gestore personalizzato dei cookie invece, è necessario implementare bloccare.  
  
 Per ulteriori informazioni, vedere [ClaimsAwareWebFarm](http://go.microsoft.com/fwlink/?LinkID=248408) \(' http:\/\/go.microsoft.com\/fwlink\/?LinkID\=248408\).  In questo esempio seguente viene mostrato un farm la cache pronto della sessione \(rispetto a un tokenreplycache\) in modo da poter utilizzare le sessioni per riferimento anziché scambiare cookie grandi; in questo esempio viene illustrato un modo più semplice di proteggere i cookie in una farm.  La cache della sessione è basato su WCF.  Rispetto alla sessione che si protegge, nell'esempio viene illustrata una nuova funzionalità in WIF 4,5 di una trasformazione dei cookie basata su machinekeys, che può essere attivato semplicemente incollando il frammento appropriato nel file web.config.  L'esempio stesso "non è coltivato", ma viene illustrato necessari per rendere l'applicazione farm\- pronta.