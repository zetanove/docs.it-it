---
title: "Using Libraries from Partially Trusted Code | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "security [.NET Framework], partially trusted code"
  - "partially trusted code"
  - "partial trust"
  - "AllowPartiallyTrustedCallersAttribute attribute"
  - "code access security, partially trusted code"
  - "APTCA"
ms.assetid: dd66cd4c-b087-415f-9c3e-94e3a1835f74
caps.latest.revision: 25
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 23
---
# Using Libraries from Partially Trusted Code
> [!NOTE]
>  Questo argomento si riferisce al comportamento di assembly con nomi sicuri ed è valido solo per assembly di [livello 1](../../../docs/framework/misc/security-transparent-code-level-1.md). Gli assembly di[Security\-Transparent Code, Level 2](../../../docs/framework/misc/security-transparent-code-level-2.md) in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] o versioni successive non sono interessati dai nomi sicuri. Per altre informazioni sulle modifiche al sistema di sicurezza, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
> [!CAUTION]
>  Sicurezza dall'accesso di codice e codice parzialmente attendibile  
>   
>  .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  La sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta. Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
>   
>  Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
 Le applicazioni che non sono ritenute del tutto attendibili dall'host o sandbox non possono chiamare librerie gestite condivise a meno che il writer delle librerie non lo consenta in modo specifico mediante l'uso dell'attributo <xref:System.Security.AllowPartiallyTrustedCallersAttribute>. Di conseguenza, i writer delle applicazioni devono tenere presente che alcune librerie non saranno disponibili da un contesto parzialmente attendibile. Per impostazione predefinita, tutto il codice che viene eseguito in un [sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md) parzialmente attendibile e non è presente nell'elenco di assembly totalmente attendibili è parzialmente attendibile. Se non si prevede che il codice venga eseguito da un contesto parzialmente attendibile o venga chiamato da un codice parzialmente attendibile, non sono rilevanti le informazioni contenute in questa sezione. Se tuttavia si scrive codice che deve interagire con codice parzialmente attendibile o agire da un contesto parzialmente attendibile, si devono prendere in considerazione i seguenti fattori:  
  
-   Le librerie devono essere firmate con un nome sicuro per essere condivise da più applicazioni. I nomi sicuri consentono al codice di essere inserito in Global Assembly Cache o aggiunto all'elenco totalmente attendibile di un <xref:System.AppDomain> di sandboxing e consente agli utenti di verificare da quale altro utente ha origine una particolare parte di codice mobile.  
  
-   Per impostazione predefinita, le librerie condivise di [livello 1](../../../docs/framework/misc/security-transparent-code-level-1.md) con nomi sicuri eseguono automaticamente un [LinkDemand](../../../docs/framework/misc/link-demands.md) implicito per l'attendibilità totale, senza che il writer delle librerie debba eseguire alcuna operazione.  
  
-   Se un chiamante non dispone dell'attendibilità totale ma continua a chiamare quel tipo di libreria, il runtime genera un'eccezione <xref:System.Security.SecurityException> e al chiamante non è consentito collegarsi alla libreria.  
  
-   Per disabilitare il **LinkDemand** automatico e impedire che venga generata un'eccezione, è possibile inserire l'attributo **AllowPartiallyTrustedCallersAttribute** nell'ambito degli assembly di una libreria condivisa. Questo attributo consente alle librerie di essere chiamate da un codice gestito parzialmente attendibile.  
  
-   Il codice parzialmente attendibile a cui è concesso l'accesso a una libreria con questo attributo continua a essere oggetto di altre restrizioni definite da <xref:System.AppDomain>.  
  
-   Non esiste un modo a livello di programmazione per un codice parzialmente attendibile di chiamare una libreria che non dispone dell'attributo **AllowPartiallyTrustedCallersAttribute** .  
  
 Per le librerie che sono private per un'applicazione specifica non è necessario un nome sicuro oppure l'attributo **AllowPartiallyTrustedCallersAttribute** e non possono essere oggetto di codice potenzialmente dannoso al di fuori dell'applicazione. Questo tipo di codice è protetto da un uso improprio intenzionale o non intenzionale mediante codice mobile parzialmente attendibile senza altre operazioni da parte dello sviluppatore.  
  
 È consigliabile abilitare in modo esplicito l'utilizzo di codice parzialmente attendibile per i tipi di codice seguenti:  
  
-   Codice che sia stato attentamente sottoposto a test relativamente alla vulnerabilità della sicurezza e sia conforme con le linee guida descritte in [Linee guida per la generazione di codice sicuro](../../../docs/standard/security/secure-coding-guidelines.md).  
  
-   Librerie del codice con nome sicuro che sono scritte in modo specifico per scenari parzialmente attendibili.  
  
-   Tutti i componenti \(parzialmente o totalmente attendibili\) firmati con un nome sicuro che saranno chiamati dal codice scaricato da Internet.  
  
> [!NOTE]
>  Alcune classi nella libreria di classi .NET Framework non dispongono dell'attributo **AllowPartiallyTrustedCallersAttribute** e non possono essere chiamate da codice parzialmente attendibile.  
  
## Vedere anche  
 [Code Access Security](../../../docs/framework/misc/code-access-security.md)