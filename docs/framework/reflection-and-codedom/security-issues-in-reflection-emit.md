---
title: "Security Issues in Reflection Emit | Microsoft Docs"
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
  - "partially trusted code"
  - "emitting dynamic assemblies, security"
  - "reflection emit, security"
  - "reflection emit, partial trust scenarios"
  - "partial trust,emitting dynamic methods"
  - "anonymously hosted dynamic methods [.NET Framework]"
  - "emitting dynamic assemblies,partial trust scenarios"
  - "dynamic assemblies, security"
ms.assetid: 0f8bf8fa-b993-478f-87ab-1a1a7976d298
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Security Issues in Reflection Emit
[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fornisce tre modalità per creare codice Microsoft Intermediate Language \(MSIL\), ciascuna con specifici problemi di sicurezza:  
  
-   [Assembly dinamici](#Dynamic_Assemblies)  
  
-   [Metodi dinamici ospitati anonimamente](#Anonymously_Hosted_Dynamic_Methods)  
  
-   [Metodi dinamici associati ad assembly esistenti](#Dynamic_Methods_Associated_with_Existing_Assemblies)  
  
 Indipendentemente dalla modalità di generazione del codice dinamico, l'esecuzione del codice generato richiede tutte le autorizzazioni necessarie per i tipi e i metodi usati dal codice generato.  
  
> [!NOTE]
>  Le autorizzazioni necessarie per la reflection sul codice e sul codice di creazione sono state modificate nelle versioni successive di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  Vedere [Informazioni sulla versione](#Version_Information) più avanti in questo argomento.  
  
<a name="Dynamic_Assemblies"></a>   
## Assembly dinamici  
 Gli assembly dinamici vengono creati usando gli overload del metodo <xref:System.AppDomain.DefineDynamicAssembly%2A?displayProperty=fullName>.  La maggior parte degli overload di questo metodo sono deprecati in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] a causa dell'eliminazione dei criteri di sicurezza a livello di computer.  Vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md). Gli overload rimanenti possono essere eseguiti da qualsiasi codice, indipendentemente dal livello di attendibilità.  Questi overload rientrano in due gruppi: quelli che specificano un elenco di attributi da applicare all'assembly dinamico quando viene creato e quelli che non lo specificano.  Se non si specifica il modello di trasparenza per l'assembly, applicando l'attributo <xref:System.Security.SecurityRulesAttribute> durante la creazione, il modello di trasparenza viene ereditato dall'assembly di creazione.  
  
> [!NOTE]
>  Gli attributi applicati all'assembly dinamico dopo averlo creato mediante il metodo <xref:System.Reflection.Emit.AssemblyBuilder.SetCustomAttribute%2A> non sono effettivi fino a quando l'assembly non viene salvato su disco e caricato di nuovo in memoria.  
  
 Il codice in un assembly dinamico può accedere a tipi e membri visibili in altri assembly.  
  
> [!NOTE]
>  Gli assembly dinamici non usano i flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> e <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> che consentono ai metodi dinamici di accedere a tipi e membri non pubblici.  
  
 Gli assembly dinamici temporanei vengono creati in memoria e non vengono mai salvati su disco, pertanto non richiedono alcuna autorizzazione di accesso ai file.  Il salvataggio di un assembly dinamico su disco richiede <xref:System.Security.Permissions.FileIOPermission> con flag appropriati.  
  
### Generazione di assembly dinamici da codice parzialmente attendibile  
 Considerare le condizioni in cui un assembly con autorizzazioni Internet può generare un assembly dinamico temporaneo ed eseguirne il codice:  
  
-   L'assembly dinamico usa solo tipi e membri pubblici di altri assembly.  
  
-   Le autorizzazioni richieste da questi tipi e membri sono incluse nel set di concessioni dell'assembly parzialmente attendibile.  
  
-   L'assembly non viene salvato su disco.  
  
-   I simboli di debug non vengono generati.  I set di autorizzazioni `Internet` e `LocalIntranet` non includono le autorizzazioni necessarie.  
  
<a name="Anonymously_Hosted_Dynamic_Methods"></a>   
## Metodi dinamici ospitati anonimamente  
 I metodi dinamici ospitati anonimamente vengono creati usando i due costruttori <xref:System.Reflection.Emit.DynamicMethod> che non specificano un tipo o un modulo associato, [DynamicMethod\(String, Type, Type\<xref:System.Reflection.Emit.DynamicMethod.%23ctor%28System.String%2CSystem.Type%2CSystem.Type%5B%5D%29> e [DynamicMethod\(String, Type, Type\<xref:System.Reflection.Emit.DynamicMethod.%23ctor%28System.String%2CSystem.Type%2CSystem.Type%5B%5D%2CSystem.Boolean%29>.  Questi costruttori inseriscono i metodi dinamici in un assembly fornito dal sistema, completamente attendibile, trasparente per la sicurezza.  Non sono necessarie autorizzazioni per usare questi costruttori o per generare il codice per i metodi dinamici.  
  
 Al contrario, quando viene creato un metodo dinamico ospitato anonimamente, viene acquisito lo stack di chiamate.  Quando il metodo viene costruito, le richieste di sicurezza vengono effettuate sullo stack di chiamate acquisito.  
  
> [!NOTE]
>  Concettualmente, le richieste vengono effettuate durante la costruzione del metodo.  In altre parole, le richieste potrebbero essere effettuate durante la creazione delle singole istruzioni MSIL.  Nell'implementazione corrente tutte le richieste vengono effettuate quando il metodo <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A?displayProperty=fullName> viene chiamato o quando viene richiamato il compilatore Just\-In\-Time \(JIT\), se il metodo viene richiamato senza chiamare <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A>.  
  
 Se il dominio applicazione lo consente, i metodi dinamici ospitati anonimamente possono ignorare i controlli di visibilità JIT, ma solo se viene rispettata la restrizione seguente: i tipi e i membri non pubblici a cui accede un metodo dinamico ospitato anonimamente devono trovarsi in assembly i cui set di concessioni sono uguali o sono subset del set di concessioni dello stack di chiamate di creazione.  Questa possibilità limitata di ignorare i controlli di visibilità JIT viene abilitata se il dominio applicazione concede <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>.  
  
-   Se il metodo usa solo tipi e membri pubblici, non sono necessarie autorizzazioni durante la costruzione.  
  
-   Se si specifica che i controlli di visibilità JIT debbano essere ignorati, la richiesta effettuata durante la costruzione del metodo includerà <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> e il set di concessioni dell'assembly che contiene il membro non pubblico a cui si accede.  
  
 Poiché il set di concessioni del membro non pubblico viene preso in considerazione, il codice parzialmente attendibile che ha ottenuto <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> non può elevare i privilegi eseguendo membri non pubblici di assembly attendibili.  
  
 Come con qualsiasi altro codice generato, l'esecuzione del metodo dinamico richiede le autorizzazioni obbligatorie per i metodi usate dal metodo dinamico.  
  
 L'assembly di sistema che ospita i metodi dinamici ospitati anonimamente usa il modello di trasparenza <xref:System.Security.SecurityRuleSet?displayProperty=fullName>, usato in .NET Framework prima di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
 Per altre informazioni, vedere la classe <xref:System.Reflection.Emit.DynamicMethod>.  
  
### Generazione di metodi dinamici ospitati anonimamente dal codice parzialmente attendibile  
 Considerare le condizioni in cui un assembly con autorizzazioni Internet può generare un metodo dinamico ospitato anonimamente ed eseguirlo:  
  
-   Il metodo dinamico usa solo tipi e membri pubblici.  Se il set di concessioni include <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>, è possibile usare i tipi e i membri non pubblici di qualsiasi assembly il cui set di concessioni sia uguale o sia un subset del set di concessioni dell'assembly di creazione.  
  
-   Le autorizzazioni necessarie per tutti i tipi e i membri usati dal metodo dinamico sono incluse nel set di concessioni dell'assembly parzialmente attendibile.  
  
> [!NOTE]
>  I metodi dinamici non supportano i simboli di debug.  
  
<a name="Dynamic_Methods_Associated_with_Existing_Assemblies"></a>   
## Metodi dinamici associati ad assembly esistenti  
 Per associare un metodo dinamico a un tipo o a un modulo in un assembly esistente, usare uno qualsiasi dei costruttori <xref:System.Reflection.Emit.DynamicMethod> che specificano il tipo o il modulo associato.  Le autorizzazioni necessarie per chiamare questi costruttori variano, poiché l'associazione di un metodo dinamico a un tipo o a un modulo esistente fornisce al metodo dinamico l'accesso ai membri e ai tipi non pubblici:  
  
-   Un metodo dinamico associato a un tipo può accedere a tutti i membri di tale tipo, anche ai membri privati, e a tutti i tipi e membri interni nell'assembly che contiene il tipo associato.  
  
-   Un metodo dinamico associato a un modulo può accedere a tutti i tipi e membri di `internal` \(`Friend` in Visual Basic, `assembly` nei metadati di Common Language Runtime\) nel modulo.  
  
 Inoltre, è possibile usare un costruttore che consente di specificare la possibilità di ignorare i controlli di visibilità del compilatore JIT.  In questo modo il metodo dinamico può accedere a tutti i tipi e membri in tutti gli assembly, indipendentemente dal livello di accesso.  
  
 Le autorizzazioni richieste dal costruttore dipendono dal livello di accesso che si decide di concedere al metodo dinamico:  
  
-   Se il metodo usa solo membri e tipi pubblici e lo si associa a un tipo o a un modulo personalizzato, non sono necessarie autorizzazioni.  
  
-   Se si specifica che devono essere ignorati i controlli di visibilità JIT, il costruttore richiede <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>.  
  
-   Se si associa il metodo dinamico a un altro tipo, anche all'interno dell'assembly, il costruttore richiede <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> e <xref:System.Security.Permissions.SecurityPermission> con il flag <xref:System.Security.Permissions.SecurityPermissionFlag?displayProperty=fullName>.  
  
-   Se si associa il metodo dinamico a un tipo o a un modulo in un altro assembly, il costruttore richiede due cose: <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> e il set di concessioni dell'assembly che contiene l'altro modulo.  Ovvero, lo stack di chiamate deve includere tutte le autorizzazioni nel set di concessioni del modulo di destinazione, oltre a <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>.  
  
    > [!NOTE]
    >  Per la compatibilità con le versioni precedenti, se la richiesta per il set di concessioni di destinazione con <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> ha esito negativo, il costruttore richiede <xref:System.Security.Permissions.SecurityPermission> con il flag <xref:System.Security.Permissions.SecurityPermissionFlag?displayProperty=fullName>.  
  
 Anche se gli elementi nell'elenco vengono descritti in termini di set di concessioni dell'assembly, tenere presente che le richieste vengono effettuate sullo stack di chiamate completo, incluso il limite del dominio applicazione.  
  
 Per altre informazioni, vedere la classe <xref:System.Reflection.Emit.DynamicMethod>.  
  
### Generazione di metodi dinamici dal codice parzialmente attendibile  
  
> [!NOTE]
>  Il metodo consigliato per generare metodi dinamici dal codice parzialmente attendibile consiste nell'usare [metodi dinamici ospitati anonimamente](#Anonymously_Hosted_Dynamic_Methods).  
  
 Considerare le condizioni in cui un assembly con autorizzazioni Internet può generare un metodo dinamico ed eseguirlo:  
  
-   Il metodo dinamico è associato al modulo o al tipo che lo genera oppure il set di concessioni include <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> ed è associato a un modulo in un assembly il cui set di concessioni è uguale o è un subset del set di concessioni dell'assembly di creazione.  
  
-   Il metodo dinamico usa solo tipi e membri pubblici.  Se il set di concessioni include <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> ed è associato a un modulo in un assembly il cui set di concessioni è uguale o è un subset del set di concessioni dell'assembly di creazione, può usare tipi e membri contrassegnati come `internal` \(`Friend` in Visual Basic, `assembly` nei metadati di Common Language Runtime\) nel modulo associato.  
  
-   Le autorizzazioni richieste da tutti i tipi e i membri usati dal metodo dinamico sono inclusi nel set di concessioni dell'assembly parzialmente attendibile.  
  
-   Il metodo dinamico non ignora i controlli di visibilità JIT.  
  
> [!NOTE]
>  I metodi dinamici non supportano i simboli di debug.  
  
<a name="Version_Information"></a>   
## Informazioni sulla versione  
 A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], i criteri di sicurezza a livello di computer vengono eliminati e la trasparenza della sicurezza diventa il meccanismo di imposizione predefinito.  Vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
 A partire da [!INCLUDE[net_v20SP1_long](../../../includes/net-v20sp1-long-md.md)], <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> non è più necessario quando si generano assembly e metodi dinamici.  Questo flag è richiesto in tutte le versioni precedenti di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
> [!NOTE]
>  <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> viene incluso per impostazione predefinita nei set di autorizzazioni denominati `FullTrust` e `LocalIntranet`, ma non nel set di autorizzazioni `Internet`.  Pertanto, nelle versioni precedenti di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], è possibile usare una libreria con autorizzazioni Internet solo se viene eseguito un <xref:System.Security.PermissionSet.Assert%2A> per <xref:System.Security.Permissions.ReflectionPermissionFlag>.  Tali librerie richiedono un'attenta revisione della sicurezza perché eventuali errori nel codice potrebbe produrre delle vulnerabilità.  [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] consente di generare codice in scenari con attendibilità parziale senza emettere alcuna richiesta di sicurezza, poiché la generazione di codice di per sé non è un'operazione con privilegi.  Ovvero, il codice generato non dispone di ulteriori autorizzazioni rispetto all'assembly che lo genera.  Questo consente alle librerie che generano il codice di essere SecurityTransparent ed elimina la necessità di asserire <xref:System.Security.Permissions.ReflectionPermissionFlag>, che semplifica l'attività di scrittura di una libreria protetta.  
  
 Inoltre, [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] introduce il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> per l'accesso a tipi e membri non pubblici da metodi dinamici parzialmente attendibili.  Le versioni precedenti di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] richiedono il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> per i metodi dinamici che accedono a membri e tipi non pubblici; si tratta di un'autorizzazione che non dovrebbe mai essere concessa a codice parzialmente attendibile.  
  
 Infine, [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] introduce i metodi ospitati anonimamente.  
  
### Informazioni su tipi e membri  
 A partire da [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)] non sono necessarie autorizzazioni per ottenere informazioni sui tipi e i membri non pubblici.  Per ottenere le informazioni necessarie a generare metodi dinamici viene usato Reflection.  Ad esempio, gli oggetti <xref:System.Reflection.MethodInfo> vengono usati per generare le chiamate al metodo.  Le versioni precedenti di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] richiedono <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>.  Per altre informazioni, vedere [Security Considerations for Reflection](../../../docs/framework/reflection-and-codedom/security-considerations-for-reflection.md).  
  
## Vedere anche  
 [Security Considerations for Reflection](../../../docs/framework/reflection-and-codedom/security-considerations-for-reflection.md)   
 [Emitting Dynamic Methods and Assemblies](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)