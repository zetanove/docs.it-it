---
title: "Autorizzazione basata su attestazioni con WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e24000a3-8fd8-4c0e-bdf0-39882cc0f6d8
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Autorizzazione basata su attestazioni con WIF
Tramite l'autorizzazione di un'applicazione relying party vengono determinate le risorse di un'identità autenticata a cui è consentito l'accesso e le operazioni eseguibili in queste risorse.  Un'autorizzazione non corretta o debole comporta la diffusione di informazioni e l'alterazione dei dati.  In questo argomento vengono descritti gli approcci disponibili per implementare l'autorizzazione per i servizi e le applicazioni Web ASP.NET in grado di riconoscere attestazioni mediante WIF \(Windows Identity Foundation\) e un servizio token di sicurezza \(STS\), ad esempio il Servizio di controllo di accesso \(ACS\) di Microsoft Azure.  
  
## Panoramica  
 Fin dalla prima versione, in .NET Framework viene fornito un meccanismo flessibile per implementare l'autorizzazione.  Questo meccanismo è basato su due interfacce semplici, vale a dire **IPrincipal** e **IIdentity**.  Le implementazioni concrete di **IIdentity** rappresentano un utente autenticato.  Ad esempio, l'implementazione di **WindowsIdentity** rappresenta un utente autenticato da Active Directory e **GenericIdentity** rappresenta un utente la cui identità viene verificata tramite un processo di autenticazione personalizzato.  Le implementazioni concrete di **IPrincipal** consentono di verificare le autorizzazioni utilizzando ruoli in base all'archivio ruoli.  Ad esempio, con **WindowsPrincipal** viene verificata l'appartenenza di **WindowsIdentity** ai gruppi Active Directory.  Questo controllo viene eseguito chiamando il metodo **IsInRole** sull'interfaccia **IPrincipal** e viene definito controllo dell'accesso basato sui ruoli \(RBAC\).  Per ulteriori informazioni, vedere [Controllo dell'accesso basato sui ruoli](../../../docs/framework/security/claims-based-authorization-using-wif.md#BKMK_1).  Le attestazioni possono essere utilizzate per trasferire le informazioni sui ruoli per supportare i comuni meccanismi dell'autorizzazione basata sui ruoli.  
  
 Inoltre, possono essere utilizzate per abilitare decisioni di autorizzazione più complesse oltre ai ruoli.  Le attestazioni possono essere basate praticamente su qualsiasi informazione sull'utente, ad esempio nome, codice di avviamento postale e così via. Un meccanismo di controllo di accesso basato su attestazioni arbitrarie viene definito autorizzazione basata sulle attestazioni.  Per ulteriori informazioni, vedere [Autorizzazione basata sulle attestazioni](../../../docs/framework/security/claims-based-authorization-using-wif.md#BKMK_2).  
  
<a name="BKMK_1"></a>   
## Controllo dell'accesso basato sui ruoli  
 Il controllo dell'accesso basato sui ruoli è un approccio di autorizzazione in cui le autorizzazioni utente vengono gestite e applicate da un'applicazione basata sui ruoli utente.  Se un utente dispone di un ruolo necessario per l'esecuzione di un'azione, l'accesso viene consentito; in caso contrario, viene negato.  
  
### Metodo IPrincipal.IsInRole  
 Per implementare l'approccio di controllo dell'accesso basato sui ruoli nelle applicazioni in grado di riconoscere attestazioni, utilizzare il metodo **IsInRole\(\)** nell'interfaccia **IPrinicpal**, come nelle applicazioni non in grado di riconoscere attestazioni.  Vi sono diversi modi per utilizzare il metodo **IsInRole\(\)**:  
  
-   Effettuando una chiamata in modo esplicito su **IPrincipal.IsInRole\("Amministratore"\)**.  In questo approccio, il risultato è un valore booleano.  Utilizzarlo nelle istruzioni condizionali.  Può essere utilizzato in modo arbitrario in qualsiasi punto nel codice.  
  
-   Utilizzando la richiesta di sicurezza **PrincipalPermission.Demand\(\)**.  In questo approccio, il risultato è un'eccezione in caso di richiesta non soddisfatta.  Deve rientrare nella strategia di gestione delle eccezioni.  La generazione delle eccezioni è molto più costosa da una prospettiva di prestazioni rispetto al ritiro di un valore booleano.  Può essere utilizzata in qualsiasi punto nel codice.  
  
-   Utilizzando gli attributi dichiarativi **\[PrincipalPermission\(SecurityAction.Demand, Role \= "Administrator"\)\]**.  Questo approccio viene chiamato dichiarativo, in quanto viene utilizzato per decorare i metodi.  Non può essere utilizzato in blocchi di codice nelle implementazioni del metodo.  Il risultato è un'eccezione in caso di richiesta non soddisfatta.  È necessario assicurarsi che rientri nella strategia di gestione delle eccezioni.  
  
-   Utilizzando l'autorizzazione URL, mediante la sezione **\<authorization\>** in **web.config**.  Questo approccio è utile quando si gestisce l'autorizzazione in un livello URL.  Si tratta del livello più grezzo tra quelli indicati in precedenza.  Il vantaggio di questo approccio è che le modifiche vengono apportate nel file di configurazione, pertanto il codice non deve essere compilato per sfruttare la modifica.  
  
### Espressione dei ruoli come attestazioni  
 Quando il metodo **IsInRole\(\)** viene chiamato, viene effettuato un controllo per verificare se l'utente corrente dispone del ruolo in questione.  Nelle applicazioni in grado di riconoscere attestazioni il ruolo è espresso da un tipo di attestazione del ruolo che deve essere disponibile nel token.  Il tipo di attestazione del ruolo viene espresso tramite l'URI seguente:  
  
 http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/role  
  
 Vi sono diversi modi per arricchire un token con un tipo di attestazione del ruolo:  
  
-   **Durate il rilascio dei token**.  Quando un utente viene autenticato, l'attestazione del ruolo può essere emessa dal servizio token di sicurezza del provider di identità o da un provider di federazioni, ad esempio il Servizio di controllo di accesso \(ACS\) di Microsoft Azure.  
  
-   **Trasformazione delle attestazioni arbitrarie in tipi di attestazioni del ruolo mediante ClaimsAuthenticationManager**.  ClaimsAuthenticationManager è un componente fornito come parte di WIF.  Consente l'intercettazione delle richieste quando tramite esse viene avviata un'applicazione, esaminando i token e trasformandoli con l'aggiunta, la modifica o la rimozione di attestazioni.  Per ulteriori informazioni sull'utilizzo di ClaimsAuthenticationManager per la trasformazione delle attestazioni, vedere [Procedura: implementare mediante WIF e ACS il controllo di accesso basato sui ruoli \(RBAC\) in un'applicazione ASP.NET in grado di riconoscere attestazioni](http://go.microsoft.com/fwlink/?LinkID=247445) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=247444\).  
  
-   **Mapping di attestazioni arbitrarie a un tipo di ruolo utilizzando la sezione di configurazione samlSecurityTokenRequirement**. Un approccio dichiarativo in cui la trasformazione delle attestazioni viene eseguita utilizzando solo la configurazione senza la necessità di eventuale codice.  
  
<a name="BKMK_2"></a>   
## Autorizzazione basata sulle attestazioni  
 L'autorizzazione basata sulle attestazioni è un approccio in cui la decisione di autorizzazione di concedere o negare l'accesso è basata sulla logica arbitraria che utilizza i dati disponibili nelle attestazioni per prendere la decisione.  Si tenga presente che nel caso del controllo dell'accesso basato sui ruoli, l'unica attestazione utilizzata è quella di tipo del ruolo.  Per controllare se l'utente appartiene o meno a un ruolo specifico, è stata utilizzata un'attestazione di tipo del ruolo.  Per illustrare il processo per prendere decisioni di autorizzazione utilizzando l'approccio basato sulle attestazioni, si tengano in considerazione i passaggi seguenti:  
  
1.  Dall'applicazione viene ricevuta una richiesta in cui l'utente deve essere autenticato.  
  
2.  Tramite WIF l'utente viene reindirizzato al provider di identità. Dopo essere stata autenticata, la richiesta di applicazione viene eseguita con un token di sicurezza associato che rappresenta l'utente che contiene le attestazioni su di esse.  Queste attestazioni vengono associate da WIF all'entità principale che rappresenta l'utente.  
  
3.  Tramite l'applicazione le attestazioni vengono passate al meccanismo della logica delle decisioni.  Può essere il codice in memoria, una chiamata a un servizio Web, una query a un database, un motore regole avanzato o l'utilizzo di ClaimsAuthorizationManager.  
  
4.  Con il meccanismo delle decisioni viene calcolato il risultato in base alle attestazioni.  
  
5.  L'accesso viene consentito se il risultato è true e viene negato se è false.  Ad esempio, la regola potrebbe essere che l'utente ha 21 anni, o anche di più, e vive nello stato di Washington.  
  
 L'oggetto <xref:System.Security.Claims.ClaimsAuthorizationManager> è utile per esternalizzare la logica delle decisioni per l'autorizzazione basata su attestazioni nelle applicazioni.  ClaimsAuthorizationManager è un componente di WIF fornito come parte di .NET 4.5. Con ClaimsAuthorizationManager è possibile intercettare le richieste in ingresso e implementare qualsiasi logica di scelta per prendere decisioni di autorizzazioni basate sulle attestazioni in ingresso.  Questo aspetto diventa importante quando è necessario modificare la logica dell'autorizzazione.  In tal caso, l'utilizzo di ClaimsAuthorizationManager non influirà sull'integrità dell'applicazione, quindi riducendo la probabilità di un errore di applicazione come risultato della modifica.  Per ulteriori informazioni su come utilizzare ClaimsAuthorizationManager per implementare il controllo dell'accesso basato sulle attestazioni, vedere [Procedura: implementare mediante WIF e ACS l'autorizzazione delle attestazioni in un'applicazione ASP.NET in grado di riconoscere attestazioni](http://go.microsoft.com/fwlink/?LinkID=247446).