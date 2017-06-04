---
title: "Elemento &lt;PreferComInsteadOfManagedRemoting&gt; | Microsoft Docs"
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
  - "<PreferComInsteadOfManagedRemoting> (elemento)"
  - "PreferComInsteadOfManagedRemoting (elemento)"
ms.assetid: a279a42a-c415-4e79-88cf-64244ebda613
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Elemento &lt;PreferComInsteadOfManagedRemoting&gt;
Specifica se il runtime utilizzerà l'interoperabilità COM anziché i servizi remoti per tutte le chiamate fra i limiti di domini di applicazione.  
  
## Sintassi  
  
```  
<PreferComInsteadOfManagedRemoting enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Indica se il runtime utilizzerà l'interoperabilità COM anziché i servizi remoti fra i limiti di domini di applicazione.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il runtime utilizzerà i servizi remoti fra i limiti di domini di applicazione.  Questa è l'impostazione predefinita.|  
|`true`|Il runtime utilizzerà l'interoperabilità COM fra i limiti di domini di applicazione.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 Quando si imposta l'attributo `enabled` su `true`, il runtime presenta il comportamento seguente:  
  
-   Il runtime non chiama [IUnknown::QueryInterface](http://go.microsoft.com/fwlink/?LinkID=144867) per un'interfaccia [IManagedObject](../../../../../ocs/framework/unmanaged-api/hosting/imanagedobject-interface.md) quando un'interfaccia [IUnknown](http://go.microsoft.com/fwlink/?LinkId=148003) fornisce il dominio tramite un'interfaccia COM.  Invece, costruisce un oggetto [Runtime Callable Wrapper](../../../../../docs/framework/interop/runtime-callable-wrapper.md) \(RCW\) attorno all'oggetto.  
  
-   Il runtime restituisce E\_NOINTERFACE quando riceve una chiamata `QueryInterface` per un'interfaccia [IManagedObject](../../../../../ocs/framework/unmanaged-api/hosting/imanagedobject-interface.md) per qualsiasi [COM Callable Wrapper](../../../../../docs/framework/interop/com-callable-wrapper.md) \(CCW\) creato in questo dominio.  
  
 Questi due comportamenti garantiscono che tutte le chiamate tramite le interfacce COM tra oggetti gestiti fra i limiti di domini di applicazione utilizzino COM e l'interoperabilità COM anziché i servizi remoti.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come specificare che il runtime deve utilizzare interoperabilità COM fra i limiti di isolamento:  
  
```  
<configuration>  
  <runtime>  
    <PreferComInsteadOfManagedRemoting enabled="true"/>  
  </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)