---
title: "Cenni preliminari sulla sicurezza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "WCF, sicurezza"
  - "Windows Communication Foundation, sicurezza"
ms.assetid: f478c80d-792d-4e7a-96bd-a2ff0b6f65f9
caps.latest.revision: 37
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 37
---
# Cenni preliminari sulla sicurezza
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è una piattaforma di programmazione distribuita basata su messaggi SOAP. La protezione dei messaggi tra i client e i servizi è pertanto essenziale per garantire la protezione dei dati.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce una piattaforma versatile e interoperativa per lo scambio di messaggi protetti basato sull'infrastruttura di sicurezza esistente e sugli standard di sicurezza riconosciuti per i messaggi SOAP.  
  
> [!NOTE]
>  Per una guida completa alla sicurezza WCF, vedere la pagina relativa al [materiale sussidiario sulla sicurezza di WCF](http://go.microsoft.com/fwlink/?LinkID=158912).  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa concetti che sono familiari a coloro che hanno creato applicazioni distribuite protette usando tecnologie esistenti quali HTTPS, la sicurezza integrata di Windows o nomi utente e password per autenticare gli utenti.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non solo si integra alle infrastrutture di sicurezza esistenti, ma estende la sicurezza distribuita anche ai domini non Windows usando messaggi SOAP protetti.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere considerato come un'implementazione di meccanismi di sicurezza esistenti, con l'ulteriore vantaggio di usare il protocollo SOAP in aggiunta ai protocolli esistenti.  Ad esempio, le credenziali che identificano un client o un servizio, quali nome utente e password o certificati X.509, hanno profili SOAP interoperativi basati su XML.  Se si usano questi profili, i messaggi vengono scambiati in modo protetto usufruendo dei vantaggi delle specifiche aperte quali le firme digitali e la crittografia XML.  Per un elenco delle specifiche, vedere [Protocolli di servizi Web supportati da associazioni di interoperabilità fornite dal sistema](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md).  
  
 Un altro servizio parallelo è COM \(Component Object Model\) sulla piattaforma Windows, che consente applicazioni distribuite protette.  COM dispone di un meccanismo di sicurezza completo mediante il quale il contesto di sicurezza può essere propagato tra i componenti. Questo meccanismo applica l'integrità, la riservatezza e l'autenticazione.  Contrariamente a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], tuttavia, COM non consente la messaggistica protetta tra piattaforme diverse.  Usando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è possibile compilare servizi e client che si estendono da domini Windows su Internet.  I messaggi interoperativi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono essenziali per la compilazione di servizi dinamici gestiti dall'azienda che garantiscono la sicurezza delle informazioni.  
  
## Vantaggi della sicurezza di Windows Communication Foundation  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è una piattaforma di programmazione distribuita basata su messaggi SOAP.  Usando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è possibile creare applicazioni che funzionano sia come servizi che come client di servizio, creando ed elaborando messaggi da un numero illimitato di altri servizi e client.  In un'applicazione distribuita di questo tipo i messaggi possono fluire da nodo a nodo, attraverso firewall, su Internet e attraverso numerosi intermediari SOAP.  Ciò introduce tutta una serie di rischi per la sicurezza dei messaggi.  Negli esempi seguenti sono illustrate alcune minacce comuni che la sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può consentire di mitigare quando si scambiano messaggi tra entità:  
  
-   Osservazione del traffico di rete per ottenere informazioni riservate.  In uno scenario di online banking, ad esempio, un cliente richiede il trasferimento di fondi da un conto a un altro.  Un utente malintenzionato intercetta il messaggio e, disponendo del numero di conto e della password, esegue successivamente un trasferimento di fondi dal conto compromesso.  
  
-   Entità non autorizzate che agiscono come servizi all'insaputa del cliente.  In questo scenario un utente malintenzionato \(l'entità non autorizzata\) agisce come un servizio online e intercetta messaggi inviati dal cliente per ottenere informazioni riservate.  L'entità non autorizzata usa quindi i dati rubati per trasferire fondi dal conto compromesso.  Questo attacco è noto anche come *attacco di phishing*.  
  
-   Modifica di messaggi per ottenere un risultato diverso da quello voluto dal chiamante.  Ad esempio, la modifica del numero di conto nel quale viene effettuato un deposito consente il trasferimento di fondi in un conto non autorizzato.  
  
-   Riproduzioni hacker in cui un hacker "nuisance" riproduce lo stesso ordine di acquisto.  Ad esempio, una libreria online riceve centinaia di ordini e invia i libri a un cliente che non li ha ordinati.  
  
-   Incapacità di un servizio di autenticare un client.  In questo caso, il servizio non può assicurare che la transazione sia stata eseguita dalla persona appropriata.  
  
 In sintesi, la sicurezza del trasferimento fornisce le garanzie seguenti:  
  
-   Autenticazione dell'endpoint servizio \(rispondente\).  
  
-   Autenticazione dell'entità client \(iniziatore\).  
  
-   Integrità del messaggio.  
  
-   Riservatezza del messaggio.  
  
-   Rilevamento riproduzione.  
  
### Integrazione con infrastrutture di sicurezza esistenti  
 Nelle distribuzioni di servizi Web sono spesso già presenti soluzioni di sicurezza quali Secure Sockets Layer \(SSL\) o il protocollo Kerberos.  Alcune distribuzioni sfruttano un'infrastruttura di sicurezza che è già stata distribuita, come i domini Windows che usano Active Directory.  Spesso è necessario integrare le distribuzioni con queste tecnologie esistenti, nonché valutare e adottare nuove tecnologie.  
  
 La sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si integra con i modelli di sicurezza del trasporto esistenti e può sfruttare l'infrastruttura esistente per modelli di sicurezza del trasferimento più recenti basati sulla sicurezza dei messaggi SOAP.  
  
### Integrazione con modelli di autenticazione esistenti  
 Un aspetto importante di qualsiasi modello di sicurezza della comunicazione è la possibilità di identificare e autenticare entità in comunicazione.  Queste entità in comunicazione usano "identità digitali", o credenziali, per l'autenticazione con i peer in comunicazione.  Con l'evolversi delle piattaforme di comunicazione distribuite sono state implementate varie funzionalità di autenticazione delle credenziali e modelli di sicurezza correlati.  Su Internet, ad esempio, l'uso di un nome utente e di una password per identificare gli utenti è prassi comune.  Sulla rete Intranet l'uso di un controller di dominio Kerberos per eseguire il backup dell'autenticazione degli utenti e dei servizi sta diventando una prassi comune.  In certi scenari, ad esempio tra due partner aziendali, i certificati possono essere usati per l'autenticazione reciproca dei partner.  
  
 Così, nel mondo dei servizi Web, dove lo stesso servizio può essere esposto ai clienti interni dell'azienda così come a partner esterni o a clienti Internet, è importante che l'infrastruttura consenta l'integrazione con questi modelli di autenticazione della sicurezza esistenti.  La sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta un'ampia varietà di tipi di credenziali \(modelli di autenticazione\), tra cui:  
  
-   Chiamante anonimo.  
  
-   Credenziale client nome utente.  
  
-   Credenziale client certificato.  
  
-   Windows \(sia protocollo Kerberos che NT LanMan \[NTLM\]\).  
  
### Standard e interoperabilità  
 In un panorama caratterizzato da grandi distribuzioni esistenti, l'omogeneità è rara.  Le piattaforme di calcolo\/comunicazione distribuite devono poter interagire con le tecnologie offerte dai diversi fornitori.  Anche la sicurezza deve essere quindi interoperativa.  
  
 Per consentire sistemi di sicurezza interoperativi, le aziende che operano nell'industria dei servizi Web hanno creato una serie di standard.  Specificamente riguardo alla sicurezza sono stati proposti alcuni standard noti: WS\-Security: SOAP Message Security \(accettato tra gli standard OASIS e già noto come WS\-Security\), WS\-Trust, WS\-SecureConversation e WS\-SecurityPolicy.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta un'ampia varietà di scenari di interoperabilità.  La classe <xref:System.ServiceModel.BasicHttpBinding> è associata allo standard Basic Security Profile \(BSP\) e la classe <xref:System.ServiceModel.WSHttpBinding> è associata agli standard di sicurezza più recenti quali WS\-Security 1.1 e WS\-SecureConversation.  Aderendo a questi standard, la sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è in grado di interagire e integrarsi con servizi Web ospitati in sistemi operativi e piattaforme diverse da Microsoft Windows.  
  
## Aree funzionali della sicurezza di WCF  
 Il sistema di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si suddivide in tre aree funzionali: sicurezza del trasferimento, controllo di accesso e controllo.  Nelle sezioni seguenti vengono descritte brevemente queste aree funzionali e vengono forniti collegamenti per altre informazioni.  
  
### Sicurezza del trasferimento  
 La sicurezza del trasferimento comprende tre funzioni di sicurezza principali: integrità, riservatezza e autenticazione.  Per *integrità* si intende la capacità di rilevare se un messaggio è stato manomesso.  Per *riservatezza* si intende la capacità di rendere illeggibile un messaggio a qualsiasi utente diverso dal destinatario desiderato. A tale scopo viene usata la crittografia.  Per *autenticazione* si intende la capacità di verificare un'identità attestata.  Nel complesso queste tre funzioni consentono di garantire che i messaggi vengano inviati in modo protetto da un punto a un altro.  
  
#### Modalità di sicurezza del trasporto e dei messaggi  
 Per implementare la sicurezza del trasferimento in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono usati due meccanismi principali: modalità di sicurezza del *trasporto* e modalità di sicurezza del *messaggio*.  
  
-   Per ottenere la sicurezza del trasferimento la *modalità di sicurezza del trasporto* usa un protocollo a livello di trasporto, ad esempio HTTPS.  La modalità di sicurezza del trasporto ha il vantaggio di essere ampiamente diffusa, disponibile su più piattaforme e meno complessa dal punto di vista computazionale.  Ha tuttavia lo svantaggio di proteggere i messaggi solo da punto a punto.  
  
-   Per implementare la sicurezza del trasferimento, la *modalità di sicurezza del messaggio* usa invece WS\-Security \(e altre specifiche\).  Poiché la sicurezza del messaggio viene applicata direttamente ai messaggi SOAP ed è contenuta negli elementi SOAP Envelope unitamente ai dati dell'applicazione, ha il vantaggio di essere indipendente dal protocollo di trasporto, di essere maggiormente estensibile e di garantire la sicurezza end\-to\-end \(anziché point\-to\-point\). Ha lo svantaggio di essere notevolmente più lenta rispetto alla modalità di sicurezza del trasporto perché deve trattare con la natura XML dei messaggi SOAP.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] queste differenze, vedere [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md).  
  
 Una terza modalità di sicurezza usa entrambe le modalità precedenti e sfrutta i vantaggi di entrambe.  Questa modalità è detta `TransportWithMessageCredential`.  In questa modalità la sicurezza del messaggio viene usata per autenticare il client e la sicurezza del trasporto viene usata per autenticare il server e fornire riservatezza e integrità dei messaggi.  La modalità di sicurezza `TransportWithMessageCredential` è infatti veloce quasi quanto la modalità di sicurezza del trasporto e fornisce estensibilità per l'autenticazione client ugualmente alla modalità di sicurezza del messaggio.  A differenza della modalità di sicurezza del messaggio, tuttavia, non fornisce la sicurezza end\-to\-end completa.  
  
### Controllo di accesso  
 Il *controllo di accesso* è anche noto come autorizzazione.  L'*autorizzazione* consente a utenti diversi di disporre di privilegi diversi per visualizzare dati.  Ad esempio, poiché i file relativi alle risorse umane di un'azienda contengono dati riservati sui dipendenti, la visualizzazione di questi dati è consentita soltanto ai dirigenti,  che possono tuttavia visualizzare soltanto i dati relativi ai propri subalterni.  In questo caso, il controllo di accesso è basato sia sul ruolo \("dirigente"\) che sull'identità specifica del dirigente \(per impedire a un dirigente di accedere ai record relativi ai subalterni di un altro dirigente\).  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] le funzionalità del controllo di accesso vengono fornite attraverso l'integrazione con la classe <xref:System.Security.Permissions.PrincipalPermissionAttribute> CLR e attraverso un set di API noto come il *modello di identità*.  Per informazioni dettagliate sul controllo di accesso e sull'autorizzazione basata sulle attestazioni, vedere [Estensione della protezione](../../../../docs/framework/wcf/extending/extending-security.md).  
  
### Controllo  
 Per *controllo* si intende la registrazione degli eventi di sicurezza nel registro eventi di Windows.  È possibile registrare eventi relativi alla sicurezza, ad esempio le operazioni di autenticazione riuscite o non riuscite.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  Per informazioni dettagliate sulla programmazione, vedere [Procedura: controllare gli eventi di sicurezza](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md).  
  
## Vedere anche  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>   
 [Protezione dei servizi](../../../../docs/framework/wcf/securing-services.md)   
 [Scenari di sicurezza comuni](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)   
 [Associazioni e protezione](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)   
 [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Autenticazione](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)   
 [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)   
 [Federazione e token emessi](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [Controllo](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)   
 [Indicazioni di sicurezza e procedure consigliate](../../../../docs/framework/wcf/feature-details/security-guidance-and-best-practices.md)   
 [Configurazione dei servizi tramite file di configurazione](../../../../docs/framework/wcf/configuring-services-using-configuration-files.md)   
 [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [Cenni preliminari sulla creazione di endpoint](../../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Estensione della protezione](../../../../docs/framework/wcf/extending/extending-security.md)   
 [Modello di sicurezza per Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)