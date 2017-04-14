---
title: "Elemento &lt;publisherPolicy&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/publisherPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/publisherPolicy"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#publisherPolicy"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<publisherPolicy> (elemento)"
  - "tag contenitore, <publisherPolicy> (elemento)"
  - "publisherPolicy (elemento)"
ms.assetid: 4613407e-d0a8-4ef2-9f81-a6acb9fdc7d4
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Elemento &lt;publisherPolicy&gt;
Specifica se nell'ambiente di esecuzione vengono applicati i criteri dell'editore.  
  
## Sintassi  
  
```  
  
<publisherPolicy apply="yes|no"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`apply`|Specifica se vengono applicati i criteri dell'editore.|  
  
## applica attributo  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`yes`|I criteri dell'editore vengono applicati.  Rappresenta l'impostazione predefinita.|  
|`no`|I criteri dell'editore non vengono applicati.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 In fase di rilascio della nuova versione di un assembly, un fornitore di componenti può includere i criteri editore per fare in modo che nelle applicazioni in cui viene utilizzata la versione precedente venga supportata la nuova versione.  Per specificare se i criteri dell'editore devono essere applicati per un assembly specifico, inserire l'elemento **\<publisherPolicy\>** nell'elemento **\<dependentAssembly\>**.  
  
 L'impostazione predefinita dell'attributo **apply** è **yes**.  Impostando l'attributo **apply** su **no**, viene eseguito l'override delle impostazioni **yes** precedenti di un assembly.  
  
 Per fare in modo che un'applicazione ignori in modo esplicito i criteri editore utilizzando l'elemento [\<publisherPolicy apply\="no"\/\>](../../../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md) nel file di configurazione dell'applicazione è necessaria un'autorizzazione.  Tale autorizzazione viene concessa impostando il flag [BindingRedirects](frlrfSystemSecurityPermissionsSecurityPermissionFlagClassTopic) sulla [classe SecurityPermission](frlrfSystemSecurityPermissionsSecurityPermissionClassTopic).  Per ulteriori informazioni, vedere [Autorizzazione di sicurezza per il reindirizzamento delle versioni di assembly](../../../../../docs/framework/configure-apps/assembly-binding-redirection-security-permission.md).  
  
## Esempio  
 Nell'esempio seguente vengono disattivati i criteri dell'editore per l'assembly, `myAssembly`.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                                    publicKeyToken="32ab4ba45e0a69a1"  
                                    culture="neutral" />  
            <publisherPolicy apply="no"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Come il runtime individua gli assembly](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Reindirizzamento delle versioni di assembly](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)