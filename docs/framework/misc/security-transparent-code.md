---
title: "Security-Transparent Code | Microsoft Docs"
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
  - "transparent code"
  - "security-transparent code"
ms.assetid: 4f3dd841-82f7-4659-aab0-6d2db2166c65
caps.latest.revision: 24
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 24
---
# Security-Transparent Code
<a name="top"></a> [!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 La sicurezza implica tre meccanismi che interagiscono tra loro: il sandboxing, le autorizzazioni e l'imposizione. Per sandboxing si intende la pratica basata sulla creazione di domini isolati in cui parte del codice viene trattata come codice completamente attendibile, mentre altro codice viene limitato con le autorizzazioni della concessione per il sandbox. Il codice dell'applicazione che viene eseguito all'interno della concessione del sandbox è considerato Transparent, ovvero non può eseguire operazioni che possono influire sulla sicurezza. La concessione impostata per il sandbox è determinata da un'evidenza \(classe <xref:System.Security.Policy.Evidence>\). L'evidenza identifica le autorizzazioni specifiche richieste dai sandbox e quali tipi di sandbox è possibile creare. L'imposizione consiste nel consentire l'esecuzione di codice Transparent solo all'interno della relativa concessione.  
  
> [!IMPORTANT]
>  I criteri di sicurezza erano un elemento fondamentale nelle versioni precedenti di .NET Framework. A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], i criteri di sicurezza sono obsoleti. L'eliminazione dei criteri di sicurezza non corrisponde alla trasparenza della sicurezza. Per informazioni sugli effetti di questa modifica, vedere [Code Access Security Policy Compatibility and Migration](../../../docs/framework/misc/code-access-security-policy-compatibility-and-migration.md).  
  
 In questo argomento viene descritto il modello di trasparenza in maggiore dettaglio. Include le sezioni seguenti:  
  
-   [Scopo del modello di trasparenza](#purpose)  
  
-   [Specifica del livello di trasparenza](#level)  
  
-   [Imposizione della trasparenza](#enforcement)  
  
<a name="purpose"></a>   
## Scopo del modello di trasparenza  
 La trasparenza è un meccanismo di imposizione che separa il codice che viene eseguito come parte dell'applicazione dal codice eseguito come parte dell'infrastruttura. La trasparenza consente di creare una barriera tra il codice autorizzato a eseguire operazioni privilegiate \(codice Critical\), ad esempio chiamare codice nativo, e il codice che non dispone di tale autorizzazione \(codice Transparent\). Il codice Transparent può eseguire comandi all'interno dei limiti del set di autorizzazioni in cui sta funzionando, ma non può eseguire, derivare o contenere codice Critical.  
  
 L'obiettivo principale dell'imposizione della trasparenza è fornire un meccanismo semplice e valido per isolare gruppi diversi di codice in base ai privilegi. Nel contesto del modello di sandboxing, questi gruppi di privilegi sono completamente attendibili \(non limitati\) o parzialmente attendibili \(limitati al set di autorizzazioni concesso al sandbox\).  
  
> [!IMPORTANT]
>  Il modello di trasparenza va oltre la sicurezza dall'accesso di codice. La trasparenza viene applicata dal compilatore JIT e rimane applicata indipendentemente dalla concessione per un assembly, inclusa l'attendibilità totale.  
  
 La trasparenza è stata introdotta in .NET Framework versione 2.0 per semplificare il modello di sicurezza e facilitare la scrittura e la distribuzione di librerie e applicazioni sicure. Il codice Transparent viene usato anche in Microsoft Silverlight per semplificare lo sviluppo di applicazioni parzialmente attendibili.  
  
> [!NOTE]
>  Quando si sviluppa un'applicazione parzialmente attendibile, è necessario tenere presenti i requisiti di autorizzazione per gli host di destinazione. È possibile sviluppare un'applicazione che usa risorse il cui uso non è consentito in alcuni host. Tale applicazione verrà compilata senza errori, ma non verrà eseguita correttamente quando verrà caricata nell'ambiente di hosting. Se l'applicazione è stata sviluppata con Visual Studio, è possibile attivare il debug in un ambiente parzialmente attendibile o in un set di autorizzazioni limitato dall'ambiente di sviluppo. Per altre informazioni, vedere [Procedura: eseguire il debug di un'applicazione ClickOnce con autorizzazioni limitate](../Topic/How%20to:%20Debug%20a%20ClickOnce%20Application%20with%20Restricted%20Permissions.md). La funzionalità Elabora autorizzazioni fornita per le applicazioni ClickOnce è anche disponibile per le applicazioni parzialmente attendibili.  
  
 [Torna all'inizio](#top)  
  
<a name="level"></a>   
## Specifica del livello di trasparenza  
 L'attributo <xref:System.Security.SecurityRulesAttribute> a livello di assembly consente di selezionare in modo esplicito le regole <xref:System.Security.SecurityRuleSet> che l'assembly seguirà. Le regole sono organizzate in un sistema a livelli numerici, dove i livelli superiori indicano un'imposizione più severa delle regole di sicurezza.  
  
 I livelli sono elencati di seguito.  
  
-   Livello 2 \(<xref:System.Security.SecurityRuleSet>\): regole di trasparenza di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
-   Livello 1 \(<xref:System.Security.SecurityRuleSet>\): regole di trasparenza di .NET Framework 2.0.  
  
 La differenza principale tra i due livelli di trasparenza è che il livello 1 non applica regole di trasparenza per le chiamate provenienti dall'esterno dell'assembly ed è disponibile solo per garantire la compatibilità.  
  
> [!IMPORTANT]
>  È necessario specificare la trasparenza di livello 1 solo per ragioni di compatibilità, ovvero specificare il livello 1 solo per codice sviluppato con .NET Framework 3.5 o versioni precedenti che usa l'attributo <xref:System.Security.AllowPartiallyTrustedCallersAttribute> o non usa il modello di trasparenza. Usare ad esempio la trasparenza di livello 1 per assembly .NET Framework 2.0 che consentono l'uso di chiamate da chiamanti parzialmente attendibili \(APTCA\). Per il codice sviluppato per [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], usare sempre la trasparenza di livello 2.  
  
### Trasparenza di livello 2  
 La trasparenza di livello 2 è stata introdotta in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]. I tre concetti principali di questo modello sono il codice Transparent, il codice SecuritySafeCritical e il codice SecurityCritical.  
  
-   Il codice Transparent, indipendentemente dalla autorizzazioni di cui dispone e anche nel caso dell'attendibilità totale, può chiamare solo altro codice Transparent o codice SecuritySafeCritical. Se il codice è parzialmente attendibile, può eseguire solo azioni consentite dal set di autorizzazioni del dominio. Il codice Transparent non può eseguire le operazioni seguenti:  
  
    -   Eseguire un'operazione <xref:System.Security.CodeAccessPermission.Assert%2A> o un'elevazione dei privilegi.  
  
    -   Contenere codice di tipo unsafe o non verificabile.  
  
    -   Chiamare direttamente codice Critical.  
  
    -   Chiamare codice nativo o codice con l'attributo <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>.  
  
    -   Chiamare un membro protetto da <xref:System.Security.Permissions.SecurityAction>.  
  
    -   Ereditare dai tipi Critical.  
  
     Inoltre, i metodi Transparent non possono eseguire l'override di metodi virtuali Critical o implementare metodi di interfaccia Critical.  
  
-   Il codice SecuritySafeCritical è completamente attendibile, ma può essere chiamato dal codice Transparent. Espone una superficie di attacco limitata di codice con attendibilità totale. Nel codice SafeCritical vengono eseguite verifiche della correttezza e della sicurezza.  
  
-   Il codice SecurityCritical può chiamare qualsiasi tipo di codice ed è completamente attendibile, ma non può essere chiamato da codice Transparent.  
  
### Trasparenza di livello 1  
 Il modello di trasparenza di livello 1 è stato introdotto in .NET Framework versione 2.0 per consentire agli sviluppatori di ridurre la quantità di codice soggetto a un controllo di sicurezza. Nonostante la trasparenza di livello 1 sia disponibile pubblicamente nella versione 2.0, è stata usata principalmente solo all'interno di Microsoft per operazioni di controllo della sicurezza. Consente agli sviluppatori di dichiarare con annotazioni quali tipi e membri possono eseguire elevazioni di sicurezza e altre azioni attendibili \(SecurityCritical\) e quali invece non possono eseguirle \(SecurityTransparent\). Il codice identificato come Transparent non richiede un alto livello di controllo della sicurezza. La trasparenza di livello 1 indica che l'imposizione della trasparenza è limitata all'interno dell'assembly. In altre parole, qualsiasi tipo o membro pubblico identificato come SecurityCritical è tale solo all'interno dell'assembly. Se si vuole applicare la sicurezza per determinati tipi e membri quando vengono chiamati dall'esterno dell'assembly, è necessario usare le richieste di collegamento per l'attendibilità totale. In caso contrario, i tipi e i membri SecurityCritical pubblicamente visibili vengono trattati come SecuritySafeCritical e possono essere chiamati da codice parzialmente attendibile esterno all'assembly.  
  
 Il modello di trasparenza di livello 1 presenta le limitazioni seguenti:  
  
-   I tipi e i membri SecurityCritical pubblici sono accessibili da codice SecurityTransparent.  
  
-   Le annotazioni di trasparenza vengono applicate solo all'interno di un assembly.  
  
-   I tipi e i membri SecurityCritical devono usare richieste di collegamento per applicare la sicurezza per le chiamate provenienti dall'esterno dell'assembly.  
  
-   Le regole di ereditarietà non vengono applicate.  
  
-   Esiste la possibilità che il codice Transparent esegua operazioni dannose quando viene eseguito con attendibilità totale.  
  
 [Torna all'inizio](#top)  
  
<a name="enforcement"></a>   
## Imposizione della trasparenza  
 Le regole di trasparenza non vengono applicate fino a quando la trasparenza non viene calcolata. In tale fase, viene generata un'eccezione <xref:System.InvalidOperationException> se una regola di trasparenza risulta violata. Il momento in cui viene calcolata la trasparenza dipende da vari fattori e non può essere previsto. Il calcolo avviene il più tardi possibile. In [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], il calcolo della trasparenza a livello di assembly si verifica prima di quanto avvenga in .NET Framework 2.0. L'unica garanzia è che il calcolo della trasparenza si verifica nel momento in cui è necessario. È un meccanismo analogo al modo in cui il compilatore JIT \(Just\-In\-Time\) può modificare il punto in cui un metodo viene compilato e gli eventuali errori in tale metodo vengono rilevati. Il calcolo della trasparenza è invisibile se il codice non contiene errori di trasparenza.  
  
## Vedere anche  
 [Security\-Transparent Code, Level 1](../../../docs/framework/misc/security-transparent-code-level-1.md)   
 [Security\-Transparent Code, Level 2](../../../docs/framework/misc/security-transparent-code-level-2.md)