---
title: "Scenari non supportati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 72027d0f-146d-40c5-9d72-e94392c8bb40
caps.latest.revision: 43
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 39
---
# Scenari non supportati
Per varie ragioni, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] non supporta alcuni scenari di sicurezza specifici. Ad esempio, i protocolli di autenticazione SSPI e Kerberos non sono implementati in [!INCLUDE[wxp](../../../../includes/wxp-md.md)] Home Edition. Pertanto, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] l'esecuzione dei servizi che utilizzano l'autenticazione di Windows su questa piattaforma non è supportata. Altri meccanismi di autenticazione, ad esempio l'autenticazione integrata basata su nome utente\/password e HTTP\/HTTPS, sono supportati se [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene eseguito in Windows XP Home Edition.  
  
## Scenari di rappresentazione  
  
### L'identità rappresentata potrebbe non fluire quando i client effettuano chiamate asincrone  
 Quando un client WCF effettua chiamate asincrone a un servizio WCF utilizzando l'autenticazione di Windows sotto rappresentazione, potrebbe verificarsi l'autenticazione con l'identità del processo client anziché con l'identità rappresentata.  
  
### Windows XP con cookie di token del contesto di sicurezza attivo  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non è supportata la rappresentazione e quando sussistono le condizioni elencate di seguito viene generata un'eccezione <xref:System.InvalidOperationException>:  
  
-   Il sistema operativo è [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  
  
-   La modalità di autenticazione genera un'identità Windows.  
  
-   La proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> di <xref:System.ServiceModel.OperationBehaviorAttribute> è impostata su <xref:System.ServiceModel.ImpersonationOption>.  
  
-   Viene creato un token del contesto di sicurezza SCT \(Security Context Token\) basato sullo stato. Per impostazione predefinita, la creazione è disattivata.  
  
 Il token SCT basato sullo stato può essere creato solo tramite un'associazione personalizzata.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Procedura: creare un token di contesto di sicurezza per una sessione sicura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md). In codice, per attivare il token occorre creare un elemento di associazione di sicurezza \(<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> o <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>\) utilizzando il metodo <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement%28System.Boolean%29?displayProperty=fullName> o il metodo <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%28System.ServiceModel.Channels.SecurityBindingElement%2CSystem.Boolean%29?displayProperty=fullName> e impostando il parametro `requireCancellation` su `false`. Il parametro fa riferimento alla memorizzazione nella cache del token SCT. L'impostazione del valore su `false` comporta l'attivazione della funzionalità del token SCT basato sullo stato.  
  
 In alternativa, per abilitare il token nella configurazione, è necessario creare un'associazione \<`customBinding`\>, quindi aggiungere un elemento \<`security`\> e infine impostare l'attributo `authenticationMode` su SecureConversation e l'attributo `requireSecurityContextCancellation` su `true`.  
  
> [!NOTE]
>  I requisiti precedenti sono specifici. Ad esempio, il metodo <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> crea un elemento di associazione che genera un'identità Windows senza tuttavia creare un token SCT. È pertanto possibile utilizzare questa identità con l'opzione `Required` di [!INCLUDE[wxp](../../../../includes/wxp-md.md)].  
  
### Possibile conflitto con ASP.NET  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] possono entrambi attivare o disattivare la rappresentazione. Quando [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] ospita un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è possibile che si verifichi un conflitto tra le impostazioni di configurazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]. In caso di conflitto, l'impostazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ha la precedenza, a meno che la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> sia impostata su <xref:System.ServiceModel.ImpersonationOption>. In questo caso, l'impostazione della rappresentazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] ha la precedenza.  
  
### Possibilità di esito negativo dei caricamenti dell'assembly in caso di utilizzo della rappresentazione  
 Se il contesto rappresentato non dispone delle autorizzazioni di accesso per caricare un assembly e se è la prima volta che il Common Language Runtime \(CLR\) tenta di caricare l'assembly per tale dominio applicazione, il dominio <xref:System.AppDomain> memorizza l'errore nella cache. I tentativi successivi di caricamento dell'assembly \(o degli assembly\) hanno esito negativo, anche dopo aver ripristinato la rappresentazione e anche se il contesto ripristinato dispone delle autorizzazioni di accesso per caricare l'assembly. Ciò è dovuto al fatto che CLR non esegue nuovi tentativi di caricamento dopo che il contesto utente è cambiato. Per risolvere il problema è necessario riavviare il dominio applicazione.  
  
> [!NOTE]
>  Il valore predefinito della proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> della classe <xref:System.ServiceModel.Security.WindowsClientCredential> è <xref:System.Security.Principal.TokenImpersonationLevel>. Nella maggior parte dei casi, un contesto di rappresentazione a livello di identificazione non dispone di alcun diritto che consenta il caricamento di assembly aggiuntivi. Poiché si tratta di un valore predefinito, questo caso risulta essere molto comune e merita particolare attenzione. La rappresentazione a livello di identificazione si verifica anche quando il processo di rappresentazione non dispone del privilegio `SeImpersonate`.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Delega e rappresentazione](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
### Requisito di negoziazione della credenziale in caso di delega  
 Per poter essere utilizzato con la funzionalità di delega, il protocollo di autenticazione Kerberos deve essere implementato con la negoziazione delle credenziali. Questa versione di Kerberos è talvolta nota come Kerberos multifase. Se si implementa l'autenticazione Kerberos senza negoziazione delle credenziali \(ovvero una versione di Kerberos anche nota come monofase o monopassaggio\), verrà generata un'eccezione.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] come implementare la negoziazione delle credenziali, vedere [Debug degli errori di autenticazione di Windows](../../../../docs/framework/wcf/feature-details/debugging-windows-authentication-errors.md).  
  
## Crittografia  
  
### Supporto di SHA\-256 solo in caso di utilizzo di chiavi simmetriche  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta diversi algoritmi di crittografia e di creazione di digest di firme che è possibile specificare utilizzando la suite di algoritmi disponibile nelle associazioni fornite dal sistema. Per implementare un meccanismo di sicurezza avanzata, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta gli algoritmi Secure Hash Algorithm \(SHA\) 2, in particolare l'algoritmo SHA\-256, per creare hash digest di firme. Questa versione supporta l'algoritmo SHA\-256 solo nei casi in cui si utilizzano chiavi simmetriche, ad esempio le chiavi Kerberos, e nei casi in cui i messaggi non vengono firmati tramite un certificato X.509.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta le firme RSA \(utilizzate nei certificati X.509\) con l'hash SHA\-256 in quanto al momento [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] non supporta l'algoritmo RSA\-SHA256.  
  
### Mancanza del supporto per gli hash SHA\-256 conformi agli standard FIPS  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta gli hash SHA\-256 conformi agli standard FIPS. Pertanto, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta le suite di algoritmi basate su SHA\-256 nei sistemi che richiedono l'utilizzo di algoritmi conformi agli standard FIPS.  
  
### Possibilità di esito negativo degli algoritmi conformi agli standard FIPS in caso di modifica del Registro di sistema  
 Lo snap\-in Impostazioni protezione locale di Microsoft Management Console \(MMC\) consente di attivare e disattivare gli algoritmi conformi agli standard FIPS. Questa impostazione può inoltre essere eseguita nel Registro di sistema. Si noti tuttavia che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta l'utilizzo del Registro di sistema per reimpostare l'impostazione. Se si esegue questa impostazione utilizzando un valore diverso da 1 oppure 0 è possibile che si verifichino risultati incoerenti tra il runtime CLR e il sistema operativo.  
  
### Restrizione sulla crittografia AES conforme agli standard FIPS  
 La crittografia AES conforme agli standard FIPS non funziona nei callback duplex nel contesto di una rappresentazione di livello di identificazione.  
  
### Certificati CNG\/KSP in Windows Server 2008  
 *Cryptography API: Next Generation \(CNG\)* è la sostituzione a lungo termine di CryptoAPI. Questa API è disponibile nel codice non gestito in [!INCLUDE[wv](../../../../includes/wv-md.md)] e [!INCLUDE[lserver](../../../../includes/lserver-md.md)].  
  
 Su piattaforme legacy \([!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] e [!INCLUDE[wxp](../../../../includes/wxp-md.md)]\) .NET Framework 2.0 non riconosce questo protocollo e utilizza il protocollo *CryptoAPI* preesistente per gestire i certificati CNG\/KSP. In [!INCLUDE[lserver](../../../../includes/lserver-md.md)] e [!INCLUDE[wv](../../../../includes/wv-md.md)] .NET Framework 3.5 non supporta questi certificati: il loro utilizzo genera un'eccezione.  
  
 Esistono due modi possibili per stabilire se un certificato utilizza KSP:  
  
-   Eseguire `p/invoke` di `CertGetCertificateContextProperty` e controllare `dwProvType` sulla proprietà `CertGetCertificateContextProperty` restituita.  
  
-   Usare il comando `certutil` dalla riga di comando per eseguire query sui certificati.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Attività di Certutil per la risoluzione dei problemi relativi ai certificati](http://go.microsoft.com/fwlink/?LinkId=120056).  
  
## Errore di sicurezza a livello di messaggio quando si utilizza la rappresentazione ASP.NET e la compatibilità con ASP.NET è obbligatoria  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta la combinazione seguente di condizioni, in quanto può impedire lo svolgimento dell'autenticazione client:  
  
-   È stata attivata la rappresentazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]. A questo scopo, nel file Web.config impostare l'attributo `impersonate` dell'elemento \<`identity`\> su `true`.  
  
-   Per abilitare la modalità di compatibilità con [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], impostare l'attributo `aspNetCompatibilityEnabled` di [\<serviceHostingEnvironment\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) su `true`.  
  
-   Viene utilizzata la protezione a livello di messaggio.  
  
 Per risolvere questo problema è sufficiente disattivare la modalità di compatibilità con [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]. In alternativa, se la modalità di compatibilità con [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] è obbligatoria, è possibile disattivare la funzionalità di rappresentazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e utilizzare invece la rappresentazione fornita in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Delega e rappresentazione](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
## Errore di indirizzo letterale IPv6  
 Le richieste di sicurezza hanno esito negativo quando il client e il servizio si trovano nello stesso computer e gli indirizzi letterali Ipv6 vengono utilizzati per il servizio.  
  
 Gli indirizzi di questo tipo funzionano se il servizio e il client sono sui computer diversi.  
  
## Errori di recupero di WSDL con trust federati  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede esattamente un documento WSDL per ogni nodo nella catena di trust federati. È opportuno prestare attenzione a non impostare un ciclo quando si specificano gli endpoint. È possibile che si verifichi un ciclo quando si utilizza un download WSDL di catene di trust federati con due o più collegamenti nello stesso documento WSDL. Uno scenario comune in cui può verificarsi questo problema consiste in un servizio federato in cui il server di token di sicurezza e il servizio sono contenuti nello stesso ServiceHost.  
  
 Un esempio di questa situazione è dato da un servizio con i tre indirizzi endpoint seguenti:  
  
-   http:\/\/localhost\/CalculatorService\/service \(il servizio\)  
  
-   http:\/\/localhost\/CalculatorService\/issue\_ticket \(STS\)  
  
-   http:\/\/localhost\/CalculatorService\/mex \(l'endpoint dei metadati\)  
  
 Viene generata un'eccezione.  
  
 È possibile risolvere questo scenario collocando l'endpoint `issue_ticket` in un'altra posizione.  
  
## Gli attributi di importazione di WSDL possono andare persi  
 WCF perde traccia degli attributi in un elemento `<wst:Claims>` in un modello `RST` quando viene eseguita un'importazione WSDL. Questa situazione avviene durante un'importazione WSDL se si specifica `<Claims>` direttamente in `WSFederationHttpBinding.Security.Message.TokenRequestParameters` o `IssuedSecurityTokenRequestParameters.AdditionalRequestParameters` anziché usare direttamente le raccolte dei tipi di attestazione.  Poiché l'importazione perde gli attributi, l'associazione non esegue correttamente una sequenza di andata e ritorno attraverso WSDL e quindi risulta errata sul lato client.  
  
 Per risolvere il problema è necessario modificare l'associazione direttamente nel client dopo aver eseguito l'importazione.  
  
## Vedere anche  
 [Considerazioni sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [Diffusione di informazioni](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [Elevazione dei privilegi](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [Denial of Service \(Negazione del servizio\)](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [Manomissioni](../../../../docs/framework/wcf/feature-details/tampering.md)   
 [Attacchi di tipo replay](../../../../docs/framework/wcf/feature-details/replay-attacks.md)