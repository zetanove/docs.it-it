---
title: "Secure Coding Guidelines for Unmanaged Code | Microsoft Docs"
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
  - "code security, unmanaged code"
  - "unmanaged code, securing"
  - "security [.NET Framework], unmanaged code"
  - "secure coding, unmanaged code"
ms.assetid: a8d15139-d368-4c9c-a747-ba757781117c
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Secure Coding Guidelines for Unmanaged Code
Alcuni codici di libreria devono chiamare codice non gestito \(ad esempio, le API del codice nativo, come Win32\). Poiché questo comporta il superamento del perimetro di sicurezza per il codice gestito, è necessaria la dovuta attenzione. Se il codice è indipendente dalla sicurezza, sia il proprio codice sia il codice da cui viene chiamato devono avere l'autorizzazione per codice non gestito \(<xref:System.Security.Permissions.SecurityPermission> con il flag <xref:System.Security.Permissions.SecurityPermissionFlag> specificato\).  
  
 Tuttavia, è spesso sconsigliabile fornire al chiamante autorizzazioni di questo tipo. In questi casi, il codice attendibile può essere intermediario, simile al wrapper gestito o al codice di libreria descritto in [Protezione del codice wrapper](../../../docs/framework/misc/securing-wrapper-code.md). Se la funzionalità di codice non gestito sottostante è totalmente sicura, può essere esposta direttamente; in caso contrario, è richiesto prima un controllo di autorizzazione appropriato \(domanda\).  
  
 Quando il codice chiama codice non gestito, ma non si vuole che i chiamanti siano autorizzati ad accedere al codice non gestito, è necessario dichiarare tale diritto. Un'asserzione blocca il percorso stack in corrispondenza del frame. È necessario assicurarsi di non creare un problema di sicurezza in questo processo. In genere, ciò significa che è necessario richiedere un'autorizzazione dei chiamanti appropriata e quindi usare il codice non gestito per eseguire solo operazioni consentite dall'autorizzazione e nient'altro. In alcuni casi \(ad esempio, una funzione GET time\-of\-day\), il codice non gestito può essere esposto direttamente ai chiamanti senza controlli di sicurezza. Il codice in cui viene eseguita l'asserzione deve consentire in ogni caso la gestione della sicurezza.  
  
 Poiché il codice gestito in cui viene fornito un percorso di codice all'interno del codice nativo rappresenta un obiettivo potenziale del codice dannoso, è necessaria estrema attenzione per determinare quale parte di codice non gestito può essere usata con sicurezza e come usarla. In genere, il codice non gestito non deve essere mai esposto direttamente a chiamanti parzialmente attendibili. Nella valutazione della sicurezza del codice non gestito nelle librerie che è possibile chiamare da codice parzialmente attendibile, sono necessarie due considerazioni principali:  
  
-   **Funzionalità** Considerare se nel codice API non gestito sia fornita una funzionalità che non consenta ai chiamanti di eseguire operazioni potenzialmente dannose La sicurezza dall'accesso di codice impiega le autorizzazioni per applicare l'accesso alle risorse; considerare quindi se l'API consente di usare file, un'interfaccia utente o il threading oppure di esporre informazioni protette. In questo caso, dal codice gestito che funge da wrapper devono essere pretese le autorizzazioni necessarie prima di consentirne l'accesso. Inoltre, quando non è protetta da un'autorizzazione, è necessario che l'accesso alla memoria sia limitato alla rigida indipendenza dei tipi.  
  
-   **Controllo dei caratteri** In un attacco di tipo comune vengono passati parametri imprevisti a metodi API di codice non gestito esposto nel tentativo di determinarne il funzionamento al di fuori delle specifiche. I sovraccarichi del buffer tramite indici non compresi nell'intervallo o valori di offset costituiscono un esempio comune di questo tipo di attacco, allo stesso modo di altri parametri che possono sfruttare bug nel codice sottostante. Di conseguenza, anche se l'API del codice non gestito è protetta dal punto di vista funzionale, implementando cioè le esigenze di autorizzazioni che si reputano necessarie, per i chiamanti parzialmente attendibili deve essere eseguito anche il controllo completo della validità dei parametri, per evitare l'esecuzione di chiamate impreviste da parte di codice dannoso tramite il livello del wrapper del codice gestito.  
  
## Uso di SuppressUnmanagedCodeSecurityAttribute  
 Un aspetto delle prestazioni è quello relativo all'asserzione e alla chiamata di codice non gestito. Per ciascuna chiamata di questo tipo, il sistema di sicurezza esige automaticamente l'autorizzazione per codice non gestito, provocando di conseguenza un percorso stack per ciascuna occorrenza. Se viene eseguita l'asserzione e viene chiamato immediatamente codice non gestito, il percorso stack può essere inutile, in quanto consiste nell'asserzione e nella chiamata al codice non gestito.  
  
 Un attributo personalizzato denominato <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> può essere applicato ai punti di ingresso del codice non gestito per disabilitare il normale controllo di sicurezza per cui si richiede l'oggetto <xref:System.Security.Permissions.SecurityPermission> con l'autorizzazione <xref:System.Security.Permissions.SecurityPermissionFlag> specificata. Prestare sempre estrema attenzione durante l'esecuzione di questa operazione, poiché determina un punto di libero accesso al codice non gestito senza alcun controllo di sicurezza in fase di esecuzione. Anche se si applica l'attributo **SuppressUnmanagedCodeSecurityAttribute**, con la compilazione JIT viene eseguito, seppure una sola volta, un controllo di sicurezza per garantire che il chiamante immediato disponga dell'autorizzazione per chiamare codice non gestito.  
  
 Se si usa l'attributo **SuppressUnmanagedCodeSecurityAttribute**, verificare i seguenti punti:  
  
-   Rendere interno il punto di ingresso del codice non gestito o, in alternativa, renderlo inaccessibile dall'esterno del codice.  
  
-   Ogni chiamata nel codice non gestito rappresenta una potenziale vulnerabilità nella sicurezza. Accertarsi che il codice non rappresenti un punto di ingresso per le chiamate indirette da parte di codice dannoso al codice non gestito e non consenta di aggirare il controllo di sicurezza. Esigere autorizzazioni, se necessario.  
  
-   Usare una convenzione di denominazione per identificare in modo esplicito la creazione di un percorso pericoloso nel codice non gestito, come descritto nella sezione seguente.  
  
## Convenzione di denominazione per i metodi di codice non gestito  
 Per denominare metodi di codice non gestito è stata stabilita una convenzione utile, di cui si consiglia l'impiego. I metodi di codice non gestito sono suddivisi in tre categorie: **safe**, **native** e **unsafe**. Queste parole chiave possono essere usate come nomi di classi all'interno delle quali sono definiti i vari tipi di punti di ingresso del codice non gestito. Nel codice sorgente, le parole chiave devono essere aggiunte al nome della classe, come in `Safe.GetTimeOfDay`, `Native.Xyz` o `Unsafe.DangerousAPI`. Ognuna delle seguenti parole chiave fornisce informazioni sulla sicurezza utili per gli sviluppatori che usano la classe relativa, come descritto nella seguente tabella.  
  
|Parola chiave|Considerazioni sulla sicurezza|  
|-------------------|------------------------------------|  
|**safe**|Sicurezza completa dalle chiamate da parte del codice, anche di quello dannoso. L'uso è analogo a quello del normale codice gestito. Una funzione che ottiene l'ora del giorno, ad esempio, è in genere sicura.|  
|**native**|Indipendente dalla sicurezza; in altre parole, codice non gestito per cui è richiesta l'autorizzazione alla chiamata di codice non gestito. Viene eseguito il controllo di sicurezza, che blocca le chiamate non autorizzate.|  
|**unsafe**|Presenza di un punto di ingresso per codice non gestito pericoloso con annullamento della sicurezza. Gli sviluppatori dovranno usare la massima attenzione nell'uso di codice non gestito di questo tipo, accertandosi che siano attivi altri tipi di sicurezza per evitare vulnerabilità di sicurezza. Questa parola chiave consente l'override del sistema di sicurezza.|  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)