---
title: "Elemento &lt;probing&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/probing"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#probing"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<probing> (elemento)"
  - "tag contenitore, <probing> (elemento)"
  - "probing (elemento)"
ms.assetid: 09c80fc9-1ba5-4192-89f7-3a79b2e4b024
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Elemento &lt;probing&gt;
Specifica le sottodirectory di base dell'applicazione per fare in modo che in Common Language Runtime venga effettuata la ricerca durante il caricamento degli assembly.  
  
## Sintassi  
  
```  
<probing privatePath="paths"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`privatePath`|Attributo obbligatorio.<br /><br /> Specifica le sottodirectory della directory di base dell'applicazione che potrebbero contenere gli assembly.  Separare ciascuna sottodirectory con un punto e virgola.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`assemblyBinding`|Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare le sottodirectory di base dell'applicazione in cui deve essere eseguita la ricerca degli assembly dall'ambiente di esecuzione.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <probing privatePath="bin;bin2\subbin;bin3"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Specifica della posizione di un assembly](../../../../../docs/framework/configure-apps/specify-assembly-location.md)   
 [Come il runtime individua gli assembly](../../../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)