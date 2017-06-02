---
title: "Secure Coding Guidelines | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "managed wrapper to native code implementation"
  - "secure coding"
  - "reusable components"
  - "library code that exposes protected resources"
  - "code, security"
  - "code security"
  - "secure coding, options"
  - "components [.NET Framework], security"
  - "code security, options"
  - "security-neutral code"
  - "security [.NET Framework], coding guidelines"
ms.assetid: 4f882d94-262b-4494-b0a6-ba9ba1f5f177
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# Secure Coding Guidelines
La sicurezza basata sull'evidenza e la sicurezza per l'accesso al codice forniscono meccanismi espliciti molto efficaci per implementare la sicurezza. Nella maggior parte dei casi, per proteggere il codice delle applicazioni è sufficiente l'infrastruttura implementata da .NET Framework. In alcuni casi è tuttavia necessaria una sicurezza aggiuntiva specifica per l'applicazione, creata mediante l'estensione del sistema di sicurezza o tramite metodi ad hoc.  
  
 L'uso delle autorizzazioni applicate da .NET Framework e di altri tipi di sicurezza imposta nel codice consente di creare barriere che impediscono l'ottenimento di informazioni da parte di malware o l'esecuzione di altre operazioni non desiderate. È inoltre necessario raggiungere un compromesso tra sicurezza e usabilità del codice in tutti gli scenari d'uso di codice attendibile.  
  
 In questa panoramica vengono descritti i diversi metodi di progettazione del codice per l'uso del sistema di sicurezza.  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] sono state apportate importanti modifiche al modello di sicurezza e alla terminologia di .NET Framework. Per altre informazioni su queste modifiche, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
## Sicurezza dall'accesso di codice e codice parzialmente attendibile  
 .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  Poiché non garantisce l'isolamento del codice, la sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta. Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
  
 Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
## Codice indipendente dalla sicurezza  
 Il codice indipendente dalla sicurezza non ha elementi espliciti in comune con il sistema di sicurezza e viene eseguito a prescindere dalle autorizzazioni ricevute Anche se le applicazioni che non riescono a intercettare eccezioni associate alle operazioni protette, come l'uso di file o le operazioni in rete, possono avere come effetto eccezioni non gestite, il codice indipendente dalla sicurezza è comunque in grado di sfruttare le tecnologie di sicurezza di .NET Framework.  
  
 Una libreria indipendente dalla sicurezza dispone di caratteristiche speciali che è necessario comprendere. Si supponga che nella libreria siano forniti elementi API che consentano di usare file o chiamare codice non gestito. Se al codice non è associata l'autorizzazione corrispondente, questo non verrà eseguito nel modo descritto. Tuttavia, anche al codice viene concessa l'autorizzazione, il codice delle applicazioni da cui tale codice viene chiamato deve disporre della stessa autorizzazione per funzionare. Se il codice chiamante non dispone dell'autorizzazione appropriata, il percorso chiamate nello stack della sicurezza per l'accesso al codice genera un oggetto <xref:System.Security.SecurityException>.  
  
## Codice di applicazioni non riutilizzabile  
 Se il codice fa parte di un'applicazione che non verrà richiamata da altro codice, la sicurezza è semplice e potrebbe non essere necessario scrivere codice speciale. Tenere comunque presente che il codice può essere chiamato da codice dannoso. Anche se la sicurezza per l'accesso al codice può impedire a codice dannoso di accedere alle risorse, con questo codice è comunque possibile leggere i valori contenuti nei campi o nelle proprietà che possono rappresentare informazioni sensibili.  
  
 Se inoltre il codice accetta input da Internet o da altre fonti inaffidabili, è opportuno evitare input dannosi.  
  
## Wrapper gestiti nell'implementazione di codice nativo  
 In genere, in uno scenario di questo tipo, viene implementata una funzionalità utile nel codice nativo da rendere disponibile per il codice gestito. I wrapper gestiti possono essere scritti in modo semplice usando platform invoke o l'interoperabilità COM. Per la riuscita di questa operazione è tuttavia necessario che i chiamanti dei wrapper dispongano di diritti per il codice non gestito. In base ai criteri predefiniti, il codice scaricato da una rete Intranet o da Internet non funzionerà con i wrapper.  
  
 Invece di assegnare a tutte le applicazioni che impiegano i wrapper diritti di codice non gestito, è preferibile fornire questi diritti solo al codice wrapper. Se la funzionalità sottostante non espone alcuna risorsa e l'implementazione è probabilmente sicura, per il wrapper è sufficiente l'asserzione dei diritti, che consente la chiamata tramite codice. Quando sono coinvolte le risorse, il codice della sicurezza deve essere analogo a quello di libreria descritto nella sezione successiva. Poiché il wrapper può esporre i chiamanti a queste risorse, la verifica attenta della sicurezza del codice nativo è necessaria e costituisce uno dei compiti del wrapper.  
  
## Codice di libreria che espone risorse protette  
 Si tratta dell'approccio più efficace e potenzialmente pericoloso, se eseguito in modo non corretto, della codifica della sicurezza: la libreria funge da interfaccia per l'accesso tramite codice ad alcune risorse non altrimenti disponibili, così come le classi di .NET Framework impongono le autorizzazioni relative alle risorse che usano. Se si espone una risorsa, è necessario per prima cosa esigere tramite codice l'autorizzazione adeguata alla risorsa \(in altre parole, eseguire un controllo di sicurezza\) e quindi eseguire un'asserzione dei relativi diritti per eseguire l'operazione vera e propria.  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)|Viene illustrato come eseguire un'applicazione parzialmente attendibile in un ambiente di sicurezza con restrizioni, in cui le autorizzazioni di accesso al codice concesse all'applicazione sono limitate.|  
|[Securing State Data](../../../docs/standard/security/securing-state-data.md)|Viene descritto come proteggere membri privati.|  
|[Securing Method Access](../../../docs/framework/misc/securing-method-access.md)|Viene descritto come proteggere i metodi dalle chiamate da parte di codice parzialmente attendibile.|  
|[Securing Wrapper Code](../../../docs/framework/misc/securing-wrapper-code.md)|Vengono descritti argomenti relativi alla sicurezza del codice che esegue il wrapping di altro codice.|  
|[Security and Public Read\-only Array Fields](../../../docs/framework/misc/security-and-public-read-only-array-fields.md)|Vengono descritte le problematiche relative alla sicurezza per il codice che usa matrici pubbliche di sola lettura disponibili nelle librerie .NET Framework.|  
|[Securing Exception Handling](../../../docs/framework/misc/securing-exception-handling.md)|Vengono descritti aspetti della sicurezza relativi alla gestione delle eccezioni.|  
|[Security and User Input](../../../docs/standard/security/security-and-user-input.md)|Vengono descritti argomenti relativi alla sicurezza delle applicazioni che accettano input dell'utente.|  
|[Security and Remoting Considerations](../../../docs/framework/misc/security-and-remoting-considerations.md)|Vengono descritti argomenti relativi alla sicurezza delle applicazioni che comunicano tra domini di applicazioni.|  
|[Security and Serialization](../../../docs/framework/misc/security-and-serialization.md)|Vengono descritti aspetti della sicurezza relativi alla serializzazione degli oggetti.|  
|[Security and Race Conditions](../../../docs/standard/security/security-and-race-conditions.md)|Viene descritto come evitare race condition nel codice.|  
|[Security and On\-the\-Fly Code Generation](../../../docs/standard/security/security-and-on-the-fly-code-generation.md)|Vengono descritti aspetti della sicurezza relativi alle applicazioni che consentono di generare codice dinamico.|  
|[Security and Setup Issues](../Topic/Security%20and%20Setup%20Issues.md)|Vengono illustrate considerazioni relative a test e installazione dell'applicazione.|  
|[Code Access Security](../../../docs/framework/misc/code-access-security.md)|Viene descritta in modo dettagliato la sicurezza dall'accesso di codice di .NET Framework e viene illustrato come usarla nel codice.|  
|[Role\-Based Security](../../../docs/standard/security/role-based-security.md)|Viene descritta in modo dettagliato la sicurezza basata sui ruoli di .NET Framework e viene illustrato come usarla nel codice.|