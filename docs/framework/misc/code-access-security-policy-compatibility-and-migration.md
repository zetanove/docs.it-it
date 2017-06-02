---
title: "Code Access Security Policy Compatibility and Migration | Microsoft Docs"
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
  - "policy migration, compatibility"
  - "CLR poliicy migration"
ms.assetid: 19cb4d39-e38a-4262-b507-458915303115
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Code Access Security Policy Compatibility and Migration
Gli aspetti relativi ai criteri di sicurezza dall'accesso di codice sono diventati obsoleti a partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)].  Di conseguenza, se si chiamano i membri e i tipi dei criteri obsoleti in modo [esplicito](#explicit_use) o [implicito](#implicit_use) \(tramite altri tipi e membri\), potrebbero verificarsi avvisi di compilazione ed eccezioni di runtime.  
  
 È possibile evitare gli avvisi e gli errori nei modi seguenti:  
  
-   Eseguendo la [migrazione](#migration) alle sostituzioni di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] per le chiamate obsolete.  
  
     \-oppure\-  
  
-   Usando [l'elemento di configurazione \<NetFx40\_LegacySecurityPolicy\>](../../../docs/framework/configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md) per acconsentire esplicitamente il comportamento dei criteri di sicurezza dall'accesso di codice legacy.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Uso esplicito](#explicit_use)  
  
-   [Uso implicito](#implicit_use)  
  
-   [Errori e avvisi](#errors_and_warnings)  
  
-   [Migrazione: sostituzione delle chiamate obsolete](#migration)  
  
-   [Compatibilità: uso dell'opzione legacy relativa ai criteri di sicurezza dall'accesso di codice](#compatibility)  
  
> [!CAUTION]
>  Sicurezza dall'accesso di codice e codice parzialmente attendibile  
>   
>  .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  La sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta.  Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
>   
>  Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
<a name="explicit_use"></a>   
## Uso esplicito  
 I membri che modificano direttamente i criteri di sicurezza o richiedono criteri di sicurezza dall'accesso di codice per il sandboxing sono obsoleti e comportano la generazione di errori per impostazione predefinita.  
  
 Di seguito vengono forniti alcuni esempi:  
  
-   <xref:System.AppDomain.SetAppDomainPolicy%2A?displayProperty=fullName>  
  
-   <xref:System.Security.HostSecurityManager.DomainPolicy%2A?displayProperty=fullName>  
  
-   <xref:System.Security.Policy.PolicyLevel.CreateAppDomainLevel%2A?displayProperty=fullName>  
  
-   <xref:System.Security.SecurityManager.LoadPolicyLevelFromString%2A?displayProperty=fullName>  
  
-   <xref:System.Security.SecurityManager.LoadPolicyLevelFromFile%2A?displayProperty=fullName>  
  
-   <xref:System.Security.SecurityManager.ResolvePolicy%2A?displayProperty=fullName>  
  
-   <xref:System.Security.SecurityManager.ResolveSystemPolicy%2A?displayProperty=fullName>  
  
-   <xref:System.Security.SecurityManager.ResolvePolicyGroups%2A?displayProperty=fullName>  
  
-   <xref:System.Security.SecurityManager.PolicyHierarchy%2A?displayProperty=fullName>  
  
-   <xref:System.Security.SecurityManager.SavePolicy%2A?displayProperty=fullName>  
  
<a name="implicit_use"></a>   
## Uso implicito  
 Numerosi assembly che caricano overload producono errori a causa dell'uso implicito di criteri di sicurezza dall'accesso di codice.  Questi overload accettano un parametro <xref:System.Security.Policy.Evidence> usato per risolvere i criteri di sicurezza dall'accesso di codice e forniscono un set di autorizzazioni per un assembly.  
  
 Ecco alcuni esempi.  Gli overload obsoleti sono quelli che accettano <xref:System.Security.Policy.Evidence> come parametro:  
  
-   <xref:System.Activator.CreateInstanceFrom%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.CreateInstanceFrom%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.CreateInstanceAndUnwrap%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.DefineDynamicAssembly%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.ExecuteAssemblyByName%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>  
  
<a name="errors_and_warnings"></a>   
## Errori e avvisi  
 Quando vengono usati, i tipi e i membri obsoleti producono i messaggi di errore seguenti.  Si noti che il tipo <xref:System.Security.Policy.Evidence?displayProperty=fullName> non è obsoleto.  
  
 Avviso in fase di compilazione:  
  
 `warning CS0618: '<API Name>' is obsolete: 'This method is obsolete and will be removed in a future release of the .NET Framework.  Please use <suggested alternate API>.  See <link> for more information.'`  
  
 Eccezioni di runtime:  
  
 <xref:System.NotSupportedException>: `This method uses CAS policy, which has been obsoleted by the .NET Framework. In order to enable CAS policy for compatibility reasons, please use the <NetFx40_LegacySecurityPolicy> configuration switch. Please see <link> for more information.`  
  
<a name="migration"></a>   
## Migrazione: sostituzione delle chiamate obsolete  
  
### Determinazione del livello di attendibilità di un assembly  
 I criteri di sicurezza dall'accesso di codice vengono spesso usati per determinare il livello di attendibilità o il set di autorizzazioni di un assembly o di un dominio dell'applicazione.  [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] espone le utili proprietà seguenti, che non richiedono la risoluzione dei criteri di sicurezza:  
  
-   <xref:System.Reflection.Assembly.PermissionSet%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.IsFullyTrusted%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.PermissionSet%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.IsFullyTrusted%2A?displayProperty=fullName>  
  
### Sandboxing di un dominio dell'applicazione  
 Il metodo <xref:System.AppDomain.SetAppDomainPolicy%2A?displayProperty=fullName> viene in genere usato per il sandboxing degli assembly in un dominio dell'applicazione.  In [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] vengono esposti membri per cui non è richiesto l'utilizzo di <xref:System.Security.Policy.PolicyLevel>. Per altre informazioni, vedere [How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
### Determinazione di un set di autorizzazioni ragionevoli o sicure per codice parzialmente attendibile  
 Gli host devono spesso determinare le autorizzazioni appropriate per il sandboxing del codice ospitato.  Prima di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], i criteri di sicurezza dall'accesso di codice fornivano, a tale scopo, il metodo <xref:System.Security.SecurityManager.ResolvePolicy%2A?displayProperty=fullName>.  Al suo posto, [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] fornisce il metodo <xref:System.Security.SecurityManager.GetStandardSandbox%2A?displayProperty=fullName>, che restituisce un set di autorizzazioni standard sicuro per l'evidenza fornita.  
  
### Scenari senza sandboxing: overload per i caricamenti di assembly  
 Il motivo per usare un overload per il caricamento di un assembly potrebbe essere l'uso di parametri che non sono altrimenti disponibili, anziché l'esecuzione del sandboxing dell'assembly.  A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], questo scenario è consentito dagli overload di caricamento degli assembly che non richiedono un oggetto <xref:System.Security.Policy.Evidence?displayProperty=fullName> come parametro, ad esempio [AppDomain.ExecuteAssembly\(String, String\[\], Byte\<xref:System.AppDomain.ExecuteAssembly%28System.String%2CSystem.String%5B%5D%2CSystem.Byte%5B%5D%2CSystem.Configuration.Assemblies.AssemblyHashAlgorithm%29?displayProperty=fullName>.  
  
 Per eseguire il sandboxing di un assembly, usare l'overload [AppDomain.CreateDomain\(String, Evidence, AppDomainSetup, PermissionSet, StrongName\<xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=fullName>.  
  
<a name="compatibility"></a>   
## Compatibilità: uso dell'opzione legacy relativa ai criteri di sicurezza dall'accesso di codice  
 L'[elemento di configurazione \<NetFx40\_LegacySecurityPolicy\>](../../../docs/framework/configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md) consente di specificare che in un processo o una libreria vengono usati i criteri di sicurezza per l'accesso al codice legacy.  Quando si abilita questo elemento, gli overload relativi ai criteri e all'evidenza funzionano in modo analogo a quanto avveniva nelle versioni precedenti del framework.  
  
> [!NOTE]
>  Il comportamento dei criteri di sicurezza dall'accesso di codice viene specificato per ogni versione runtime, pertanto la modifica di questi criteri per una versione runtime non influisce sui criteri di sicurezza dall'accesso di codice di un'altra versione.  
  
```  
<configuration>  
   <runtime>  
      <NetFx40_LegacySecurityPolicy enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)