---
title: "Protezione di WCF Data Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "protezione dell'applicazione [WCF Data Services]"
  - "WCF Data Services, sicurezza"
ms.assetid: 99fc2baa-a040-4549-bc4d-f683d60298af
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Protezione di WCF Data Services
In questo argomento vengono illustrate alcune considerazioni sulla sicurezza che riguardano in modo particolare lo sviluppo, la distribuzione e l'esecuzione di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] e di applicazioni che accedono ai servizi che supportano [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)].  È consigliabile inoltre seguire le raccomandazioni relative alla creazione di applicazioni [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] protette.  
  
 Quando si pianifica come proteggere un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] basato su [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], è necessario considerare l'autenticazione \(il processo che consente di individuare e verificare l'identità di un'entità\) e l'autorizzazione \(il processo che consente di determinare se un'entità autenticata dispone dell'accesso alle risorse richieste\).  È necessario considerare anche se crittografare il messaggio tramite SSL.  
  
## Autenticazione di richieste del client  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] non implementa alcun tipo di autenticazione propria, piuttosto si basa sul provisioning di autenticazione dell'host del servizio dati.  Ciò vuole dire che il servizio presuppone che qualsiasi richiesta che riceve sia già stata autenticata dall'host di rete e che l'host abbia identificato correttamente il principio della richiesta tramite le interfacce fornite da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  Le opzioni di autenticazione e gli approcci sono illustrati in [Serie di autenticazione e OData](http://go.microsoft.com/fwlink/?LinkId=200381).  
  
### Opzioni di autenticazione per un servizio dati WCF  
 Nella tabella seguente vengono elencati alcuni dei meccanismi di autenticazione che sono disponibili per facilitare l'autenticazione delle richieste a un servizio dati WCF.  
  
|Opzioni di autenticazione|Descrizione|  
|-------------------------------|-----------------|  
|Autenticazione anonima|Quando l'autenticazione anonima HTTP è abilitata, qualsiasi principio è in grado di connettersi al servizio dati.  Le credenziali non sono richieste per l'accesso anonimo.  Utilizzare questa opzione solo quando si desidera consentire a chiunque l'accesso al servizio dati.|  
|Autenticazione di base e digest|Le credenziali composte da un nome utente e da una password sono richieste per l'autenticazione.  Supporta l'autenticazione di client non Windows. **Security Note:**  Le credenziali di autenticazione di base \(nome utente e password\) vengono inviate in chiaro e possono essere intercettate.  L'autenticazione digest invia un hash basato sulle credenziali fornite che la rende più sicura dell'autenticazione di base.  Entrambe le autenticazioni sono vulnerabili agli attacchi man\-in\-the\-middle.  Quando si utilizzano questi metodi di autenticazione, è necessario considerare di crittografare le comunicazione fra il client e il servizio dati tramite Secure Sockets Layer \(SSL\). <br /><br /> Microsoft Internet Information Services \(IIS\) fornisce un'implementazione dell'autenticazione digest e di base per le richieste HTTP in un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  Questa implementazione del provider di Autenticazione di Windows consente a un'applicazione client .NET Framework di fornire le credenziali nell'intestazione HTTP della richiesta al servizio dati per negoziare con facilità l'autenticazione di un utente Windows.  Per ulteriori informazioni, vedere [Riferimenti tecnici per l'autenticazione digest](http://go.microsoft.com/fwlink/?LinkId=200408).<br /><br /> Quando si desidera che il servizio dati utilizzi l'autenticazione di base secondo un servizio di autenticazione personalizzato e non con le credenziali di Windows, è necessario implementare un modulo HTTP [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] personalizzato per l'autenticazione.<br /><br /> [!INCLUDE[crexample](../../../../includes/crexample-md.md)] su come utilizzare uno schema di autenticazione di base personalizzato con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], vedere l'argomento [Autenticazione di base personalizzata](http://go.microsoft.com/fwlink/?LinkID=200388) in [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e le serie di autenticazione.|  
|Autenticazione di Windows|Le credenziali basate su Windows vengono scambiate tramite NTLM o Kerberos.  Questo meccanismo è più sicuro rispetto all'autenticazione di base o digest, ma richiede che il client sia un'applicazione basata su Windows.  IIS fornisce anche un'implementazione dell'autenticazione di Windows per le richieste HTTP in un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  Per ulteriori informazioni, vedere [ASP.NET Forms Authentication Overview](../Topic/ASP.NET%20Forms%20Authentication%20Overview.md).<br /><br /> [!INCLUDE[crexample](../../../../includes/crexample-md.md)] su come utilizzare l'autenticazione di Windows con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], vedere l'argomento [Autenticazione di Windows](http://go.microsoft.com/fwlink/?LinkID=200384) in [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e le serie di autenticazione.|  
|Autenticazione basata su form [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]|L'autenticazione basata su form consente di autenticare gli utenti mediante un codice personalizzato e di gestire un token di autenticazione in un cookie o nell'URL di pagina.  Viene eseguita l'autenticazione del nome utente e della password degli utenti utilizzando un form di accesso creato dall'utente.  Le richieste non autenticate vengono reindirizzate a una pagina di accesso, dove l'utente fornisce le credenziali e invia il form.  Se l'applicazione autentica la richiesta, il sistema elabora un ticket contenente una chiave per la ridefinizione dell'identità per le richieste successive.  Per ulteriori informazioni, vedere [Forms Authentication Provider](../Topic/Forms%20Authentication%20Provider.md). **Security Note:**  Per impostazione predefinita, il cookie contenente il ticket dell'autenticazione basata su form non è protetto quando si utilizza l'autenticazione basata su form in un'applicazione Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  È opportuno richiedere SSL per proteggere il ticket di autenticazione e le credenziali di accesso iniziale. <br /><br /> [!INCLUDE[crexample](../../../../includes/crexample-md.md)] su come utilizzare l'autenticazione basata su form con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], vedere l'argomento [Autenticazione basata su form](http://go.microsoft.com/fwlink/?LinkID=200389) in [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e le serie di autenticazione.|  
|Autenticazione basata sulle attestazioni|Nell'autenticazione basata sulle attestazioni, il servizio dati utilizza un servizio del provider di identità di "terze parti" attendibile per autenticare l'utente.  Il provider di identità autentica positivamente l'utente che sta richiedendo l'accesso alle risorse del servizio dati e rilascia un token che concede l'accesso alle risorse richieste.  Questo token viene quindi presentato al servizio dati che concede l'accesso all'utente in base alla relazione di trust con il servizio di identità che ha rilasciato il token di accesso.<br /><br /> Il provider di autenticazione basato sulle attestazioni risulta conveniente perché può essere utilizzato per autenticare vari tipi di client tra i vari domini trust.  Utilizzando un provider di terze parti di questo tipo, il servizio dati può scaricare i requisiti di gestione e autenticazione degli utenti.  OAuth 2.0 è un protocollo di autenticazione basato sulle attestazioni supportato dal Controllo di accesso AppFabric di Microsoft Azure per l'autorizzazione federata come servizio.  Questo protocollo supporta i servizi basati sul REST.  [!INCLUDE[crexample](../../../../includes/crexample-md.md)] di come utilizzare OAuth 2.0 con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], vedere l'argomento [OData e OAuth](http://go.microsoft.com/fwlink/?LinkId=200514) in [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e le serie di autenticazione.|  
  
<a name="clientAuthentication"></a>   
### Autenticazione nella libreria client  
 Per impostazione predefinita, la libreria client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] non fornisce le credenziali quando viene eseguita una richiesta a un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Quando le credenziali di accesso sono richieste dal servizio dati per autenticare un utente, è possibile fornire queste credenziali in un elemento <xref:System.Net.NetworkCredential> a cui accede la proprietà <xref:System.Data.Services.Client.DataServiceContext.Credentials%2A> di <xref:System.Data.Services.Client.DataServiceContext>, come nell'esempio seguente:  
  
  
  
 Per ulteriori informazioni, vedere [Procedura: specificare le credenziali del client per una richiesta del servizio dati](../../../../docs/framework/data/wcf/specify-client-creds-for-a-data-service-request-wcf.md).  
  
 Quando il servizio dati richiede credenziali di accesso che non possono essere specificate tramite un oggetto <xref:System.Net.NetworkCredential>, ad esempio un cookie o un token basato sulle attestazioni, è necessario impostare manualmente le intestazioni nella richiesta HTTP, generalmente le intestazioni `Authorization` e `Cookie`.  Per ulteriori informazioni su questo tipo di scenario di autenticazione, vedere l'argomento [OData e autenticazione: hook lato client](http://go.microsoft.com/fwlink/?LinkID=200385).  Per un esempio su come impostare le intestazioni HTTP in un messaggio di richiesta, vedere [Procedura: impostare le intestazioni nella richiesta del client](../../../../docs/framework/data/wcf/how-to-set-headers-in-the-client-request-wcf-data-services.md).  
  
## Rappresentazione  
 Generalmente il servizio dati accede alle risorse richieste, ad esempio i file sul server o un database, tramite le credenziali del processo di lavoro che ospita il servizio dati.  Quando si utilizza la rappresentazione, è possibile eseguire le applicazioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] con l'identità Windows \(account utente\) dell'utente che effettua la richiesta.  La rappresentazione è di uso comune in applicazioni che si basano su IIS per autenticare l'utente e le credenziali di questo principio sono utilizzate per accedere alle risorse richieste.  Per ulteriori informazioni, vedere [ASP.NET Impersonation](../Topic/ASP.NET%20Impersonation.md).  
  
## Configurazione dell'autorizzazione del servizio dati  
 L'autorizzazione è il conferimento dell'accesso alle risorse dell'applicazione concesso a un principio o un processo identificato in base a un'autenticazione precedentemente riuscita.  Come regola generale, è opportuno concedere agli utenti del servizio dati solo i diritti sufficienti per eseguire le operazioni richieste dalle applicazioni client.  
  
### Restrizione dell'accesso alle risorse del servizio dati  
 Per impostazione predefinita, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] concede l'accesso in lettura e scrittura comune alle risorse del servizio dati \(set di entità e operazioni del servizio\) a qualsiasi utente in grado di accedere al servizio dati.  Le regole che definiscono l'accesso in lettura e scrittura possono essere specificate separatamente per ogni set di entità esposto dal servizio dati così come per qualsiasi operazione del servizio.  Si consiglia di limitare l'accesso in lettura e scrittura solo alle risorse richieste dall'applicazione client.  Per ulteriori informazioni, vedere [Diritti minimi di accesso alle risorse](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md#accessRequirements).  
  
### Intercettori basati sulla regola di implementazione  
 Gli intercettori consentono di intercettare le richieste delle risorse del servizio dati prima che vengano elaborate dal servizio dati.  Per ulteriori informazioni, vedere [Intercettori](../../../../docs/framework/data/wcf/interceptors-wcf-data-services.md).  Gli intercettori consentono di concedere l'autorizzazione in base all'utente autenticato che effettua la richiesta.  [!INCLUDE[crexample](../../../../includes/crexample-md.md)] come limitare l'accesso alle risorse del servizio dati in base all'identità di un utente autenticato, vedere [Procedura: intercettare messaggi del servizio dati](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md).  
  
### Restrizione dell'accesso all'archivio dati persistente e alle risorse locali  
 È opportuno concedere agli account utilizzati per accedere all'archivio persistente solo i diritti in un database o nel file system sufficienti a supportare i requisiti del servizio dati.  Quando viene utilizzata l'autenticazione anonima, questo è l'account utilizzato per eseguire l'applicazione hosting.  Per ulteriori informazioni, vedere [Procedura: sviluppare un servizio WCF in esecuzione in IIS](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md).  Quando viene utilizzata la rappresentazione, agli utenti autenticati deve essere concesso l'accesso alle risorse, generalmente come parte di un gruppo di Windows.  
  
## Altre considerazioni sulla sicurezza  
  
### Protezione dei dati nel payload  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] si basa sul protocollo HTTP.  In un messaggio HTTP, è possibile che l'intestazione contenga credenziali dell'utente rilevanti, a seconda dell'autenticazione implementata dal servizio dati.  È possibile che anche il corpo del messaggio contenga dati del cliente rilevanti che devono essere protetti.  In entrambi i casi, si consiglia di utilizzare SSL per proteggere queste informazioni in rete.  
  
### Intestazioni dei messaggi e cookie ignorati  
 Le intestazioni delle richieste HTTP, diverse da quelle che dichiarano i tipi di contenuto e i percorsi delle risorse, vengono ignorate e non vengono mai impostate dal servizio dati.  
  
 I cookie possono essere utilizzati come parte di uno schema di autenticazione, ad esempio con Autenticazione basata su form [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  Tuttavia, qualsiasi cookie HTTP impostato su una richiesta in entrata viene ignorato da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  È possibile che l'host di un servizio dati elabori il cookie, ma il runtime di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] non analizza mai né restituisce cookie.  Anche la libreria client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] non elabora i cookie inviati nella risposta.  
  
### Requisiti dell'hosting personalizzato  
 Per impostazione predefinita, i servizi [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] vengono creati come un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] ospitata in IIS.  In tal modo il servizio dati potrà utilizzare i comportamenti sicuri della piattaforma.  È possibile definire i servizi [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] ospitati da un host personalizzato.  Per ulteriori informazioni, vedere [Hosting del servizio dati](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md).  I componenti e la piattaforma che ospitano un servizio dati devono assicurare i seguenti comportamenti di sicurezza per impedire attacchi sul servizio dati:  
  
-   Limitare la lunghezza dell'URI accettata in una richiesta del servizio dati per tutte le possibili operazioni.  
  
-   Limitare la dimensione dei messaggi HTTP in ingresso e in uscita.  
  
-   Limitare il numero totale di richieste in sospeso in qualsiasi momento.  
  
-   Limitare la dimensione delle intestazioni HTTP e relativi valori e fornire l'accesso [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] ai dati dell'intestazione.  
  
-   Rilevare e contrastare gli attacchi noti, ad esempio attacchi di tipo riproduzione di messaggi e SYN TCP.  
  
### Valori non ulteriormente codificati  
 I valori delle proprietà inviati al servizio dati non sono ulteriormente codificati dal runtime di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  Ad esempio, quando una proprietà di stringa di un'entità contiene contenuto HTML formattato, i tag non vengono codificati nel formato HTML dal servizio dati.  Il servizio dati non codifica ulteriormente neanche i valori di proprietà nella risposta.  La libreria client inoltre non esegue nessuna codifica aggiuntiva.  
  
### Considerazioni per le applicazioni client  
 Le seguenti considerazioni sulla sicurezza si applicano a tutte le applicazioni che utilizzano il client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per accedere ai servizi [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]:  
  
-   La libreria client presuppone che i protocolli utilizzati per accedere al servizio dati forniscano un livello di sicurezza appropriato.  
  
-   La libreria client utilizza tutti i valori predefiniti per i timeout e le opzioni di analisi degli stack di trasporto forniti dalla piattaforma sottostante.  
  
-   La libreria client non legge le impostazioni dai file di configurazione dell'applicazione.  
  
-   La libreria client non implementa alcun meccanismo di accesso tra domini.  Al contrario, utilizza i meccanismi forniti dallo stack HTTP sottostante.  
  
-   La libreria client non dispone di elementi dell'interfaccia utente e non visualizza i dati né esegue il rendering dei dati che riceve o invia.  
  
-   È opportuno che le applicazioni client convalidino sempre l'input dell'utente e i dati accettati da servizi non attendibili.  
  
## Vedere anche  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)