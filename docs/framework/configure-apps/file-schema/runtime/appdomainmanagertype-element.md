---
title: "Elemento &lt;appDomainManagerType&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
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
  - "<appDomainManagerType> (elemento)"
  - "appDomainManagerType (elemento)"
ms.assetid: ae8d5a7e-e7f7-47f7-98d9-455cc243a322
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;appDomainManagerType&gt;
Specifica il tipo che funge da gestore del dominio di applicazione predefinito.  
  
## Sintassi  
  
```  
<appDomainManagerAssembly   
   value="type name" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`value`|Attributo obbligatorio.  Specifica il nome del tipo, compreso lo spazio dei nomi, che funge da gestore del dominio di applicazione predefinito nel processo.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Per specificare il tipo del gestore di dominio di applicazione è necessario specificare sia questo elemento sia l'elemento [\<appDomainManagerAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md).  Se uno di questi elementi non viene specificato, l'altro viene ignorato.  
  
 Quando il dominio di applicazione predefinito viene caricato, se il tipo specificato non esiste nell'assembly specificato dall'elemento [\<appDomainManagerAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md) viene generato l'oggetto <xref:System.TypeLoadException> e risulta impossibile avviare il processo.  
  
 Quando si specifica il tipo di gestore del dominio di applicazione predefinito, gli altri domini di applicazione creati a partire dal dominio di applicazione predefinito ereditano il tipo di gestore di dominio di applicazione.  Utilizzare le proprietà <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=fullName> e <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=fullName> per specificare un tipo di gestore di dominio di applicazione diverso per un nuovo dominio di applicazione.  
  
 Per specificare il tipo di gestore di dominio di applicazione è necessario che l'applicazione disponga di attendibilità totale. Ad esempio, un'applicazione in esecuzione nel desktop dispone di attendibilità totale. Se l'applicazione non dispone di attendibilità totale, viene generato un oggetto <xref:System.TypeLoadException>.  
  
 Il formato del tipo e dello spazio dei nomi è lo stesso formato utilizzato per la proprietà <xref:System.Type.FullName%2A?displayProperty=fullName>.  
  
 Questo elemento di configurazione è disponibile solo in [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] e versioni successive.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come specificare che il gestore del dominio di applicazione predefinito di un processo è il tipo `MyMgr` nell'assembly `AdMgrExample`.  
  
```  
<configuration>  
   <runtime>  
      <appDomainManagerType value="MyMgr" />  
      <appDomainManagerAssembly   
         value="AdMgrExample, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6856bccf150f00b3" />  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.AppDomainSetup.AppDomainManagerType%2A?displayProperty=fullName>   
 <xref:System.AppDomainSetup.AppDomainManagerAssembly%2A?displayProperty=fullName>   
 [Elemento \<appDomainManagerAssembly\>](../../../../../docs/framework/configure-apps/file-schema/runtime/appdomainmanagerassembly-element.md)   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Metodo SetAppDomainManagerType](../Topic/ICLRControl::SetAppDomainManagerType%20Method.md)