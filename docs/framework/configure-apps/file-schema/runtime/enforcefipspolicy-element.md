---
title: "Elemento &lt;enforceFIPSPolicy&gt; | Microsoft Docs"
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
  - "<enforceFIPSPolicy> (elemento)"
  - "enforceFIPSPolicy (elemento)"
  - "FIPS (Federal Information Processing Standards)"
  - "FIPS"
ms.assetid: c35509c4-35cf-43c0-bb47-75e4208aa24e
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Elemento &lt;enforceFIPSPolicy&gt;
Specifica se imporre un requisito di configurazione del computer per cui gli algoritmi di crittografia devono essere conformi agli standard FIPS \(Federal Information Processing Standards\).  
  
## Sintassi  
  
```  
<enforceFIPSPolicy enabled="true|false" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|enabled|Attributo obbligatorio.<br /><br /> Specifica se abilitare l'imposizione di un requisito di configurazione del computer per cui gli algoritmi di crittografia devono essere conformi agli standard FIPS.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`true`|Se il computer è configurato in modo da richiedere agli algoritmi di crittografia la conformità alle FIPS, tale requisito verrà applicato.  Se una classe implementa un algoritmo che non è conforme alle FIPS, i costruttori o i metodi `Create` per tale classe generano eccezioni quando vengono eseguiti su tale computer.  Questa è l'impostazione predefinita.|  
|`false`|Gli algoritmi di crittografia utilizzati dall'applicazione non devono essere conformi alle FIPS, indipendentemente dalla configurazione del computer.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 A partire da .NET Framework 2.0, la creazione di classi che implementano gli algoritmi di crittografia è controllata dalla configurazione del computer.  Se il computer è configurato in modo da richiedere agli algoritmi di essere conformi alle FIPS e la classe implementa un algoritmo che non è conforme alle FIPS, qualsiasi tentativo di creare un'istanza di tale classe genera un'eccezione.  I costruttori generano un'eccezione <xref:System.InvalidOperationException> e i metodi `Create` generano un'eccezione <xref:System.Reflection.TargetInvocationException> con un'eccezione interna <xref:System.InvalidOperationException>.  
  
 Se l'applicazione viene eseguita su computer in cui le configurazioni richiedono conformità alle FIPS e l'applicazione utilizza un algoritmo che non è conforme alle FIPS, è possibile utilizzare questo elemento nel file di configurazione per impedire l'applicazione della conformità agli standard FIPS da parte del CLR \(Common Language Runtime\).  Questo elemento è stato introdotto in [!INCLUDE[net_v20SP1_long](../../../../../includes/net-v20sp1-long-md.md)].  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come impedire l'applicazione della conformità agli standard FIPS da parte di CLR.  
  
```  
<configuration>  
    <runtime>  
        <enforceFIPSPolicy enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Cryptography Model](../../../../../docs/standard/security/cryptography-model.md)