---
title: "Elemento &lt;bindingRedirect&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/bindingRedirect"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#bindingRedirect"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<bindingRedirect> (elemento)"
  - "bindingRedirect (elemento)"
  - "tag contenitore, <bindingRedirect> (elemento)"
ms.assetid: 67784ecd-9663-434e-bd6a-26975e447ac0
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;bindingRedirect&gt;
Reindirizza una versione dell'assembly in un'altra.  
  
## Sintassi  
  
```  
  
   <bindingRedirect    
oldVersion="existing assembly version"  
newVersion="new assembly version"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`oldVersion`|Attributo obbligatorio.<br /><br /> Specifica la versione dell'assembly richiesta in origine.  Il formato del numero di versione dell'assembly è *major.minor.build.revision*.  I valori validi per ogni parte del numero di versione sono compresi tra 0 e 65535.<br /><br /> È inoltre possibile specificare una gamma di versioni nel seguente formato:<br /><br /> *n.n.n.n \- n.n.n.n*|  
|`newVersion`|Attributo obbligatorio.<br /><br /> Specifica la versione dell'assembly da utilizzare al posto della versione richiesta in origine nel formato: *n.n.n.n*<br /><br /> Questo valore può specificare una versione precedente di `oldVersion`.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|Nessuno||  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`assemblyBinding`|Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`dependentAssembly`|Incapsula i criteri di associazione e il percorso dell'assembly per ciascun assembly.  Utilizzare un elemento dependentAssembly per ciascun assembly.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Quando si compila un'applicazione .NET Framework in base a un assembly con un nome sicuro, per impostazione predefinita tale versione dell'assembly viene utilizzata dall'applicazione in fase di esecuzione, anche se è disponibile una nuova versione.  È possibile tuttavia configurare l'applicazione in modo che venga eseguita in base a una versione più recente dell'assembly.  Per ulteriori informazioni su come tali file vengono gestiti nell'ambiente di esecuzione per determinare la versione dell'assembly da utilizzare, vedere [Modalità di individuazione di assembly dell'ambiente di esecuzione](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).  
  
 È possibile reindirizzare più versioni di assembly includendo più elementi `bindingRedirect` in un elemento `dependentAssembly`.  È inoltre possibile reindirizzare una versione più recente a una versione precedente dell'assembly.  
  
 Il reindirizzamento esplicito dell'associazione di assembly in un file di configurazione di un'applicazione richiede un'autorizzazione di sicurezza,  che vale per il reindirizzamento degli assembly .NET Framework e di quelli di altri produttori.  Tale autorizzazione viene concessa impostando il flag [BindingRedirects](frlrfSystemSecurityPermissionsSecurityPermissionFlagClassTopic) sulla [classe SecurityPermission](frlrfSystemSecurityPermissionsSecurityPermissionClassTopic).  Per ulteriori informazioni, vedere [Autorizzazione di sicurezza per il reindirizzamento delle versioni di assembly](../../../../../docs/framework/configure-apps/assembly-binding-redirection-security-permission.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come reindirizzare una versione dell'assembly a un'altra.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Reindirizzamento delle versioni di assembly](../../../../../docs/framework/configure-apps/redirect-assembly-versions.md)