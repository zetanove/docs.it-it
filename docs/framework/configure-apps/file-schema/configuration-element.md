---
title: "Elemento &lt;Configuration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<configuration> (elemento)"
  - "configuration (elemento)"
  - "tag contenitore, <configuration> (elemento)"
ms.assetid: 2ec1c9dc-2e5c-4ef0-9958-81670ab88449
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;Configuration&gt;
Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.  
  
 **\<configurazione\>**  
  
## Sintassi  
  
```  
  
      <configuration>   
   <!-- configuration settings -->   
</configuration>  
```  
  
## Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<assemblyBinding\>](../../../../docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)|Specifica i criterio di associazione degli assembly al livello di configurazione.|  
|[Schema delle impostazioni di avvio](../../../../docs/framework/configure-apps/file-schema/startup/index.md)|Tutti gli elementi presenti nello schema delle impostazioni di avvio.|  
|[Schema delle impostazioni dell'ambiente di esecuzione](../../../../docs/framework/configure-apps/file-schema/runtime/index.md)|Tutti gli elementi presenti nello schema delle impostazioni dell'ambiente di esecuzione.|  
|[Schema delle impostazioni remote](http://msdn.microsoft.com/it-it/dc2d1e62-9af7-4ca1-99fd-98b93bb4db9e)|Tutti gli elementi presenti nello schema delle impostazioni remote.|  
|[Schema delle impostazioni di rete](../../../../docs/framework/configure-apps/file-schema/network/index.md)|Tutti gli elementi presenti nello schema delle impostazioni di rete.|  
|[Schema delle impostazioni di crittografia](../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)|Tutti gli elementi presenti nello schema delle impostazioni di crittografia.|  
|[Schema delle sezioni di configurazione](../../../../docs/framework/configure-apps/file-schema/configuration-sections-schema.md)|Tutti gli elementi presenti nello schema delle impostazioni delle sezioni di configurazione.|  
|[Schema delle impostazioni di traccia e debug](../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)|Tutti gli elementi presenti nello schema delle impostazioni di traccia e debug.|  
|[Schema delle impostazioni ASP.NET](http://msdn.microsoft.com/it-it/116608f3-c03d-4413-9fc7-978703e18b0f)|Tutti gli elementi nello schema di configurazione di ASP.NET, che include gli elementi per la configurazione dei siti Web e delle applicazioni di ASP.NET.  Utilizzato nei file Web.config.|  
|[Schema delle impostazioni dei servizi Web XML](http://msdn.microsoft.com/it-it/f84d6d55-1add-4eb7-ae46-33df5833ea2e)|Tutti gli elementi presenti nello schema delle impostazioni dei servizi Web.|  
|[Schema delle impostazioni Web](../../../../docs/framework/configure-apps/file-schema/web/index.md)|Tutti gli elementi nello schema delle impostazioni Web, che include gli elementi per la configurazione del funzionamento di ASP.NET con un'applicazione host, come IIS.  Utilizzato nei file aspnet.config.|  
  
## Note  
 Ciascun file di configurazione deve contenere un unico elemento **\<configuration\>**.  
  
## Vedere anche  
 [Schema dei file di configurazione](../../../../docs/framework/configure-apps/file-schema/index.md)