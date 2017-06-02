---
title: "Elemento &lt;developmentMode&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/developmentMode"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#developmentMode"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<developmentMode> (elemento)"
  - "tag contenitore, <developmentMode> (elemento)"
  - "developmentMode (elemento)"
ms.assetid: 60e79a8c-415a-497d-be29-b9d0fd9bdee3
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Elemento &lt;developmentMode&gt;
Specifica se nell'ambiente di esecuzione viene effettuata una ricerca degli assembly nelle directory definite dalla variabile di ambiente DEVPATH.  
  
## Sintassi  
  
```  
<developmentMode developerInstallation="true | false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|**developerInstallation**|Specifica se nell'ambiente di esecuzione viene effettuata una ricerca degli assembly nelle directory definite dalla variabile di ambiente DEVPATH.|  
  
## Attributo DeveloperInstallation  
  
|Valore|Descrizione|  
|------------|-----------------|  
|**true**|Viene effettuata una ricerca degli assembly nelle directory specificate dalla variabile di ambiente DEVPATH.|  
|**false**|Non viene effettuata alcuna ricerca degli assembly nelle directory specificate dalla variabile di ambiente DEVPATH.  Questo è il valore predefinito.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Utilizzare questa impostazione solo in fase di sviluppo.  In fase di runtime non vengono controllate le versioni degli assembly con nome sicuro individuate mediante la variabile DEVPATH,  ma viene utilizzato il primo assembly individuato.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come impostare la ricerca di assembly in fase di runtime nelle directory specificate dalla variabile di ambiente DEVPATH.  
  
```  
<configuration>  
   <runtime>  
      <developmentMode developerInstallation="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Procedura: individuare assembly mediante DEVPATH](../../../../../docs/framework/configure-apps/how-to-locate-assemblies-by-using-devpath.md)