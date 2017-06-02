---
title: "Key Security Concepts | Microsoft Docs"
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
  - "unauthorized access"
  - "permissions [.NET Framework]"
  - "security [.NET Framework], about security"
ms.assetid: 3cfced4f-ea02-4e66-ae98-d69286363e98
caps.latest.revision: 22
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# Key Security Concepts
Microsoft .NET Framework offre la trasparenza della sicurezza, la sicurezza per l'accesso di codice e la sicurezza basata sui ruoli per risolvere i problemi di sicurezza relativi al codice mobile e fornire un supporto che consenta di abilitare i componenti per determinare le operazioni per cui gli utenti dispongono di autorizzazioni.  Questi meccanismi di sicurezza usano un modello semplice e coerente in modo che gli sviluppatori esperti in sicurezza per l'accesso di codice possano usare facilmente la sicurezza basata sui ruoli e viceversa.  La sicurezza per l'accesso di codice e la sicurezza basata sui ruoli vengono implementate usando un'infrastruttura comune fornita da Common Language Runtime.  
  
> [!NOTE]
>  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], la trasparenza della sicurezza è il meccanismo di imposizione predefinito.  La trasparenza della sicurezza separa il codice che viene eseguito come parte dell'applicazione dal codice eseguito come parte dell'infrastruttura.  Per altre informazioni, vedere [Security\-Transparent Code](../../../docs/framework/misc/security-transparent-code.md).  
  
 Poiché usano lo stesso modello e infrastruttura, la sicurezza per l'accesso di codice e la sicurezza basata sui ruoli condividono vari concetti di base, descritti in questa sezione.  Assicurarsi di avere sufficiente dimestichezza con questi concetti prima di leggere la documentazione per la sicurezza basata sui ruoli e la sicurezza per l'accesso di codice di .NET Framework.  
  
## Autorizzazioni di sicurezza  
 Common Language Runtime consente al codice di eseguire solo le operazioni che è autorizzato a eseguire.  Il runtime usa oggetti chiamati autorizzazioni per applicare restrizioni sul codice gestito.  Il runtime fornisce le classi di autorizzazione predefinite in diversi spazi dei nomi e supporta anche la progettazione e l'implementazione di classi di autorizzazione personalizzate.  
  
 Esistono due tipi di autorizzazione, ciascuno con uno scopo specifico:  
  
-   Le autorizzazioni di accesso al codice consentono l'accesso a una risorsa protetta o la possibilità di eseguire un'operazione protetta.  
  
-   Le autorizzazioni di sicurezza basate sui ruoli offrono un meccanismo per individuare se un utente \(o l'agente che opera per conto dell'utente\) dispone di una specifica identità o è membro di un ruolo specificato.  <xref:System.Security.Permissions.PrincipalPermission> è l'unica autorizzazione di sicurezza basata sui ruoli.  
  
 Le autorizzazioni di sicurezza possono essere fornite come classi di autorizzazioni \(sicurezza imperativa\) o come attributi che rappresentano una classe di autorizzazioni \(sicurezza dichiarativa\).  La classe base per le autorizzazioni di sicurezza è <xref:System.Security.CodeAccessPermission?displayProperty=fullName>; la classe base per gli attributi di autorizzazioni di sicurezza è <xref:System.Security.Permissions.CodeAccessSecurityAttribute?displayProperty=fullName>.  
  
 A un'applicazione, sotto forma di assembly, viene concesso un set di autorizzazioni durante la fase di caricamento in un dominio applicazione.  Le concessioni in genere vengono effettuate usando i set di autorizzazioni predefiniti determinati dal metodo <xref:System.Security.SecurityManager.GetStandardSandbox%2A?displayProperty=fullName>.  Il set di concessioni determina le autorizzazioni disponibili per il codice.  Il runtime concede le autorizzazioni in base alla posizione di origine del codice \(ad esempio, il computer locale, intranet locale o Internet\).  Al codice è anche possibile concedere autorizzazioni speciali se viene caricato in una sandbox.  Per altre informazioni sull'esecuzione di codice in una sandbox, vedere [How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
 Gli impieghi principali delle autorizzazioni sono i seguenti:  
  
-   Il codice di libreria può richiedere che i chiamanti dispongano di autorizzazioni specifiche.  Se si inserisce <xref:System.Security.CodeAccessPermission.Demand%2A> per un'autorizzazione nel proprio codice, tutto il codice che usa il codice personale deve disporre di tale autorizzazione per l'esecuzione.  Le richieste possono essere usate per determinare se i chiamanti dispongono dell'accesso a risorse specifiche o per individuare l'identità del chiamante.  
  
-   Il codice può usare le autorizzazioni per negare l'accesso alle risorse da proteggere.  È possibile usare <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName> per specificare un set di autorizzazioni limitato, negando implicitamente tutte le altre autorizzazioni.  Tuttavia, non è consigliabile usare <xref:System.Security.Permissions.SecurityAction> per impedire l'accesso al fine di proteggere la risorsa da un uso improprio intenzionale.  Gli assembly chiamati, che hanno implicitamente negato le autorizzazioni nel set di concessioni, possono eseguire l'override delle autorizzazioni negate eseguendo <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName> per qualsiasi autorizzazione desiderata.  Ad esempio, se è consentito solo <xref:System.Security.Permissions.UIPermission> e viene chiamato un assembly che contiene implicitamente <xref:System.Security.Permissions.FileIOPermission>, l'assembly può solo eseguire solo <xref:System.Security.Permissions.SecurityAction> per <xref:System.Security.Permissions.FileIOPermission> ed eseguire operazioni di file.  L'unico modo per proteggere in modo sicuro le risorse da codice non attendibile negli assembly di riferimento consiste nell'eseguire tale codice con un set di concessioni che non include tali autorizzazioni.  
  
### Autorizzazioni di accesso al codice  
 Le autorizzazioni di accesso al codice sono oggetti di autorizzazione che consentono di proteggere le risorse e le operazioni da un uso non autorizzato.  Sono una parte fondamentale del meccanismo di Common Language Runtime per applicare restrizioni di sicurezza al codice gestito.  
  
 Ogni autorizzazione di accesso al codice rappresenta uno dei seguenti diritti:  
  
-   Il diritto di accesso a una risorsa protetta, ad esempio file o variabili di ambiente.  
  
-   Il diritto di esecuzione di un'operazione protetta, ad esempio l'accesso al codice non gestito.  
  
 Il codice può richiedere tutte le autorizzazioni di accesso al codice, mentre il runtime decide quali autorizzazioni concedere, se disponibili.  
  
 Ogni autorizzazione di accesso al codice deriva dalla classe <xref:System.Security.CodeAccessPermission>, quindi tutte le autorizzazioni di accesso al codice dispongono di metodi in comune, ad esempio **Demand**, **Assert**, **Deny**, **PermitOnly**, **IsSubsetOf**, **Intersect** e **Union**.  
  
> [!IMPORTANT]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], il supporto runtime è stato rimosso per applicare le richieste di autorizzazione <xref:System.Security.Permissions.SecurityAction>, <xref:System.Security.Permissions.SecurityAction>, <xref:System.Security.Permissions.SecurityAction> e <xref:System.Security.Permissions.SecurityAction>.  Queste richieste non devono essere usate nel codice basato su [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] o versione successiva.  Per altre informazioni su questa e altre modifiche, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
### Autorizzazioni di sicurezza basata sui ruoli  
 <xref:System.Security.Permissions.PrincipalPermission> è un'autorizzazione di sicurezza basata sui ruoli che può essere usata per determinare se un utente dispone di un'identità specificata o è un membro di un ruolo specificato.  **PrincipalPermission** è l'unica autorizzazione di sicurezza basata sui ruoli fornita dalla libreria di classi .NET Framework.  
  
## Indipendenza dai tipi e sicurezza  
 Il codice indipendente dai tipi accede solo alle posizioni di memoria per le quali dispone di autorizzazioni.  In questo contesto, per indipendenza dai tipi si intende l'indipendenza dai tipi di memoria, che non deve essere confusa con il concetto più generico di indipendenza dai tipi. Ad esempio, un codice indipendente dai tipi non può leggere i valori dei campi privati di un altro oggetto.  Accede ai tipi solo in modalità ben definite e consentite.  
  
 Durante la compilazione Just\-In\-Time \(JIT\), un processo di verifica facoltativo esamina i metadati e MSIL \(Microsoft Intermediate Language\) di un metodo su cui eseguire la compilazione JIT in codice macchina nativo per verificare che siano indipendenti dai tipi.  Questo processo viene ignorato se il codice dispone dell'autorizzazione per ignorare la verifica.  Per altre informazioni sulla verifica, vedere [Processo di esecuzione gestita](../../../docs/standard/managed-execution-process.md).  
  
 Sebbene la verifica dell'indipendenza dai tipi non sia obbligatoria per l'esecuzione di codice gestito, l'indipendenza dai tipi ha un ruolo fondamentale nell'imposizione della sicurezza e nell'isolamento dell'assembly.  Quando il codice è indipendente dai tipi, Common Language Runtime può isolare completamente i singoli assembly.  Questo isolamento contribuisce a garantire che gli assembly non interferiscano tra loro, aumentando l'affidabilità dell'applicazione.  I componenti indipendenti dai tipi possono essere eseguiti in modo sicuro nello stesso processo anche se sono attendibili a livelli diversi.  Quando il codice non è indipendente dai tipi possono verificarsi effetti collaterali indesiderati.  Il runtime, ad esempio, non è in grado di impedire al codice gestito di effettuare chiamate a codice nativo \(non gestito\) e di eseguire operazioni dannose.  Quando il codice è indipendente dai tipi, il meccanismo di imposizione della sicurezza del runtime ne impedisce l'accesso al codice nativo a meno che non disponga delle autorizzazioni.  Per essere eseguito, tutto il codice non indipendente dai tipi deve aver ottenuto <xref:System.Security.Permissions.SecurityPermission> con il membro di enumerazione passato <xref:System.Security.Permissions.SecurityPermissionAttribute.SkipVerification%2A>.  
  
 Per altre informazioni, vedere [NIB: Writing Verifiably Type\-Safe Code](http://msdn.microsoft.com/it-it/d18f10ef-3b48-4f47-8726-96714021547b).  
  
## Principal  
 Un'entità rappresenta l'identità e il ruolo di un utente e agisce per conto dell'utente.  La sicurezza basata sui ruoli in .NET Framework supporta tre tipi di entità:  
  
-   Le entità generiche rappresentano utenti e ruoli che esistono indipendentemente dai ruoli e dagli utenti di Windows.  
  
-   Le entità di Windows rappresentano gli utenti di Windows e i relativi ruoli \(o i gruppi di Windows\).  Un'entità di Windows può rappresentare un altro utente, il che significa che l'entità può accedere a una risorsa per conto dell'utente presentando l'identità appartenente a tale utente.  
  
-   Le entità personalizzate possono essere definite da un'applicazione secondo le modalità richieste dalla specifica applicazione.  Possono estendere la nozione di base di identità e di ruoli dell'entità.  
  
 Per altre informazioni, vedere [Principal and Identity Objects](../../../docs/standard/security/principal-and-identity-objects.md).  
  
## Autenticazione  
 L'autenticazione è il processo di individuazione e verifica dell'identità di un'entità eseguito esaminando e convalidando le credenziali dell'utente rispetto a un'autorità specificata.  Le informazioni ottenute durante l'autenticazione possono essere usate direttamente dal codice.  È anche possibile usare la sicurezza basata sui ruoli di .NET Framework per autenticare l'utente corrente e per determinare se consentire a tale entità di accedere al codice.  Vedere gli overload del metodo <xref:System.Security.Principal.WindowsPrincipal.IsInRole%2A?displayProperty=fullName> per esempi su come autenticare l'entità per ruoli specifici.  Ad esempio, è possibile usare l'overload <xref:System.Security.Principal.WindowsPrincipal.IsInRole%28System.String%29?displayProperty=fullName> per determinare se l'utente corrente è un membro del gruppo Administrators.  
  
 Un'ampia gamma di meccanismi di autenticazione usati oggi, molti dei quali possono essere usati con la sicurezza basata sui ruoli di .NET Framework.  Alcuni dei meccanismi più diffusi sono il meccanismo di base, il digest, il Passport, il sistema operativo \(ad esempio NTLM o Kerberos\) o i meccanismi definiti dall'applicazione.  
  
### Esempio  
 L'esempio seguente richiede che l'entità attiva sia un amministratore.  Il parametro `name` è `null`, che consente a qualsiasi utente con ruolo di amministratore di passare la richiesta.  
  
> [!NOTE]
>  In Windows Vista, 	la funzionalità Controllo dell'account utente determina i privilegi di un utente.  Ai membri del gruppo Administrators predefinito vengono assegnati due token di accesso in fase di esecuzione, ovvero un token di accesso utente standard e un token di accesso amministratore.  Per impostazione predefinita, viene assegnato il ruolo dell'utente standard.  Per eseguire il codice che richiede un ruolo da amministratore è necessario elevare i privilegi da utente standard ad amministratore.  È possibile farlo quando si avvia un'applicazione facendo clic con il pulsante destro del mouse sull'icona dell'applicazione e indicando l'opzione di esecuzione come amministratore.  
  
 [!code-cpp[Classic PrincipalPermission Example#1](../../../samples/snippets/cpp/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/CPP/source.cpp#1)]
 [!code-csharp[Classic PrincipalPermission Example#1](../../../samples/snippets/csharp/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/CS/source.cs#1)]
 [!code-vb[Classic PrincipalPermission Example#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/VB/source.vb#1)]  
  
 L'esempio seguente mostra come determinare l'identità dell'entità e i ruoli disponibili per l'entità.  Un'applicazione di questo esempio potrebbe essere la conferma che l'utente corrente ha un ruolo autorizzato all'uso dell'applicazione.  
  
 [!code-cpp[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/CPP/source.cpp#1)]
 [!code-csharp[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/CS/source.cs#1)]
 [!code-vb[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/VB/source.vb#1)]  
  
## Autorizzazione  
 L'autorizzazione è il processo che consente di determinare se un'entità è autorizzata a eseguire un'azione richiesta.  L'autorizzazione si verifica dopo l'autenticazione e usa le informazioni di identità e i ruoli dell'entità per determinare a quali risorse può accedere.  È possibile usare la sicurezza basata sui ruoli di .NET Framework per implementare l'autorizzazione.  
  
## Problemi di sicurezza per le parole chiave virtuali interne  
 Evitare di basare la sicurezza dell'applicazione su un membro contrassegnato con il modificatore [internal](../Topic/internal%20\(C%23%20Reference\).md) [virtual](../Topic/virtual%20\(C%23%20Reference\).md) in C\# \(modificatore [Overload](../Topic/Overloads%20\(Visual%20Basic\).md) [Overridable](../Topic/Overridable%20\(Visual%20Basic\).md) [Friend](../Topic/Friend%20\(Visual%20Basic\).md) in Visual Basic\).  Sebbene i membri contrassegnati con questi modificatori possano essere modificati solo da altri membri all'interno dell'assembly corrente, questa regola viene applicata solo dai linguaggi C\# e Visual Basic.  Il runtime non applica questa regola.  È quindi possibile eseguire l'override dei membri contrassegnati come **internal virtual**in C\# e **Overloads Overridable Friend** in Visual Basic usando Microsoft Intermediate Language o qualsiasi altro linguaggio che non applichi questa regola.  
  
## Vedere anche  
 [Key Security Concepts](../../../docs/standard/security/key-security-concepts.md)