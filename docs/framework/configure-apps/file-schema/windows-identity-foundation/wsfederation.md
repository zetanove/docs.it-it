---
title: "&lt;wsFederation&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c537f770-68bd-4f82-96ad-6424ad91369f
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;wsFederation&gt;
Fornisce la configurazione per il <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\).  
  
## Sintassi  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation authenticationType=xs:string (URI)  
        freshness=xs:decimal  
        homerealm=xs:string (URI)  
        issuer=xs:string (URI)  
        persistentCookiesOnPassiveRedirects=xs:boolean  
        passiveRedirectEnabled=xs:boolean  
        policy=xs:string (URI)  
        realm=xs:string (URI)  
        reply=xs:string (URI)  
        request=xs:string (URI)  
        requestPtr=xs:string (URI)  
        requireHttps=xs:boolean  
        resource=xs:string (URI)  
        signInQueryString=xs:string  
        signOutQueryString=xs:string  
        signOutReply=xs:string (URL)  
    </wsFederation>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|authenticationType|URI che specifica il tipo di autenticazione.  Imposta il parametro wauth di accesso richiesta WS\-Federation.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che il parametro wauth non è incluso nella richiesta.|  
|freschezza|Il desiderato validità massima delle richieste di autenticazione, in minuti.  Imposta il parametro wfresh di accesso richiesta WS\-Federation.  Parametro facoltativo.  Il valore predefinito è zero.  Parametro facoltativo. **Warning:**  Nella prossima versione di.NET Framework 4.5, il `freshness` attributo sarà di tipo `xs:string` e il valore predefinito sarà `null`.|  
|homeRealm|Area di autenticazione principale del provider di identità \(IP\) da utilizzare per l'autenticazione.  Imposta il parametro di WS\-Federation sign\-in richiesta Wh.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che il parametro Wh non è incluso nella richiesta.|  
|issuer|L'URI dell'emittente del token previsto.  Imposta le richieste di accesso URL WS\-Federation base e l'uscita richieste necessarie.|  
|persistentCookiesOnPassiveRedirects|Specifica se i cookie permanenti vengono emessi sull'autenticazione.  Parametro facoltativo.  Il valore predefinito è "false", i cookie non vengono rilasciati.|  
|passiveRedirectEnabled|Specifica se il WSFAM è abilitato per reindirizzare automaticamente le richieste non autorizzate per un servizio STS.  Parametro facoltativo.  Il valore predefinito è "true", verranno reindirizzate automaticamente le richieste non autorizzate.|  
|policy|Un URL che specifica la posizione dei criteri pertinenti per l'utilizzo di richieste di accesso.  Il valore predefinito è una stringa vuota.  Imposta il parametro di WS\-Federation sign\-in richiesta wp.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che il parametro wp non è incluso nella richiesta.|  
|realm|L'URI dell'area di autenticazione richiesta.  \(Un URI che identifica la controparte \(RP\) per il servizio token di protezione \(STS\).\) Imposta il parametro di richiesta wtrealm WS\-Federation sign\-in richiesta.  Obbligatorio.|  
|risposta|Un URL che identifica l'indirizzo in cui l'applicazione di terze parti \(RP\) componente desidera di ricevere le risposte dal servizio Token protezione \(STS\).  Imposta il parametro wreply di accesso richiesta WS\-Federation.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che il parametro wreply non è incluso nella richiesta.|  
|richiesta|La richiesta di rilascio di token.  Imposta il parametro wreq di accesso richiesta WS\-Federation.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che il parametro wreq non è incluso nella richiesta.  Escluso il wreq o il parametro wreqptr nella richiesta implica che il servizio STS sapere il tipo di token per il rilascio.|  
|requestPtr|Un URL che specifica la posizione della richiesta di rilascio di token.  Imposta il parametro wreqptr di richiesta.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che il parametro wreqptr non è incluso nella richiesta.  Escluso il wreq o il parametro wreqptr nella richiesta implica che il servizio STS sapere il tipo di token per il rilascio.|  
|requireHttps|Specifica se la comunicazione con il servizio token di protezione \(STS\) deve utilizzare il protocollo HTTPS.  Parametro facoltativo.  Il valore predefinito è "true", è necessario utilizzare HTTPS.|  
|risorsa|Un URI che identifica la risorsa a cui si accede, controparte \(RP\) ai per il servizio token di protezione \(STS\).  Parametro facoltativo.  Imposta il parametro wres di accesso richiesta WS\-Federation.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che il parametro wres non è incluso nella richiesta. **Note:**  WRES è un parametro legacy.  Specificare il `realm` attributo da utilizzare il parametro wtrealm.|  
|signInQueryString|Fornisce un punto di estendibilità per specificare i parametri di query di applicazione definito nell'URL di accesso richiesta WS\-Federation.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che senza parametri aggiuntivi da includere nella richiesta.  I parametri vengono specificati come un frammento di stringa di query mediante la seguente sintassi: `“param1=value1&param2=value2&param3=value3”` e così via. **Note:**  In un file di configurazione di "&" carattere nella stringa di query deve essere specificato utilizzando il riferimento all'entità, `&`.|  
|signOutQueryString|Fornisce un punto di estendibilità per specificare i parametri di query di applicazione definito nell'URL di accesso richiesta WS\-Federation.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che senza parametri aggiuntivi da includere nella richiesta.  I parametri vengono specificati come un frammento di stringa di query mediante la seguente sintassi: `“param1=value1&param2=value2&param3=value3”` e così via. **Note:**  In un file di configurazione di "&" carattere nella stringa di query deve essere specificato utilizzando il riferimento all'entità, `&`.|  
|signOutReply|Specifica l'URL a cui deve essere reindirizzato il client dal servizio token di protezione \(STS\) durante l'uscita attraverso il protocollo WS\-Federation passivo.  Imposta il parametro wreply su una richiesta di disconnessione di WS\-Federation.  Parametro facoltativo.  Il valore predefinito è una stringa vuota, specifica che senza parametri aggiuntivi da includere nella richiesta.|  
  
### Elementi figlio  
 Nessuno  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)|Contiene le impostazioni che configurano il <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) e il <xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\).|  
  
## Note  
 È possibile utilizzare la `<wsFederation>` elemento per configurare le impostazioni predefinite dei parametri WS\-Federation e il comportamento predefinito per il WSFAM.  Impostazioni dei parametri definite in WS\-Federation il `<wsFederation>` equivalente proprietà esposte dall'insieme di elementi di <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> classe.  Queste proprietà rimangono invariate per ogni richiesta emessa dalla WSFAM.  È possibile modificare i parametri di WS\-Federation dinamicamente durante una richiesta di elaborazione mediante l'aggiunta di gestori eventi per gli eventi esposti da WSFAM; ad esempio, il <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider> evento.  Per ulteriori informazioni, vedere la documentazione relativa alla classe <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>.  
  
 Il `<wsFederation>` elemento è rappresentato dal <xref:System.IdentityModel.Services.Configuration.WSFederationElement> classe.  L'oggetto di configurazione è rappresentato dal <xref:System.IdentityModel.Services.Configuration.WSFederationConfiguration> classe.  Un singolo <xref:System.IdentityModel.Services.Configuration.WSFederationConfiguration> istanza è impostato sui <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> oggetto a cui si accede tramite il <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName> proprietà e fornisce la configurazione per il WSFAM.  
  
## Esempio  
 Nel XML che segue un `<wsFederation>` elemento che specifica le impostazioni per il WSFAM.  
  
> [!WARNING]
>  In questo esempio, il WSFAM non è necessario utilizzare HTTPS.  Infatti, il `requireHttps` attributo sul `<wsFederation>` è impostato `false`.  Come può presentare un rischio di protezione, questa impostazione non è consigliata per la maggior parte degli ambienti di produzione.  
  
```  
<wsFederation passiveRedirectEnabled="true"   
  issuer="http://localhost:15839/wsFederationSTS/Issue"   
  realm="http://localhost:50969/"   
  reply="http://localhost:50969/"   
  requireHttps="false"   
  signOutReply="http://localhost:50969/SignedOutPage.html"   
  signOutQueryString="Param1=value2&Param2=value2"   
  persistentCookiesOnPassiveRedirects="true" />  
  
```  
  
## Vedere anche  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>   
 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>