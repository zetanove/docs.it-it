---
title: "Utilizzo della rappresentazione con la protezione del trasporto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 426df8cb-6337-4262-b2c0-b96c2edf21a9
caps.latest.revision: 12
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# Utilizzo della rappresentazione con la protezione del trasporto
La *rappresentazione* consiste nella capacità di un'applicazione server di assumere l'identità del client.In genere i servizi utilizzano la rappresentazione al momento della convalida dell'accesso alle risorse.L'applicazione server è in esecuzione tramite un account del servizio ma quando il server accetta una connessione client, rappresenta il client. In questo modo i controlli di accesso vengono eseguiti utilizzando le credenziali client.La protezione del trasporto è un meccanismo utilizzato sia per il passaggio delle credenziali che per la protezione della comunicazione tramite quelle credenziali.In questo argomento viene illustrato l'utilizzo della sicurezza del trasporto in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] con la funzionalità della rappresentazione.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] rappresentazione tramite la sicurezza del messaggio, vedere [Delega e rappresentazione](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md).  
  
## Cinque livelli di rappresentazione  
 La protezione del trasporto si avvale di cinque livelli di rappresentazione, come descritto nella tabella seguente.  
  
|Livello di rappresentazione|Descrizione|  
|---------------------------------|-----------------|  
|None|L'applicazione server non tenta di rappresentare il client.|  
|Anonymous|L'applicazione server è in grado di eseguire controlli di accesso a fronte delle credenziali client, ma non riceve alcuna informazione sull'identità del client.Questo livello di rappresentazione è significativo solo per comunicazioni su computer, ad esempio le named pipe.L'utilizzo di `Anonymous` con una connessione remota innalza il livello di rappresentazione a Identify.|  
|Identify|L'applicazione conosce l'identità del client ed è in grado di eseguire la convalida dell'accesso a fronte delle credenziali client, ma non è in grado di rappresentare il client.Identify è il livello di rappresentazione predefinito utilizzato con le credenziali SSPI in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], a meno che il provider di token non fornisca un livello di rappresentazione diverso.|  
|Impersonate|Oltre a eseguire controlli di accesso, l'applicazione server è in grado di accedere alle risorse nel server come client.L'applicazione server non è in grado di accedere alle risorse su computer remoti tramite l'identità del client poiché il token rappresentato non dispone di credenziali di rete.|  
|Delegate|Oltre ad avere le stesse funzionalità di `Impersonate`, il livello di rappresentazione Delegate consente all'applicazione server l'accesso a risorse in computer remoti utilizzando l'identità del client e il passaggio dell'identità ad altre applicazioni.<br /><br /> **Importante** Per utilizzare queste funzionalità aggiuntive, l'account di dominio server deve essere contrassegnato come attendibile per la delega nel controller di dominio.È impossibile utilizzare questo livello di rappresentazione con account di dominio client contrassegnati come riservati.|  
  
 I livelli utilizzati più comunemente con la protezione del trasporto sono `Identify` e `Impersonate`.I livelli `None` e `Anonymous` non sono consigliati per un utilizzo tipico. Molti trasporti inoltre non supportano l'utilizzo di tali livelli con l'autenticazione.Il livello `Delegate` è una funzionalità potente che deve essere utilizzata con cautela.Solo ad applicazioni server attendibili deve essere fornita l'autorizzazione per delegare credenziali.  
  
 L'utilizzo della rappresentazione ai livelli `Impersonate` o `Delegate` richiede che l'applicazione server disponga del privilegio `SeImpersonatePrivilege`.Un'applicazione dispone di questo privilegio per impostazione predefinita se è in esecuzione in un account nel gruppo Administrators o in un account con un SID del servizio \(Servizio di rete, Servizio locale o Sistema locale\).La rappresentazione non richiede autenticazione reciproca tra client e server.È impossibile utilizzare alcuni schemi di autenticazione che supportano la rappresentazione, ad esempio NTLM, con l'autenticazione reciproca.  
  
## Problemi specifici del trasporto con la rappresentazione  
 La scelta di un trasporto in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] influisce sulle possibili scelte per la rappresentazione.In questa sezione vengono descritti i problemi che influiscono sui trasporti standard HTTP e sui trasporti delle named pipe in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].I trasporti personalizzati presentano restrizioni relative al supporto per la rappresentazione.  
  
### Trasporto di named pipe  
 Gli elementi seguenti vengono utilizzati con il trasporto di named pipe:  
  
-   Il trasporto di named pipe è concepito per l'utilizzo solo nel computer locale.Il trasporto di named pipe in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] impedisce in modo esplicito le connessioni tra computer.  
  
-   Non è possibile utilizzare le named pipe con livelli di rappresentazione `Impersonate` o `Delegate`.La named pipe non è in grado di imporre la garanzia su computer con questi livelli di rappresentazione.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulle named pipe, vedere [Scelta di un trasporto](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md).  
  
### Trasporto HTTP  
 Le associazioni che utilizzano il trasporto HTTP, <xref:System.ServiceModel.WSHttpBinding> e <xref:System.ServiceModel.BasicHttpBinding>, supportano numerosi schemi di autenticazione, come spiegato in [Informazioni sull'autenticazione HTTP](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md).Il livello di rappresentazione supportato dipende dallo schema di autenticazione.Gli elementi seguenti vengono utilizzati con il trasporto HTTP:  
  
-   Lo schema di autenticazione `Anonymous` ignora la rappresentazione.  
  
-   Lo schema di autenticazione `Basic` supporta solo il livello `Delegate`.Tutti i livelli di rappresentazione inferiori vengono aggiornati.  
  
-   Lo schema di autenticazione `Digest` supporta solo i livelli `Impersonate` e `Delegate`.  
  
-   Lo schema di autenticazione `NTLM`, selezionabile direttamente o tramite negoziazione, supporta solo il livello `Delegate` nel computer locale.  
  
-   Lo schema di autenticazione Kerberos, selezionabile solo tramite negoziazione, può essere utilizzato con qualsiasi livello di rappresentazione supportato.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sul trasporto HTTP, vedere [Scelta di un trasporto](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md).  
  
## Vedere anche  
 [Delega e rappresentazione](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)   
 [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)   
 [Procedura: rappresentare un client in un servizio](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)   
 [Informazioni sull'autenticazione HTTP](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)