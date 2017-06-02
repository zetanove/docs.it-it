---
title: "Elemento &lt;qualifyAssembly&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#qualifyAssembly"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/qualifyAssembly"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<qualifyAssembly> (elemento)"
  - "tag contenitore, <qualifyAssembly> (elemento)"
  - "qualifyAssembly (elemento)"
ms.assetid: ad6442f6-1a9d-43b6-b733-04ac1b7f9b82
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Elemento &lt;qualifyAssembly&gt;
Specifica il nome completo dell'assembly da caricare in modo dinamico quando viene utilizzato un nome parziale.  
  
## Sintassi  
  
```  
  
      <qualifyAssembly partialName=  
      "PartialAssemblyName"  
                 fullName="FullAssemblyName"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`partialName`|Attributo obbligatorio.<br /><br /> Specifica il nome parziale dell'assembly, così come è visualizzato nel codice.|  
|`fullName`|Attributo obbligatorio.<br /><br /> Specifica il nome parziale dell'assembly, così come è visualizzato nella Global Assembly Cache.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`assemblyBinding`|Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Se si chiama il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> mediante nomi di assembly parziali, in Common Language Runtime la ricerca dell'assembly viene eseguita solo nella directory di base dell'applicazione.  Utilizzare l'elemento **\<qualifyAssembly\>** nel file di configurazione dell'applicazione per tutte le informazioni sull'assembly, ovvero nome, versione, token di chiave pubblica e impostazioni cultura, e fare in modo che in Common Language Runtime la ricerca dell'assembly venga eseguita nella Global Assembly Cache.  
  
 È necessario che l'attributo **fullName** comprenda i quattro campi relativi all'identità dell'assembly, ovvero nome, versione, token di chiave pubblica e impostazioni cultura,  e che l'attributo **partialName** includa un riferimento parziale a un assembly.  È necessario specificare almeno il nome in formato testo dell'assembly \(condizione più comune\), ma è possibile includere anche la versione, il token di chiave pubblica o le impostazioni cultura oppure una qualsiasi combinazione di tali elementi. È tuttavia necessario non includere tutti e quattro gli elementi.  È necessario che l'elemento **partialName** corrisponda al nome specificato nella chiamata.  Non è possibile, ad esempio, specificare `"math"` come attributo **partialName** nel file di configurazione e chiamare `Assembly.Load("math, Version=3.3.3.3")` all'interno del codice.  
  
## Esempio  
 Nell'esempio seguente la chiamata `Assembly.Load("math")`  viene modificata in `Assembly.Load("math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral")`.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <qualifyAssembly partialName="math"   
                         fullName=  
"math,version=1.0.0.0,publicKeyToken=a1690a5ea44bab32,culture=neutral"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Come il runtime individua gli assembly](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [NIB: Partial Assembly References](http://msdn.microsoft.com/it-it/ec90f07a-398c-4306-9401-0fc5ff9cb59f)