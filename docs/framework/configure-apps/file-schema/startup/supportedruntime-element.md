---
title: "Elemento &lt;supportedRuntime&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#supportedRuntime"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/supportedRuntime"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<supportedRuntime> (elemento)"
  - "supportedRuntime (elemento)"
ms.assetid: 1ae16e23-afbe-4de4-b413-bc457f37b69f
caps.latest.revision: 33
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 28
---
# Elemento &lt;supportedRuntime&gt;
Specifica le versioni di Common Language Runtime supportate dall'applicazione. È necessario utilizzare questo elemento in tutte le applicazioni compilate con la versione 1.1 o successiva di .NET Framework.  
  
 [\<configuration\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<startup\>](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md)  
  
 **\<supportedRuntime\>**  
  
## Sintassi  
  
```  
  
<supportedRuntime version="runtime version" sku="sku id"/>  
```  
  
## Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|**version**|Attributo facoltativo.<br /><br /> Valore stringa mediante il quale viene specificata la versione di Common Language Runtime \(CLR\) supportata da questa applicazione. Per i valori validi dell'attributo `version`, vedere la sezione [Valori di "runtime version"](#version). **Note:**  Tramite .NET Framework 3.5, il valore "*runtime version*" ha il formato *major*.*minor*.*build*. A partire da [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], sono necessari solo i numeri delle versioni principale e secondaria \(vale a dire, "v4.0" anziché "v4.0.30319"\). È consigliabile la stringa più corta.|  
|**sku**|Attributo facoltativo.<br /><br /> Valore stringa che specifica il codice di riferimento del prodotto \(SKU\), che a sua volta specifica la versione di .NET Framework supportata dall'applicazione.<br /><br /> A partire da .NET Framework 4.0, si consiglia l'uso dell'attributo `sku`.  Quando è presente, indica la versione di .NET Framework di destinazione dell'app.<br /><br /> Per i valori validi dell'attributo SKU, vedere la sezione [Valori di "sku id"](#sku).|  
  
## Note  
 Se l'elemento **\<supportedRuntime\>** non è presente nel file di configurazione dell'applicazione, viene utilizzata la versione di CLR impiegata per compilare l'applicazione.  
  
 È necessario utilizzare l'elemento **\<supportedRuntime\>** in tutte le applicazioni compilate con la versione 1.1 o successiva di CLR. Nelle applicazioni compilate per supportare esclusivamente la versione 1.0 è necessario utilizzare l'elemento [\<requiredRuntime\>](../../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md).  
  
> [!NOTE]
>  Se si utilizza la funzione [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md) per specificare il file di configurazione, è necessario utilizzare l'elemento `<requiredRuntime>` per tutte le versioni del runtime. L'elemento `<supportedRuntime>` viene ignorato quando si utilizza [CorBindToRuntimeByCfg](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md).  
  
 Per le app che supportano le versioni di runtime da .NET Framework 1.1 a 3.5, quando sono supportate più versioni, il primo elemento deve indicare la versione preferita, mentre l'ultimo elemento quella meno desiderata. Per le app che supportano .NET Framework 4.0 o versioni successive, l'attributo `version` indica la versione CLR, comune a .NET Framework 4 e versioni successive, e l'attributo `sku` indica l'unica versione di .NET Framework di destinazione dell'app.  
  
> [!NOTE]
>  Se nell'applicazione vengono utilizzati percorsi di attivazione legacy, quale la [funzione CorBindToRuntimeEx](../../../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md), e si desidera attivare la versione 4 di CLR anziché una versione precedente per tali percorsi oppure, se l'applicazione viene compilata con [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] ma dipende da un assembly in modalità mista compilato con una versione precedente di .NET Framework, non sarà sufficiente specificare [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] nell'elenco dei runtime supportati. Inoltre, nell'[elemento \<startup\>](../../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md) del file di configurazione, è necessario impostare l'attributo `useLegacyV2RuntimeActivationPolicy` su `true`. Tuttavia, se questo attributo viene impostato su `true` tutti i componenti compilati con le versioni precedenti di .NET Framework vengono eseguiti utilizzando [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] invece dei runtime con cui sono stati compilati.  
  
 È inoltre consigliabile testare l'applicazione con tutte le versioni di .NET Framework in cui possono essere eseguite.  
  
<a name="version"></a>   
## Valori di "runtime version"  
 La tabella seguente elenca i valori validi per il valore *runtime version* dell'attributo `version`.  
  
|Versione di .NET Framework|Attributo `version`|  
|--------------------------------|-------------------------|  
|1.0|"v1.0.3705"|  
|1.1|"v1.1.4322"|  
|2.0|"v2.0.50727"|  
|3.0|"v2.0.50727"|  
|3.5|"v2.0.50727"|  
|4.0|"v4.0"|  
|4.5|"v4.0"|  
|4.5.1|"v4.0"|  
|4.5.2|"v4.0"|  
|4.6|"v4.0"|  
|4.6.1|"v4.0"|  
  
<a name="sku"></a>   
## Valori di "sku id"  
 La tabella seguente elenca le versioni di .NET Framework a partire da .NET Framework 4 supportate dall'attributo `sku`.  Si noti che l'attributo `sku` a partire da .NET Framework 4 indica la versione di .NET Framework di destinazione dell'app.  
  
|Versione di .NET Framework|Attributo `sku`|  
|--------------------------------|---------------------|  
|4.0|".NETFramework,Version\=v4.0"|  
|4.0, Client Profile|".NETFramework,Version\=v4.0,Profile\=Client"|  
|4.0, aggiornamento piattaforma 1|.NETFramework,Version\=v4.0.1|  
|4.0, Client Profile, aggiornamento 1|.NETFramework, Version\=v4.0.1, Profile\=Client|  
|4.0, aggiornamento piattaforma 2|.NETFramework,Version\=v4.0.2|  
|4.0, Client Profile, aggiornamento 2|.NETFramework, Version\=v4.0.2, Profile\=Client|  
|4.0, aggiornamento piattaforma 3|.NETFramework,Version\=v4.0.3|  
|4.0, Client Profile, aggiornamento 3|.NETFramework,Version\=v4.0.3,Profile\=Client|  
|4.5|".NETFramework,Version\=v4.5"|  
|4.5.1|".NETFramework,Version\=v4.5.1"|  
|4.5.2|".NETFramework,Version\=v4.5.2"|  
|4.6|".NETFramework,Version\=v4.6"|  
|4.6.1|".NETFramework,Version\=v4.6.1"|  
  
 La tabella seguente illustra le versioni installate di .NET Framework 4 che verranno eseguite in un'applicazione, per diversi valori dell'attributo `sku`, quando l'attributo `version` è v4.0 e l'attributo `sku` identifica .NET Framework 4 o uno degli aggiornamenti della piattaforma \(PU\).  
  
|Valore dell'attributo `sku`.|4.0 client|4.0 completa|4.0 Client \+ PU 1|4.0 completa \+ PU 1|4.0 Client \+ PU 2|4.0 completa \+ PU 2|4.0 Client \+ PU 3|4.0 completa \+ PU 3|4.5 e versioni successive|  
|----------------------------------|----------------|------------------|------------------------|--------------------------|------------------------|--------------------------|------------------------|--------------------------|-------------------------------|  
|.NETFramework, Version\=v4.0, Profile\=Client|Sì|Sì|Sì|Sì|Sì|Sì|Sì|Sì|Sì|  
|.NETFramework,Versione\=v4.0||Sì||Sì||Sì||Sì|Sì|  
|.NETFramework, Version\=v4.0.1, Profile\=Client|||Sì|Sì|Sì|Sì|Sì|Sì|Sì|  
|.NETFramework,Version\=v4.0.1||||Sì||Sì||Sì|Sì|  
|.NETFramework, Version\=v4.0.2, Profile\=Client|||||Sì|Sì|Sì|Sì|Sì|  
|.NETFramework,Version\=v4.0.2||||||Sì||Sì|Sì|  
|.NETFramework,Version\=v4.0.3,Profile\=Client|||||||Sì|Sì|Sì|  
|.NETFramework,Version\=v4.0.3||||||||Sì|Sì|  
  
## Esempio  
 L'esempio seguente illustra come specificare la versione di runtime in un file di configurazione. Il file di configurazione indica che l'app è destinata a .NET Framework 4.6.  
  
```xml  
  
<configuration> <startup> <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" /> </startup> </configuration>  
  
```  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione.  
  
## Vedere anche  
 [Schema delle impostazioni di avvio](../../../../../docs/framework/configure-apps/file-schema/startup/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [\<PaveOver\> Specifica della versione di runtime da utilizzare](http://msdn.microsoft.com/it-it/c376208d-980d-42b4-865b-fbe0d9cc97c2)   
 [Esecuzione side\-by\-side in\-process](../../../../../docs/framework/deployment/in-process-side-by-side-execution.md)