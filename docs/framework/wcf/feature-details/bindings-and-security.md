---
title: "Associazioni e protezione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "associazione [WCF]"
  - "associazione [WCF], protezione"
  - "Sicurezza WCF"
  - "Windows Communication Foundation, protezione"
ms.assetid: 4de03dd3-968a-4e65-af43-516e903d7f95
caps.latest.revision: 42
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 42
---
# Associazioni e protezione
Le associazioni fornite dal sistema incluse in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] offrono un modo rapido per programmare applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Tutte le associazioni, tranne una, dispongono di uno schema di sicurezza predefinito attivo.In questo argomento viene illustrato come selezionare l'associazione corretta per la sicurezza desiderata.  
  
 Per una panoramica della sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] programmazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tramite associazioni, vedere [Programmazione delle funzionalità di sicurezza di WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md).  
  
 Se è già stata selezionata un'associazione, è possibile trovare ulteriori informazioni sui comportamenti in fase di esecuzione associati alla sicurezza in [Comportamenti di sicurezza](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md).  
  
 Alcune funzionalità di sicurezza non sono programmabili tramite le associazioni fornite dal sistema.Per un maggiore controllo sull'utilizzo di un'associazione personalizzata, vedere [Funzionalità di sicurezza con associazioni personalizzate](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md).  
  
## Funzionalità di sicurezza delle associazioni  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] include numerose associazioni fornite dal sistema che soddisfano la maggior parte delle necessità.È inoltre possibile creare un'associazione personalizzata se una determinata associazione non è sufficiente.Per un elenco delle associazioni fornite dal sistema, vedere [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] associazioni personalizzate, vedere [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
 Ogni associazione in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si presenta in due forme: come API e come elemento XML utilizzato in un file di configurazione.`WSHttpBinding` \(API\), ad esempio, ha un equivalente in [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  
  
 Nella sezione seguente vengono elencate entrambe le forme per ogni associazione e vengono riepilogate le funzionalità di sicurezza.  
  
### BasicHttp  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.BasicHttpBinding>. Nella configurazione, utilizzare [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md).  
  
 Questa associazione è progettata per l'utilizzo con una gamma di tecnologie esistenti, incluse le seguenti:  
  
-   Servizi Web ASP.NET \(ASMX\), versione 1.  
  
-   Applicazioni Web Service Enhancements \(WSE\).  
  
-   Basic Profile come definito nella specifica Web Services Interoperability \(WS\-I\) \([http:\/\/go.microsoft.com\/fwlink\/?LinkId\=38995](http://go.microsoft.com/fwlink/?LinkId=38955), il contenuto potrebbe essere in inglese\).  
  
-   Basic Security Profile come definito in WS\-I.  
  
 Per impostazione predefinita, questa associazione non è protetta.È progettata per interagire con i servizi ASMX.Quando la sicurezza è attivata, l'associazione è progettata per l'interazione con meccanismi di sicurezza di Internet Information Services \(IIS\), ad esempio l'autenticazione di base, digest e la sicurezza di Windows integrata.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Panoramica sulla sicurezza del trasporto](../../../../docs/framework/wcf/feature-details/transport-security-overview.md).Questa associazione supporta:  
  
-   Sicurezza del trasporto HTTPS.  
  
-   Autenticazione di base HTTP.  
  
-   WS\-Security.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)], <xref:System.ServiceModel.BasicHttpSecurity>, <xref:System.ServiceModel.BasicHttpMessageSecurity>, <xref:System.ServiceModel.BasicHttpMessageCredentialType> e <xref:System.ServiceModel.BasicHttpSecurityMode>.  
  
### WSHttpBinding  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.WSHttpBinding>. Nella configurazione, utilizzare [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  
  
 Per impostazione predefinita, questa associazione implementa la specifica WS\-Security e fornisce interoperabilità con servizi che implementano le specifiche WS\-\*.Sono supportati:  
  
-   Sicurezza del trasporto HTTPS.  
  
-   WS\-Security.  
  
-   Protezione del trasporto HTTPS con sicurezza della credenziale messaggi SOAP per l'autenticazione del chiamante.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.WSHttpSecurity>, <xref:System.ServiceModel.MessageSecurityOverHttp>, <xref:System.ServiceModel.MessageCredentialType>, <xref:System.ServiceModel.SecurityMode>, <xref:System.ServiceModel.HttpTransportSecurity>, <xref:System.ServiceModel.HttpClientCredentialType>, e <xref:System.ServiceModel.HttpProxyCredentialType>.  
  
### WSDualHttpBinding  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.WSDualHttpBinding>. Nella configurazione, utilizzare [\<wsDualHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md).  
  
 Questa associazione è progettata per consentire applicazioni di servizio duplex.Implementa la specifica WS\-Security per la protezione del trasferimento basata sul messaggio.La protezione del trasporto non è disponibile.Per impostazione predefinita, fornisce le funzionalità seguenti:  
  
-   Implementa WS\-Reliable Messaging per l'affidabilità.  
  
-   Implementa WS\-Security per la protezione e l'autenticazione del trasferimento.  
  
-   Utilizza HTTP per il recapito dei messaggi.  
  
-   Utilizza la codifica dei messaggi testo\/XML.  
  
 Tramite WS\-Security \(protezione a livello di messaggio\), l'associazione consente di configurare i parametri seguenti:  
  
-   Suite di algoritmi di sicurezza per determinare l'algoritmo di crittografia.  
  
-   Opzioni dell'associazione per:  
  
    -   Fornitura di credenziali del servizio disponibili fuori banda nel client.  
  
    -   Fornitura di credenziali del servizio negoziate dal servizio come parte della configurazione del canale.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.WSDualHttpSecurity> e <xref:System.ServiceModel.WSDualHttpSecurityMode>.  
  
### NetTcpBinding  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.NetTcpBinding>. Nella configurazione, utilizzare [\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).  
  
 Questa associazione è ottimizzata per le comunicazioni tra computer.Per impostazione predefinita, dispone delle caratteristiche seguenti:  
  
-   Implementa la protezione a livello di trasporto.  
  
-   Utilizza la protezione di Windows per la protezione e l'autenticazione del trasferimento.  
  
-   Utilizza TCP per il trasporto.  
  
-   Implementa la codifica messaggi binaria.  
  
-   Implementa WS\-Reliable Messaging.  
  
 Le opzioni includono:  
  
-   Sicurezza a livello di messaggio \(tramite WS\-Security\).  
  
-   Sicurezza del trasporto con credenziali messaggio: riservatezza e integrità fornite da Transport Layer Security \(TLS\) su TCP e credenziali per l'autorizzazione fornite da WS\-Security.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetTcpSecurity>, <xref:System.ServiceModel.TcpTransportSecurity>, <xref:System.ServiceModel.TcpClientCredentialType>, <xref:System.ServiceModel.MessageSecurityOverTcp>, e <xref:System.ServiceModel.MessageCredentialType>.  
  
### NetNamedPipeBinding  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.NetNamedPipeBinding>. Nella configurazione, utilizzare [\<netNamedPipeBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netnamedpipebinding.md).  
  
 Questa associazione è ottimizzata per le comunicazioni tra processi \(in genere nello stesso computer\).Per impostazione predefinita, questa associazione dispone delle caratteristiche seguenti:  
  
-   Utilizza la sicurezza del trasporto per il trasferimento e l'autenticazione dei messaggi.  
  
-   Utilizza le named pipe per il recapito dei messaggi.  
  
-   Implementa la codifica messaggi binaria.  
  
-   Crittografia e firma dei messaggi.  
  
 Le opzioni includono:  
  
-   Autenticazione tramite la sicurezza di Windows.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetNamedPipeSecurity>, <xref:System.ServiceModel.NetNamedPipeSecurityMode> e <xref:System.ServiceModel.NamedPipeTransportSecurity>.  
  
### MsmqIntegrationBinding  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>. Nella configurazione, utilizzare [\<msmqIntegrationBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegrationbinding.md).  
  
 Questa associazione è ottimizzata per la creazione di client e servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che interagiscono con endpoint Accodamento messaggi Microsoft \(MSMQ\) non [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Per impostazione predefinita, questa associazione utilizza la sicurezza del trasporto e fornisce le caratteristiche di sicurezza seguenti:  
  
-   Possibilità di disattivare la sicurezza \(None\).  
  
-   Sicurezza del trasporto MSMQ \(Transport\).  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.NetMsmqSecurity> e <xref:System.ServiceModel.NetMsmqSecurityMode>.  
  
### NetMsmqBinding  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.NetMsmqBinding>. Nella configurazione, utilizzare [\<netMsmqBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md).  
  
 Questa associazione viene utilizzata per la creazione di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che richiedono il supporto di messaggi in coda MSMQ.  
  
 Per impostazione predefinita, questa associazione utilizza la sicurezza del trasporto e fornisce le caratteristiche di sicurezza seguenti:  
  
-   Possibilità di disattivare la sicurezza \(None\).  
  
-   Sicurezza del trasporto MSMQ \(Transport\).  
  
-   Sicurezza dei messaggi basati su SOAP \(Message\).  
  
-   Trasporto simultaneo e sicurezza dei messaggi \(Both\).  
  
-   Tipi di credenziale client supportati: None, Windows, UserName, Certificate, IssuedToken.  
  
 La credenziale <xref:System.ServiceModel.MessageCredentialType> è supportata solo quando la modalità di sicurezza è impostata su <xref:System.ServiceModel.NetMsmqSecurityMode> o su <xref:System.ServiceModel.NetMsmqSecurityMode>.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.MessageSecurityOverMsmq> e <xref:System.ServiceModel.MsmqTransportSecurity>.  
  
### WSFederationHttpBinding  
 Nel codice, utilizzare la classe <xref:System.ServiceModel.WSFederationHttpBinding>. Nella configurazione, utilizzare [\<wsFederationHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md).  
  
 Per impostazione predefinita, questa associazione utilizza WS\-Security \(sicurezza a livello di messaggio\).  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Federazione](../../../../docs/framework/wcf/feature-details/federation.md), <xref:System.ServiceModel.WSFederationHttpSecurity> e <xref:System.ServiceModel.WSFederationHttpSecurityMode>.  
  
## Associazioni personalizzate  
 Se i requisiti non vengono soddisfatti da alcuna associazione fornita dal sistema, è possibile creare un'associazione personalizzata con un elemento di associazione di sicurezza personalizzato.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Funzionalità di sicurezza con associazioni personalizzate](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md).  
  
## Scelte di associazioni  
 Nella tabella seguente vengono riepilogate le funzionalità offerte nell'impostazione della modalità di sicurezza, ovvero vengono elencate le funzionalità disponibili quando la modalità di sicurezza è impostata su `Transport`, `Message` o `TransportWithMessageCredential`.L'utilizzo di questa tabella consente di trovare le funzionalità di sicurezza più appropriate per l'applicazione.  
  
|Impostazione|Funzionalità|  
|------------------|------------------|  
|Transport|Autenticazione server<br /><br /> Autenticazione client<br /><br /> Sicurezza point\-to\-point<br /><br /> Interoperabilità<br /><br /> Accelerazione hardware<br /><br /> Velocità effettiva elevata<br /><br /> Firewall di sicurezza<br /><br /> Applicazioni con latenza elevata<br /><br /> Ripetizione della crittografia attraverso più hop|  
|Message|Autenticazione server<br /><br /> Autenticazione client<br /><br /> Sicurezza end\-to\-end<br /><br /> Interoperabilità<br /><br /> Attestazioni complesse<br /><br /> Federazione<br /><br /> Autenticazione a più fattori<br /><br /> Token personalizzati<br /><br /> Servizio notary\/timestamp<br /><br /> Applicazioni con latenza elevata<br /><br /> Persistenza di firme del messaggio|  
|TransportWithMessageCredential|Autenticazione server<br /><br /> Autenticazione client<br /><br /> Sicurezza point\-to\-point<br /><br /> Interoperabilità<br /><br /> Accelerazione hardware<br /><br /> Velocità effettiva elevata<br /><br /> Richieste del client Dettagliate<br /><br /> Federazione<br /><br /> Autenticazione a più fattori<br /><br /> Token personalizzati<br /><br /> Firewall di sicurezza<br /><br /> Applicazioni con latenza elevata<br /><br /> Ripetizione della crittografia attraverso più hop|  
  
 Nella tabella seguente vengono elencate le associazioni che supportano le impostazioni delle varie modalità.Selezionare un'associazione dalla tabella per creare l'endpoint del servizio.  
  
|Associazione|Supporto modalità trasporto|Supporto modalità messaggio|Supporto TransportWithMessageCredential|  
|------------------|---------------------------------|---------------------------------|---------------------------------------------|  
|`BasicHttpBinding`|Sì|Sì|Sì|  
|`WSHttpBinding`|Sì|Sì|Sì|  
|`WSDualHttpBinding`|No|Sì|No|  
|`NetTcpBinding`|Sì|Sì|Sì|  
|`NetNamedPipeBinding`|Sì|No|No|  
|`NetMsmqBinding`|Sì|Sì|No|  
|`MsmqIntegrationBinding`|Sì|No|No|  
|`wsFederationHttpBinding`|No|Sì|Sì|  
  
## Credenziali di trasporto nelle associazioni  
 Nella tabella seguente vengono elencati i tipi di credenziali client disponibili quando si utilizza `BasicHttpBinding` o `WSHttpBinding` nella modalità di sicurezza del trasporto.  
  
|Tipo|Descrizione|  
|----------|-----------------|  
|None|Specifica che il client non deve presentare alcuna credenziale.Il client viene pertanto autenticato come anonimo.|  
|Autenticazione di base|Autenticazione di base.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'articolo su RFC 2617, Autenticazione HTTP: autenticazione di base e digest, disponibile all'indirizzo [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=84023](http://go.microsoft.com/fwlink/?LinkId=84023) \(il contenuto potrebbe essere in inglese\).|  
|Digest|Autenticazione digest.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'articolo su RFC 2617, Autenticazione HTTP: autenticazione di base e digest, disponibile all'indirizzo [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=84023](http://go.microsoft.com/fwlink/?LinkId=84023) \(il contenuto potrebbe essere in inglese\).|  
|NTLM|Autenticazione NT LAN Manager \(NTLM\).|  
|Windows|Autenticazione Windows.|  
|Certificate|Autenticazione eseguita mediante un certificato.|  
|IssuedToken|Consente al servizio di richiedere l'autenticazione del client tramite un token emesso da un servizio token di sicurezza o da [!INCLUDE[infocard](../../../../includes/infocard-md.md)].[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Federazione e token emessi](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).|  
  
### Credenziali client dei messaggi nelle associazioni  
 Nella tabella seguente vengono elencati i tipi di credenziali client disponibili quando si utilizza un'associazione nella modalità di sicurezza dei messaggi.  
  
|Tipo|Descrizione|  
|----------|-----------------|  
|Nessuna|Consente al servizio di interagire con client anonimi.|  
|Windows|Consente gli scambi di messaggi SOAP nel contesto autenticato di una credenziale di Windows.|  
|UserName|Consente al servizio di richiedere che l'autenticazione del client sia eseguita tramite una credenziale di tipo nome utente.Si noti che quando la modalità di sicurezza è impostata su `TransportWithMessageCredential`, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non supporta l'invio di un digest delle password, né la derivazione delle chiavi basata su password e neppure l'utilizzo di tali chiavi per implementare la modalità di sicurezza dei messaggi.Di conseguenza, quando si utilizzano credenziali di tipo nome utente, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiede che il trasporto sia protetto.|  
|Certificato|Consente al servizio di richiedere che l'autenticazione del client sia basata su un certificato.|  
|IssuedToken|Consente al servizio di utilizzare un servizio token di sicurezza per fornire un token personalizzato.|  
  
## Vedere anche  
 [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Selezione di un tipo di credenziale](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)   
 [Funzionalità di sicurezza con associazioni personalizzate](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)   
 [Comportamenti di sicurezza](../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Sicurezza e protezione](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)